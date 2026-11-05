---
id: in-table-master-detail-in-html-document
url: assembly/python-net/in-table-master-detail-in-html-document
title: In-Table Master-Detail in HTML Document
weight: 4
description: "In-Table Master-Detail in HTML Document with GroupDocs.Assembly for Python via .NET: the template, the Python data and the code."
keywords: in-table master-detail in html document, GroupDocs.Assembly, Python, report generation
productName: GroupDocs.Assembly for Python via .NET
hideChildren: False
---
{{< alert style="info" >}}In this article, we will use GroupDocs.Assembly to generate In-Table Master-Detail report in HTML Document format.{{< /alert >}}{{< alert style="info" >}}The example reads the shop data described in [The Business Layer]({{< ref "assembly/python-net/developer-guide/basic-usage/working-with-a-business-case/the-business-layer.md" >}}).{{< /alert >}}

## In-Table Master-Detail in HTML Document

### Reporting Requirement

As a report developer, you are required to represent customers' total orders prices and price of each product separately with the following key requirements:

*   The report must show each customer along with his total orders prices.
*   It must also show each individual product ordered by the customers.
*   It must show sum of the order prices.
*   It must represent all the information in tabular form.
*   The report must be generated in the HTML Document.

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

### Download  In-Table Master-Detail Template

Please download the sample In-Table Master-Detail document we created in this article:

*   [in-table-master-detail.html](/assembly/python-net/_sample_files/developer-guide/advanced-usage/working-with-table-reports-master-detail/in-table-master-detail-in-html-document/in-table-master-detail.html)

### Generating The Report

{{< tabs "example1" >}}
{{< tab "Python" >}}
```python
import json

from groupdocs.assembly import DataSourceInfo, DocumentAssembler

with open("customers.json", encoding="utf-8") as f:
    customers = json.load(f)

assembler = DocumentAssembler()
assembler.assemble_document("in-table-master-detail.html", "in-table-master-detail-report.html", DataSourceInfo(customers, "customers"))
```
{{< /tab >}}
{{< tab "in-table-master-detail.html" >}}
{{< tab-text >}}
The following sample file is used in this example: [in-table-master-detail.html](/assembly/python-net/_sample_files/developer-guide/advanced-usage/working-with-table-reports-master-detail/in-table-master-detail-in-html-document/in-table-master-detail.html)
{{< /tab-text >}}
{{< /tab >}}
{{< tab "customers.json" >}}
{{< tab-text >}}
The following sample file is used in this example: [customers.json](/assembly/python-net/_sample_files/developer-guide/advanced-usage/working-with-table-reports-master-detail/in-table-master-detail-in-html-document/customers.json)
{{< /tab-text >}}
{{< /tab >}}
{{< tab "in-table-master-detail-report.html" >}}  
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
[Download full output](/assembly/python-net/_output_files/developer-guide/advanced-usage/working-with-table-reports-master-detail/in-table-master-detail-in-html-document/generating_the_report/in-table-master-detail-report.html)
{{< /tab >}}
{{< /tabs >}}
