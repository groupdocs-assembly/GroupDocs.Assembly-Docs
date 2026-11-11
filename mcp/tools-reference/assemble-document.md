---
id: mcp-tool-assemble-document
url: assembly/mcp/tools-reference/assemble-document
title: assemble_document
weight: 2
description: "The assemble_document MCP tool fills a Word, Excel, PowerPoint, Markdown, HTML or e-mail template with JSON, XML, CSV or spreadsheet data and saves the document — tables, charts, images and barcodes included — locally."
keywords: assemble_document MCP tool, generate document from template AI, fill Word template JSON, generate PDF from template locally, report from CSV MCP
productName: GroupDocs.Assembly MCP Server
generated: true
serverVersion: 26.11.0
toc: True
---

`assemble_document` fills a template with data and saves the result — a contract, invoice, letter or report — in the template's format or another (`format: "pdf"`). The data is inline JSON the agent writes (`dataJson`) or a file (`data`: JSON, XML, CSV, or a spreadsheet/Word/presentation table). Example prompt: *"Fill contract-template.docx for Contoso Pharma and save it as a PDF."*

**Tool description (as the AI agent sees it):**

> Generates a document from a template and data: fills the template's <<[field]>>, <<foreach>>, <<if>>, table, chart, image and barcode tags with values and saves the result — a contract, invoice, letter, report or e-mail built from a Word, Excel, PowerPoint, Markdown, HTML or e-mail template. Use it whenever the user asks to generate, fill in, populate or produce a document from a template. Templates: DOCX, DOC, RTF, ODT, TXT, Markdown, HTML, XLSX, XLS, ODS, PPTX, PPT, ODP, MSG, EML and more. Data: pass 'dataJson' (a JSON object or array, inline) or 'data' (a .json, .xml, .csv/.tsv file, or a spreadsheet, Word or presentation document whose table is the data). A JSON object's keys are the names the template uses ({"customer":{…},"items":[…]} fills <<[customer.Name]>> and <<foreach [i in items]>>); an array, XML, CSV or table is given the name the template uses for it automatically, or pass 'dataSourceName'. Call get_template_fields first to see which names and fields a template expects and a JSON skeleton to fill. Output: the template's own format by default; set 'format' (e.g. pdf, docx, html, md) to save it as another format of the same family, or as PDF. Do NOT pre-check whether files exist — just pass the filename the user provided; a file that cannot be found returns the list of available files instead. Returns 'Assembled …' with the saved path ('Saved to: …') of '<template>_assembled.<ext>'. On failure isError is set and the text starts with 'Document assembly failed for'; a field the data lacks is named in the message.

## Parameters

| Name | Type | Required | Description |
|---|---|---|---|
| `template` | object | yes | The template document (DOCX, XLSX, PPTX, Markdown, HTML, TXT, MSG, EML, …) containing <<…>> tags — [FileInput shape]({{< ref "assembly/mcp/tools-reference/_index.md#the-fileinput-shape" >}}) |
| `dataJson` | string | no | The data as inline JSON: an object whose keys are the names used in the template, or an array. Use this OR 'data' |
| `data` | object | no | The data as a file: .json, .xml, .csv or .tsv, or a spreadsheet/Word/presentation document whose table holds the data. Use this OR 'dataJson' — [FileInput shape]({{< ref "assembly/mcp/tools-reference/_index.md#the-fileinput-shape" >}}) |
| `dataSourceName` | string | no | The name the template uses for the data (e.g. 'customers' in <<foreach [c in customers]>>). Default: worked out from the template |
| `format` | string | no | Output format extension (default: the template's own), e.g. 'pdf', 'docx', 'html', 'md', 'xlsx', 'pptx', 'eml' |
| `outputName` | string | no | Output file name (the extension follows the output format). Default: '<template>_assembled.<ext>' |
| `allowMissingMembers` | boolean | no | Treat fields missing from the data as empty instead of failing (default false) |
| `removeEmptyParagraphs` | boolean | no | Remove paragraphs that become empty after tags are replaced (default false) |
| `updateFields` | boolean | no | Update fields (page numbers, tables of contents) and spreadsheet formulas in the result (default false) |
| `inlineErrors` | boolean | no | Write template syntax errors into the output next to the faulty tag instead of failing — for debugging a template (default false) |
| `dataTable` | integer | no | Document data only: which table (worksheet for spreadsheets) holds the data, 1-based (default 1) |
| `hasHeaders` | boolean | no | CSV and document-table data: the first row holds column names (default true) |
| `csvDelimiter` | string | no | CSV data: the column delimiter, one character or 'tab' (default ',' — tab for .tsv) |

## Example call

```json
{
  "name": "assemble_document",
  "arguments": {
    "template": {
      "filePath": "contract-template.docx"
    },
    "dataJson": "{\"contract\":{...},\"customer\":{...},\"items\":[...]}",
    "format": "pdf"
  }
}
```

## Result

A short report and the saved file — captured from server 26.11.0 (the evaluation note is trimmed; the server prints the full path inside your storage folder):

```text
Assembled 'contract-template.docx' with inline JSON (JSON object) as PDF
Saved to: …/contract-template_assembled.pdf
```

With a data file the report says how the data was read — useful when a spreadsheet has several tables:

```text
Assembled 'sales-report.docx' with 'sales.xlsx' (table 1 (3 column(s):
Region, Quarter, Revenue) as 'sales') as PDF
Saved to: …/sales-report_assembled.pdf
```

(Wrapped for width.) Options worth knowing:

| Option | Default | Use it when |
|---|---|---|
| `outputName` | `<template>_assembled.<ext>` | you want `SA-2026-118-contoso.docx` |
| `allowMissingMembers` | false | some records lack optional fields — print nothing instead of failing |
| `removeEmptyParagraphs` | false | conditional blocks leave blank lines |
| `updateFields` | false | the template has a table of contents, page numbers or spreadsheet formulas |
| `inlineErrors` | false | debugging: write template errors into the output next to the tag |
| `dataTable` / `hasHeaders` / `csvDelimiter` | 1 / true / `,` | table and CSV data |

On failure the text starts with `Document assembly failed for '<template>':`, then the engine message and a plain-words hint, and `isError` is set. Two you will meet:

```text
Document assembly failed for 'contract-template.docx': ... Can not get the
value of member 'Email' on type ''. ... The template reads 'Email', which the
data does not have. Check the spelling (names are case-sensitive) with
get_template_fields and add it to the data. A list that is empty in the data
has no fields at all, so reading one fails too; pass allowMissingMembers=true
to output nothing for missing members and empty lists.
```

```text
Document assembly failed for 'order-lines.docx': ... Unexpected end of
template. A block tag is not closed: every <<foreach>> needs <</foreach>> and
every <<if>> needs <</if>>.
```

(Exception type prefixes elided with `...`.)

## Example prompts

* *"Fill contract-template.docx for Contoso Pharma and save it as a PDF."*
* *"Build the Q3 sales report from sales.xlsx."*
* *"Generate the release notes PDF from data/release-4.2.0.json."*
* *"Turn product-readme.md into a Word document for Northwind Gateway."*

See it used end-to-end: [Generate documents with AI agents]({{< ref "assembly/mcp/use-cases/generate-documents-with-ai-agents.md" >}}).
