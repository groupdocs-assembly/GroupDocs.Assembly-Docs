---
id: generate-excel-reports-from-template
url: assembly/net/generate-excel-reports-from-template
title: Generate Excel Reports from a Template
linkTitle: Excel reports from a template
weight: 4
description: "Fill a spreadsheet template from JSON and keep it a workbook: repeated rows, native numeric cells, formulas that still work, and empty rows removed."
keywords: generate Excel report from template C#, XLSX template engine, Excel report from JSON, spreadsheet report .NET, RemoveEmptyParagraphs
productName: GroupDocs.Assembly for .NET
hideChildren: False
toc: True
---

Finance asks for the workbook, not a PDF of it. That means the result has to stay a spreadsheet:
numbers in numeric cells, the formulas of the template intact, the filters still usable.

A GroupDocs.Assembly template for a spreadsheet is an ordinary `.xlsx` with tags in cells, so the
people who own the report keep editing it in Excel.

{{< alert style="info" >}}
A runnable implementation of this page is on GitHub:
[excel-reports-from-template-net](https://github.com/groupdocs-assembly/excel-reports-from-template-net).
{{< /alert >}}

## A repeating row

A `<<foreach>>` that opens in a cell of a row and closes in a cell of the same row makes the whole
row repeat, pushing everything below it down:

| Client | Manager | Contract Price |
|---|---|---|
| `<<foreach [c in ds]>><<[c.Client]>>` | `<<[c.Manager]>>` | `<<[c.Price]>><</foreach>>` |

```csharp
DocumentAssembler assembler = new DocumentAssembler();
assembler.AssembleDocument(
    Path.Combine(TemplatesPath, "Data table.xlsx"),
    Path.Combine(OutputPath, "contracts.xlsx"),
    new DataSourceInfo(new JsonDataSource(Path.Combine(DataSourcesPath, "contracts.json")), "ds"));
```

with

```json
[
  { "Client": "Quayside Bistro",   "Manager": "A. Petrova",   "Price": 18400 },
  { "Client": "Northwind Traders", "Manager": "J. Okonkwo",   "Price": 42100 },
  { "Client": "Fabrikam Catering", "Manager": "M. Lindqvist", "Price": 7300 }
]
```

`Price` lands in a numeric cell, not as text that looks like a number. That single property is the
difference between a report somebody can pivot and a report somebody has to retype.

## Dropping the rows a condition left empty

{{< alert style="info" >}}`RemoveEmptyParagraphs` covers spreadsheet and plain text templates since version 26.11.{{< /alert >}}

```csharp
DocumentAssembler assembler = new DocumentAssembler
{
    Options = DocumentAssemblyOptions.RemoveEmptyParagraphs
};

assembler.AssembleDocument(
    Path.Combine(TemplatesPath, "Empty paragraph.xlsx"),
    Path.Combine(OutputPath, "compact.xlsx"),
    new DataSourceInfo("dummy", "dummy"));
```

In a spreadsheet a paragraph is a line of text, so a `<<if>>` that renders nothing no longer leaves
its blank rows behind. A report with several optional blocks used to end up full of gaps that
somebody deleted by hand every month. See
[Removing empty paragraphs]({{< ref "/assembly/net/developer-guide/advanced-usage/removing-empty-paragraphs.md" >}}).

## What else belongs in a workbook template

*   **Several tables on one sheet**, each with its own data source: pass more than one
    `DataSourceInfo` to `AssembleDocument`, with a name each.
*   **Charts** whose series come from the data, including
    [series colours]({{< ref "/assembly/net/developer-guide/advanced-usage/working-with-chart-series-coloring/chart-series-coloring-in-spreadsheet-document.md" >}})
    taken from a field.
*   **Grouping and aggregates** inside the expressions: `GroupBy`, `Sum`, `Count`, `Average`. The
    summary row is part of the template, not of your code.
*   **Formulas**: the template's own formulas survive, and
    [they can be recalculated]({{< ref "/assembly/net/developer-guide/advanced-usage/calculate-formula-while-assembling-spreadsheet-documents.md" >}})
    while the document is assembled.
*   **PDF from the same call**, for the copy that gets attached to an e-mail: add
    `new LoadSaveOptions(FileFormat.Pdf)`.

## Formats

ODS, XLS and XLT templates work the same way as XLSX; the full list is on
[Supported document formats]({{< ref "/assembly/net/getting-started/supported-document-formats.md" >}}).

## What to read next

*   [Generate a Word report from a template]({{< ref "/assembly/net/use-cases/generate-word-report-from-template.md" >}}) — the same engine, a document
*   [Generate presentations from JSON]({{< ref "/assembly/net/use-cases/generate-presentations-from-json.md" >}}) — the same engine, a deck
*   Blog: [Generate Excel reports from a template in C#](https://blog.groupdocs.com/assembly/generate-excel-reports-from-template-csharp/)
*   GitHub: [excel-reports-from-template-net](https://github.com/groupdocs-assembly/excel-reports-from-template-net)
