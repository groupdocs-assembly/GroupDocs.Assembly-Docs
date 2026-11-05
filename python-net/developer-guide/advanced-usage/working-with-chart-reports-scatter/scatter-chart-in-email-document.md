---
id: scatter-chart-in-email-document
url: assembly/python-net/scatter-chart-in-email-document
title: Scatter Chart in Email Document
weight: 4
description: "Scatter Chart in Email Document with GroupDocs.Assembly for Python via .NET: the template, the Python data and the code."
keywords: scatter chart in email document, GroupDocs.Assembly, Python, report generation
productName: GroupDocs.Assembly for Python via .NET
hideChildren: False
---
{{< alert style="info" >}}In this article, we will use GroupDocs.Assembly to generate a Scatter Chart report in Email Document format.{{< /alert >}}

## Scatter Chart in Email Document

### Creating a Scatter Chart

Please following below steps to create Scatter Chart in MS Outlook 2013:

1.  Create a new Email.
2.  Click in the email where you want to insert the chart, click the "Insert" tab, and then click "Chart" in the illustrations group to open the "Insert Chart" dialog box.
3.  Select "XY (Scatter)".
4.  Preview "Scatter" and press OK to insert the chart and Worksheet template to your email.
5.  Edit the Worksheet with your data to update the chart.
6.  Save the template.

### Reporting Requirement

As a report developer, you are required to show contract prices by month with the following key requirements:

*   Report must be in .eml or .msg format.
*   It must add email recipient, css and subject of the email.
*   Report must show information on a Scatter Chart.
*   It must indicate Price of each order by month.

### Adding Syntax to be evaluated by GroupDocs.Assembly Engine

#### Chart Title

```text
Total Order Prices by Months<<foreach [in orders
.GroupBy(c => c.OrderDate.Month)]>>
```

#### Chart Data (Excel)

<table cellspacing="0" cellpadding="0" style="border-collapse: collapse; margin-left: 0pt;"><tbody><tr style="height: 15pt;"><td style="border-bottom-color: rgb(0, 0, 0); border-bottom-style: solid; border-bottom-width: 0.75pt; border-left-color: rgb(0, 0, 0); border-left-style: solid; border-left-width: 0.75pt; border-right-color: rgb(0, 0, 0); border-right-style: solid; border-right-width: 0.75pt; border-top-color: rgb(0, 0, 0); border-top-style: solid; border-top-width: 0.75pt; padding-left: 5.03pt; padding-right: 5.03pt; vertical-align: top; width: 47.2pt;"><p style="margin-top: 0pt; margin-right: 0pt; margin-bottom: 0pt; margin-left: 0pt;"><span style="font-family: Calibri; font-size: 11pt;">X-Values</span></p></td><td style="border-bottom-color: rgb(0, 0, 0); border-bottom-style: solid; border-bottom-width: 0.75pt; border-left-color: rgb(0, 0, 0); border-left-style: solid; border-left-width: 0.75pt; border-right-color: rgb(0, 0, 0); border-right-style: solid; border-right-width: 0.75pt; border-top-color: rgb(0, 0, 0); border-top-style: solid; border-top-width: 0.75pt; padding-left: 5.03pt; padding-right: 5.03pt; vertical-align: top; width: 258.2pt;"><p style="margin-top: 0pt; margin-right: 0pt; margin-bottom: 0pt; margin-left: 0pt;"><span style="font-family: Calibri; font-size: 11pt;">Total Order Price&lt;&lt;x [Key]&gt;&gt;&lt;&lt;y [Sum(c =&gt; </span><span style="font-family: Calibri; font-size: 11pt;">c.Price</span><span style="font-family: Calibri; font-size: 11pt;">)]&gt;&gt;</span></p></td></tr><tr style="height: 15pt;"><td style="border-bottom-color: rgb(0, 0, 0); border-bottom-style: solid; border-bottom-width: 0.75pt; border-left-color: rgb(0, 0, 0); border-left-style: solid; border-left-width: 0.75pt; border-right-color: rgb(0, 0, 0); border-right-style: solid; border-right-width: 0.75pt; border-top-color: rgb(0, 0, 0); border-top-style: solid; border-top-width: 0.75pt; padding-left: 5.03pt; padding-right: 5.03pt; vertical-align: top; width: 47.2pt;"><p style="margin-top: 0pt; margin-right: 0pt; margin-bottom: 0pt; margin-left: 0pt;"><span style="font-family: Calibri; font-size: 11pt;">0.7</span></p></td><td style="border-bottom-color: rgb(0, 0, 0); border-bottom-style: solid; border-bottom-width: 0.75pt; border-left-color: rgb(0, 0, 0); border-left-style: solid; border-left-width: 0.75pt; border-right-color: rgb(0, 0, 0); border-right-style: solid; border-right-width: 0.75pt; border-top-color: rgb(0, 0, 0); border-top-style: solid; border-top-width: 0.75pt; padding-left: 5.03pt; padding-right: 5.03pt; vertical-align: top; width: 258.2pt;"><p style="margin-top: 0pt; margin-right: 0pt; margin-bottom: 0pt; margin-left: 0pt;"><span style="font-family: Calibri; font-size: 11pt;">2.7</span></p></td></tr><tr style="height: 15pt;"><td style="border-bottom-color: rgb(0, 0, 0); border-bottom-style: solid; border-bottom-width: 0.75pt; border-left-color: rgb(0, 0, 0); border-left-style: solid; border-left-width: 0.75pt; border-right-color: rgb(0, 0, 0); border-right-style: solid; border-right-width: 0.75pt; border-top-color: rgb(0, 0, 0); border-top-style: solid; border-top-width: 0.75pt; padding-left: 5.03pt; padding-right: 5.03pt; vertical-align: top; width: 47.2pt;"><p style="margin-top: 0pt; margin-right: 0pt; margin-bottom: 0pt; margin-left: 0pt;"><span style="font-family: Calibri; font-size: 11pt;">1.8</span></p></td><td style="border-bottom-color: rgb(0, 0, 0); border-bottom-style: solid; border-bottom-width: 0.75pt; border-left-color: rgb(0, 0, 0); border-left-style: solid; border-left-width: 0.75pt; border-right-color: rgb(0, 0, 0); border-right-style: solid; border-right-width: 0.75pt; border-top-color: rgb(0, 0, 0); border-top-style: solid; border-top-width: 0.75pt; padding-left: 5.03pt; padding-right: 5.03pt; vertical-align: top; width: 258.2pt;"><p style="margin-top: 0pt; margin-right: 0pt; margin-bottom: 0pt; margin-left: 0pt;"><span style="font-family: Calibri; font-size: 11pt;">3.2</span></p></td></tr><tr style="height: 15pt;"><td style="border-bottom-color: rgb(0, 0, 0); border-bottom-style: solid; border-bottom-width: 0.75pt; border-left-color: rgb(0, 0, 0); border-left-style: solid; border-left-width: 0.75pt; border-right-color: rgb(0, 0, 0); border-right-style: solid; border-right-width: 0.75pt; border-top-color: rgb(0, 0, 0); border-top-style: solid; border-top-width: 0.75pt; padding-left: 5.03pt; padding-right: 5.03pt; vertical-align: top; width: 47.2pt;"><p style="margin-top: 0pt; margin-right: 0pt; margin-bottom: 0pt; margin-left: 0pt;"><span style="font-family: Calibri; font-size: 11pt;">2.6</span></p></td><td style="border-bottom-color: rgb(0, 0, 0); border-bottom-style: solid; border-bottom-width: 0.75pt; border-left-color: rgb(0, 0, 0); border-left-style: solid; border-left-width: 0.75pt; border-right-color: rgb(0, 0, 0); border-right-style: solid; border-right-width: 0.75pt; border-top-color: rgb(0, 0, 0); border-top-style: solid; border-top-width: 0.75pt; padding-left: 5.03pt; padding-right: 5.03pt; vertical-align: top; width: 258.2pt;"><p style="margin-top: 0pt; margin-right: 0pt; margin-bottom: 0pt; margin-left: 0pt;"><span style="font-family: Calibri; font-size: 11pt;">0.8</span></p></td></tr></tbody></table>

{{< alert style="success" >}}For detailed technical information about syntax,expressions and report generation by the engine, please visit: [Working with GroupDocs.Assembly Engine]({{< ref "assembly/python-net/developer-guide/basic-usage/working-with-groupdocs.assembly-engine/_index.md" >}}).{{< /alert >}}

### Download Scatter Chart Template

Please download the sample Scatter Chart document we created in this article:

*   [scatter-chart.msg](/assembly/python-net/_sample_files/developer-guide/advanced-usage/working-with-chart-reports-scatter/scatter-chart-in-email-document/scatter-chart.msg)

### Generating The Report

{{< alert style="info" >}}The example reads the shop data described in [The Business Layer]({{< ref "assembly/python-net/developer-guide/basic-usage/working-with-a-business-case/the-business-layer.md" >}}).{{< /alert >}}

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
assembler.assemble_document("scatter-chart.msg", "scatter-chart-report.msg", [
    DataSourceInfo(orders, "orders"),
    DataSourceInfo("Harbor Lane Provisions <orders@harborlane.example>", "sender"),
    DataSourceInfo(["Quayside Bistro <orders@quaysidebistro.example>", "jonas.weber@harborlane.example"], "recipients"),
    DataSourceInfo("amara.osei@harborlane.example", "cc"),
    DataSourceInfo("Scatter chart", "subject"),
])
```
{{< /tab >}}
{{< tab "scatter-chart.msg" >}}
{{< tab-text >}}
The following sample file is used in this example: [scatter-chart.msg](/assembly/python-net/_sample_files/developer-guide/advanced-usage/working-with-chart-reports-scatter/scatter-chart-in-email-document/scatter-chart.msg)
{{< /tab-text >}}
{{< /tab >}}
{{< tab "orders.json" >}}
{{< tab-text >}}
The following sample file is used in this example: [orders.json](/assembly/python-net/_sample_files/developer-guide/advanced-usage/working-with-chart-reports-scatter/scatter-chart-in-email-document/orders.json)
{{< /tab-text >}}
{{< /tab >}}
{{< tab "scatter-chart-report.msg" >}}  
```text
Binary file (MSG, 51 KB)
```
[Download full output](/assembly/python-net/_output_files/developer-guide/advanced-usage/working-with-chart-reports-scatter/scatter-chart-in-email-document/generating_the_report/scatter-chart-report.msg)
{{< /tab >}}
{{< /tabs >}}
