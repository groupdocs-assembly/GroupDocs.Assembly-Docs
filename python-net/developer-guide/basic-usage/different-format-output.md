---
id: assembly-basic-usage-different-format-output
url: assembly/python-net/basic-usage-different-format-output
linktitle: Generate Output in Different Format
title: Generate Output in Different Format
weight: 13
description: "Save documents assembled in Python in a different format than the template (DOCX to PDF, DOCX to HTML, XLSX to PDF), by file extension or with LoadSaveOptions."
keywords: format conversion, PDF output, HTML output, XPS output, convert format, change format, output format, DOCX to PDF, LoadSaveOptions, Python
productName: GroupDocs.Assembly for Python via .NET
hideChildren: False
---

## Overview

GroupDocs.Assembly for Python via .NET allows you to generate output documents in a different format than the template. For example, you can create a DOCX template but output a PDF, or create an XLSX template but output a PDF. With file paths, the output format is determined by the file extension of the output path; with streams, [LoadSaveOptions](https://reference.groupdocs.com/assembly/python-net/groupdocs.assembly/loadsaveoptions/) names it.

The main class involved is:
- [DocumentAssembler](https://reference.groupdocs.com/assembly/python-net/groupdocs.assembly/documentassembler/) - assembles documents and converts to output format

Here are the steps to generate output in a different format:

* Create a template document in one format (e.g., DOCX)
* Specify an output path with a different file extension (e.g., .pdf, .html)
* Assemble the document using DocumentAssembler
* The output will be automatically converted to the specified format

{{< alert style="info" >}}
Format conversion is automatic based on the output file extension. Supported conversions depend on the template format - Word templates can convert to PDF, HTML, and more, while spreadsheet templates have more limited conversion options.
{{< /alert >}}

## Convert DOCX Template to PDF

Generate a PDF from a Word template:

{{< tabs "example1" >}}
{{< tab "Python" >}}
```python
from datetime import datetime
from decimal import Decimal

from groupdocs.assembly import DataSourceInfo, DocumentAssembler

# DOCX template, PDF output
template_path = "customer-invoice.docx"
output_path = "customer-invoice-report.pdf"

invoice_data = {
    "CustomerName": "Quayside Bistro",
    "Amount": Decimal("552.00"),
    "Date": datetime(2015, 1, 14),
}

assembler = DocumentAssembler()
assembler.assemble_document(template_path, output_path, DataSourceInfo(invoice_data, "invoice"))

print("PDF generated from DOCX template.")
```
{{< /tab >}}
{{< tab "customer-invoice.docx" >}}
{{< tab-text >}}
The following sample file is used in this example: [customer-invoice.docx](/assembly/python-net/_sample_files/developer-guide/basic-usage/different-format-output/customer-invoice.docx)
{{< /tab-text >}}
{{< /tab >}}
{{< tab "customer-invoice-report.pdf" >}}  
```text
Binary file (PDF, 20 KB)
```
[Download full output](/assembly/python-net/_output_files/developer-guide/basic-usage/different-format-output/convert_docx_template_to_pdf/customer-invoice-report.pdf)
{{< /tab >}}
{{< /tabs >}}

## Convert DOCX Template to HTML

Generate an HTML file from a Word template:

{{< tabs "example2" >}}
{{< tab "Python" >}}
```python
from groupdocs.assembly import DataSourceInfo, DocumentAssembler

# DOCX template, HTML output
template_path = "monthly-report.docx"
output_path = "monthly-report-report.html"

report_data = {
    "Title": "Monthly Report",
    "Month": "January 2015",
}

assembler = DocumentAssembler()
assembler.assemble_document(template_path, output_path, DataSourceInfo(report_data, "report"))

print("HTML generated from DOCX template.")
```
{{< /tab >}}
{{< tab "monthly-report.docx" >}}
{{< tab-text >}}
The following sample file is used in this example: [monthly-report.docx](/assembly/python-net/_sample_files/developer-guide/basic-usage/different-format-output/monthly-report.docx)
{{< /tab-text >}}
{{< /tab >}}
{{< tab "monthly-report-report.html" >}}  
```text
<html><head><meta http-equiv="Content-Type" content="text/html; charset=utf-8" /><meta http-equiv="Content-Style-Type" content="text/css" /><meta name="generator" content="Aspose.Words for .NET 26.7.0" /><title></title></head><body style="font-family:'Times New Roman'; font-size:12pt"><div><h1 style="margin-top:12pt; margin-bottom:3pt; page-break-after:avoid; font-size:11pt"><span style="font-family:Calibri; font-weight:normal">Monthly Report</span></h1><p style="margin-top:0pt; margin-bottom:0p
[TRUNCATED]
```
[Download full output](/assembly/python-net/_output_files/developer-guide/basic-usage/different-format-output/convert_docx_template_to_html/monthly-report-report.html)
{{< /tab >}}
{{< /tabs >}}

## Convert DOCX Template to XPS

Generate an XPS document from a Word template:

{{< tabs "example3" >}}
{{< tab "Python" >}}
```python
from groupdocs.assembly import DataSourceInfo, DocumentAssembler

# DOCX template, XPS output
template_path = "price-notice.docx"
output_path = "price-notice-report.xps"

document_data = {
    "Title": "Price Notice",
    "Content": "From 1 March 2015, Chestnut honey is 7.80 per jar.",
}

assembler = DocumentAssembler()
assembler.assemble_document(template_path, output_path, DataSourceInfo(document_data, "document"))

print("XPS generated from DOCX template.")
```
{{< /tab >}}
{{< tab "price-notice.docx" >}}
{{< tab-text >}}
The following sample file is used in this example: [price-notice.docx](/assembly/python-net/_sample_files/developer-guide/basic-usage/different-format-output/price-notice.docx)
{{< /tab-text >}}
{{< /tab >}}
{{< tab "price-notice-report.xps" >}}  
```text
Binary file (XPS, 50 KB)
```
[Download full output](/assembly/python-net/_output_files/developer-guide/basic-usage/different-format-output/convert_docx_template_to_xps/price-notice-report.xps)
{{< /tab >}}
{{< /tabs >}}

## Convert XLSX Template to PDF

Generate a PDF from an Excel template:

{{< tabs "example4" >}}
{{< tab "Python" >}}
```python
from groupdocs.assembly import DataSourceInfo, DocumentAssembler

# XLSX template, PDF output
template_path = "sales-summary.xlsx"
output_path = "sales-summary-report.pdf"

data = {
    "ReportTitle": "Sales Report",
    "Quarter": "Q1 2015",
}

assembler = DocumentAssembler()
assembler.assemble_document(template_path, output_path, DataSourceInfo(data, "report"))

print("PDF generated from XLSX template.")
```
{{< /tab >}}
{{< tab "sales-summary.xlsx" >}}
{{< tab-text >}}
The following sample file is used in this example: [sales-summary.xlsx](/assembly/python-net/_sample_files/developer-guide/basic-usage/different-format-output/sales-summary.xlsx)
{{< /tab-text >}}
{{< /tab >}}
{{< tab "sales-summary-report.pdf" >}}  
```text
Binary file (PDF, 32 KB)
```
[Download full output](/assembly/python-net/_output_files/developer-guide/basic-usage/different-format-output/convert_xlsx_template_to_pdf/sales-summary-report.pdf)
{{< /tab >}}
{{< /tabs >}}

## Convert PPTX Template to PDF

Generate a PDF from a PowerPoint template:

{{< tabs "example5" >}}
{{< tab "Python" >}}
```python
from groupdocs.assembly import DataSourceInfo, DocumentAssembler

# PPTX template, PDF output
template_path = "quarterly-slides.pptx"
output_path = "quarterly-slides-report.pdf"

presentation_data = {
    "Title": "Quarterly Review",
    "Quarter": "Q1 2015",
}

assembler = DocumentAssembler()
assembler.assemble_document(template_path, output_path, DataSourceInfo(presentation_data, "presentation"))

print("PDF generated from PPTX template.")
```
{{< /tab >}}
{{< tab "quarterly-slides.pptx" >}}
{{< tab-text >}}
The following sample file is used in this example: [quarterly-slides.pptx](/assembly/python-net/_sample_files/developer-guide/basic-usage/different-format-output/quarterly-slides.pptx)
{{< /tab-text >}}
{{< /tab >}}
{{< tab "quarterly-slides-report.pdf" >}}  
```text
Binary file (PDF, 28 KB)
```
[Download full output](/assembly/python-net/_output_files/developer-guide/basic-usage/different-format-output/convert_pptx_template_to_pdf/quarterly-slides-report.pdf)
{{< /tab >}}
{{< /tabs >}}

## Convert Email Template to PDF

Generate a PDF from an email template (an EML message here; an MSG template works the same way):

{{< tabs "example6" >}}
{{< tab "Python" >}}
```python
from groupdocs.assembly import DataSourceInfo, DocumentAssembler

# EML template, PDF output
template_path = "invoice-notice.eml"
output_path = "invoice-notice-report.pdf"

email_data = {
    "Recipient": "Quayside Bistro <orders@quaysidebistro.example>",
    "Subject": "Invoice for order 10001",
    "Body": "Your invoice for order 10001 comes to 552.00 and is due by 13 February 2015.",
}

assembler = DocumentAssembler()
assembler.assemble_document(template_path, output_path, DataSourceInfo(email_data, "email"))

print("PDF generated from email template.")
```
{{< /tab >}}
{{< tab "invoice-notice.eml" >}}
{{< tab-text >}}
The following sample file is used in this example: [invoice-notice.eml](/assembly/python-net/_sample_files/developer-guide/basic-usage/different-format-output/invoice-notice.eml)
{{< /tab-text >}}
{{< /tab >}}
{{< tab "invoice-notice-report.pdf" >}}  
```text
Binary file (PDF, 1 KB)
```
[Download full output](/assembly/python-net/_output_files/developer-guide/basic-usage/different-format-output/convert_email_template_to_pdf/invoice-notice-report.pdf)
{{< /tab >}}
{{< /tabs >}}

## Choose the Format with LoadSaveOptions

A stream has no file extension, so the report keeps the template's format unless [LoadSaveOptions](https://reference.groupdocs.com/assembly/python-net/groupdocs.assembly/loadsaveoptions/) names another one. Pass it before the data sources:

{{< tabs "example7" >}}
{{< tab "Python" >}}
```python
import io
from datetime import datetime
from decimal import Decimal

from groupdocs.assembly import DataSourceInfo, DocumentAssembler, FileFormat, LoadSaveOptions

invoice_data = {
    "CustomerName": "Lantern Street Café",
    "Amount": Decimal("522.00"),
    "Date": datetime(2015, 2, 3),
}

with open("customer-invoice.docx", "rb") as template_stream, io.BytesIO() as output_stream:
    assembler = DocumentAssembler()
    assembler.assemble_document(template_stream, output_stream, LoadSaveOptions(FileFormat.PDF),
                                DataSourceInfo(invoice_data, "invoice"))

    with open("customer-invoice-from-stream.pdf", "wb") as f:
        f.write(output_stream.getvalue())

print("PDF generated from a DOCX template stream.")
```
{{< /tab >}}
{{< tab "customer-invoice.docx" >}}
{{< tab-text >}}
The following sample file is used in this example: [customer-invoice.docx](/assembly/python-net/_sample_files/developer-guide/basic-usage/different-format-output/customer-invoice.docx)
{{< /tab-text >}}
{{< /tab >}}
{{< tab "customer-invoice-from-stream.pdf" >}}  
```text
Binary file (PDF, 20 KB)
```
[Download full output](/assembly/python-net/_output_files/developer-guide/basic-usage/different-format-output/choose_the_format_with_loadsaveoptions/customer-invoice-from-stream.pdf)
{{< /tab >}}
{{< /tabs >}}

## Supported Format Conversions

The following conversions are supported:

**From Word Processing (DOCX, DOC, RTF, etc.):**
- PDF, XPS, HTML, MHTML, EPUB, TIFF, SVG, PS, PCL, Markdown, TXT, XAML

**From Spreadsheet (XLSX, XLS, etc.):**
- PDF, XPS, HTML, MHTML, TIFF

**From Presentation (PPTX, PPT, etc.):**
- PDF, XPS, TIFF

**From Email (MSG, EML, etc.):**
- PDF, XPS, HTML, MHTML, Markdown, TXT, XAML

{{< alert style="warning" >}}
Not all format combinations are supported. Word processing templates have the most conversion options, while spreadsheet and presentation templates have more limited output formats.
{{< /alert >}}

### Advanced Usage Topics

To learn more about format-specific options, conversion settings, and advanced format handling, please refer to the [advanced usage section]({{< ref "assembly/python-net/developer-guide/advanced-usage/_index.md" >}}).

## More resources

### GitHub Examples

You may easily run the code above and see the feature in action in our GitHub examples:

* [GroupDocs.Assembly for .NET examples, plugins, and showcase](https://github.com/groupdocs-assembly/GroupDocs.Assembly-for-.NET)
* [GroupDocs.Assembly for Java examples, plugins, and showcase](https://github.com/groupdocs-assembly/GroupDocs.Assembly-for-Java)
* [GroupDocs.Assembly for Python via .NET examples, plugins, and showcase](https://github.com/groupdocs-assembly/GroupDocs.Assembly-for-Python-via-.NET)

### Free Online Apps

Along with the full-featured library, we provide simple but powerful free online apps.

To assemble documents from templates and data sources, you can use the online apps from the **[GroupDocs.Assembly App Product Family](https://products.groupdocs.app/assembly/family)**.
