---
id: changing-background-color-dynamically
url: assembly/python-net/changing-background-color-dynamically
title: Changing Background Color Dynamically
weight: 36
description: "Changing Background Color Dynamically with GroupDocs.Assembly for Python via .NET: the template, the Python data and the code."
keywords: changing background color dynamically, GroupDocs.Assembly, Python, report generation
productName: GroupDocs.Assembly for Python via .NET
hideChildren: False
---
You can set text background color for document contents dynamically using backColor tags.

### The Code

{{< alert style="info" >}}The example reads the shop data described in [The Business Layer]({{< ref "assembly/python-net/developer-guide/basic-usage/working-with-a-business-case/the-business-layer.md" >}}).{{< /alert >}}

{{< tabs "example1" >}}
{{< tab "Python" >}}
```python
import json

from groupdocs.assembly import DataSourceInfo, DocumentAssembler

with open("orders.json", encoding="utf-8") as f:
    orders = json.load(f)

assembler = DocumentAssembler()
assembler.assemble_document("background-color.docx", "background-color-report.docx", [
    DataSourceInfo(orders, "orders"),
    DataSourceInfo("Coral", "color"),
])
```
{{< /tab >}}
{{< tab "background-color.docx" >}}
{{< tab-text >}}
The following sample file is used in this example: [background-color.docx](/assembly/python-net/_sample_files/developer-guide/advanced-usage/changing-background-color-dynamically/background-color.docx)
{{< /tab-text >}}
{{< /tab >}}
{{< tab "orders.json" >}}
{{< tab-text >}}
The following sample file is used in this example: [orders.json](/assembly/python-net/_sample_files/developer-guide/advanced-usage/changing-background-color-dynamically/orders.json)
{{< /tab-text >}}
{{< /tab >}}
{{< tab "background-color-report.docx" >}}  
```text
Binary file (DOCX, 11 KB)
```
[Download full output](/assembly/python-net/_output_files/developer-guide/advanced-usage/changing-background-color-dynamically/the_code/background-color-report.docx)
{{< /tab >}}
{{< /tabs >}}

### Download

*   [Change Background Color Dynamically.docx](https://github.com/groupdocs-assembly/GroupDocs.Assembly-for-.NET/blob/master/Examples/Data/Source/Word%20Templates/In-Table%20List%20with%20Running%20(Progressive)%20Total_BackgroundColor.docx)
