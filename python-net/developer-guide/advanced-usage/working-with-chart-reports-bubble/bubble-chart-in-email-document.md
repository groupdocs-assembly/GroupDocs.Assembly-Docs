---
id: bubble-chart-in-email-document
url: assembly/python-net/bubble-chart-in-email-document
title: Bubble Chart in Email Document
weight: 4
description: "Bubble Chart in Email Document with GroupDocs.Assembly for Python via .NET: the template, the Python data and the code."
keywords: bubble chart in email document, GroupDocs.Assembly, Python, report generation
productName: GroupDocs.Assembly for Python via .NET
hideChildren: False
---
{{< alert style="info" >}}In this article, we will use GroupDocs.Assembly to generate a Bubble Chart report in Email Document.{{< /alert >}}{{< alert style="info" >}}The example reads the shop data described in [The Business Layer]({{< ref "assembly/python-net/developer-guide/basic-usage/working-with-a-business-case/the-business-layer.md" >}}).{{< /alert >}}

## Bubble Chart in Email Document

### Reporting Requirement

As a report developer, you are required to share your sales/orders dynamically with the following key requirements:

*   A report must be in .eml or .msg format.
*   It must add email recipient, CSS and subject of the email.
*   Retrieve total order Prices by Months.

### Adding Syntax to be evaluated by GroupDocs.Assembly Engine

##### Chart Title

```text
Orders Prices by Months<<foreach [in orders
.GroupBy(c => c.OrderDate.Month)]>><<x[Key]>>

```

##### Chart Data (Excel)

<table border="1" cellspacing="0" cellpadding="0" width="623" style="width: 467.5pt; border-collapse: collapse; border-top-color: initial; border-top-style: none; border-top-width: initial; border-right-color: initial; border-right-style: none; border-right-width: initial; border-bottom-color: initial; border-bottom-style: none; border-bottom-width: initial; border-left-color: initial; border-left-style: none; border-left-width: initial;"><tbody><tr><td width="108" valign="top" style="width: 80.75pt; border-top-color: windowtext; border-top-style: solid; border-top-width: 1pt; border-right-color: windowtext; border-right-style: solid; border-right-width: 1pt; border-bottom-color: windowtext; border-bottom-style: solid; border-bottom-width: 1pt; border-left-color: windowtext; border-left-style: solid; border-left-width: 1pt; padding-top: 0in; padding-right: 5.4pt; padding-bottom: 0in; padding-left: 5.4pt;"><p style="margin-bottom: 0.0001pt; line-height: normal;"><span style="color: black;">X-Values</span></p></td><td width="438" valign="top" style="width: 328.5pt; border-top-color: windowtext; border-top-style: solid; border-top-width: 1pt; border-right-color: windowtext; border-right-style: solid; border-right-width: 1pt; border-bottom-color: windowtext; border-bottom-style: solid; border-bottom-width: 1pt; border-left-color: initial; border-left-style: none; border-left-width: initial; padding-top: 0in; padding-right: 5.4pt; padding-bottom: 0in; padding-left: 5.4pt;"><p style="margin-bottom: 0.0001pt; line-height: normal;"><span style="color: black;">Total Order Price&lt;&lt;y [sum(c =&gt; c.Price)]&gt;&gt;&lt;&lt;size[Count()]&gt;&gt;</span></p></td><td width="78" valign="top" style="width: 58.25pt; border-top-color: windowtext; border-top-style: solid; border-top-width: 1pt; border-right-color: windowtext; border-right-style: solid; border-right-width: 1pt; border-bottom-color: windowtext; border-bottom-style: solid; border-bottom-width: 1pt; border-left-color: initial; border-left-style: none; border-left-width: initial; padding-top: 0in; padding-right: 5.4pt; padding-bottom: 0in; padding-left: 5.4pt;"><p style="margin-bottom: 0.0001pt; line-height: normal;"><span style="color: black;">Size</span></p></td></tr><tr><td width="108" valign="top" style="width: 80.75pt; border-top-color: initial; border-top-style: none; border-top-width: initial; border-right-color: windowtext; border-right-style: solid; border-right-width: 1pt; border-bottom-color: windowtext; border-bottom-style: solid; border-bottom-width: 1pt; border-left-color: windowtext; border-left-style: solid; border-left-width: 1pt; padding-top: 0in; padding-right: 5.4pt; padding-bottom: 0in; padding-left: 5.4pt;"><p align="right" style="margin-bottom: 0.0001pt; text-align: right; line-height: normal;"><span style="color: black;">0.7</span></p></td><td width="438" valign="top" style="width: 328.5pt; border-top-color: initial; border-top-style: none; border-top-width: initial; border-left-color: initial; border-left-style: none; border-left-width: initial; border-bottom-color: windowtext; border-bottom-style: solid; border-bottom-width: 1pt; border-right-color: windowtext; border-right-style: solid; border-right-width: 1pt; padding-top: 0in; padding-right: 5.4pt; padding-bottom: 0in; padding-left: 5.4pt;"><p align="right" style="margin-bottom: 0.0001pt; text-align: right; line-height: normal;"><span style="color: black;">2.7</span></p></td><td width="78" valign="top" style="width: 58.25pt; border-top-color: initial; border-top-style: none; border-top-width: initial; border-left-color: initial; border-left-style: none; border-left-width: initial; border-bottom-color: windowtext; border-bottom-style: solid; border-bottom-width: 1pt; border-right-color: windowtext; border-right-style: solid; border-right-width: 1pt; padding-top: 0in; padding-right: 5.4pt; padding-bottom: 0in; padding-left: 5.4pt;"><p align="right" style="margin-bottom: 0.0001pt; text-align: right; line-height: normal;"><span style="color: black;">10</span></p></td></tr><tr><td width="108" valign="top" style="width: 80.75pt; border-top-color: initial; border-top-style: none; border-top-width: initial; border-right-color: windowtext; border-right-style: solid; border-right-width: 1pt; border-bottom-color: windowtext; border-bottom-style: solid; border-bottom-width: 1pt; border-left-color: windowtext; border-left-style: solid; border-left-width: 1pt; padding-top: 0in; padding-right: 5.4pt; padding-bottom: 0in; padding-left: 5.4pt;"><p align="right" style="margin-bottom: 0.0001pt; text-align: right; line-height: normal;"><span style="color: black;">1.8</span></p></td><td width="438" valign="top" style="width: 328.5pt; border-top-color: initial; border-top-style: none; border-top-width: initial; border-left-color: initial; border-left-style: none; border-left-width: initial; border-bottom-color: windowtext; border-bottom-style: solid; border-bottom-width: 1pt; border-right-color: windowtext; border-right-style: solid; border-right-width: 1pt; padding-top: 0in; padding-right: 5.4pt; padding-bottom: 0in; padding-left: 5.4pt;"><p align="right" style="margin-bottom: 0.0001pt; text-align: right; line-height: normal;"><span style="color: black;">3.2</span></p></td><td width="78" valign="top" style="width: 58.25pt; border-top-color: initial; border-top-style: none; border-top-width: initial; border-left-color: initial; border-left-style: none; border-left-width: initial; border-bottom-color: windowtext; border-bottom-style: solid; border-bottom-width: 1pt; border-right-color: windowtext; border-right-style: solid; border-right-width: 1pt; padding-top: 0in; padding-right: 5.4pt; padding-bottom: 0in; padding-left: 5.4pt;"><p align="right" style="margin-bottom: 0.0001pt; text-align: right; line-height: normal;"><span style="color: black;">4</span></p></td></tr><tr><td width="108" valign="top" style="width: 80.75pt; border-top-color: initial; border-top-style: none; border-top-width: initial; border-right-color: windowtext; border-right-style: solid; border-right-width: 1pt; border-bottom-color: windowtext; border-bottom-style: solid; border-bottom-width: 1pt; border-left-color: windowtext; border-left-style: solid; border-left-width: 1pt; padding-top: 0in; padding-right: 5.4pt; padding-bottom: 0in; padding-left: 5.4pt;"><p align="right" style="margin-bottom: 0.0001pt; text-align: right; line-height: normal;"><span style="color: black;">2.6</span></p></td><td width="438" valign="top" style="width: 328.5pt; border-top-color: initial; border-top-style: none; border-top-width: initial; border-left-color: initial; border-left-style: none; border-left-width: initial; border-bottom-color: windowtext; border-bottom-style: solid; border-bottom-width: 1pt; border-right-color: windowtext; border-right-style: solid; border-right-width: 1pt; padding-top: 0in; padding-right: 5.4pt; padding-bottom: 0in; padding-left: 5.4pt;"><p align="right" style="margin-bottom: 0.0001pt; text-align: right; line-height: normal;"><span style="color: black;">0.8</span></p></td><td width="78" valign="top" style="width: 58.25pt; border-top-color: initial; border-top-style: none; border-top-width: initial; border-left-color: initial; border-left-style: none; border-left-width: initial; border-bottom-color: windowtext; border-bottom-style: solid; border-bottom-width: 1pt; border-right-color: windowtext; border-right-style: solid; border-right-width: 1pt; padding-top: 0in; padding-right: 5.4pt; padding-bottom: 0in; padding-left: 5.4pt;"><p align="right" style="margin-bottom: 0.0001pt; text-align: right; line-height: normal;"><span style="color: black;">8</span></p></td></tr></tbody></table>
{{< alert style="success" >}}For detailed technical information about syntax, expressions and report generation by the engine, please visit: [Working with GroupDocs.Assembly Engine]({{< ref "assembly/python-net/developer-guide/basic-usage/working-with-groupdocs.assembly-engine/_index.md" >}}).{{< /alert >}}

### Download Bubble Chart Template

Please download the sample Bubble Chart document we used in this article:

*   [bubble-chart.msg](/assembly/python-net/_sample_files/developer-guide/advanced-usage/working-with-chart-reports-bubble/bubble-chart-in-email-document/bubble-chart.msg)

### Generating The Report

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
assembler.assemble_document("bubble-chart.msg", "bubble-chart-report.msg", [
    DataSourceInfo(orders, "orders"),
    DataSourceInfo("Harbor Lane Provisions <orders@harborlane.example>", "sender"),
    DataSourceInfo(["Quayside Bistro <orders@quaysidebistro.example>", "jonas.weber@harborlane.example"], "recipients"),
    DataSourceInfo("amara.osei@harborlane.example", "cc"),
    DataSourceInfo("Bubble chart", "subject"),
])
```
{{< /tab >}}
{{< tab "bubble-chart.msg" >}}
{{< tab-text >}}
The following sample file is used in this example: [bubble-chart.msg](/assembly/python-net/_sample_files/developer-guide/advanced-usage/working-with-chart-reports-bubble/bubble-chart-in-email-document/bubble-chart.msg)
{{< /tab-text >}}
{{< /tab >}}
{{< tab "orders.json" >}}
{{< tab-text >}}
The following sample file is used in this example: [orders.json](/assembly/python-net/_sample_files/developer-guide/advanced-usage/working-with-chart-reports-bubble/bubble-chart-in-email-document/orders.json)
{{< /tab-text >}}
{{< /tab >}}
{{< tab "bubble-chart-report.msg" >}}  
```text
Binary file (MSG, 63 KB)
```
[Download full output](/assembly/python-net/_output_files/developer-guide/advanced-usage/working-with-chart-reports-bubble/bubble-chart-in-email-document/generating_the_report/bubble-chart-report.msg)
{{< /tab >}}
{{< /tabs >}}
