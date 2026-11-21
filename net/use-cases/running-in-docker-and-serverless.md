---
id: running-in-docker-and-serverless
url: assembly/net/running-in-docker-and-serverless
title: Running in Docker and Serverless
linkTitle: Docker and serverless
weight: 7
description: "Run document generation on Linux: the fonts a container needs, how to prove they are there with GeneratePreview, and what changes in Azure Functions, AWS Lambda and Cloud Run."
keywords: GroupDocs.Assembly Docker, document generation Linux, fonts in container, Azure Functions document generation, AWS Lambda report, serverless
productName: GroupDocs.Assembly for .NET
hideChildren: False
toc: True
---

Document generation moves to Linux the moment it goes into a container, a Kubernetes job or a
function. The code does not change. The image does — and the thing that catches everybody is
**fonts**.

{{< alert style="info" >}}
A runnable implementation of this page is on GitHub:
[document-generation-docker-net](https://github.com/groupdocs-assembly/document-generation-docker-net).
{{< /alert >}}

## Fonts

The .NET runtime images ship without fonts. Nothing in the assembly step fails when they are
missing: the document is produced, text is laid out with whatever substitute can be found, and the
result is wrong in ways nobody sees until a reader opens it — a line break in a new place, a table
that overflows, one page that became two.

```dockerfile
FROM mcr.microsoft.com/dotnet/runtime:8.0
WORKDIR /work

RUN apt-get update \
 && apt-get install -y --no-install-recommends fontconfig fonts-liberation \
 && rm -rf /var/lib/apt/lists/*
```

*   `fontconfig` is what makes fonts discoverable at all.
*   `fonts-liberation` provides metric-compatible substitutes for Arial, Times New Roman and
    Courier New, which is what most templates ask for.

A template that uses other fonts needs those fonts in the image too: copy them into
`/usr/share/fonts` and run `fc-cache -f`.

## Prove it, do not assume it

A DOCX hides a font problem. Rendering does not — which is what makes
`GeneratePreview` a good smoke test for an image.

{{< alert style="info" >}}`DocumentAssembler.GeneratePreview` is available since version 26.11.{{< /alert >}}

```csharp
PreviewOptions previewOptions = new PreviewOptions(
    pageNumber => File.Create(Path.Combine(outputDirectory, $"page{pageNumber}.png")),
    (pageNumber, pageStream) => pageStream.Dispose());

previewOptions.PreviewFormat = PreviewFormats.PNG;
previewOptions.Resolution = 120;   // dots per inch, 96 by default

new DocumentAssembler().GeneratePreview(documentPath, previewOptions);
```

Render one page in the build of the image and compare it with a reference. A missing font becomes a
failing build instead of a support ticket.

## The full Dockerfile

```dockerfile
FROM mcr.microsoft.com/dotnet/sdk:8.0 AS build
WORKDIR /src
COPY . .
RUN dotnet publish src/DockerReports/DockerReports.csproj -c Release -o /app

FROM mcr.microsoft.com/dotnet/runtime:8.0
WORKDIR /work

RUN apt-get update \
 && apt-get install -y --no-install-recommends fontconfig fonts-liberation \
 && rm -rf /var/lib/apt/lists/*

COPY --from=build /app /app
COPY templates /work/templates
COPY data /work/data

ENTRYPOINT ["dotnet", "/app/report.dll"]
CMD ["report"]
```

## Serverless

The same image is the base of an Azure Functions custom handler, an AWS Lambda container image or a
Cloud Run job. Three things to plan for:

*   **Cold start.** The first assembly in a process pays for loading the engine. Keep an instance
    warm if the first request is user-facing, or accept that it is slower.
*   **Writable space.** Assemble to streams. A function's file system is small, temporary and
    sometimes read-only; nothing in document assembly requires a file.
*   **The licence.** Ship it as a secret rather than inside the image, and apply it once per
    process, not per invocation.

## Memory and throughput

A document is assembled in memory, so the working set follows the size of the data and of the
output rather than the number of templates. Two habits keep a batch predictable:

*   assemble to a stream and dispose it, rather than keeping the result around;
*   process in batches, and let the process exit between them in a job — a container that runs one
    batch and stops cannot leak.

## Licensing

Apply the licence once at start-up. The path can come from an environment variable so the image
stays free of it:

```csharp
string? path = Environment.GetEnvironmentVariable("GROUPDOCS_ASSEMBLY_LICENSE");

if (!string.IsNullOrWhiteSpace(path) && File.Exists(path))
    new License().SetLicense(path);
```

See [Evaluation limitations and licensing]({{< ref "/assembly/net/getting-started/evaluation-limitations-and-licensing.md" >}}).

## What to read next

*   [Generate reports in ASP.NET Core]({{< ref "/assembly/net/use-cases/generate-reports-in-aspnet-core.md" >}}) — the service that runs in this image
*   [Generating document previews]({{< ref "/assembly/net/developer-guide/advanced-usage/generating-document-previews.md" >}}) — the rendering options
*   [System requirements]({{< ref "/assembly/net/getting-started/system-requirements.md" >}})
*   Blog: [Generating documents in Docker with .NET](https://blog.groupdocs.com/assembly/generate-documents-in-docker-dotnet/)
*   GitHub: [document-generation-docker-net](https://github.com/groupdocs-assembly/document-generation-docker-net)
