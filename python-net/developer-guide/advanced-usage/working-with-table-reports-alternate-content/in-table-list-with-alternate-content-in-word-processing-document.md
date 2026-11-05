---
id: in-table-list-with-alternate-content-in-word-processing-document
url: assembly/python-net/in-table-list-with-alternate-content-in-word-processing-document
title: In-Table List With Alternate Content in Word Processing Document
weight: 1
description: "In-Table List With Alternate Content in Word Processing Document with GroupDocs.Assembly for Python via .NET: the template, the Python data and the code."
keywords: in-table list with alternate content in word processing document, GroupDocs.Assembly, Python, report generation
productName: GroupDocs.Assembly for Python via .NET
hideChildren: False
---
{{< alert style="info" >}}In this article, we will use GroupDocs.Assembly to generate a In-Table List With Alternate Content report in Word Processing Document format based on the use case: [Working with a Business Case]({{< ref "assembly/python-net/developer-guide/basic-usage/working-with-a-business-case/_index.md" >}}).{{< /alert >}}

## In-Table List With Alternate Content in Microsoft Word Document

### Creating a In-Table List With Alternate Content

Practicing the following steps you can create In-Table List With Alternate Content Template in MS Word 2013.

1.  Click the document where you want to add the table.
2.  Press "Insert" tab to insert the table.
3.  Insert a 2X3 table.
4.  Save the template.

### Reporting Requirement

As a report developer, you are required to represent your products and their prices with the following key requirements:

*   Report must show each product along with its price.
*   It must show sum of all the prices.
*   It must represent all the information in tabular form.
*   Report must be generated in the Word Processing Document.

### Adding Syntax to be evaluated by GroupDocs.Assembly Engine

<table class="gd-assembly">
	<tbody>
		<tr>
			<td>Products</td>
			<td>Order Price</td>
		</tr>
		<tr align="center">
			<td colspan="2">&lt;&lt;if [!Any()]>>No data</td>
		</tr>
		<tr>
			<td>&lt;&lt;else>>&lt;&lt;foreach [in orders]>><br>&lt;&lt;[Product.ProductName]>></td>
			<td>&lt;&lt;[Price]>>&lt;&lt;/foreach>></td>
		</tr>
		<tr>
			<td>Total:</td>
			<td>&lt;&lt;[Sum(c => c.Price)]>>&lt;&lt;/if>></td>
		</tr>
	</tbody>
</table>

{{< alert style="success" >}}For detailed technical information about syntax,expressions and report generation by the engine, please visit: [Working with GroupDocs.Assembly Engine]({{< ref "assembly/python-net/developer-guide/basic-usage/working-with-groupdocs.assembly-engine/_index.md" >}}).{{< /alert >}}

### Download In-Table List With Alternate Content Template

Please download the sample In-Table List With Alternate Content document we created in this article:

*   [in-table-list-with-alternate-content.docx](/assembly/python-net/_sample_files/developer-guide/advanced-usage/working-with-table-reports-alternate-content/in-table-list-with-alternate-content-in-word-processing-document/in-table-list-with-alternate-content.docx)

### Generating The Report

{{< alert style="info" >}}The example reads the shop data described in [The Business Layer]({{< ref "assembly/python-net/developer-guide/basic-usage/working-with-a-business-case/the-business-layer.md" >}}).{{< /alert >}}

{{< tabs "example1" >}}
{{< tab "Python" >}}
```python
import json

from groupdocs.assembly import DataSourceInfo, DocumentAssembler

with open("orders.json", encoding="utf-8") as f:
    orders = json.load(f)

assembler = DocumentAssembler()
assembler.assemble_document("in-table-list-with-alternate-content.docx", "in-table-list-with-alternate-content-report.docx", DataSourceInfo(orders, "orders"))
```
{{< /tab >}}
{{< tab "in-table-list-with-alternate-content.docx" >}}
{{< tab-text >}}
The following sample file is used in this example: [in-table-list-with-alternate-content.docx](/assembly/python-net/_sample_files/developer-guide/advanced-usage/working-with-table-reports-alternate-content/in-table-list-with-alternate-content-in-word-processing-document/in-table-list-with-alternate-content.docx)
{{< /tab-text >}}
{{< /tab >}}
{{< tab "orders.json" >}}
{{< tab-text >}}
The following sample file is used in this example: [orders.json](/assembly/python-net/_sample_files/developer-guide/advanced-usage/working-with-table-reports-alternate-content/in-table-list-with-alternate-content-in-word-processing-document/orders.json)
{{< /tab-text >}}
{{< /tab >}}
{{< tab "in-table-list-with-alternate-content-report.docx" >}}  
```text
Binary file (DOCX, 10 KB)
```
[Download full output](/assembly/python-net/_output_files/developer-guide/advanced-usage/working-with-table-reports-alternate-content/in-table-list-with-alternate-content-in-word-processing-document/generating_the_report/in-table-list-with-alternate-content-report.docx)
{{< /tab >}}
{{< /tabs >}}

## In-Table List With Alternate Content in OpenOffice Document

### Creating the Template

OpenDocument Text (ODT) is a word processing document format which can be used as an alternative to Microsoft Word Document (DOC/DOCX) formats. Since ODT is not a Microsoft Proprietary format, there are multiple software (including Microsoft Office and Apache OpenOffice) available to create, open, edit and save this format. For more information on the available software to work with ODT, please visit [wikipedia article](https://en.wikipedia.org/wiki/OpenDocument#Software).

In this topic, we 'll not reinvent the wheel to recreate a template for generating an 'In-Table List with Alternate Content' report in ODT format. Instead, we'll save the existing template to ODT format using Microsoft Office. In order to achieve this; assuming you are using Microsoft Office 2010, please follow below steps:

1.  Open existing template we created in previous topic.
2.  Click "File" and select "Save As".
3.  Select "OpenDocument Text" from "Save As Type" drop down.
4.  Click "Save".

### Download Template

### Generating the report

### ODT Template and Report in Apache OpenOffice

In order to check compatibility of ODT between Microsoft Office 2010 and Apache OpenOffice 4.1.2, we performed below tests:

*   We opened the ODT template created through Microsoft Office 2010 in Apache OpenOffice 4.1.2. The template opened successfully in Apache OpenOffice without any issues or formatting losses.
*   We opened the ODT report generated through GroupDocs.Assembly in Apache OpenOffice 4.1.2. The report opened successfully in Apache OpenOffice without any issues or formatting losses.
