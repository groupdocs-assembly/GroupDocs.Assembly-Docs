---
id: in-table-list-with-alternate-content-in-email-document
url: assembly/python-net/in-table-list-with-alternate-content-in-email-document
title: In-Table List With Alternate Content in Email Document
weight: 5
description: "In-Table List With Alternate Content in Email Document with GroupDocs.Assembly for Python via .NET: the template, the Python data and the code."
keywords: in-table list with alternate content in email document, GroupDocs.Assembly, Python, report generation
productName: GroupDocs.Assembly for Python via .NET
hideChildren: False
---
{{< alert style="info" >}}In this article, we will use GroupDocs.Assembly to generate a In-Table List With Alternate Content report in Email Document format.{{< /alert >}}

## In-Table List With Alternate Content in Email Document

### Creating a In-Table List With Alternate Content

Practicing the following steps you can create In-Table List With Alternate Content Template in MS Outlook 2013.

1.  Add a new email.
2.  Press "Insert" tab to insert the table.
3.  Insert a 2X3 table.
4.  Save the template.

### Reporting Requirement

As a report developer, you are required to represent your clients and their prices with the following key requirements:

*   Report must be in .eml or .msg format.
*   It must add email recipient, css and subject of the email.
*   Report must show each product along with its price.
*   It must show sum of all the prices.
*   It must represent all the information in tabular form.

### Adding Syntax to be evaluated by GroupDocs.Assembly Engine

<table cellspacing="0" cellpadding="0" style="border-collapse: collapse; margin-left: 0pt; width: 457pt;"><tbody><tr><td style="background-color: rgb(91, 155, 213); border-bottom-color: rgb(255, 255, 255); border-bottom-style: solid; border-bottom-width: 3pt; border-left-color: rgb(255, 255, 255); border-left-style: solid; border-left-width: 1pt; border-right-color: rgb(255, 255, 255); border-right-style: solid; border-right-width: 1pt; border-top-color: rgb(255, 255, 255); border-top-style: solid; border-top-width: 1pt; padding-left: 4.9pt; padding-right: 4.9pt; padding-top: 0.25pt; vertical-align: top; width: 267.2pt;"><p style="font-size: 11pt; line-height: 107%; margin-top: 0pt; margin-right: 0pt; margin-bottom: 0pt; margin-left: 0pt;"><span style="color: rgb(255, 255, 255); font-family: Calibri; font-size: 11pt; font-weight: bold;">Products</span></p></td><td style="background-color: rgb(91, 155, 213); border-bottom-color: rgb(255, 255, 255); border-bottom-style: solid; border-bottom-width: 3pt; border-left-color: rgb(255, 255, 255); border-left-style: solid; border-left-width: 1pt; border-right-color: rgb(255, 255, 255); border-right-style: solid; border-right-width: 1pt; border-top-color: rgb(255, 255, 255); border-top-style: solid; border-top-width: 1pt; padding-left: 4.9pt; padding-right: 4.9pt; padding-top: 0.25pt; vertical-align: top; width: 167.2pt;"><p style="font-size: 11pt; line-height: 107%; margin-top: 0pt; margin-right: 0pt; margin-bottom: 0pt; margin-left: 0pt;"><span style="color: rgb(255, 255, 255); font-family: Calibri; font-size: 11pt; font-weight: bold;">Order Price</span></p></td></tr><tr><td colspan="2" style="background-color: rgb(91, 155, 213); border-bottom-color: rgb(255, 255, 255); border-bottom-style: solid; border-bottom-width: 1pt; border-left-color: rgb(255, 255, 255); border-left-style: solid; border-left-width: 1pt; border-right-color: rgb(255, 255, 255); border-right-style: solid; border-right-width: 1pt; border-top-color: rgb(255, 255, 255); border-top-style: solid; border-top-width: 3pt; padding-left: 4.9pt; padding-right: 4.9pt; vertical-align: top; width: 445.2pt;"><p style="font-size: 11pt; line-height: 107%; margin-top: 0pt; margin-right: 0pt; margin-bottom: 0pt; margin-left: 0pt; text-align: center;"><span style="color: rgb(255, 255, 255); font-family: Calibri; font-size: 11pt; font-weight: bold;">&lt;&lt;if [!Any()]&gt;&gt;No data</span></p></td></tr><tr><td style="background-color: rgb(91, 155, 213); border-bottom-color: rgb(255, 255, 255); border-bottom-style: solid; border-bottom-width: 1pt; border-left-color: rgb(255, 255, 255); border-left-style: solid; border-left-width: 1pt; border-right-color: rgb(255, 255, 255); border-right-style: solid; border-right-width: 1pt; border-top-color: rgb(255, 255, 255); border-top-style: solid; border-top-width: 1pt; padding-left: 4.9pt; padding-right: 4.9pt; padding-top: 0.25pt; vertical-align: top; width: 267.2pt;"><p style="font-size: 11pt; line-height: 107%; margin-top: 0pt; margin-right: 0pt; margin-bottom: 0pt; margin-left: 0pt;"><span style="color: rgb(255, 255, 255); font-family: Calibri; font-size: 11pt; font-weight: bold;">&lt;&lt;else&gt;&gt;&lt;&lt;</span><span style="color: rgb(255, 255, 255); font-family: Calibri; font-size: 11pt; font-weight: bold;">foreach</span><span style="color: rgb(255, 255, 255); font-family: Calibri; font-size: 11pt; font-weight: bold;"> [in orders]&gt;&gt;&lt;&lt;[</span><span style="color: rgb(255, 255, 255); font-family: Calibri; font-size: 11pt; font-weight: bold;">Product.ProductName</span><span style="color: rgb(255, 255, 255); font-family: Calibri; font-size: 11pt; font-weight: bold;">]&gt;&gt;</span></p></td><td style="background-color: rgb(234, 239, 247); border-bottom-color: rgb(255, 255, 255); border-bottom-style: solid; border-bottom-width: 1pt; border-left-color: rgb(255, 255, 255); border-left-style: solid; border-left-width: 1pt; border-right-color: rgb(255, 255, 255); border-right-style: solid; border-right-width: 1pt; border-top-color: rgb(255, 255, 255); border-top-style: solid; border-top-width: 1pt; padding-left: 4.9pt; padding-right: 4.9pt; padding-top: 0.25pt; vertical-align: top; width: 167.2pt;"><p style="font-size: 11pt; line-height: 107%; margin-top: 0pt; margin-right: 0pt; margin-bottom: 0pt; margin-left: 0pt;"><span style="font-family: Calibri; font-size: 11pt;">&lt;&lt;[Price]&gt;&gt;&lt;&lt;/</span><span style="font-family: Calibri; font-size: 11pt;">foreach</span><span style="font-family: Calibri; font-size: 11pt;">&gt;&gt;</span></p></td></tr><tr><td style="background-color: rgb(91, 155, 213); border-bottom-color: rgb(255, 255, 255); border-bottom-style: solid; border-bottom-width: 1pt; border-left-color: rgb(255, 255, 255); border-left-style: solid; border-left-width: 1pt; border-right-color: rgb(255, 255, 255); border-right-style: solid; border-right-width: 1pt; border-top-color: rgb(255, 255, 255); border-top-style: solid; border-top-width: 1pt; padding-left: 4.9pt; padding-right: 4.9pt; padding-top: 0.25pt; vertical-align: top; width: 267.2pt;"><p style="font-size: 11pt; line-height: 107%; margin-top: 0pt; margin-right: 0pt; margin-bottom: 0pt; margin-left: 0pt;"><span style="color: rgb(255, 255, 255); font-family: Calibri; font-size: 11pt; font-weight: bold;">Total:</span></p></td><td style="background-color: rgb(210, 222, 239); border-bottom-color: rgb(255, 255, 255); border-bottom-style: solid; border-bottom-width: 1pt; border-left-color: rgb(255, 255, 255); border-left-style: solid; border-left-width: 1pt; border-right-color: rgb(255, 255, 255); border-right-style: solid; border-right-width: 1pt; border-top-color: rgb(255, 255, 255); border-top-style: solid; border-top-width: 1pt; padding-left: 4.9pt; padding-right: 4.9pt; padding-top: 0.25pt; vertical-align: top; width: 167.2pt;"><p style="font-size: 11pt; line-height: 107%; margin-top: 0pt; margin-right: 0pt; margin-bottom: 0pt; margin-left: 0pt;"><span style="font-family: Calibri; font-size: 11pt;">&lt;&lt;[Sum(c =&gt; </span><span style="font-family: Calibri; font-size: 11pt;">c.Price</span><span style="font-family: Calibri; font-size: 11pt;">)]&gt;&gt;&lt;&lt;/if&gt;&gt;</span></p></td></tr><tr style="height: 0pt;"><td style="width: 278pt; border-top-color: initial; border-top-style: none; border-top-width: initial; border-right-color: initial; border-right-style: none; border-right-width: initial; border-bottom-color: initial; border-bottom-style: none; border-bottom-width: initial; border-left-color: initial; border-left-style: none; border-left-width: initial;"></td><td style="width: 178pt; border-top-color: initial; border-top-style: none; border-top-width: initial; border-right-color: initial; border-right-style: none; border-right-width: initial; border-bottom-color: initial; border-bottom-style: none; border-bottom-width: initial; border-left-color: initial; border-left-style: none; border-left-width: initial;"></td></tr></tbody></table>

{{< alert style="success" >}}For detailed technical information about syntax,expressions and report generation by the engine, please visit: Working with GroupDocs.Assembly Engine{{< /alert >}}

### Download In-Table List With Alternate Content Template

Please download the sample In-Table List With Alternate Content document we used in this article:

*   [in-table-list-with-alternate-content.msg](/assembly/python-net/_sample_files/developer-guide/advanced-usage/working-with-table-reports-alternate-content/in-table-list-with-alternate-content-in-email-document/in-table-list-with-alternate-content.msg)

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
assembler.assemble_document("in-table-list-with-alternate-content.msg", "in-table-list-with-alternate-content-report.msg", [
    DataSourceInfo(orders, "orders"),
    DataSourceInfo("Harbor Lane Provisions <orders@harborlane.example>", "sender"),
    DataSourceInfo(["Quayside Bistro <orders@quaysidebistro.example>", "jonas.weber@harborlane.example"], "recipients"),
    DataSourceInfo("amara.osei@harborlane.example", "cc"),
    DataSourceInfo("In table list with alternate content", "subject"),
])
```
{{< /tab >}}
{{< tab "in-table-list-with-alternate-content.msg" >}}
{{< tab-text >}}
The following sample file is used in this example: [in-table-list-with-alternate-content.msg](/assembly/python-net/_sample_files/developer-guide/advanced-usage/working-with-table-reports-alternate-content/in-table-list-with-alternate-content-in-email-document/in-table-list-with-alternate-content.msg)
{{< /tab-text >}}
{{< /tab >}}
{{< tab "orders.json" >}}
{{< tab-text >}}
The following sample file is used in this example: [orders.json](/assembly/python-net/_sample_files/developer-guide/advanced-usage/working-with-table-reports-alternate-content/in-table-list-with-alternate-content-in-email-document/orders.json)
{{< /tab-text >}}
{{< /tab >}}
{{< tab "in-table-list-with-alternate-content-report.msg" >}}  
```text
Binary file (MSG, 48 KB)
```
[Download full output](/assembly/python-net/_output_files/developer-guide/advanced-usage/working-with-table-reports-alternate-content/in-table-list-with-alternate-content-in-email-document/generating_the_report/in-table-list-with-alternate-content-report.msg)
{{< /tab >}}
{{< /tabs >}}
