---
id: assembly-basic-usage-same-format-output
url: assembly/python-net/basic-usage-same-format-output
linktitle: Generate Output in Same Format
title: Generate Output in Same Format as Template
weight: 12
description: "Save documents assembled in Python in the same format as the template (DOCX to DOCX, XLSX to XLSX, PPTX to PPTX, EML to EML)."
keywords: same format, output format, save document, preserve format, DOCX output, XLSX output, PPTX output, EML output, Python
productName: GroupDocs.Assembly for Python via .NET
hideChildren: False
---

## Overview

By default, GroupDocs.Assembly for Python via .NET saves assembled documents in the same format as the template. This means a DOCX template produces a DOCX output, an XLSX template produces an XLSX output, and so on. With file paths, the output format is determined by the file extension of the output path.

The main class involved is:
- [DocumentAssembler](https://reference.groupdocs.com/assembly/python-net/groupdocs.assembly/documentassembler/) - assembles documents and determines output format

Here are the steps to generate output in the same format:

* Create a template document in your desired format (DOCX, XLSX, PPTX, etc.)
* Specify an output path with the same file extension as the template
* Assemble the document using DocumentAssembler
* The output will automatically be in the same format as the template

{{< alert style="info" >}}
The output format is automatically determined by the file extension of the output path. No additional configuration is needed to preserve the template format.
{{< /alert >}}

## Generate DOCX from DOCX Template

Generate a Word document from a Word template:

{{< tabs "example1" >}}
{{< tab "Python" >}}
```python
from datetime import datetime
from decimal import Decimal

from groupdocs.assembly import DataSourceInfo, DocumentAssembler

# Template and output are both DOCX
template_path = "invoice-letter.docx"
output_path = "invoice-letter-report.docx"

invoice_data = {
    "CustomerName": "Quayside Bistro",
    "Amount": Decimal("552.00"),
    "Date": datetime(2015, 1, 14),
}

assembler = DocumentAssembler()
assembler.assemble_document(template_path, output_path, DataSourceInfo(invoice_data, "invoice"))

print("DOCX document generated from DOCX template.")
```
{{< /tab >}}
{{< tab "invoice-letter.docx" >}}
{{< tab-text >}}
The following sample file is used in this example: [invoice-letter.docx](/assembly/python-net/_sample_files/developer-guide/basic-usage/same-format-output/invoice-letter.docx)
{{< /tab-text >}}
{{< /tab >}}
{{< tab "invoice-letter-report.docx" >}}  
```text
Binary file (DOCX, 7 KB)
```
[Download full output](/assembly/python-net/_output_files/developer-guide/basic-usage/same-format-output/generate_docx_from_docx_template/invoice-letter-report.docx)
{{< /tab >}}
{{< /tabs >}}

## Generate XLSX from XLSX Template

Generate an Excel spreadsheet from an Excel template:

{{< tabs "example2" >}}
{{< tab "Python" >}}
```python
from groupdocs.assembly import DataSourceInfo, DocumentAssembler

# Template and output are both XLSX
template_path = "monthly-sales.xlsx"
output_path = "monthly-sales-report.xlsx"

report_data = {
    "Title": "Monthly Sales",
    "Month": "January 2015",
}

assembler = DocumentAssembler()
assembler.assemble_document(template_path, output_path, DataSourceInfo(report_data, "report"))

print("XLSX document generated from XLSX template.")
```
{{< /tab >}}
{{< tab "monthly-sales.xlsx" >}}
{{< tab-text >}}
The following sample file is used in this example: [monthly-sales.xlsx](/assembly/python-net/_sample_files/developer-guide/basic-usage/same-format-output/monthly-sales.xlsx)
{{< /tab-text >}}
{{< /tab >}}
{{< tab "monthly-sales-report.xlsx" >}}  
```text
Binary file (XLSX, 7 KB)
```
[Download full output](/assembly/python-net/_output_files/developer-guide/basic-usage/same-format-output/generate_xlsx_from_xlsx_template/monthly-sales-report.xlsx)
{{< /tab >}}
{{< /tabs >}}

## Generate PPTX from PPTX Template

Generate a PowerPoint presentation from a PowerPoint template:

{{< tabs "example3" >}}
{{< tab "Python" >}}
```python
from groupdocs.assembly import DataSourceInfo, DocumentAssembler

# Template and output are both PPTX
template_path = "quarterly-review.pptx"
output_path = "quarterly-review-report.pptx"

presentation_data = {
    "Title": "Quarterly Review",
    "Quarter": "Q1 2015",
}

assembler = DocumentAssembler()
assembler.assemble_document(template_path, output_path, DataSourceInfo(presentation_data, "presentation"))

print("PPTX document generated from PPTX template.")
```
{{< /tab >}}
{{< tab "quarterly-review.pptx" >}}
{{< tab-text >}}
The following sample file is used in this example: [quarterly-review.pptx](/assembly/python-net/_sample_files/developer-guide/basic-usage/same-format-output/quarterly-review.pptx)
{{< /tab-text >}}
{{< /tab >}}
{{< tab "quarterly-review-report.pptx" >}}  
```text
Binary file (PPTX, 30 KB)
```
[Download full output](/assembly/python-net/_output_files/developer-guide/basic-usage/same-format-output/generate_pptx_from_pptx_template/quarterly-review-report.pptx)
{{< /tab >}}
{{< /tabs >}}

## Generate an Email from an Email Template

Generate an email message from an email template. The example uses an EML template, a MIME message you can write in any text editor; an Outlook MSG template is assembled the same way, into an `.msg` output path:

{{< tabs "example4" >}}
{{< tab "Python" >}}
```python
from groupdocs.assembly import DataSourceInfo, DocumentAssembler

# Template and output are both EML
template_path = "invoice-email.eml"
output_path = "invoice-email-report.eml"

email_data = {
    "Recipient": "Quayside Bistro <orders@quaysidebistro.example>",
    "Subject": "Invoice for order 10001",
    "Body": "Your invoice for order 10001 comes to 552.00 and is due by 13 February 2015.",
}

assembler = DocumentAssembler()
assembler.assemble_document(template_path, output_path, DataSourceInfo(email_data, "email"))

print("EML document generated from EML template.")
```
{{< /tab >}}
{{< tab "invoice-email.eml" >}}
{{< tab-text >}}
The following sample file is used in this example: [invoice-email.eml](/assembly/python-net/_sample_files/developer-guide/basic-usage/same-format-output/invoice-email.eml)
{{< /tab-text >}}
{{< /tab >}}
{{< tab "invoice-email-report.eml" >}}  
```text
Binary file (EML, 855 bytes)
```
[Download full output](/assembly/python-net/_output_files/developer-guide/basic-usage/same-format-output/generate_an_email_from_an_email_template/invoice-email-report.eml)
{{< /tab >}}
{{< /tabs >}}

In the template, tags work in the subject and the body. In the `To:` header, the tag sits in a quoted display name and is replaced by the whole recipient address:

```text
To: "<<[email.Recipient]>>" <customer@harborlane.example>
Subject: <<[email.Subject]>>
```

## Using Streams with Same Format

When using streams, the format is still preserved based on the template format:

{{< tabs "example5" >}}
{{< tab "Python" >}}
```python
import io
from datetime import datetime
from decimal import Decimal

from groupdocs.assembly import DataSourceInfo, DocumentAssembler

# Load DOCX template into a stream
with open("invoice-letter.docx", "rb") as f:
    template_bytes = f.read()

with io.BytesIO(template_bytes) as template_stream, io.BytesIO() as output_stream:
    data = {"CustomerName": "Lantern Street Café", "Amount": Decimal("522.00"), "Date": datetime(2015, 2, 3)}

    assembler = DocumentAssembler()
    assembler.assemble_document(template_stream, output_stream, DataSourceInfo(data, "invoice"))

    with open("invoice-letter-from-stream.docx", "wb") as f:
        f.write(output_stream.getvalue())

print("Document generated from stream in same format.")
```
{{< /tab >}}
{{< tab "invoice-letter.docx" >}}
{{< tab-text >}}
The following sample file is used in this example: [invoice-letter.docx](/assembly/python-net/_sample_files/developer-guide/basic-usage/same-format-output/invoice-letter.docx)
{{< /tab-text >}}
{{< /tab >}}
{{< tab "invoice-letter-from-stream.docx" >}}  
```text
Binary file (DOCX, 7 KB)
```
[Download full output](/assembly/python-net/_output_files/developer-guide/basic-usage/same-format-output/using_streams_with_same_format/invoice-letter-from-stream.docx)
{{< /tab >}}
{{< /tabs >}}

## Format Compatibility

The following formats support same-format output:

- **Word Processing**: DOCX, DOC, RTF, ODT, OTT
- **Spreadsheet**: XLSX, XLS, XLSM, ODS
- **Presentation**: PPTX, PPT, PPTM, ODP
- **Email**: MSG, EML, EMLX
- **Other**: HTML, TXT, XML

{{< alert style="warning" >}}
Some older formats (like DOC, XLS, PPT) may have limitations compared to their newer counterparts (DOCX, XLSX, PPTX). For best results, use the newer Office Open XML formats.
{{< /alert >}}

### Advanced Usage Topics

To learn more about format conversion, saving to different formats, and format-specific options, please refer to [Generate Output in Different Format]({{< ref "assembly/python-net/developer-guide/basic-usage/different-format-output.md" >}}) and the [advanced usage section]({{< ref "assembly/python-net/developer-guide/advanced-usage/_index.md" >}}).

## More resources

### GitHub Examples

You may easily run the code above and see the feature in action in our GitHub examples:

* [GroupDocs.Assembly for .NET examples, plugins, and showcase](https://github.com/groupdocs-assembly/GroupDocs.Assembly-for-.NET)
* [GroupDocs.Assembly for Java examples, plugins, and showcase](https://github.com/groupdocs-assembly/GroupDocs.Assembly-for-Java)
* [GroupDocs.Assembly for Python via .NET examples, plugins, and showcase](https://github.com/groupdocs-assembly/GroupDocs.Assembly-for-Python-via-.NET)

### Free Online Apps

Along with the full-featured library, we provide simple but powerful free online apps.

To assemble documents from templates and data sources, you can use the online apps from the **[GroupDocs.Assembly App Product Family](https://products.groupdocs.app/assembly/family)**.
