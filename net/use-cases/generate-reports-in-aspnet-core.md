---
id: generate-reports-in-aspnet-core
url: assembly/net/generate-reports-in-aspnet-core
title: Generate Reports in ASP.NET Core
linkTitle: Reports in ASP.NET Core
weight: 6
description: "Take JSON in a request, fill a Word template and stream back a DOCX or a PDF, plus a PNG preview of the first page - all in memory, with no files on disk."
keywords: ASP.NET Core document generation, download DOCX from web API, generate PDF ASP.NET Core, minimal API report, document preview web
productName: GroupDocs.Assembly for .NET
hideChildren: False
toc: True
---

The request a web application actually receives is "give me this as a Word file". This page is the
small, complete version of that: a minimal API that takes JSON, fills a template and streams back
the document — with a rendered first page so the reader sees the report before downloading it.

{{< alert style="info" >}}
A runnable implementation of this page is on GitHub:
[aspnet-core-report-download-net](https://github.com/groupdocs-assembly/aspnet-core-report-download-net).
{{< /alert >}}

## Keep everything in memory

A web request has no business writing intermediate files: two requests would collide over the same
name, and a container would need a writable disk for no reason. Both the template and the report are
streams.

```csharp
public byte[] Assemble(string json, bool asPdf)
{
    using MemoryStream data = new(Encoding.UTF8.GetBytes(json));
    using MemoryStream report = new();
    using FileStream template = File.OpenRead(Path.Combine(TemplatesPath, "Customer orders.docx"));

    DocumentAssembler assembler = new();

    if (asPdf)
    {
        assembler.AssembleDocument(
            template, report,
            new LoadSaveOptions(FileFormat.Pdf),
            new DataSourceInfo(new JsonDataSource(data), "customers"));
    }
    else
    {
        assembler.AssembleDocument(
            template, report,
            new DataSourceInfo(new JsonDataSource(data), "customers"));
    }

    return report.ToArray();
}
```

{{< alert style="warning" >}}
There is no overload that takes a template **path** and an output **stream**. When the report goes
to a stream, open the template as a stream too.
{{< /alert >}}

## The endpoint

```csharp
app.MapPost("/api/reports", async (HttpRequest request, ReportBuilder reports, string? format) =>
{
    using StreamReader reader = new(request.Body);
    string json = await reader.ReadToEndAsync();

    bool asPdf = string.Equals(format, "pdf", StringComparison.OrdinalIgnoreCase);

    try
    {
        byte[] report = reports.Assemble(json, asPdf);

        return Results.File(
            report,
            asPdf ? "application/pdf" : "application/vnd.openxmlformats-officedocument.wordprocessingml.document",
            asPdf ? "customer-orders.pdf" : "customer-orders.docx");
    }
    catch (Exception exception)
    {
        // A template or data error belongs to the caller, not to the server.
        return Results.BadRequest(new { error = exception.Message });
    }
});
```

`Results.File` with a file name sets `Content-Disposition`, which is what makes the browser
download rather than display.

## A preview instead of a viewer

{{< alert style="info" >}}`DocumentAssembler.GeneratePreview` is available since version 26.11.{{< /alert >}}

```csharp
public byte[] PreviewPage(byte[] document, int pageNumber, int resolution)
{
    using MemoryStream source = new(document);
    MemoryStream? page = null;

    PreviewOptions previewOptions = new(
        _ => page = new MemoryStream(),
        (_, _) => { /* the stream is read after GeneratePreview returns */ })
    {
        PreviewFormat = PreviewFormats.PNG,
        PageNumbers = new[] { pageNumber },   // 1-based
        Resolution = resolution
    };

    new DocumentAssembler().GeneratePreview(source, previewOptions);
    return page!.ToArray();
}
```

Before 26.11, showing a report in a browser meant converting the whole document to HTML and
accepting that it would not look like the file, or embedding a viewer. One page as a PNG is smaller
than either, and it is exactly what the reader is about to download. Full options on
[Generating document previews]({{< ref "/assembly/net/developer-guide/advanced-usage/generating-document-previews.md" >}}).

Note the second callback. The release callback runs while `GeneratePreview` is still working, so a
stream you intend to read afterwards must not be disposed there.

## Before this goes to production

*   **Apply the licence once**, in the constructor of a singleton, not per request.
*   **Limit the request body.** It is read whole into memory.
*   **Return `400`, not `500`**, for a template or data error — it is the caller's input. With
    `InlineErrorMessages` you can return the document instead and let the reader see where it broke;
    see [Templates for incomplete data]({{< ref "/assembly/net/use-cases/templates-for-incomplete-data.md" >}}).
*   **Install fonts in the image.** Rendering lays text out, and the .NET runtime images ship
    without fonts — see
    [Running in Docker and serverless]({{< ref "/assembly/net/use-cases/running-in-docker-and-serverless.md" >}}).
*   **Cache nothing by accident.** `DocumentAssembler` is cheap to create; share the template file,
    not the assembler.

## What to read next

*   [Running in Docker and serverless]({{< ref "/assembly/net/use-cases/running-in-docker-and-serverless.md" >}}) — the image this service runs in
*   [Generating document previews]({{< ref "/assembly/net/developer-guide/advanced-usage/generating-document-previews.md" >}}) — formats, page numbers, resolution
*   Blog: [Generate and download reports in ASP.NET Core](https://blog.groupdocs.com/assembly/generate-and-download-reports-aspnet-core/)
*   GitHub: [aspnet-core-report-download-net](https://github.com/groupdocs-assembly/aspnet-core-report-download-net)
