---
id: mcp-supported-formats
url: assembly/mcp/supported-formats
title: Supported formats
weight: 4
description: "The GroupDocs.Assembly MCP server fills Word, Excel, PowerPoint, OpenDocument, Markdown, HTML, text and e-mail templates, saves them as PDF, DOCX, XLSX, PPTX, HTML, Markdown and more, and reads JSON, XML, CSV and document tables as data."
keywords: MCP server supported formats, document generation template formats, generate PDF from Word template, data formats JSON XML CSV MCP
productName: GroupDocs.Assembly MCP Server
toc: True
---

The lists below are what [`get_supported_formats`]({{< ref "assembly/mcp/tools-reference/get-supported-formats.md" >}}) returns on server 26.11.0. The library's canonical matrix: [supported document formats]({{< ref "assembly/net/getting-started/supported-document-formats.md" >}}).

## Templates and what they can be saved as

| Family | Template formats | Save formats |
|---|---|---|
| Word processing | DOCX, DOC, DOCM, DOTX, DOTM, DOT, RTF, ODT, OTT, TXT, MD, HTML, HTM, MHTML, XML, WordML | DOCX, DOC, DOCM, DOTX, DOTM, DOT, RTF, ODT, OTT, TXT, MD, HTML, MHTML, XML, WordML, **PDF**, XPS, EPUB, PS, PCL, SVG, TIFF |
| Spreadsheet | XLSX, XLS, XLSM, XLSB, XLTX, XLTM, XLT, ODS | XLSX, XLS, XLSM, XLSB, XLTX, XLTM, ODS, HTML, MHTML, XML, **PDF**, XPS, PCL, TIFF |
| Presentation | PPTX, PPT, PPTM, PPS, PPSX, PPSM, POTX, POTM, POT, ODP, OTP | PPTX, PPT, PPTM, PPS, PPSX, POTX, POT, ODP, OTP, HTML, **PDF**, XPS, TIFF |
| Email | MSG, EML, EMLX | EML, EMLX, MSG and every Word-processing save format |

## Data

| Kind | Extensions | How the template sees it |
|---|---|---|
| JSON | `.json`, or inline `dataJson` | an object's keys are the names the template uses; an array is named after the template's data source |
| XML | `.xml` | named after the template's data source |
| CSV | `.csv`, `.tsv` | one collection; first row is column names unless `hasHeaders: false`; `csvDelimiter` sets the separator |
| Document table | XLSX, XLS, XLSM, XLSB, ODS, DOCX, DOC, ODT, RTF, PPTX, PPT, ODP | a table of the document (a worksheet for spreadsheets), chosen with `dataTable` |

**Three rules that explain most results**

* **Text templates can be inspected; binary ones cannot.** DOCX, XLSX, PPTX, Markdown, HTML and EML templates are read by [`get_template_fields`]({{< ref "assembly/mcp/tools-reference/get-template-fields.md" >}}); DOC, XLS, PPT and MSG templates are not — generate them with `inlineErrors: true` to see their problems, and pass `dataSourceName` with array, CSV or table data.
* **Markdown and HTML are templates too.** `product-readme.md` with `<<[product]>>` tags generated a DOCX in our tests; a Markdown template can be saved as any Word-processing format.
* **E-mail output needs a license to look right.** In evaluation mode the HTML body of an e-mail template is replaced by the evaluation line.
