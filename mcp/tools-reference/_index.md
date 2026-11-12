---
id: mcp-tools-reference
url: assembly/mcp/tools-reference
title: Tools reference
weight: 2
description: "Complete reference of every tool the GroupDocs.Assembly MCP server exposes to AI agents, with parameters, example prompts, and results."
keywords: MCP tools document generation, assemble_document MCP tool, get_template_fields, mail merge MCP tool, template engine tools for AI agents
productName: GroupDocs.Assembly MCP Server
generated: true
serverVersion: 26.11.0
toc: True
---

Complete reference of every tool the GroupDocs.Assembly MCP server exposes to AI agents, with parameters, example prompts, and results. Captured from a live `tools/list` call against server version **26.11.0** (raw capture: `tools-list.generated.json` in this section's source).

| Tool | What it does |
|---|---|
| [`get_template_fields`]({{< ref "assembly/mcp/tools-reference/get-template-fields.md" >}}) | Lists a template's tags, the data names it uses, and a JSON skeleton of the data to fill |
| [`assemble_document`]({{< ref "assembly/mcp/tools-reference/assemble-document.md" >}}) | Fills a template with data (inline JSON, or a JSON/XML/CSV/spreadsheet file) and saves the document |
| [`assemble_per_record`]({{< ref "assembly/mcp/tools-reference/assemble-per-record.md" >}}) | Mail merge: one document per record of a JSON array, named by a record field |
| [`get_document_info`]({{< ref "assembly/mcp/tools-reference/get-document-info.md" >}}) | Inspects a template or a data file: family, tags, data names, data shape, save formats |
| [`get_supported_formats`]({{< ref "assembly/mcp/tools-reference/get-supported-formats.md" >}}) | Lists template formats, the formats each can be saved as, and the data formats read |
| [`get_license_status`]({{< ref "assembly/mcp/tools-reference/get-license-status.md" >}}) | Reports the active licensing mode and, under metered licensing, consumption |

## How the tools address templates and data

Templates and data files are **names in the storage folder** (or inline content). The data can also be inline JSON the agent writes itself:

| Argument | Shape | Example |
|---|---|---|
| `template` | a FileInput — the document with `<<…>>` tags | `{ "filePath": "contract-template.docx" }` |
| `dataJson` | inline JSON: an object whose keys are the template's data names, or an array | `"{\"customer\":{\"Name\":\"Contoso Pharma\"}}"` |
| `data` | a FileInput — `.json`, `.xml`, `.csv`/`.tsv`, or a spreadsheet, Word or presentation **table** | `{ "filePath": "sales.xlsx" }` |
| `dataSourceName` | the name the template uses for the data, when the server cannot work it out | `"ds"` in `<<foreach [c in ds]>>` |
| `recordsPath` | per-record only: where the array sits inside a JSON object | `"contributors"` |
| `file` | a FileInput — any template or data file to inspect | `{ "filePath": "customers.json" }` |

Pass **either** `dataJson` **or** `data`, not both. How the template sees the data:

```text
data you give            what the template sees                how to name it
-----------------------  ------------------------------------  ----------------
JSON object              its keys: contract, customer, items   nothing to do
JSON array / XML / CSV   one collection                        worked out from
spreadsheet / Word table   (columns are the members)             the template, or
                                                                 dataSourceName
"2026-11-12T00:00:00"    a date - format it in the template    <<[d]:"d MMMM yyyy">>
{{name}} in a template   left as text - not Assembly syntax    use <<[name]>>
```

**Output names.** `assemble_document` writes `<template>_assembled.<ext>` unless you pass `outputName`; `format` picks the extension (`pdf`, `docx`, `html`, `md`, `xlsx`, `pptx`, `eml`…; default: the template's own). `assemble_per_record` writes one file per record, named by `fileNameField` (`Contoso Pharma.pdf`) or by a running number. Files are written to the storage folder (or `GROUPDOCS_MCP_OUTPUT_PATH`); the template and the data are never modified, and an existing file is never replaced — a second run with the same name writes `<name> (1).<ext>`.

**Dates in JSON data.** Write them as ISO **with a time** — `"2026-11-12T00:00:00"` — and format them in the template: `<<[contract.Date]:"d MMMM yyyy">>` prints *12 November 2026*. Two traps, both seen on server 26.11.0: a date-only string (`"2026-11-12"`) is read as a date and shifted by the machine's UTC offset — on a UTC+2 machine it printed as **11 November**, even with a format string — and `"12.11.2026"` is read month-first, as 11 December. An unformatted date prints like `11/12/2026 12:00:00 AM`. The Docker image runs in UTC.

## The FileInput shape

`template`, `data` and `file` all take the same object — pass **either** a name from your storage folder **or** inline content:

```json
{ "template": { "filePath": "contract-template.docx" } }
```

| Field | Type | Description |
|---|---|---|
| `filePath` | string | File path or name in the configured storage folder (sub-folders work: `templates/release-notes.docx`) |
| `fileContent` | string | Base64-encoded file content (alternative to `filePath`) |
| `fileName` | string | Original filename with extension — required with `fileContent`; on its own it is resolved from the storage folder like `filePath` |

A name that is not found returns the list of files the server can see, so the agent can correct itself.

## The template language in one table

| In the template | Does | Example |
|---|---|---|
| `<<[expr]>>` | prints a value | `<<[customer.Name]>>` |
| `<<[expr]:"format">>` | prints a formatted date or number | `<<[contract.Date]:"d MMMM yyyy">>` |
| `<<foreach [x in list]>>…<</foreach>>` | repeats a block — or a table row, when the tags open in the first cell and close in the last | `<<foreach [item in items]>><<[item.Title]>>` |
| `<<if [cond]>>…<</if>>` | conditional content | `<<if [contract.Discount > 0]>>A discount applies.<</if>>` |
| `<<[list.Sum(i => …)]>>` | LINQ-style aggregates | `<<[items.Sum(i => i.Quantity * i.UnitPrice)]>>` |
| chart title `<<foreach [r in sales]>><<x [r.Region]>>`, series name `<<y [r.Revenue]>>` | fills a chart | see [reports with charts]({{< ref "assembly/mcp/use-cases/reports-with-tables-and-charts-from-data-files.md" >}}) |
| `<<image […]>>`, `<<barcode […]>>`, `<<doc […]>>` | images, barcodes, inserted documents | the library's [template syntax]({{< ref "assembly/net/developer-guide/basic-usage/working-with-groupdocs.assembly-engine/template-syntax-part-2-of-2.md" >}}) |

`{{name}}` is **not** Assembly syntax: it stays in the output as text, and [`get_template_fields`]({{< ref "assembly/mcp/tools-reference/get-template-fields.md" >}}) says so. The full grammar: [template syntax, part 1]({{< ref "assembly/net/developer-guide/basic-usage/working-with-groupdocs.assembly-engine/template-syntax-part-1-of-2.md" >}}) and [part 2]({{< ref "assembly/net/developer-guide/basic-usage/working-with-groupdocs.assembly-engine/template-syntax-part-2-of-2.md" >}}).
