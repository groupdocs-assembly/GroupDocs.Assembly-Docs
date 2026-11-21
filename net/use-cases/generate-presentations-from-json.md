---
id: generate-presentations-from-json
url: assembly/net/generate-presentations-from-json
title: Generate PowerPoint Presentations from JSON
linkTitle: PowerPoint from JSON
weight: 5
description: "Build a PowerPoint deck from a JSON file: a table that grows with the data, an image in every row and relative image paths resolved against the template."
keywords: generate PowerPoint from JSON C#, create PPTX from JSON, PPTX template engine .NET, image in table cell presentation, deck from data, presentation report .NET, PowerPoint without Office
productName: GroupDocs.Assembly for .NET
hideChildren: False
toc: True
---

A product catalogue, a monthly review, a partner deck: the layout is fixed and the content comes
from data. The template stays a `.pptx` that a designer owns, and nothing in your code knows about
slide geometry.

{{< alert style="info" >}}
A runnable implementation of this page is on GitHub:
[powerpoint-decks-from-json-net](https://github.com/groupdocs-assembly/powerpoint-decks-from-json-net).
{{< /alert >}}

## A table that grows, with a picture in every row

One row of the table carries the tags, and the row repeats once per element:

```text
<<foreach [p in products]>><<[p.Name]>>   <<image [p.Photo] -fitHeight>><</foreach>>
```

```json
[
  { "Name": "Espresso beans, 1 kg", "Photo": "../data/Logo.jpg" },
  { "Name": "Oat milk, 1 l",        "Photo": "../data/no-photo.jpg" }
]
```

```csharp
DocumentAssembler assembler = new DocumentAssembler();
assembler.AssembleDocument(
    Path.Combine(TemplatesPath, "Image in table cell.pptx"),
    Path.Combine(OutputPath, "catalogue.pptx"),
    new DataSourceInfo(new JsonDataSource(Path.Combine(DataSourcesPath, "products.json")), "products"));
```

Two parts of that are new in 26.11.

{{< alert style="info" >}}Images in table cells of presentations and relative image paths are supported since version 26.11.{{< /alert >}}

**An `<<image>>` tag may sit in a table cell of a presentation.** The picture becomes the fill of
the cell and repeats with the row, including rows produced by `foreach`. Before, an image in a
presentation had to live in its own shape, which does not survive a table that grows. See
[Insert images dynamically]({{< ref "/assembly/net/developer-guide/basic-usage/insert-images-dynamically.md" >}}).

**The path may be relative.** It is resolved against the folder of the template, so the data can
carry `../data/Logo.jpg` instead of a path that only works on one machine. `-fitHeight` lets the
row grow so the picture keeps its aspect ratio.

## Templates read from a stream

A template read from a stream has no folder of its own, so the base for relative paths has to be
given explicitly. Forgetting this is the usual reason a working file-based call starts producing
empty cells after it is changed to streams:

```csharp
LoadSaveOptions options = new LoadSaveOptions(FileFormat.Pdf);
options.ResourceLoadBaseUri = TemplatesPath;

using (FileStream template = File.OpenRead(Path.Combine(TemplatesPath, "Image in table cell.pptx")))
using (FileStream report = File.Create(Path.Combine(OutputPath, "catalogue.pdf")))
{
    assembler.AssembleDocument(
        template,
        report,
        options,
        new DataSourceInfo(new JsonDataSource(Path.Combine(DataSourcesPath, "products.json")), "products"));
}
```

## What else a deck template can do

*   **Charts** built from the data, with
    [series and point colours]({{< ref "/assembly/net/developer-guide/advanced-usage/working-with-chart-series-coloring/chart-series-coloring-in-presentation-document.md" >}})
    taken from fields.
*   **Bulleted and numbered lists** that expand from a collection.
*   **Master-detail** layouts: a slide section per customer, a row per order.
*   **A document table as the data source**, when the data arrives as a table inside another
    presentation or workbook.

## Formats

ODP, POTX, PPT and POT templates work the same way as PPTX; the full list is on
[Supported document formats]({{< ref "/assembly/net/getting-started/supported-document-formats.md" >}}).

## Frequently asked questions

**How do you generate a PowerPoint presentation from JSON in C#?**
Put `<<foreach>>` tags in one row of a table in a `.pptx`, point `JsonDataSource` at the JSON array
and call `DocumentAssembler.AssembleDocument`. The row repeats once per record.

**Can an image be placed inside a table cell of a slide?**
Yes, since version 26.11. The picture becomes the fill of the cell and repeats with the row,
including rows produced by `foreach`.

**Can image paths in the data be relative?**
Yes, resolved against the folder of the template. A template read from a stream has no folder, so
set `LoadSaveOptions.ResourceLoadBaseUri`.

**Is Microsoft PowerPoint required on the server?**
No. The formats are read and written by the library itself.

**Which presentation formats can be used as templates?**
PPTX, PPT, POTX, POT and ODP.

## What to read next

*   [Generate Excel reports from a template]({{< ref "/assembly/net/use-cases/generate-excel-reports-from-template.md" >}}) — the same engine, a workbook
*   [Running in Docker and serverless]({{< ref "/assembly/net/use-cases/running-in-docker-and-serverless.md" >}}) — rendering a deck to images, and the fonts it needs
*   Blog: [Generate PowerPoint presentations from JSON in C#](https://blog.groupdocs.com/assembly/generate-powerpoint-decks-from-json-csharp/)
*   GitHub: [powerpoint-decks-from-json-net](https://github.com/groupdocs-assembly/powerpoint-decks-from-json-net)
