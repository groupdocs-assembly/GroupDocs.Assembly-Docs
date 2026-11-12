---
id: mcp-uc-one-document-per-record-mail-merge
url: assembly/mcp/use-cases/one-document-per-record-mail-merge
title: How to generate one document per record (mail merge) with an AI agent
linkTitle: One document per record
weight: 2
description: "Mail merge with an AI agent over MCP, locally: one letter, certificate or invoice per record of a JSON array, each file named after a field, with failed records listed instead of stopping the run."
keywords: mail merge AI agent, one document per record, generate letters per customer, bulk PDF generation locally, assemble_per_record MCP
productName: GroupDocs.Assembly MCP Server
toc: True
structuredData:
    showOrganization: True
    howTo:
        name: "How to generate one document per record (mail merge) with an AI agent"
        description: "Mail merge with an AI agent over MCP, locally: one letter, certificate or invoice per record of a JSON array, each file named after a field, with failed records listed instead of stopping the run."
        steps:
        - name: "Install the server"
          text: "Run the GroupDocs.Assembly MCP server with Docker or dnx and register it in your AI client."
        - name: "Put the documents in the storage folder"
          text: "Point GROUPDOCS_MCP_STORAGE_PATH at the folder that holds the files the agent should use."
        - name: "Ask the agent"
          text: "Write a welcome letter for every customer in customers.json, as PDFs named after the customer, and tell me which ones failed."
---

Run the GroupDocs.Assembly MCP server locally and one prompt gives you a document per record — a welcome letter per customer, a certificate per attendee, an invoice per order — each file named after a field of its record, with any bad record listed instead of stopping the run:

```bash
GROUPDOCS_MCP_STORAGE_PATH=$(pwd)/templates dnx GroupDocs.Assembly.Mcp --yes
```

> Write a welcome letter for every customer in customers.json, as PDFs named after the customer, and tell me which ones failed.

{{< alert style="info" >}}
The commands and config snippets on this page are for the **.NET** build of the server — the only platform available today. Installation and client setup: [MCP server for .NET]({{< ref "assembly/net/mcp/_index.md" >}}). Other platforms will expose the same tools with their own launch command; everything else on this page applies unchanged.
{{< /alert >}}

## Prerequisites

* The server registered in your AI client — [quick start]({{< ref "assembly/mcp/getting-started/_index.md" >}}).
* A template that speaks about **one** record (`<<[customer.Name]>>`, `<<[customer.Plan]>>`) and a JSON array of records in the storage folder.

## The calls

```text
customers.json  [ {Name:"Contoso Pharma", ...}, ... 5 records ]
        |
assemble_per_record {"template":{"filePath":"welcome-letter.docx"},
                     "data":{"filePath":"customers.json"},
                     "fileNameField":"Name","format":"pdf"}
        |
        +--> Contoso Pharma.pdf
        +--> Fabrikam Logistics.pdf
        +--> Tailspin Toys.pdf
        +--> Litware Labs.pdf
        '--> "Assembled 4 of 5 ... 1 record(s) failed: record 4: ...
              The template reads 'FirstInvoice', which the data does not have"
             (the bad record is listed; the other four are still written)
```

## What the agent sees

Captured from server 26.11.0 with five customers — the fourth has no `FirstInvoice` (the evaluation note that opens each response is trimmed):

```text
-> get_document_info {"file":{"filePath":"customers.json"}}
<- { "dataKind": "json", "data": { "root": "array", "length": 5 } }

-> get_template_fields {"template":{"filePath":"welcome-letter.docx"}}
<- { "dataSourceNames": [ "customer" ],
     "fields": [ "customer.Contact", "customer.Plan", "customer.Name",
                 "customer.Manager", "customer.FirstInvoice" ] }

-> assemble_per_record {"template":{"filePath":"welcome-letter.docx"},
     "data":{"filePath":"customers.json"},"fileNameField":"Name",
     "format":"pdf"}
<- Assembled 4 of 5 document(s) from 'welcome-letter.docx' with
   'customers.json', one per record (each record as 'customer'), as PDF.
   Saved to:
   …/Contoso Pharma.pdf
   …/Fabrikam Logistics.pdf
   …/Tailspin Toys.pdf
   …/Litware Labs.pdf
   1 record(s) failed:
   record 4: InvalidOperationException: ... Can not get the value of member
   'FirstInvoice' on type 'System.Data.DataRow'. The template reads
   'FirstInvoice', which the data does not have. ...
```

Three things to notice:

* **One record is `customer`.** The server named each record after the template's data source; no `dataSourceName` was needed.
* **The run did not stop.** Four letters were written; record 4 is listed with the field it lacks. Fix the record, or pass `allowMissingMembers: true` to print nothing there.
* **Files are named by `fileNameField`.** Without it they are numbered. A name that already exists is never overwritten: the new file gets ` (1)`.

## A safety cap

`maxDocuments` (default 100, at most 1000) refuses a run larger than you expected:

```text
-> assemble_per_record {..., "maxDocuments":3}
<- Per-record assembly failed for 'welcome-letter.docx': there are 5 records,
   more than maxDocuments=3. Raise 'maxDocuments' (up to 1000) or pass fewer
   records.
```

## Expected result

One PDF per good record in the storage folder, named after the customer, and a list of the records that failed with the reason for each.

## Troubleshooting

| Symptom | Cause | Fix |
|---|---|---|
| *"record 4: … The template reads 'FirstInvoice', which the data does not have."* | that record lacks a field | add it, or `allowMissingMembers: true` |
| *"there are 5 records, more than maxDocuments=3"* | the cap | raise `maxDocuments` |
| The array is inside an object (`{"customers":[…]}`) | the server needs to know where | `recordsPath: "customers"` |

## FAQ

**Can the records come from a CSV or a spreadsheet?** Per-record assembly reads JSON. The agent converts the rows to a JSON array first — or, for one document listing every row, use `assemble_document` with a `<<foreach>>`.

**Can each letter go out by e-mail?** Start from an e-mail template (`.eml`/`.msg`): it saves as `eml`, `emlx` or `msg`, one message file per record; sending them is a job for your mail tooling. A Word template cannot be saved as e-mail — the server answers *"a WordProcessing template cannot be saved as 'eml'"*. Unlicensed, the HTML body is replaced by the evaluation line.

**Can files be named by a nested field?** `fileNameField` reads the record itself: `Name` for the flat records above. A dotted path such as `order.Number` works only when each record nests an object; otherwise every record fails with *"the record has no 'customer.Name' field to name its file"*.

**How large can a run be?** Up to 1000 records per call with `maxDocuments`; split larger sets.

## Add to your CLAUDE.md or AGENTS.md

Agents follow project instructions about *when* to use a tool. Paste this into the instruction file your agent reads (`CLAUDE.md`, `AGENTS.md`, `.github/copilot-instructions.md`, `.cursorrules`):

```text
For one document per person/order, use groupdocs-assembly assemble_per_record
with fileNameField set to a unique field. Report failed records by number and
field; never fill missing values by guessing.
```

## Honest limits

* **Evaluation mode:** every generated document starts with an *Evaluation Only* line, workbooks gain a worksheet, and e-mail templates lose their HTML body. [Licensing]({{< ref "assembly/mcp/getting-started/licensing.md" >}}).
* **`<<[name]>>`, not `{{name}}`:** other engines' placeholders stay in the output as text.
* **Templates are trusted input:** image and document tags load the paths and URLs their expressions return.
* **Dates:** write them as `"2026-11-12T00:00:00"` and format them in the template; a date-only string can shift by a day on machines east of UTC.

## Related

* [Generate documents with AI agents]({{< ref "assembly/mcp/use-cases/generate-documents-with-ai-agents.md" >}})
* [Reports with tables and charts]({{< ref "assembly/mcp/use-cases/reports-with-tables-and-charts-from-data-files.md" >}})
* [Inspect and fix a template]({{< ref "assembly/mcp/use-cases/inspect-and-fix-a-template.md" >}})
* [From notes or email to a document]({{< ref "assembly/mcp/use-cases/build-a-document-from-data-the-agent-extracted.md" >}})
* [Reports from repository data]({{< ref "assembly/mcp/use-cases/generate-reports-from-repository-data.md" >}})
* [On-premise deployment]({{< ref "assembly/mcp/use-cases/on-premise-document-generation.md" >}})
* [Tools reference]({{< ref "assembly/mcp/tools-reference/_index.md" >}}) · [Licensing]({{< ref "assembly/mcp/getting-started/licensing.md" >}}) · [Troubleshooting & FAQ]({{< ref "assembly/mcp/troubleshooting-faq.md" >}})
* Questions: [Assembly forum](https://forum.groupdocs.com/c/assembly/15)

## Read more

* [A hundred personalised PDFs from one prompt: mail merge with an AI agent](https://blog.groupdocs.com/assembly/mail-merge-one-document-per-record-ai-agent-mcp/) — the same scenario on the GroupDocs blog, with worked examples and the trade-offs.

