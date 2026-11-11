---
id: mcp-tool-get-document-info
url: assembly/mcp/tools-reference/get-document-info
title: get_document_info
weight: 4
description: "The get_document_info MCP tool inspects a template or a data file before generating: format family, tag count, data names, save formats, and the shape of JSON, CSV or spreadsheet data."
keywords: get_document_info MCP, inspect data file AI agent, spreadsheet columns MCP, template info document generation
productName: GroupDocs.Assembly MCP Server
generated: true
serverVersion: 26.11.0
toc: True
---

`get_document_info` inspects a file **as a template, as data, or both**: its family, how many tags it has and the data names they use, the formats it can be saved as, and — for a data file — the shape of the data (JSON root and length, CSV columns, the tables of a spreadsheet and their columns). Example prompt: *"What columns does sales.xlsx have?"*

**Tool description (as the AI agent sees it):**

> Inspects a file before generating documents with it, as a template, as data, or both: its template family, size, how many <<…>> tags it has and the data names they use, which formats it can be saved to, and — for a data file — the shape of the data (JSON object keys or array length, CSV columns, the tables of a spreadsheet, Word or presentation document and their columns). Supports DOCX, DOC, RTF, ODT, TXT, Markdown, HTML, XLSX, XLS, ODS, PPTX, PPT, ODP, MSG, EML templates and JSON, XML, CSV, TSV data. Call it when the user asks whether a file is a template, what a data file contains, or what a template can be saved as. Do NOT pre-check whether files exist — just pass the filename the user provided; a file that cannot be found returns the list of available files instead. Returns JSON: { fileName, extension, size, family, isTemplate, tagCount, dataSourceNames[], canSaveTo[], dataKind, data }. family is one of WordProcessing, Spreadsheet, Presentation, Email, or null for a data-only file; isTemplate is null when tags cannot be read (binary DOC/XLS/PPT/MSG). On failure isError is set and the text starts with 'Document-info lookup failed for'.

## Parameters

| Name | Type | Required | Description |
|---|---|---|---|
| `file` | object | yes |  — [FileInput shape]({{< ref "assembly/mcp/tools-reference/_index.md#the-fileinput-shape" >}}) |

## Example call

```json
{
  "name": "get_document_info",
  "arguments": {
    "file": {
      "filePath": "sales.xlsx"
    }
  }
}
```

## Result

JSON — captured from server 26.11.0 (`canSaveTo` trimmed):

```json
{
  "fileName": "sales.xlsx",
  "extension": "xlsx",
  "size": 4955,
  "family": "Spreadsheet",
  "isTemplate": false,
  "tagCount": 0,
  "dataSourceNames": [],
  "canSaveTo": [ "xlsx", "xls", "ods", "html", "pdf", ... ],
  "dataKind": "table",
  "data": {
    "tableCount": 1,
    "tables": [ { "number": 1,
                  "columns": [ "Region", "Quarter", "Revenue" ] } ],
    "note": "Column names are read from each table's first row; pass
             hasHeaders=false to assemble_document when the first row is
             data. Use 'dataTable' to pick a table."
  }
}
```

For a JSON file it reports the root and its size — `customers.json` gave `"dataKind": "json", "data": { "root": "array", "length": 5 }`. For a binary template such as `.msg`, `isTemplate` and `tagCount` are `null`: the tags cannot be read without generating.

## Example prompts

* *"What columns does sales.xlsx have?"*
* *"How many records are in customers.json?"*
* *"Is this file a template, and what can I save it as?"*
