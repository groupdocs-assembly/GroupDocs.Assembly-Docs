---
id: in-table-list-with-filtering-grouping-and-ordering-in-html-document
url: assembly/python-net/in-table-list-with-filtering-grouping-and-ordering-in-html-document
title: In-Table List with Filtering Grouping and Ordering in HTML Document
weight: 4
description: "In-Table List with Filtering Grouping and Ordering in HTML Document with GroupDocs.Assembly for Python via .NET: the template, the Python data and the code."
keywords: in-table list with filtering grouping and ordering in html document, GroupDocs.Assembly, Python, report generation
productName: GroupDocs.Assembly for Python via .NET
hideChildren: False
---
{{< alert style="info" >}}In this article, we will use GroupDocs.Assembly to generate an In-Table Master-Detail report in HTML Document format.{{< /alert >}}{{< alert style="info" >}}The example reads the shop data described in [The Business Layer]({{< ref "assembly/python-net/developer-guide/basic-usage/working-with-a-business-case/the-business-layer.md" >}}).{{< /alert >}}

## In-Table Master-Detail in HTML Document

### Reporting Requirement

As a report developer, you are required to represent customers' orders information with the following key requirements:

*   Report must show each customer along with sum of prices of his orders.
*   It must represent all the information in tabular form.
*   Report must be generated in the Presentation Document.

### Adding Syntax to be evaluated by GroupDocs.Assembly Engine

<table cellspacing="0" cellpadding="0" style="border-collapse: collapse; margin-left: 0pt; width: 457pt;"><tbody><tr><td style="background-color: rgb(91, 155, 213); border-bottom-color: rgb(255, 255, 255); border-bottom-style: solid; border-bottom-width: 3pt; border-left-color: rgb(255, 255, 255); border-left-style: solid; border-left-width: 1pt; border-right-color: rgb(255, 255, 255); border-right-style: solid; border-right-width: 1pt; border-top-color: rgb(255, 255, 255); border-top-style: solid; border-top-width: 1pt; padding-left: 4.9pt; padding-right: 4.9pt; padding-top: 0.25pt; vertical-align: top; width: 267.2pt;"><p style="font-size: 11pt; line-height: 107%; margin-top: 0pt; margin-right: 0pt; margin-bottom: 0pt; margin-left: 0pt;"><span style="color: rgb(255, 255, 255); font-family: Calibri; font-size: 11pt; font-weight: bold;">Customer</span></p></td><td style="background-color: rgb(91, 155, 213); border-bottom-color: rgb(255, 255, 255); border-bottom-style: solid; border-bottom-width: 3pt; border-left-color: rgb(255, 255, 255); border-left-style: solid; border-left-width: 1pt; border-right-color: rgb(255, 255, 255); border-right-style: solid; border-right-width: 1pt; border-top-color: rgb(255, 255, 255); border-top-style: solid; border-top-width: 1pt; padding-left: 4.9pt; padding-right: 4.9pt; padding-top: 0.25pt; vertical-align: top; width: 167.2pt;"><p style="font-size: 11pt; line-height: 107%; margin-top: 0pt; margin-right: 0pt; margin-bottom: 0pt; margin-left: 0pt;"><span style="color: rgb(255, 255, 255); font-family: Calibri; font-size: 11pt; font-weight: bold;">Order Price</span></p></td></tr><tr><td style="background-color: rgb(91, 155, 213); border-bottom-color: rgb(255, 255, 255); border-bottom-style: solid; border-bottom-width: 1pt; border-left-color: rgb(255, 255, 255); border-left-style: solid; border-left-width: 1pt; border-right-color: rgb(255, 255, 255); border-right-style: solid; border-right-width: 1pt; border-top-color: rgb(255, 255, 255); border-top-style: solid; border-top-width: 3pt; padding-left: 4.9pt; padding-right: 4.9pt; vertical-align: top; width: 267.2pt;"><p style="font-size: 11pt; line-height: 107%; margin-top: 0pt; margin-right: 0pt; margin-bottom: 0pt; margin-left: 0pt;"><span style="color: rgb(255, 255, 255); font-family: Calibri; font-size: 11pt; font-weight: bold;">&lt;&lt;</span><span style="color: rgb(255, 255, 255); font-family: Calibri; font-size: 11pt; font-weight: bold;">foreach</span><span style="color: rgb(255, 255, 255); font-family: Calibri; font-size: 11pt; font-weight: bold;"> [in orders</span></p><p style="font-size: 11pt; line-height: 107%; margin-top: 0pt; margin-right: 0pt; margin-bottom: 0pt; margin-left: 0pt;"><span style="color: rgb(255, 255, 255); font-family: Calibri; font-size: 11pt; font-weight: bold;">.Where(c =&gt; </span><span style="color: rgb(255, 255, 255); font-family: Calibri; font-size: 11pt; font-weight: bold;">c.OrderDate.Year</span><span style="color: rgb(255, 255, 255); font-family: Calibri; font-size: 11pt; font-weight: bold;"> == 2015)</span></p><p style="font-size: 11pt; line-height: 107%; margin-top: 0pt; margin-right: 0pt; margin-bottom: 0pt; margin-left: 0pt;"><span style="color: rgb(255, 255, 255); font-family: Calibri; font-size: 11pt; font-weight: bold;">.</span><span style="color: rgb(255, 255, 255); font-family: Calibri; font-size: 11pt; font-weight: bold;">GroupBy</span><span style="color: rgb(255, 255, 255); font-family: Calibri; font-size: 11pt; font-weight: bold;">(c =&gt; </span><span style="color: rgb(255, 255, 255); font-family: Calibri; font-size: 11pt; font-weight: bold;">c.Customer</span><span style="color: rgb(255, 255, 255); font-family: Calibri; font-size: 11pt; font-weight: bold;">)</span></p><p style="font-size: 11pt; line-height: 107%; margin-top: 0pt; margin-right: 0pt; margin-bottom: 0pt; margin-left: 0pt;"><span style="color: rgb(255, 255, 255); font-family: Calibri; font-size: 11pt; font-weight: bold;">.</span><span style="color: rgb(255, 255, 255); font-family: Calibri; font-size: 11pt; font-weight: bold;">OrderBy</span><span style="color: rgb(255, 255, 255); font-family: Calibri; font-size: 11pt; font-weight: bold;">(g =&gt; </span><span style="color: rgb(255, 255, 255); font-family: Calibri; font-size: 11pt; font-weight: bold;">g.Key.CustomerName</span><span style="color: rgb(255, 255, 255); font-family: Calibri; font-size: 11pt; font-weight: bold;">)]&gt;&gt;&lt;&lt;[</span><span style="color: rgb(255, 255, 255); font-family: Calibri; font-size: 11pt; font-weight: bold;">Key.CustomerName</span><span style="color: rgb(255, 255, 255); font-family: Calibri; font-size: 11pt; font-weight: bold;">]&gt;&gt;</span></p></td><td style="background-color: rgb(210, 222, 239); border-bottom-color: rgb(255, 255, 255); border-bottom-style: solid; border-bottom-width: 1pt; border-left-color: rgb(255, 255, 255); border-left-style: solid; border-left-width: 1pt; border-right-color: rgb(255, 255, 255); border-right-style: solid; border-right-width: 1pt; border-top-color: rgb(255, 255, 255); border-top-style: solid; border-top-width: 3pt; padding-left: 4.9pt; padding-right: 4.9pt; vertical-align: top; width: 167.2pt;"><p style="font-size: 11pt; line-height: 107%; margin-top: 0pt; margin-right: 0pt; margin-bottom: 0pt; margin-left: 0pt;"><span style="font-family: Calibri; font-size: 11pt;">&lt;&lt;[Sum(c =&gt; </span><span style="font-family: Calibri; font-size: 11pt;">c.Price</span><span style="font-family: Calibri; font-size: 11pt;">)]&gt;&gt;&lt;&lt;/</span><span style="font-family: Calibri; font-size: 11pt;">foreach</span><span style="font-family: Calibri; font-size: 11pt;">&gt;&gt;</span></p></td></tr></tbody></table>
{{< alert style="success" >}}For detailed technical information about syntax, expressions and report generation by the engine, please visit: [Working with GroupDocs.Assembly Engine]({{< ref "assembly/python-net/developer-guide/basic-usage/working-with-groupdocs.assembly-engine/_index.md" >}}).{{< /alert >}}

### Download In-Table List with Filtering, Grouping, and Ordering Template

Please download the sample document we created in this article:

*   [in-table-list-with-filtering.html](/assembly/python-net/_sample_files/developer-guide/advanced-usage/working-with-table-reports-filtered-ordered-grouped/in-table-list-with-filtering-grouping-and-ordering-in-html-document/in-table-list-with-filtering.html)

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
assembler.assemble_document("in-table-list-with-filtering.html", "in-table-list-with-filtering-report.html", DataSourceInfo(orders, "orders"))
```
{{< /tab >}}
{{< tab "in-table-list-with-filtering.html" >}}
{{< tab-text >}}
The following sample file is used in this example: [in-table-list-with-filtering.html](/assembly/python-net/_sample_files/developer-guide/advanced-usage/working-with-table-reports-filtered-ordered-grouped/in-table-list-with-filtering-grouping-and-ordering-in-html-document/in-table-list-with-filtering.html)
{{< /tab-text >}}
{{< /tab >}}
{{< tab "orders.json" >}}
{{< tab-text >}}
The following sample file is used in this example: [orders.json](/assembly/python-net/_sample_files/developer-guide/advanced-usage/working-with-table-reports-filtered-ordered-grouped/in-table-list-with-filtering-grouping-and-ordering-in-html-document/orders.json)
{{< /tab-text >}}
{{< /tab >}}
{{< tab "in-table-list-with-filtering-report.html" >}}  
```text
<html>
<body>
<table>
<tr>
<th>
Customer
</th>
<th>
Order Price
</th>
[TRUNCATED]
```
[Download full output](/assembly/python-net/_output_files/developer-guide/advanced-usage/working-with-table-reports-filtered-ordered-grouped/in-table-list-with-filtering-grouping-and-ordering-in-html-document/generating_the_report/in-table-list-with-filtering-report.html)
{{< /tab >}}
{{< /tabs >}}
