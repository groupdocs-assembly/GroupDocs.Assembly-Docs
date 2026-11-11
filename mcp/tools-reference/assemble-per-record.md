---
id: mcp-tool-assemble-per-record
url: assembly/mcp/tools-reference/assemble-per-record
title: assemble_per_record
weight: 3
description: "The assemble_per_record MCP tool performs a mail merge: one document per record of a JSON array — a letter per customer, a certificate per attendee — named by a record field, with failed records listed instead of stopping the run."
keywords: assemble_per_record MCP tool, mail merge AI agent, one document per record, generate letters per customer, bulk PDF generation MCP
productName: GroupDocs.Assembly MCP Server
generated: true
serverVersion: 26.11.0
toc: True
---

`assemble_per_record` is a **mail merge**: it fills the same template once for every element of a JSON array and saves each result as its own file, named by a record field (`fileNameField`) or a running number. A bad record is listed, the rest are still written. Example prompt: *"Write a welcome letter for every customer in customers.json, as PDFs named after the customer."*

**Tool description (as the AI agent sees it):**

> Generates one document per record — a mail merge: a letter per customer, a certificate per attendee, an invoice per order — by filling the same template once for every element of a JSON array, and saves each result as its own file. Use it when the user wants separate documents for each row or record; use assemble_document for one document that lists all records. Templates: DOCX, DOC, RTF, ODT, TXT, Markdown, HTML, XLSX, PPTX, MSG, EML and more. Data: 'dataJson' (inline) or 'data' (a .json file) holding an array of objects, or an object with the array under 'recordsPath' (found automatically when the object has exactly one array). Each record is the template's data for one document: its keys are the names the template uses (<<[Name]>>), or name the record with 'dataSourceName' (<<[customer.Name]>> → 'customer'; worked out from the template when omitted). Files are named '<template>_<n>.<ext>', or after a record field with 'fileNameField'. At most 'maxDocuments' records (default 100, up to 1000). Do NOT pre-check whether files exist — just pass the filename the user provided; a file that cannot be found returns the list of available files instead. Returns 'Assembled N of M document(s) …' followed by one saved path per line, and the record number and reason for any record that failed. On failure isError is set and the text starts with 'Per-record assembly failed for'.

## Parameters

| Name | Type | Required | Description |
|---|---|---|---|
| `template` | object | yes | The template document (DOCX, XLSX, PPTX, Markdown, HTML, TXT, MSG, EML, …) containing <<…>> tags — [FileInput shape]({{< ref "assembly/mcp/tools-reference/_index.md#the-fileinput-shape" >}}) |
| `dataJson` | string | no | The records as inline JSON: an array of objects, or an object holding the array. Use this OR 'data' |
| `data` | object | no | The records as a .json file: an array of objects, or an object holding the array. Use this OR 'dataJson' — [FileInput shape]({{< ref "assembly/mcp/tools-reference/_index.md#the-fileinput-shape" >}}) |
| `recordsPath` | string | no | Where the array is when the JSON is an object, as a dotted path (e.g. 'customers' or 'batch.items'). Default: its only array |
| `dataSourceName` | string | no | The name the template uses for one record (e.g. 'customer' in <<[customer.Name]>>). Default: worked out from the template |
| `fileNameField` | string | no | A record field whose value names each output file (e.g. 'InvoiceNumber' or 'customer.Name'). Default: a running number |
| `format` | string | no | Output format extension (default: the template's own), e.g. 'pdf', 'docx', 'eml' |
| `maxDocuments` | integer | no | Refuse to run when there are more records than this (default 100, at most 1000) |
| `allowMissingMembers` | boolean | no | Treat fields missing from a record as empty instead of failing that record (default false) |
| `removeEmptyParagraphs` | boolean | no | Remove paragraphs that become empty after tags are replaced (default false) |
| `updateFields` | boolean | no | Update fields (page numbers, tables of contents) and spreadsheet formulas in each result (default false) |

## Example call

```json
{
  "name": "assemble_per_record",
  "arguments": {
    "template": {
      "filePath": "welcome-letter.docx"
    },
    "data": {
      "filePath": "customers.json"
    },
    "fileNameField": "Name",
    "format": "pdf"
  }
}
```

## Result

Captured from server 26.11.0 with five customers, one of them missing `FirstInvoice` (evaluation note trimmed; the server prints full paths inside your storage folder):

```text
Assembled 4 of 5 document(s) from 'welcome-letter.docx' with
'customers.json', one per record (each record as 'customer'), as PDF.
Saved to:
…/Contoso Pharma.pdf
…/Fabrikam Logistics.pdf
…/Tailspin Toys.pdf
…/Litware Labs.pdf
1 record(s) failed:
record 4: InvalidOperationException: An error has been encountered at the
end of expression 'customer.FirstInvoice]>'. Can not get the value of member
'FirstInvoice' on type 'System.Data.DataRow'. The template reads
'FirstInvoice', which the data does not have. ...
```

(Wrapped for width; the record message continues with the same hint as `assemble_document`.)

* **One record = one data name.** The server names each record after the template's data source (`customer` in `<<[customer.Name]>>`); override with `dataSourceName`.
* **Arrays inside an object:** pass `recordsPath` (`"contributors"`, `"batch.items"`).
* **A safety cap:** `maxDocuments` (default 100, at most 1000) refuses larger runs — *"Per-record assembly failed for 'welcome-letter.docx': there are 5 records, more than maxDocuments=3. Raise 'maxDocuments' (up to 1000) or pass fewer records."*
* **JSON only.** For CSV or spreadsheet rows, the agent converts them to a JSON array first — or use one `<<foreach>>` document with [`assemble_document`]({{< ref "assembly/mcp/tools-reference/assemble-document.md" >}}).

## Example prompts

* *"Write a welcome letter for every customer in customers.json, as PDFs named after the customer."*
* *"One certificate per contributor in data/contributors-2026.json."*
* *"Make an invoice for each order in orders.json and tell me which ones failed."*

See it used end-to-end: [One document per record (mail merge)]({{< ref "assembly/mcp/use-cases/one-document-per-record-mail-merge.md" >}}).
