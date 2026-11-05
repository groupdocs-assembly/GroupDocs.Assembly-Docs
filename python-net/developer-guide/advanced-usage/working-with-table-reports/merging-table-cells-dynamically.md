---
id: merging-table-cells-dynamically
url: assembly/python-net/merging-table-cells-dynamically
title: Merging Table Cells Dynamically
weight: 6
description: "Merging Table Cells Dynamically with GroupDocs.Assembly for Python via .NET: the template, the Python data and the code."
keywords: merging table cells dynamically, GroupDocs.Assembly, Python, report generation
productName: GroupDocs.Assembly for Python via .NET
hideChildren: False
---
{{< alert style="info" >}}The example reads the shop data described in [The Business Layer]({{< ref "assembly/python-net/developer-guide/basic-usage/working-with-a-business-case/the-business-layer.md" >}}).{{< /alert >}}

Using GroupDocs.Assembly for Python via .NET, you can merge table cells with equal textual contents within your reports dynamically using **cellMerge** tags. Syntax of a **cellMerge** tag is defined as follows:

```
<<cellMerge -horz>>
```

{{< alert style="warning" >}}A horz switch is optional. If the switch is present, it denotes a cell merging operation in a horizontal direction. If the switch is missing, it means that a cell merging operation is to be performed in a vertical direction (the default).{{< /alert >}}

For two or more successive table cells to be merged dynamically in either direction by the engine, the following requirements must be met:

*   Each of the cells must contain a **cellMerge** tag denoting a cell merging operation in the same direction.
*   Each of the cells must not be already merged in another direction.
*   The cells must have equal textual contents (ignoring leading and trailing whitespaces).

Consider the following template:

<table style="background-color: white; background-image: initial; border-collapse: collapse; border-top-color: initial; border-top-style: none; border-top-width: initial; border-right-color: initial; border-right-style: none; border-right-width: initial; border-bottom-color: initial; border-bottom-style: none; border-bottom-width: initial; border-left-color: initial; border-left-style: none; border-left-width: initial;"><tbody><tr><td style="width: 89.625px; border-top-color: windowtext; border-top-style: solid; border-top-width: 1pt; border-right-color: windowtext; border-right-style: solid; border-right-width: 1pt; border-bottom-color: windowtext; border-bottom-style: solid; border-bottom-width: 1pt; border-left-color: windowtext; border-left-style: solid; border-left-width: 1pt; padding-top: 0in; padding-right: 5.4pt; padding-bottom: 0in; padding-left: 5.4pt;"><p style="margin-bottom: 0.0001pt; line-height: normal;"><strong><span style="font-family: &quot;Courier New&quot;; color: rgb(127, 127, 127);">...</span></strong></p></td><td style="width: 368.625px; border-top-color: windowtext; border-top-style: solid; border-top-width: 1pt; border-right-color: windowtext; border-right-style: solid; border-right-width: 1pt; border-bottom-color: windowtext; border-bottom-style: solid; border-bottom-width: 1pt; border-image-source: initial; border-image-slice: initial; border-image-width: initial; border-image-outset: initial; border-image-repeat: initial; border-left-color: initial; border-left-style: none; border-left-width: initial; padding-top: 0in; padding-right: 5.4pt; padding-bottom: 0in; padding-left: 5.4pt;"><p style="margin-bottom: 0.0001pt; line-height: normal;"><strong><span style="font-family: &quot;Courier New&quot;; color: rgb(127, 127, 127);">...</span></strong></p></td><td style="width: 98.625px; border-top-color: windowtext; border-top-style: solid; border-top-width: 1pt; border-right-color: windowtext; border-right-style: solid; border-right-width: 1pt; border-bottom-color: windowtext; border-bottom-style: solid; border-bottom-width: 1pt; border-image-source: initial; border-image-slice: initial; border-image-width: initial; border-image-outset: initial; border-image-repeat: initial; border-left-color: initial; border-left-style: none; border-left-width: initial; padding-top: 0in; padding-right: 5.4pt; padding-bottom: 0in; padding-left: 5.4pt;"><p style="margin-bottom: 0.0001pt; line-height: normal;"><strong><span style="font-family: &quot;Courier New&quot;; color: rgb(127, 127, 127);">...</span></strong></p></td></tr><tr><td style="width: 89.625px; border-right-color: windowtext; border-right-style: solid; border-right-width: 1pt; border-bottom-color: windowtext; border-bottom-style: solid; border-bottom-width: 1pt; border-left-color: windowtext; border-left-style: solid; border-left-width: 1pt; border-image-source: initial; border-image-slice: initial; border-image-width: initial; border-image-outset: initial; border-image-repeat: initial; border-top-color: initial; border-top-style: none; border-top-width: initial; padding-top: 0in; padding-right: 5.4pt; padding-bottom: 0in; padding-left: 5.4pt;"><p style="margin-bottom: 0.0001pt; line-height: normal;"><strong><span style="font-family: &quot;Courier New&quot;; color: rgb(127, 127, 127);">...</span></strong></p></td><td style="width: 368.625px; border-top-color: initial; border-top-style: none; border-top-width: initial; border-left-color: initial; border-left-style: none; border-left-width: initial; border-bottom-color: windowtext; border-bottom-style: solid; border-bottom-width: 1pt; border-right-color: windowtext; border-right-style: solid; border-right-width: 1pt; padding-top: 0in; padding-right: 5.4pt; padding-bottom: 0in; padding-left: 5.4pt;"><p style="margin-bottom: 0.0001pt; line-height: normal;"><strong><span style="font-family: &quot;Courier New&quot;; color: rgb(127, 127, 127);">&lt;&lt;cellMerge&gt;&gt;&lt;&lt;[</span><span style="font-family: &quot;Courier New&quot;; color: rgb(127, 127, 127);"><span style="font-family: Consolas;">Variable1</span></span></strong><strong><span style="font-family: &quot;Courier New&quot;; color: rgb(127, 127, 127);">]&gt;&gt;</span></strong></p></td><td style="width: 98.625px; border-top-color: initial; border-top-style: none; border-top-width: initial; border-left-color: initial; border-left-style: none; border-left-width: initial; border-bottom-color: windowtext; border-bottom-style: solid; border-bottom-width: 1pt; border-right-color: windowtext; border-right-style: solid; border-right-width: 1pt; padding-top: 0in; padding-right: 5.4pt; padding-bottom: 0in; padding-left: 5.4pt;"><p style="margin-bottom: 0.0001pt; line-height: normal;"><strong><span style="font-family: &quot;Courier New&quot;; color: rgb(127, 127, 127);">...</span></strong></p></td></tr><tr><td style="width: 89.625px; border-right-color: windowtext; border-right-style: solid; border-right-width: 1pt; border-bottom-color: windowtext; border-bottom-style: solid; border-bottom-width: 1pt; border-left-color: windowtext; border-left-style: solid; border-left-width: 1pt; border-image-source: initial; border-image-slice: initial; border-image-width: initial; border-image-outset: initial; border-image-repeat: initial; border-top-color: initial; border-top-style: none; border-top-width: initial; padding-top: 0in; padding-right: 5.4pt; padding-bottom: 0in; padding-left: 5.4pt;"><p style="margin-bottom: 0.0001pt; line-height: normal;"><strong><span style="font-family: &quot;Courier New&quot;; color: rgb(127, 127, 127);">...</span></strong></p></td><td style="width: 368.625px; border-top-color: initial; border-top-style: none; border-top-width: initial; border-left-color: initial; border-left-style: none; border-left-width: initial; border-bottom-color: windowtext; border-bottom-style: solid; border-bottom-width: 1pt; border-right-color: windowtext; border-right-style: solid; border-right-width: 1pt; padding-top: 0in; padding-right: 5.4pt; padding-bottom: 0in; padding-left: 5.4pt;"><p style="margin-bottom: 0.0001pt; line-height: normal;"><strong><span style="font-family: &quot;Courier New&quot;; color: rgb(127, 127, 127);">&lt;&lt;cellMerge&gt;&gt;&lt;&lt;[</span><span style="font-family: &quot;Courier New&quot;; color: rgb(127, 127, 127);"><span style="font-family: Consolas;">Variable2</span></span></strong><strong><span style="font-family: &quot;Courier New&quot;; color: rgb(127, 127, 127);">]&gt;&gt;</span></strong></p></td><td style="width: 98.625px; border-top-color: initial; border-top-style: none; border-top-width: initial; border-left-color: initial; border-left-style: none; border-left-width: initial; border-bottom-color: windowtext; border-bottom-style: solid; border-bottom-width: 1pt; border-right-color: windowtext; border-right-style: solid; border-right-width: 1pt; padding-top: 0in; padding-right: 5.4pt; padding-bottom: 0in; padding-left: 5.4pt;"><p style="margin-bottom: 0.0001pt; line-height: normal;"><strong><span style="font-family: &quot;Courier New&quot;; color: rgb(127, 127, 127);">...</span></strong></p></td></tr><tr><td style="width: 89.625px; border-right-color: windowtext; border-right-style: solid; border-right-width: 1pt; border-bottom-color: windowtext; border-bottom-style: solid; border-bottom-width: 1pt; border-left-color: windowtext; border-left-style: solid; border-left-width: 1pt; border-image-source: initial; border-image-slice: initial; border-image-width: initial; border-image-outset: initial; border-image-repeat: initial; border-top-color: initial; border-top-style: none; border-top-width: initial; padding-top: 0in; padding-right: 5.4pt; padding-bottom: 0in; padding-left: 5.4pt;"><p style="margin-bottom: 0.0001pt; line-height: normal;"><strong><span style="font-family: &quot;Courier New&quot;; color: rgb(127, 127, 127);">...</span></strong></p></td><td style="width: 368.625px; border-top-color: initial; border-top-style: none; border-top-width: initial; border-left-color: initial; border-left-style: none; border-left-width: initial; border-bottom-color: windowtext; border-bottom-style: solid; border-bottom-width: 1pt; border-right-color: windowtext; border-right-style: solid; border-right-width: 1pt; padding-top: 0in; padding-right: 5.4pt; padding-bottom: 0in; padding-left: 5.4pt;"><p style="margin-bottom: 0.0001pt; line-height: normal;"><strong><span style="font-family: &quot;Courier New&quot;; color: rgb(127, 127, 127);">...</span></strong></p></td><td style="width: 98.625px; border-top-color: initial; border-top-style: none; border-top-width: initial; border-left-color: initial; border-left-style: none; border-left-width: initial; border-bottom-color: windowtext; border-bottom-style: solid; border-bottom-width: 1pt; border-right-color: windowtext; border-right-style: solid; border-right-width: 1pt; padding-top: 0in; padding-right: 5.4pt; padding-bottom: 0in; padding-left: 5.4pt;"><p style="margin-bottom: 0.0001pt; line-height: normal;"><strong><span style="font-family: &quot;Courier New&quot;; color: rgb(127, 127, 127);">...</span></strong></p></td></tr></tbody></table>
{{< alert style="warning" >}}The cellMerge tag works only if Variable1 and Variable2 have the same values.{{< /alert >}}

## Merging Table Cells Dynamically in Word Processing Document 

### The Code

{{< tabs "example1" >}}
{{< tab "Python" >}}
```python
import json

from groupdocs.assembly import DataSourceInfo, DocumentAssembler

with open("customer.json", encoding="utf-8") as f:
    customer = json.load(f)

assembler = DocumentAssembler()
assembler.assemble_document("merging-table-cells-dynamically.docx", "merging-table-cells-dynamically-report.docx", DataSourceInfo(customer, "customer"))
```
{{< /tab >}}
{{< tab "merging-table-cells-dynamically.docx" >}}
{{< tab-text >}}
The following sample file is used in this example: [merging-table-cells-dynamically.docx](/assembly/python-net/_sample_files/developer-guide/advanced-usage/working-with-table-reports/merging-table-cells-dynamically/merging-table-cells-dynamically.docx)
{{< /tab-text >}}
{{< /tab >}}
{{< tab "customer.json" >}}
{{< tab-text >}}
The following sample file is used in this example: [customer.json](/assembly/python-net/_sample_files/developer-guide/advanced-usage/working-with-table-reports/merging-table-cells-dynamically/customer.json)
{{< /tab-text >}}
{{< /tab >}}
{{< tab "merging-table-cells-dynamically-report.docx" >}}  
```text
Binary file (DOCX, 10 KB)
```
[Download full output](/assembly/python-net/_output_files/developer-guide/advanced-usage/working-with-table-reports/merging-table-cells-dynamically/the_code/merging-table-cells-dynamically-report.docx)
{{< /tab >}}
{{< /tabs >}}

### Download

*   [Merging Cells Dynamically.docx](https://github.com/groupdocs-assembly/GroupDocs.Assembly-for-.NET/blob/master/Examples/Data/Source/Word%20Templates/Merging%20Cells%20Dynamically.docx "Merging Cells Dynamically.docx")

## Merging Table Cells Dynamically in Presentation Document 

### The Code

{{< tabs "example2" >}}
{{< tab "Python" >}}
```python
import json

from groupdocs.assembly import DataSourceInfo, DocumentAssembler

with open("customer.json", encoding="utf-8") as f:
    customer = json.load(f)

assembler = DocumentAssembler()
assembler.assemble_document("merging-table-cells-dynamically.pptx", "merging-table-cells-dynamically-report.pptx", DataSourceInfo(customer, "customer"))
```
{{< /tab >}}
{{< tab "merging-table-cells-dynamically.pptx" >}}
{{< tab-text >}}
The following sample file is used in this example: [merging-table-cells-dynamically.pptx](/assembly/python-net/_sample_files/developer-guide/advanced-usage/working-with-table-reports/merging-table-cells-dynamically/merging-table-cells-dynamically.pptx)
{{< /tab-text >}}
{{< /tab >}}
{{< tab "customer.json" >}}
{{< tab-text >}}
The following sample file is used in this example: [customer.json](/assembly/python-net/_sample_files/developer-guide/advanced-usage/working-with-table-reports/merging-table-cells-dynamically/customer.json)
{{< /tab-text >}}
{{< /tab >}}
{{< tab "merging-table-cells-dynamically-report.pptx" >}}  
```text
Binary file (PPTX, 33 KB)
```
[Download full output](/assembly/python-net/_output_files/developer-guide/advanced-usage/working-with-table-reports/merging-table-cells-dynamically/the_code_2/merging-table-cells-dynamically-report.pptx)
{{< /tab >}}
{{< /tabs >}}

### Download

*   [Merging Cells Dynamically.pptx](https://github.com/groupdocs-assembly/GroupDocs.Assembly-for-.NET/blob/master/Examples/Data/Source/Presentation%20Templates/Merging%20Cells%20Dynamically.pptx "Merging Cells Dynamically.pptx")

## Merging Table Cells Dynamically in Spreadsheet Document 

### The Code

{{< tabs "example3" >}}
{{< tab "Python" >}}
```python
import json

from groupdocs.assembly import DataSourceInfo, DocumentAssembler

with open("customer.json", encoding="utf-8") as f:
    customer = json.load(f)

assembler = DocumentAssembler()
assembler.assemble_document("merging-table-cells-dynamically.xlsx", "merging-table-cells-dynamically-report.xlsx", DataSourceInfo(customer, "customer"))
```
{{< /tab >}}
{{< tab "merging-table-cells-dynamically.xlsx" >}}
{{< tab-text >}}
The following sample file is used in this example: [merging-table-cells-dynamically.xlsx](/assembly/python-net/_sample_files/developer-guide/advanced-usage/working-with-table-reports/merging-table-cells-dynamically/merging-table-cells-dynamically.xlsx)
{{< /tab-text >}}
{{< /tab >}}
{{< tab "customer.json" >}}
{{< tab-text >}}
The following sample file is used in this example: [customer.json](/assembly/python-net/_sample_files/developer-guide/advanced-usage/working-with-table-reports/merging-table-cells-dynamically/customer.json)
{{< /tab-text >}}
{{< /tab >}}
{{< tab "merging-table-cells-dynamically-report.xlsx" >}}  
```text
Binary file (XLSX, 9 KB)
```
[Download full output](/assembly/python-net/_output_files/developer-guide/advanced-usage/working-with-table-reports/merging-table-cells-dynamically/the_code_3/merging-table-cells-dynamically-report.xlsx)
{{< /tab >}}
{{< /tabs >}}

### Download

*   [Merging Cells Dynamically.xlsx](https://github.com/groupdocs-assembly/GroupDocs.Assembly-for-.NET/blob/master/Examples/Data/Source/Spreadsheet%20Templates/Merging%20Cells%20Dynamically.xlsx "Merging Cells Dynamically.xlsx")

## Merging Table Cells Dynamically in Email Document 

### The Code

{{< tabs "example4" >}}
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

with open("customer.json", encoding="utf-8") as f:
    customer = json.load(f, object_hook=parse_dates)

assembler = DocumentAssembler()
assembler.assemble_document("merging-table-cells-dynamically.msg", "merging-table-cells-dynamically-report.msg", [
    DataSourceInfo(customer, "customer"),
    DataSourceInfo("Harbor Lane Provisions <orders@harborlane.example>", "sender"),
    DataSourceInfo(["Quayside Bistro <orders@quaysidebistro.example>", "jonas.weber@harborlane.example"], "recipients"),
    DataSourceInfo("amara.osei@harborlane.example", "cc"),
    DataSourceInfo("Merging table cells dynamically", "subject"),
])
```
{{< /tab >}}
{{< tab "merging-table-cells-dynamically.msg" >}}
{{< tab-text >}}
The following sample file is used in this example: [merging-table-cells-dynamically.msg](/assembly/python-net/_sample_files/developer-guide/advanced-usage/working-with-table-reports/merging-table-cells-dynamically/merging-table-cells-dynamically.msg)
{{< /tab-text >}}
{{< /tab >}}
{{< tab "customer.json" >}}
{{< tab-text >}}
The following sample file is used in this example: [customer.json](/assembly/python-net/_sample_files/developer-guide/advanced-usage/working-with-table-reports/merging-table-cells-dynamically/customer.json)
{{< /tab-text >}}
{{< /tab >}}
{{< tab "merging-table-cells-dynamically-report.msg" >}}  
```text
Binary file (MSG, 36 KB)
```
[Download full output](/assembly/python-net/_output_files/developer-guide/advanced-usage/working-with-table-reports/merging-table-cells-dynamically/the_code_4/merging-table-cells-dynamically-report.msg)
{{< /tab >}}
{{< /tabs >}}

### Download

*   [Merging Cells Dynamically.msg](https://github.com/groupdocs-assembly/GroupDocs.Assembly-for-.NET/blob/master/Examples/Data/Source/Email%20Templates/Merging%20Cells%20Dynamically.msg "Merging Cells Dynamically.msg")
