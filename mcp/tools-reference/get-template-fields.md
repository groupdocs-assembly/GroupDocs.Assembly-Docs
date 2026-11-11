---
id: mcp-tool-get-template-fields
url: assembly/mcp/tools-reference/get-template-fields
title: get_template_fields
weight: 1
description: "The get_template_fields MCP tool lists a document template's tags, the data names it uses and a JSON skeleton of the data to fill, so an AI agent knows exactly what to supply — without generating anything."
keywords: get_template_fields MCP tool, what fields does a template need, template data schema AI, JSON skeleton from Word template
productName: GroupDocs.Assembly MCP Server
generated: true
serverVersion: 26.11.0
toc: True
---

`get_template_fields` reads a template and tells the agent **what data it needs**: every `<<…>>` tag, the data names (`contract`, `customer`, `items`), the fields it reads, and a **JSON skeleton** to fill in and pass to [`assemble_document`]({{< ref "assembly/mcp/tools-reference/assemble-document.md" >}}) as `dataJson`. Nothing is generated. Example prompt: *"What data does contract-template.docx need?"*

**Tool description (as the AI agent sees it):**

> Lists what a template needs before generating a document from it: every <<…>> tag, the names it uses for its data, the fields it reads, and a JSON skeleton of the data to fill in and pass to assemble_document as 'dataJson'. Use it when the user asks what data a template expects, or before calling assemble_document with data you have to build. Reads DOCX, DOTX, DOCM, RTF, ODT, TXT, Markdown, HTML, XLSX, XLTX, ODS, PPTX, POTX, ODP and EML templates; binary DOC, XLS, PPT and MSG templates cannot be read without generating them (readable=false). Processes no data and does not run the engine. Do NOT pre-check whether files exist — just pass the filename the user provided; a file that cannot be found returns the list of available files instead. Returns JSON: { fileName, family, readable, tagCount, dataSourceNames[], fields[], dataSkeleton, tags: [{ tag, kind, part }], tagsTruncated, notes[] }. fields use '[]' for lists ('customers[].Name'). The skeleton is inferred from the tags; check it against your data. On failure isError is set and the text starts with 'Template inspection failed for'.

## Parameters

| Name | Type | Required | Description |
|---|---|---|---|
| `template` | object | yes | The template document to inspect — [FileInput shape]({{< ref "assembly/mcp/tools-reference/_index.md#the-fileinput-shape" >}}) |

## Example call

```json
{
  "name": "get_template_fields",
  "arguments": {
    "template": {
      "filePath": "contract-template.docx"
    }
  }
}
```

## Result

JSON — captured from server 26.11.0 (the `tags` array is trimmed to its first entries):

```json
{
  "fileName": "contract-template.docx",
  "family": "WordProcessing",
  "readable": true,
  "tagCount": 17,
  "dataSourceNames": [ "contract", "customer", "items" ],
  "fields": [ "contract.Number", "contract.Date", "contract.Discount",
              "customer.Name", "customer.Address", "customer.Contact",
              "customer.Email",
              "items[].Title", "items[].Quantity", "items[].UnitPrice" ],
  "dataSkeleton": {
    "contract": { "Number": "", "Date": "", "Discount": "" },
    "customer": { "Name": "", "Address": "", "Contact": "", "Email": "" },
    "items": [ { "Title": "", "Quantity": 0, "UnitPrice": 0 } ]
  },
  "tags": [
    { "tag": "<<[contract.Number]>>", "kind": "expression", "part": "body" },
    { "tag": "<<foreach [item in items]>>", "kind": "foreach", "part": "body" },
    ...
  ],
  "tagsTruncated": false,
  "notes": [ "fields and dataSkeleton are inferred from the tags, not from
              the engine; values computed by Select/GroupBy projections are
              not followed." ]
}
```

| Field | Meaning |
|---|---|
| `readable` | `false` for binary templates (`.msg`, `.doc`, `.xls`, `.ppt`) — their tags cannot be read without generating |
| `dataSourceNames` | the top-level names the data must provide |
| `fields` | every member read; `items[].Title` means *a list of objects with `Title`* |
| `dataSkeleton` | the data shape to fill — numbers where the template does arithmetic |
| `notes` | what the inference could not see, and syntax problems such as `{{…}}` placeholders |

On a document with `{{…}}` placeholders, `tagCount` is 0 and a note says *"The template contains 2 '{{…}}' placeholder(s). GroupDocs.Assembly does not process that syntax and leaves it as text; write <<[name]>> instead."* It inspects tags statically: an unclosed `<<foreach>>` is still listed — the engine reports it when you generate.

## Example prompts

* *"What data does contract-template.docx need?"*
* *"Give me the JSON I have to fill for this template."*
* *"Why does this template not fill in? Check its placeholders."*

See it used end-to-end: [Inspect and fix a template]({{< ref "assembly/mcp/use-cases/inspect-and-fix-a-template.md" >}}).
