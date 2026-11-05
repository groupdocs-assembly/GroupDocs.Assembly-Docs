---
id: individual-series-point-coloring-in-email-document
url: assembly/python-net/individual-series-point-coloring-in-email-document
title: Individual Series Point Coloring in Email Document
weight: 4
description: "Individual Series Point Coloring in Email Document with GroupDocs.Assembly for Python via .NET: the template, the Python data and the code."
keywords: individual series point coloring in email document, GroupDocs.Assembly, Python, report generation
productName: GroupDocs.Assembly for Python via .NET
hideChildren: False
---
{{< alert style="info" >}}The example reads the shop data described in [The Business Layer]({{< ref "assembly/python-net/developer-guide/basic-usage/working-with-a-business-case/the-business-layer.md" >}}).{{< /alert >}}

## Individual Series Point Coloring in Email Document

Please follow below steps to create Pie Chart in MS Outlook 2013:

1.  Create a new Email
2.  Click the "Insert" tab, and then click "Chart" in the illustrations group to open the "Insert Chart" dialog box
3.  Select "Pie"
4.  Preview "Pie" and press OK to insert the chart and Worksheet template to your email
5.  Edit the Worksheet with your data to update the chart

### Reporting Requirement

As a report developer, you are required to share your customer orders details dynamically with the following key requirements:

*   The report must show information on a Pie Chart
*   It must indicate customer name with value (price of the orders purchased)
*   The report must be generated in the Email Document

### Adding Syntax to be evaluated by GroupDocs.Assembly Engine

#### Chart Title

```text
Total Order Price<<foreach [in customers]>>
<<x [CustomerName]>>
```

#### Chart Data (Excel)

|   | Total Order Price<<y [Order.Sum(c => c.Price)]>><<pointColor [Color] >> |
| --- | --- |
| A | 8.2 |
| B | 3.2 |
| C | 1.5 |
| D | 1.2 |

{{< alert style="success" >}}For detailed technical information about syntax, expressions and report generation by the engine, please visit: [Working with GroupDocs.Assembly Engine]({{< ref "assembly/python-net/developer-guide/basic-usage/working-with-groupdocs.assembly-engine/_index.md" >}}){{< /alert >}}

### Download Pie Chart Template

Please download the sample Pie Chart document we created in this article:

*   [dynamic-chart-point-series-color.msg](/assembly/python-net/_sample_files/developer-guide/advanced-usage/working-with-individual-series-point-coloring/individual-series-point-coloring-in-email-document/dynamic-chart-point-series-color.msg)

### Generating The Report

For a chart with dynamic data, you can set colors of individual chart series points dynamically based upon expressions. To use the feature, do the following steps:

*   Declare a chart with dynamic data in the usual way
*   For chart series with points to be colored dynamically, define corresponding color expressions in names of these series using **pointColor** tags having the following syntax:
  
    ```text
    <<pointColor [color_expression]>>
    ```
    

A color expression must return a value of one of the following types:

*   A string containing the name of a known color, that is, the case-insensitive name of a member of the [KnownColor](https://msdn.microsoft.com/en-us/library/system.drawing.knowncolor(v=vs.110).aspx) enumeration such as "red"
*   An integer value defining RGB (red, green, blue) components of the color such as 0xFFFF00 (yellow)
*   A value of the [Color](http://msdn.microsoft.com/en-us/library/system.drawing.color(v=vs.110).aspx) type

Following code snippet generates the report:

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

with open("customers.json", encoding="utf-8") as f:
    customers = json.load(f, object_hook=parse_dates)

assembler = DocumentAssembler()
assembler.assemble_document("dynamic-chart-point-series-color.msg", "dynamic-chart-point-series-color-report.msg", [
    DataSourceInfo(customers, "customers"),
    DataSourceInfo("Harbor Lane Provisions <orders@harborlane.example>", "sender"),
    DataSourceInfo(["Quayside Bistro <orders@quaysidebistro.example>", "jonas.weber@harborlane.example"], "recipients"),
    DataSourceInfo("amara.osei@harborlane.example", "cc"),
    DataSourceInfo("Dynamic chart point series color", "subject"),
])
```
{{< /tab >}}
{{< tab "dynamic-chart-point-series-color.msg" >}}
{{< tab-text >}}
The following sample file is used in this example: [dynamic-chart-point-series-color.msg](/assembly/python-net/_sample_files/developer-guide/advanced-usage/working-with-individual-series-point-coloring/individual-series-point-coloring-in-email-document/dynamic-chart-point-series-color.msg)
{{< /tab-text >}}
{{< /tab >}}
{{< tab "customers.json" >}}
{{< tab-text >}}
The following sample file is used in this example: [customers.json](/assembly/python-net/_sample_files/developer-guide/advanced-usage/working-with-individual-series-point-coloring/individual-series-point-coloring-in-email-document/customers.json)
{{< /tab-text >}}
{{< /tab >}}
{{< tab "dynamic-chart-point-series-color-report.msg" >}}  
```text
Binary file (MSG, 46 KB)
```
[Download full output](/assembly/python-net/_output_files/developer-guide/advanced-usage/working-with-individual-series-point-coloring/individual-series-point-coloring-in-email-document/generating_the_report/dynamic-chart-point-series-color-report.msg)
{{< /tab >}}
{{< /tabs >}}
