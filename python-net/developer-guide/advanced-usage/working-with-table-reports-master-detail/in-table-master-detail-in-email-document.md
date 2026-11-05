---
id: in-table-master-detail-in-email-document
url: assembly/python-net/in-table-master-detail-in-email-document
title: In-Table Master-Detail in Email Document
weight: 5
description: "In-Table Master-Detail in Email Document with GroupDocs.Assembly for Python via .NET: the template, the Python data and the code."
keywords: in-table master-detail in email document, GroupDocs.Assembly, Python, report generation
productName: GroupDocs.Assembly for Python via .NET
hideChildren: False
---
{{< alert style="info" >}}In this article, we will use GroupDocs.Assembly to generate an In-Table Master-Detail report in Email Document format.{{< /alert >}}{{< alert style="info" >}}The example reads the shop data described in [The Business Layer]({{< ref "assembly/python-net/developer-guide/basic-usage/working-with-a-business-case/the-business-layer.md" >}}).{{< /alert >}}

## In-Table Master-Detail in Email Document

### Creating a In-Table Master-Detail

Practising the following steps you can create In-Table Master-Detail Template in MS Outlook 2013.

1.  Create a new Email.
2.  Click the email where you want to add the table.
3.  Press "Insert" tab to insert the table.
4.  Insert a 2x4 table.
5.  Save the template.

### Reporting Requirement

As a report developer, you are required to represent the following key requirements:

*   The report must be in .eml or .msg format.
*   It must add email recipient, CSS and subject of the email.
*   The report must show each customer along with his total orders prices.
*   It must also show each individual product ordered by the customers.
*   It must show sum of the order prices.
*   It must represent all the information in tabular form.

### Adding Syntax to be evaluated by GroupDocs.Assembly Engine

<table class="tbl1">
	<tbody>
		<tr>
			<td colspan="2"> &lt;&lt;foreach [in customers]>> &lt;&lt;foreach [in Order]>> &lt;&lt;/foreach>> &lt;&lt;/foreach>></td>
		</tr>
		<tr>
			<td>Customer</td>
			<td>Order Price</td>
		</tr>
		<tr>
			<td><<[CustomerName]>>
</td>
			<td><<[Order.Sum(c => c.Price)]>></td>
		</tr>
		<tr>
			<td colspan="2">  <<[Product.ProductName]>> <<[Price]>></td>
		</tr>
		<tr>
			<td>Total:</td>
			<td><<[Sum( m => m.Order.Sum( c => c.Price))]>></td>
		</tr>
	</tbody>
</table>

{{< alert style="success" >}}For detailed technical information about syntax, expressions and report generation by the engine, please visit: [Working with GroupDocs.Assembly Engine]({{< ref "assembly/python-net/developer-guide/basic-usage/working-with-groupdocs.assembly-engine/_index.md" >}}).{{< /alert >}}

### Download In-Table Master-Detail Template

Please download the sample In-Table Master-Detail document we created in this article:

*   [in-table-master-detail.msg](/assembly/python-net/_sample_files/developer-guide/advanced-usage/working-with-table-reports-master-detail/in-table-master-detail-in-email-document/in-table-master-detail.msg)

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

with open("customers.json", encoding="utf-8") as f:
    customers = json.load(f, object_hook=parse_dates)

assembler = DocumentAssembler()
assembler.assemble_document("in-table-master-detail.msg", "in-table-master-detail-report.msg", [
    DataSourceInfo(customers, "customers"),
    DataSourceInfo("Harbor Lane Provisions <orders@harborlane.example>", "sender"),
    DataSourceInfo(["Quayside Bistro <orders@quaysidebistro.example>", "jonas.weber@harborlane.example"], "recipients"),
    DataSourceInfo("amara.osei@harborlane.example", "cc"),
    DataSourceInfo("In table master detail", "subject"),
])
```
{{< /tab >}}
{{< tab "in-table-master-detail.msg" >}}
{{< tab-text >}}
The following sample file is used in this example: [in-table-master-detail.msg](/assembly/python-net/_sample_files/developer-guide/advanced-usage/working-with-table-reports-master-detail/in-table-master-detail-in-email-document/in-table-master-detail.msg)
{{< /tab-text >}}
{{< /tab >}}
{{< tab "customers.json" >}}
{{< tab-text >}}
The following sample file is used in this example: [customers.json](/assembly/python-net/_sample_files/developer-guide/advanced-usage/working-with-table-reports-master-detail/in-table-master-detail-in-email-document/customers.json)
{{< /tab-text >}}
{{< /tab >}}
{{< tab "in-table-master-detail-report.msg" >}}  
```text
Binary file (MSG, 55 KB)
```
[Download full output](/assembly/python-net/_output_files/developer-guide/advanced-usage/working-with-table-reports-master-detail/in-table-master-detail-in-email-document/generating_the_report/in-table-master-detail-report.msg)
{{< /tab >}}
{{< /tabs >}}
