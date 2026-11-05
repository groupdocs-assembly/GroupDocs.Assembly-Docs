---
id: changing-target-file-format
url: assembly/python-net/changing-target-file-format
title: Changing Target File Format
weight: 38
description: "Changing Target File Format with GroupDocs.Assembly for Python via .NET: the template, the Python data and the code."
keywords: changing target file format, GroupDocs.Assembly, Python, report generation
productName: GroupDocs.Assembly for Python via .NET
hideChildren: False
---
{{< alert style="info" >}}The example reads the shop data described in [The Business Layer]({{< ref "assembly/python-net/developer-guide/basic-usage/working-with-a-business-case/the-business-layer.md" >}}).{{< /alert >}}

GroupDocs.Assembly provides a powerful feature to change the target file format of an assembled document using file extension or explicit specification. [GroupDocs.Assembly](https://reference.groupdocs.com/assembly/python-net/groupdocs.assembly/) API provides the ability to change target file format when assembling the following file formats:

*   Word Processing documents
*   Spreadsheet documents 
*   Presentation documents 
*   Email documents 
*   Text documents 

Supported output file formats depending on input file formats can be found at [this page]({{< ref "assembly/python-net/getting-started/supported-document-formats.md" >}}).

## Changing Target File Format using File Extension

{{< tabs "example1" >}}
{{< tab "Python" >}}
```python
import json
from datetime import datetime

from groupdocs.assembly import DataSourceInfo, DocumentAssembler

def parse_dates(item):
    # JSON has no dates: turn the order dates into datetime objects for the template
    for key in ("OrderDate", "ShippingDate"):
        if key in item:
            item[key] = datetime.strptime(item[key], "%Y-%m-%dT%H:%M:%S")
    return item

with open("orders.json", encoding="utf-8") as f:
    orders = json.load(f, object_hook=parse_dates)

assembler = DocumentAssembler()
assembler.assemble_document("bubble-chart.docx", "bubble-chart-report.pdf", DataSourceInfo(orders, "orders"))
```
{{< /tab >}}
{{< tab "bubble-chart.docx" >}}
{{< tab-text >}}
The following sample file is used in this example: [bubble-chart.docx](/assembly/python-net/_sample_files/developer-guide/advanced-usage/changing-target-file-format/bubble-chart.docx)
{{< /tab-text >}}
{{< /tab >}}
{{< tab "orders.json" >}}
{{< tab-text >}}
The following sample file is used in this example: [orders.json](/assembly/python-net/_sample_files/developer-guide/advanced-usage/changing-target-file-format/orders.json)
{{< /tab-text >}}
{{< /tab >}}
{{< tab "bubble-chart-report.pdf" >}}  
```text
Binary file (PDF, 44 KB)
```
[Download full output](/assembly/python-net/_output_files/developer-guide/advanced-usage/changing-target-file-format/changing_target_file_format_using_file_extension/bubble-chart-report.pdf)
{{< /tab >}}
{{< /tabs >}}

{{< tabs "example2" >}}
{{< tab "Python" >}}
```python
from groupdocs.assembly import DataSourceInfo, DocumentAssembler

assembler = DocumentAssembler()
assembler.assemble_document("conversion-template.pptx", "conversion-template-report.pptx", DataSourceInfo("Harbor Lane Provisions", "product"))
```
{{< /tab >}}
{{< tab "conversion-template.pptx" >}}
{{< tab-text >}}
The following sample file is used in this example: [conversion-template.pptx](/assembly/python-net/_sample_files/developer-guide/advanced-usage/changing-target-file-format/conversion-template.pptx)
{{< /tab-text >}}
{{< /tab >}}
{{< tab "conversion-template-report.pptx" >}}  
```text
Binary file (PPTX, 38 KB)
```
[Download full output](/assembly/python-net/_output_files/developer-guide/advanced-usage/changing-target-file-format/changing_target_file_format_using_file_extension_2/conversion-template-report.pptx)
{{< /tab >}}
{{< /tabs >}}

{{< tabs "example3" >}}
{{< tab "Python" >}}
```python
from groupdocs.assembly import DataSourceInfo, DocumentAssembler

assembler = DocumentAssembler()
assembler.assemble_document("conversion-template.pot", "conversion-template-report.pot", DataSourceInfo("Harbor Lane Provisions", "product"))
```
{{< /tab >}}
{{< tab "conversion-template.pot" >}}
{{< tab-text >}}
The following sample file is used in this example: [conversion-template.pot](/assembly/python-net/_sample_files/developer-guide/advanced-usage/changing-target-file-format/conversion-template.pot)
{{< /tab-text >}}
{{< /tab >}}
{{< tab "conversion-template-report.pot" >}}  
```text
Binary file (POT, 180 KB)
```
[Download full output](/assembly/python-net/_output_files/developer-guide/advanced-usage/changing-target-file-format/changing_target_file_format_using_file_extension_3/conversion-template-report.pot)
{{< /tab >}}
{{< /tabs >}}

{{< tabs "example4" >}}
{{< tab "Python" >}}
```python
from groupdocs.assembly import DataSourceInfo, DocumentAssembler

assembler = DocumentAssembler()
assembler.assemble_document("conversion-template.otp", "conversion-template-report.otp", DataSourceInfo("Harbor Lane Provisions", "product"))
```
{{< /tab >}}
{{< tab "conversion-template.otp" >}}
{{< tab-text >}}
The following sample file is used in this example: [conversion-template.otp](/assembly/python-net/_sample_files/developer-guide/advanced-usage/changing-target-file-format/conversion-template.otp)
{{< /tab-text >}}
{{< /tab >}}
{{< tab "conversion-template-report.otp" >}}  
```text
Binary file (OTP, 7 KB)
```
[Download full output](/assembly/python-net/_output_files/developer-guide/advanced-usage/changing-target-file-format/changing_target_file_format_using_file_extension_4/conversion-template-report.otp)
{{< /tab >}}
{{< /tabs >}}

{{< tabs "example5" >}}
{{< tab "Python" >}}
```python
from groupdocs.assembly import DataSourceInfo, DocumentAssembler

assembler = DocumentAssembler()
assembler.assemble_document("conversion-template.xlsx", "conversion-template-report.xlsx", DataSourceInfo("Harbor Lane Provisions", "product"))
```
{{< /tab >}}
{{< tab "conversion-template.xlsx" >}}
{{< tab-text >}}
The following sample file is used in this example: [conversion-template.xlsx](/assembly/python-net/_sample_files/developer-guide/advanced-usage/changing-target-file-format/conversion-template.xlsx)
{{< /tab-text >}}
{{< /tab >}}
{{< tab "conversion-template-report.xlsx" >}}  
```text
Binary file (XLSX, 9 KB)
```
[Download full output](/assembly/python-net/_output_files/developer-guide/advanced-usage/changing-target-file-format/changing_target_file_format_using_file_extension_5/conversion-template-report.xlsx)
{{< /tab >}}
{{< /tabs >}}

{{< tabs "example6" >}}
{{< tab "Python" >}}
```python
from groupdocs.assembly import DataSourceInfo, DocumentAssembler

assembler = DocumentAssembler()
assembler.assemble_document("conversion-template.xlt", "conversion-template-report.xlt", DataSourceInfo("Harbor Lane Provisions", "product"))
```
{{< /tab >}}
{{< tab "conversion-template.xlt" >}}
{{< tab-text >}}
The following sample file is used in this example: [conversion-template.xlt](/assembly/python-net/_sample_files/developer-guide/advanced-usage/changing-target-file-format/conversion-template.xlt)
{{< /tab-text >}}
{{< /tab >}}
{{< tab "conversion-template-report.xlt" >}}  
```text
Binary file (XLT, 14 KB)
```
[Download full output](/assembly/python-net/_output_files/developer-guide/advanced-usage/changing-target-file-format/changing_target_file_format_using_file_extension_6/conversion-template-report.xlt)
{{< /tab >}}
{{< /tabs >}}
