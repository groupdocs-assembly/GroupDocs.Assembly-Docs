---
id: generate-excel-reports-from-template
url: assembly/net/generate-excel-reports-from-template
title: Generate Excel Reports from a Template
linkTitle: Excel reports from a template
weight: 4
description: "Generate an Excel report from a template in C#: repeating rows from JSON, UseSpreadsheetDataTypes so numbers stay numbers, totals as template expressions, and empty rows removed."
keywords: generate Excel report from template C#, how to generate Excel report from template, XLSX template engine C#, Excel report from JSON, UseSpreadsheetDataTypes, spreadsheet report .NET, RemoveEmptyParagraphs, Excel template engine without Office
productName: GroupDocs.Assembly for .NET
hideChildren: False
toc: True
---

To generate an Excel report from a template in C#, put `<<foreach>>` tags in the cells of an
`.xlsx`, fill it with `DocumentAssembler.AssembleDocument`, and set
`DocumentAssemblyOptions.UseSpreadsheetDataTypes` so numbers, dates and booleans keep their native
cell types. No Microsoft Excel is involved, and the template stays a workbook the report owner
edits themselves.

Finance asks for the workbook, not a PDF of it, and that is a different job: the result has to stay
a spreadsheet — numbers in numeric cells, totals that recalculate, filters that still work.

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
| `Total` | | `<<[ds.Sum(c => c.Price)]>>` |

```csharp
DocumentAssembler assembler = new DocumentAssembler
{
    Options = DocumentAssemblyOptions.UseSpreadsheetDataTypes
};

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

## Keeping numbers numeric: `UseSpreadsheetDataTypes`

By default the engine writes every value into a cell as a string. The report looks correct and is
useless for anything a spreadsheet is for: `SUM` over the column returns 0, sorting is
alphabetical, and a pivot table refuses the field.

`DocumentAssemblyOptions.UseSpreadsheetDataTypes` writes numbers, dates and booleans with their
native cell types instead. The difference is visible in the file itself — a text cell carries
`t="s"`, a numeric one carries the value:

```xml
<!-- default -->                    <c r="C2" t="s"><v>6</v></c>
<!-- UseSpreadsheetDataTypes -->    <c r="C2"><v>18400</v></c>
```

and visible on screen as alignment, because Excel puts real numbers against the right edge of the
cell and leaves text against the left.

## Totals: a template expression, not a worksheet formula

A `SUM()` placed under the repeating row does **not** survive assembly. The row it refers to is
replaced while the data expands, and the result is `SUM(#REF!)`.

Compute the total in the template instead, over the same collection the rows came from:

```text
<<[ds.Sum(c => c.Price)]>>
```

With `UseSpreadsheetDataTypes` on, the total lands as a number as well, so formulas written on top
of it afterwards work. Formulas that do not point at the repeating range are untouched and
[can be recalculated]({{< ref "/assembly/net/developer-guide/advanced-usage/calculate-formula-while-assembling-spreadsheet-documents.md" >}})
during assembly.

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
*   **PDF from the same call**, for the copy that gets attached to an e-mail: add
    `new LoadSaveOptions(FileFormat.Pdf)`.

## Formats

ODS, XLS and XLT templates work the same way as XLSX; the full list is on
[Supported document formats]({{< ref "/assembly/net/getting-started/supported-document-formats.md" >}}).

## Frequently asked questions

**How do you generate an Excel report from a template in C#?**
Put `<<foreach [c in ds]>>` … `<</foreach>>` tags in the cells of an `.xlsx`, then call
`DocumentAssembler.AssembleDocument` with the template, the output path and a `DataSourceInfo`.
Set `DocumentAssemblyOptions.UseSpreadsheetDataTypes` so the values keep their types.

**Why are the numbers text in the generated workbook?**
`UseSpreadsheetDataTypes` is off by default. Without it every value is written as a string, which
is why `SUM` returns 0 and sorting is alphabetical.

**Why does a `SUM` formula turn into `SUM(#REF!)`?**
It referenced the repeating row, which is replaced during assembly. Use a template expression such
as `<<[ds.Sum(c => c.Price)]>>` for aggregates over the repeated data.

**Can the same template produce a PDF?**
Yes — add `new LoadSaveOptions(FileFormat.Pdf)` to the same `AssembleDocument` call.

**Is Microsoft Excel required on the server?**
No. GroupDocs.Assembly reads and writes the formats itself, on Windows and on Linux.

## What to read next

*   [Generate a Word report from a template]({{< ref "/assembly/net/use-cases/generate-word-report-from-template.md" >}}) — the same engine, a document
*   [Generate presentations from JSON]({{< ref "/assembly/net/use-cases/generate-presentations-from-json.md" >}}) — the same engine, a deck
*   Blog: [Generate Excel reports from a template in C#](https://blog.groupdocs.com/assembly/generate-excel-reports-from-template-csharp/)
*   GitHub: [excel-reports-from-template-net](https://github.com/groupdocs-assembly/excel-reports-from-template-net)
