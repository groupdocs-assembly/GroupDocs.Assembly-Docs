---
id: mcp-uc-generate-documents-with-ai-agents
url: assembly/mcp/use-cases/generate-documents-with-ai-agents
title: How to generate documents from templates with AI agents using MCP
linkTitle: Generate with AI agents
weight: 1
description: "Generate contracts, invoices and letters from Word, Excel or PowerPoint templates with an AI agent over MCP, locally: the agent fills the template's data, the engine renders the document."
keywords: generate documents from template AI agent, MCP document generation, fill Word template with JSON, Claude generate contract PDF, template engine for AI agents
productName: GroupDocs.Assembly MCP Server
toc: True
structuredData:
    showOrganization: True
    howTo:
        name: "How to generate documents from templates with AI agents using MCP"
        description: "Generate contracts, invoices and letters from Word, Excel or PowerPoint templates with an AI agent over MCP, locally: the agent fills the template's data, the engine renders the document."
        steps:
        - name: "Install the server"
          text: "Run the GroupDocs.Assembly MCP server with Docker or dnx and register it in your AI client."
        - name: "Put the documents in the storage folder"
          text: "Point GROUPDOCS_MCP_STORAGE_PATH at the folder that holds the files the agent should use."
        - name: "Ask the agent"
          text: "What data does contract-template.docx need? Fill it for Contoso Pharma with the three services below and save it as a PDF."
---

Run the GroupDocs.Assembly MCP server locally and your agent can turn a template plus a few facts into a finished document — it asks the template what data it needs, fills that in, and the engine renders the contract, invoice or letter. Nothing is uploaded:

```bash
dnx GroupDocs.Assembly.Mcp --yes
```

> What data does contract-template.docx need? Fill it for Contoso Pharma with the three services below and save it as a PDF.

{{< alert style="info" >}}
The commands and config snippets on this page are for the **.NET** build of the server — the only platform available today. Installation and client setup: [MCP server for .NET]({{< ref "assembly/net/mcp/_index.md" >}}). Other platforms will expose the same tools with their own launch command; everything else on this page applies unchanged.
{{< /alert >}}

## Prerequisites

* The .NET 10 SDK (or Docker) and the server registered in your AI client — [quick start]({{< ref "assembly/mcp/getting-started/_index.md" >}}).
* A template with `<<…>>` tags in the storage folder (`GROUPDOCS_MCP_STORAGE_PATH`). The one below has a header, a services table that repeats per item, a total and a conditional discount line:

```text
Service Agreement <<[contract.Number]>>
Date: <<[contract.Date]:"d MMMM yyyy">>
Customer: <<[customer.Name]>>, <<[customer.Address]>>
| <<foreach [item in items]>><<[item.Title]>> | <<[item.Quantity]>> | ...
|   <<[item.UnitPrice]>> | <<[item.Quantity * item.UnitPrice]>><</foreach>> |
Total: <<[items.Sum(i => i.Quantity * i.UnitPrice)]>> EUR
<<if [contract.Discount > 0]>>A discount of <<[contract.Discount]>> percent
applies.<</if>>
```

## The pattern

```text
user              agent                        Assembly MCP server
 |  "Make the contract for this order: Contoso Pharma, 12 months ..."  |
 |---------------->|                                                   |
 |                 |-- get_template_fields ------------------------->|
 |                 |   {"template":{"filePath":                        |
 |                 |     "contract-template.docx"}}                    |
 |                 |<- {"dataSourceNames":["contract","customer",      |
 |                 |    "items"], "dataSkeleton":{"customer":{"Name":  |
 |                 |    ""...}, "items":[{"Title":"","Quantity":0}]}} -|
 |                 |   the agent fills the skeleton from the order     |
 |                 |-- assemble_document --------------------------->|
 |                 |   {"template":{...},"dataJson":"{...}",           |
 |                 |    "format":"pdf"}                                |
 |                 |<- "Assembled 'contract-template.docx' with inline |
 |                 |    JSON (JSON object) as PDF" --------------------|
 |<- "Contract SA-2026-118 is ready: 3 services, total 75500 EUR."     |
   the model writes the data; layout, tables and wording come from the template
```

1. **Ask the template** — [`get_template_fields`]({{< ref "assembly/mcp/tools-reference/get-template-fields.md" >}}) returns the data names and a JSON skeleton.
2. **Fill the data** — the agent writes the skeleton's values from your message.
3. **Render** — [`assemble_document`]({{< ref "assembly/mcp/tools-reference/assemble-document.md" >}}) fills the template and saves the document.

## What the agent sees

Captured from server 26.11.0 (the evaluation note that opens each response is trimmed):

```text
-> get_template_fields {"template":{"filePath":"contract-template.docx"}}
<- { "tagCount": 17,
     "dataSourceNames": [ "contract", "customer", "items" ],
     "dataSkeleton": {
       "contract": { "Number": "", "Date": "2026-01-31T00:00:00",
                      "Discount": "" },
       "customer": { "Name": "", "Address": "", "Contact": "", "Email": "" },
       "items": [ { "Title": "", "Quantity": 0, "UnitPrice": 0 } ] } }

-> assemble_document {"template":{"filePath":"contract-template.docx"},
                      "dataJson":"<the filled skeleton>","format":"pdf"}
<- Assembled 'contract-template.docx' with inline JSON (JSON object) as PDF
   Saved to: …/contract-template_assembled.pdf
```

The data the agent passed:

```json
{"contract":{"Number":"SA-2026-118","Date":"2026-11-12T00:00:00",
             "Discount":5},
 "customer":{"Name":"Contoso Pharma","Address":"Keizersgracht 210, Amsterdam",
             "Contact":"Dr. Lena Brandt",
             "Email":"lena.brandt@contoso.example"},
 "items":[{"Title":"Managed hosting","Quantity":12,"UnitPrice":4800},
          {"Title":"24/7 support","Quantity":12,"UnitPrice":1200},
          {"Title":"Onboarding workshop","Quantity":1,"UnitPrice":3500}]}
```

The skeleton seeds `contract.Date` with a sample ISO date **with a time**, because the template formats it as a date — keep that shape. The server prints the full path inside your storage folder; it is shortened here.

## Expected result

`contract-template_assembled.pdf`: the services table has three rows (57600, 14400 and 3500 EUR), the total reads **75500 EUR**, the discount line appears because `Discount` is 5, and the date reads *12 November 2026*. In evaluation mode the first line of the document is *"Evaluation Only. Created with GroupDocs.Assembly 26.7…"*.

## Troubleshooting

| Symptom | Cause | Fix |
|---|---|---|
| *"Can not get the value of member 'Email' … The template reads 'Email', which the data does not have."* | a field missing from the data (names are case-sensitive) | add it, or `allowMissingMembers: true` |
| `{{name}}` printed as is | not Assembly syntax | write `<<[name]>>` — `get_template_fields` flags it |
| A date one day early | a date-only ISO string on a machine east of UTC | `"2026-11-12T00:00:00"` and a format in the template |

## FAQ

**Can the agent change the layout?** Not through this server — and that is the point. Change the template in Word, Excel or PowerPoint; the next run uses it.

**Which output formats?** The template's own, or any save format of its family — PDF for every family; HTML and Markdown for Word templates. See [supported formats]({{< ref "assembly/mcp/supported-formats.md" >}}).

**Do I need to write the JSON myself?** No. The agent writes it from the skeleton; you check the values.

## Add to your CLAUDE.md or AGENTS.md

Agents follow project instructions about *when* to use a tool. Paste this into the instruction file your agent reads (`CLAUDE.md`, `AGENTS.md`, `.github/copilot-instructions.md`, `.cursorrules`):

```text
To produce a contract, invoice or letter, never write the document yourself:
call get_template_fields on the template in ./templates, fill its dataSkeleton
from the user's facts, then assemble_document with dataJson. Show the data first.
```

## Honest limits

* **Evaluation mode:** every generated document starts with an *Evaluation Only* line, workbooks gain a worksheet, and e-mail templates lose their HTML body. [Licensing]({{< ref "assembly/mcp/getting-started/licensing.md" >}}).
* **`<<[name]>>`, not `{{name}}`:** other engines' placeholders stay in the output as text.
* **Templates are trusted input:** image and document tags load the paths and URLs their expressions return.
* **Dates:** write them as `"2026-11-12T00:00:00"` and format them in the template; a date-only string can shift by a day on machines east of UTC.

## Related

* [One document per record (mail merge)]({{< ref "assembly/mcp/use-cases/one-document-per-record-mail-merge.md" >}})
* [Reports with tables and charts]({{< ref "assembly/mcp/use-cases/reports-with-tables-and-charts-from-data-files.md" >}})
* [Inspect and fix a template]({{< ref "assembly/mcp/use-cases/inspect-and-fix-a-template.md" >}})
* [From notes or email to a document]({{< ref "assembly/mcp/use-cases/build-a-document-from-data-the-agent-extracted.md" >}})
* [Reports from repository data]({{< ref "assembly/mcp/use-cases/generate-reports-from-repository-data.md" >}})
* [On-premise deployment]({{< ref "assembly/mcp/use-cases/on-premise-document-generation.md" >}})
* [Tools reference]({{< ref "assembly/mcp/tools-reference/_index.md" >}}) · [Licensing]({{< ref "assembly/mcp/getting-started/licensing.md" >}}) · [Troubleshooting & FAQ]({{< ref "assembly/mcp/troubleshooting-faq.md" >}})
* Questions: [Assembly forum](https://forum.groupdocs.com/c/assembly/15)

## Read more

* [Let the model fill in the data, not write the document](https://blog.groupdocs.com/assembly/let-the-model-fill-the-data-not-write-the-document-mcp/) — the same scenario on the GroupDocs blog, with worked examples and the trade-offs.

