---
id: mcp-uc-build-a-document-from-data-the-agent-extracted
url: assembly/mcp/use-cases/build-a-document-from-data-the-agent-extracted
title: How to turn notes or an email into a finished document with an AI agent
linkTitle: From notes to document
weight: 5
description: "Turn an email, meeting notes or a pasted order into a finished contract or invoice with an AI agent over MCP, locally: the agent extracts the data into the template's skeleton, the engine renders the document."
keywords: turn email into contract AI, generate invoice from order email, notes to document AI agent, structured data extraction to template, fill template from text
productName: GroupDocs.Assembly MCP Server
toc: True
structuredData:
    showOrganization: True
    howTo:
        name: "How to turn notes or an email into a finished document with an AI agent"
        description: "Turn an email, meeting notes or a pasted order into a finished contract or invoice with an AI agent over MCP, locally: the agent extracts the data into the template's skeleton, the engine renders the document."
        steps:
        - name: "Install the server"
          text: "Run the GroupDocs.Assembly MCP server with Docker or dnx and register it in your AI client."
        - name: "Put the documents in the storage folder"
          text: "Point GROUPDOCS_MCP_STORAGE_PATH at the folder that holds the files the agent should use."
        - name: "Ask the agent"
          text: "Here is the order from Contoso Pharma's email. Make the service agreement SA-2026-118 from contract-template.docx and save it as SA-2026-118-contoso.docx."
---

Paste an order, an email or meeting notes, and your agent turns them into a finished document: it extracts the facts into the template's data skeleton, and the GroupDocs.Assembly MCP server — running locally — renders the contract. If the agent forgets a field, the server says which one:

```bash
dnx GroupDocs.Assembly.Mcp --yes
```

> Here is the order from Contoso Pharma's email. Make the service agreement SA-2026-118 from contract-template.docx and save it as SA-2026-118-contoso.docx.

{{< alert style="info" >}}
The commands and config snippets on this page are for the **.NET** build of the server — the only platform available today. Installation and client setup: [MCP server for .NET]({{< ref "assembly/net/mcp/_index.md" >}}). Other platforms will expose the same tools with their own launch command; everything else on this page applies unchanged.
{{< /alert >}}

## Prerequisites

* The server registered in your AI client — [quick start]({{< ref "assembly/mcp/getting-started/_index.md" >}}).
* A template whose fields match what the documents usually say — see [generate documents with AI agents]({{< ref "assembly/mcp/use-cases/generate-documents-with-ai-agents.md" >}}).

## The calls

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

## What the agent sees

The email gave the services, the customer and the contact, but not the contact's e-mail address — so the agent's first data had no `customer.Email`. Captured from server 26.11.0 (the evaluation note that opens each response is trimmed):

```text
-> get_template_fields {"template":{"filePath":"contract-template.docx"}}
<- { "fields": [ "contract.Number", "contract.Date", "contract.Discount",
     "customer.Name", "customer.Address", "customer.Contact",
     "customer.Email", "items[].Title", "items[].Quantity",
     "items[].UnitPrice" ], "dataSkeleton": { ... } }

-> assemble_document {"template":{"filePath":"contract-template.docx"},
     "dataJson":"<order without customer.Email>"}
<- Document assembly failed for 'contract-template.docx': ... Can not get the
   value of member 'Email' on type ''. ... The template reads 'Email', which
   the data does not have. Check the spelling (names are case-sensitive) with
   get_template_fields and add it to the data. A list that is empty in the
   data has no fields at all, so reading one fails too; pass
   allowMissingMembers=true to output nothing for missing members and empty
   lists.

-> assemble_document {"template":{"filePath":"contract-template.docx"},
     "dataJson":"<order with customer.Email>",
     "outputName":"SA-2026-118-contoso.docx"}
<- Assembled 'contract-template.docx' with inline JSON (JSON object) as DOCX
   Saved to: …/SA-2026-118-contoso.docx
```

The right move after the failure is **to ask you** for the address, not to invent one — say so in your agent instructions (below). `allowMissingMembers: true` is for fields that may legitimately be empty, not for facts the agent could not find.

## Expected result

`SA-2026-118-contoso.docx` with the customer block, three service rows, the total of 75500 EUR and the discount line — and, before it, a JSON object you can read in ten seconds to check what the agent extracted.

## Troubleshooting

| Symptom | Cause | Fix |
|---|---|---|
| *"The template reads 'Email', which the data does not have."* | the source text did not contain it | ask the user; add the field |
| A number printed as text with a currency sign | the agent copied `"4,800 EUR"` into a numeric field | numbers in the skeleton are numbers — tell the agent to keep them numeric |
| A date one day early | `"2026-11-12"` on a machine east of UTC | `"2026-11-12T00:00:00"` |

## FAQ

**Is the extraction reliable?** It is the model's reading of your text; that is why the data is a small JSON object you can review before the document exists. The layout and the arithmetic are not the model's — the template does those.

**Can it read the email file itself?** Your agent reads it with its own tools (or another GroupDocs server, such as [Parser](https://docs.groupdocs.com/parser/mcp/)). This server takes the data the agent produced.

**Does the email leave my machine?** The server reads nothing but the template and writes the document locally. What you paste into the conversation goes to your model provider, as always.

## Add to your CLAUDE.md or AGENTS.md

Agents follow project instructions about *when* to use a tool. Paste this into the instruction file your agent reads (`CLAUDE.md`, `AGENTS.md`, `.github/copilot-instructions.md`, `.cursorrules`):

```text
When asked to turn notes or an email into a document: call get_template_fields,
fill the dataSkeleton only with facts present in the source, show me the JSON,
and ask for anything missing instead of using allowMissingMembers or guessing.
```

## Honest limits

* **Evaluation mode:** every generated document starts with an *Evaluation Only* line, workbooks gain a worksheet, and e-mail templates lose their HTML body. [Licensing]({{< ref "assembly/mcp/getting-started/licensing.md" >}}).
* **`<<[name]>>`, not `{{name}}`:** other engines' placeholders stay in the output as text.
* **Templates are trusted input:** image and document tags load the paths and URLs their expressions return.
* **Dates:** write them as `"2026-11-12T00:00:00"` and format them in the template; a date-only string can shift by a day on machines east of UTC.

## Related

* [Generate documents with AI agents]({{< ref "assembly/mcp/use-cases/generate-documents-with-ai-agents.md" >}})
* [One document per record (mail merge)]({{< ref "assembly/mcp/use-cases/one-document-per-record-mail-merge.md" >}})
* [Reports with tables and charts]({{< ref "assembly/mcp/use-cases/reports-with-tables-and-charts-from-data-files.md" >}})
* [Inspect and fix a template]({{< ref "assembly/mcp/use-cases/inspect-and-fix-a-template.md" >}})
* [Reports from repository data]({{< ref "assembly/mcp/use-cases/generate-reports-from-repository-data.md" >}})
* [On-premise deployment]({{< ref "assembly/mcp/use-cases/on-premise-document-generation.md" >}})
* [Tools reference]({{< ref "assembly/mcp/tools-reference/_index.md" >}}) · [Licensing]({{< ref "assembly/mcp/getting-started/licensing.md" >}}) · [Troubleshooting & FAQ]({{< ref "assembly/mcp/troubleshooting-faq.md" >}})
* Questions: [Assembly forum](https://forum.groupdocs.com/c/assembly/15)

## Read more

* [Let the model fill in the data, not write the document](https://blog.groupdocs.com/assembly/let-the-model-fill-the-data-not-write-the-document-mcp/) — the same scenario on the GroupDocs blog, with worked examples and the trade-offs.

