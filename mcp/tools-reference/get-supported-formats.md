---
id: mcp-tool-get-supported-formats
url: assembly/mcp/tools-reference/get-supported-formats
title: get_supported_formats
weight: 5
description: "The get_supported_formats MCP tool lists the template formats GroupDocs.Assembly fills, the formats each family can be saved as, and the data formats it reads."
keywords: get_supported_formats MCP, template formats document generation, save template as PDF, data formats JSON XML CSV
productName: GroupDocs.Assembly MCP Server
generated: true
serverVersion: 26.11.0
toc: True
---

`get_supported_formats` answers *can it do that?*: the template formats per family (Word processing, Spreadsheet, Presentation, Email), what each can be saved as, and the data formats read. With a `file`, only that template's save targets. Example prompt: *"Can an Excel template be saved as PDF?"*

**Tool description (as the AI agent sees it):**

> Lists the template formats GroupDocs.Assembly fills, the formats each kind of template can be saved as, and the data formats it reads. Call it when the user asks which formats are supported, or whether a template can be saved as PDF, DOCX, HTML or another format. Returns JSON. Without 'file', the full catalog: { families: [{ family, templateFormats[], saveFormats[] }], dataFormats: [{ kind, extensions[], note }] }; with 'file', the save targets of that template: { fileName, family, saveFormats[] }. Extensions are lower-case without a dot; families are WordProcessing (including TXT, Markdown and HTML templates), Spreadsheet, Presentation and Email. Do NOT pre-check whether files exist — just pass the filename the user provided; a file that cannot be found returns the list of available files instead. On failure isError is set and the text starts with 'Supported-formats lookup failed for'.

## Parameters

| Name | Type | Required | Description |
|---|---|---|---|
| `file` | object | no | Optional template: return only the formats this template can be saved as — [FileInput shape]({{< ref "assembly/mcp/tools-reference/_index.md#the-fileinput-shape" >}}) |

## Example call

```json
{
  "name": "get_supported_formats",
  "arguments": {}
}
```

## Result

JSON — captured from server 26.11.0 (lists trimmed):

```json
{
  "families": [
    { "family": "WordProcessing",
      "templateFormats": [ "docx", "doc", "rtf", "odt", "txt", "md",
                           "html", ... ],
      "saveFormats": [ "docx", "pdf", "html", "md", "epub", "xps", ... ] },
    { "family": "Spreadsheet",
      "templateFormats": [ "xlsx", "xls", "xlsm", "ods", ... ],
      "saveFormats": [ "xlsx", "pdf", "html", "xps", ... ] },
    { "family": "Presentation", ... },
    { "family": "Email",
      "templateFormats": [ "msg", "eml", "emlx" ], ... }
  ],
  "dataFormats": [
    { "kind": "json", "extensions": [ "json" ], "note": "An object's keys
      are the names the template uses; an array is named after the
      template's data source. Also accepted inline as 'dataJson'." },
    { "kind": "xml", ... },
    { "kind": "csv", "extensions": [ "csv", "tsv" ], ... },
    { "kind": "table", "extensions": [ "xlsx", "xls", "docx", "pptx",
      ... ], "note": "A table (a worksheet for spreadsheets) of the
      document, chosen with 'dataTable'." }
  ]
}
```

The full lists: [Supported formats]({{< ref "assembly/mcp/supported-formats.md" >}}).

## Example prompts

* *"Can an Excel template be saved as PDF?"*
* *"Which data formats can I generate documents from?"*
* *"What can I save contract-template.docx as?"*
