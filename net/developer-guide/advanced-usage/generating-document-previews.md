---
id: generating-document-previews
url: assembly/net/generating-document-previews
title: Generating Document Previews
weight: 45
description: "Render pages of templates, assembled reports and other documents to PNG, JPEG or BMP images with DocumentAssembler.GeneratePreview and PreviewOptions."
keywords: document preview, page preview, GeneratePreview, PreviewOptions, PreviewFormats, Resolution, thumbnail, PNG, JPEG, BMP
productName: GroupDocs.Assembly for .NET
hideChildren: False
---
{{< alert style="info" >}}This feature is supported by version 26.11 or greater.{{< /alert >}}

`DocumentAssembler.GeneratePreview` renders pages of a document to images. The document can be a template, a document assembled by GroupDocs.Assembly, or any other document of a supported format: word processing, spreadsheet, presentation, email or text. `PreviewOptions` follows the preview options of other GroupDocs products.

The document is passed by a path or a stream:

*   `void GeneratePreview(string documentPath, PreviewOptions previewOptions)`
*   `void GeneratePreview(Stream documentStream, PreviewOptions previewOptions)`

## Preview Options

| Member | Description |
| --- | --- |
| `CreatePageStream` | A delegate called for every page to get the stream the page image is written to. Passed to the constructor. |
| `ReleasePageStream` | An optional delegate called when a page image has been written, to close or process its stream. Passed to the constructor. |
| `PreviewFormat` | The image format: `PreviewFormats.PNG` (the default), `PreviewFormats.JPEG` or `PreviewFormats.BMP`. |
| `PageNumbers` | The numbers of the pages to render, starting from 1. All pages by default. |
| `Width`, `Height` | The size of page images in pixels. When both are set, pages are scaled to fit that size keeping their aspect ratio, and `Resolution` is ignored. |
| `Resolution` | The resolution of page images in dots per inch, 96 by default. |

## Rendering Pages of an Assembled Report

The example assembles a report into memory and renders its pages to PNG files:

```csharp
using System.IO;
using GroupDocs.Assembly;
using GroupDocs.Assembly.Data;

DocumentAssembler assembler = new DocumentAssembler();

using (FileStream template = File.OpenRead("Customer orders.docx"))
using (MemoryStream report = new MemoryStream())
{
    assembler.AssembleDocument(template, report,
        new DataSourceInfo(new JsonDataSource("Customers.json"), "customers"));
    report.Position = 0;

    // A stream is created for every page and released when the page is written.
    PreviewOptions options = new PreviewOptions(
        pageNumber => File.Create($"page{pageNumber}.png"),
        (pageNumber, pageStream) => pageStream.Dispose());
    options.PreviewFormat = PreviewFormats.PNG;
    options.Resolution = 120;               // dots per inch; 96 by default
    // options.PageNumbers = new[] { 1, 2 }; // all pages by default

    assembler.GeneratePreview(report, options);
}
```

## Rendering Selected Pages of a Template

To preview a template itself, pass its path. Here the first page is rendered to a JPEG image that fits in 400 × 400 pixels:

```csharp
PreviewOptions options = new PreviewOptions(pageNumber => File.Create($"template-page{pageNumber}.jpg"),
    (pageNumber, pageStream) => pageStream.Dispose());
options.PreviewFormat = PreviewFormats.JPEG;
options.PageNumbers = new[] { 1 };
options.Width = 400;
options.Height = 400;

new DocumentAssembler().GeneratePreview("Customer orders.docx", options);
```

{{< alert style="info" >}}Previews are generated without loading any external resources.{{< /alert >}}

Example: [GenerateDocumentPreview.cs](https://github.com/groupdocs-assembly/GroupDocs.Assembly-for-.NET/blob/master/Examples/GroupDocs.Assembly.Examples.CSharp/AdvancedUsage/GenerateDocumentPreview.cs).

A preview served from a web request: [Generate and download reports in ASP.NET Core]({{< ref "/assembly/net/use-cases/generate-reports-in-aspnet-core.md" >}}). Previews are also the quickest way to prove a Linux image has the fonts it needs: [Document generation in Docker and serverless]({{< ref "/assembly/net/use-cases/running-in-docker-and-serverless.md" >}}).
