---
id: common-master-detail-image-in-spreadsheet-document
url: assembly/python-net/common-master-detail-image-in-spreadsheet-document
title: Common Master-Detail Image in Spreadsheet Document
weight: 2
description: "Common Master-Detail Image in Spreadsheet Document with GroupDocs.Assembly for Python via .NET: the template, the Python data and the code."
keywords: common master-detail image in spreadsheet document, GroupDocs.Assembly, Python, report generation
productName: GroupDocs.Assembly for Python via .NET
hideChildren: False
---
{{< alert style="info" >}}In this article, we will use GroupDocs.Assembly to generate a Common Master-Detail Image report in Spreadsheet Document format based on the use case: [Working with a Business Case]({{< ref "assembly/python-net/developer-guide/basic-usage/working-with-a-business-case/_index.md" >}}).{{< /alert >}}{{< alert style="info" >}}The example reads the shop data described in [The Business Layer]({{< ref "assembly/python-net/developer-guide/basic-usage/working-with-a-business-case/the-business-layer.md" >}}).{{< /alert >}}

## Common Master-Detail Image in Microsoft Excel Document

### Creating a Common Master-Detail Image

Please follow below steps to create Common Master-Detail Image Template in MS Excel 2013:

1.  Create a new Workbook.
2.  Insert a shape to display image in it.
3.  Go to Insert Tab and select shape by clicking on Shape Icon.
4.  Save the document.

### Reporting Requirement

As a report developer, you are required to represent the information of the customers and products with the following key requirements:

*   Report must show customers' picture and name.
*   It must associate the customers with their products.
*   Report must be generated in the Spreadsheet Document.

### Adding Syntax to be evaluated by GroupDocs.Assembly Engine

&lt;&lt;foreach \[in customers\]>>

<table class="gd-assembly1"cellspacing="0" cellpadding="0" style="border-collapse: collapse; float: bottom; margin-top: 0pt; margin-right: 9pt; margin-bottom: 0pt; margin-left: 9pt; width: 132.15pt; height: 132.15pt ">
	<tbody>
		<tr>
			<td style="vertical-align: top;">&lt;&lt;image [customer.Photo]>></td>
		</tr>
	</tbody>
</table>

**&lt;&lt;[CustomerName]>>**

**Clients: &lt;&lt;foreach [in Order]>>&lt;&lt;[IndexOf() != 0 ? ", " : ""]>>&lt;&lt;[Product.ProductName]>>&lt;&lt;/foreach>>**

{{< alert style="success" >}}For detailed technical information about syntax, expressions and report generation by the engine, please visit: [Working with GroupDocs.Assembly Engine]({{< ref "assembly/python-net/developer-guide/basic-usage/working-with-groupdocs.assembly-engine/_index.md" >}}).{{< /alert >}}

### Download Common Master-DetailTemplate

Please download the sample Common Master-Detail document we created in this article:

*   [common-master-detail.xlsx](/assembly/python-net/_sample_files/developer-guide/advanced-usage/working-with-image-reports-common-master-detail/common-master-detail-image-in-spreadsheet-document/common-master-detail.xlsx)

### Generating The Report

{{< tabs "example1" >}}
{{< tab "Python" >}}
```python
import json

from groupdocs.assembly import DataSourceInfo, DocumentAssembler

with open("customers.json", encoding="utf-8") as f:
    customers = json.load(f)

assembler = DocumentAssembler()
assembler.assemble_document("common-master-detail.xlsx", "common-master-detail-report.xlsx", DataSourceInfo(customers, "customers"))
```
{{< /tab >}}
{{< tab "common-master-detail.xlsx" >}}
{{< tab-text >}}
The following sample file is used in this example: [common-master-detail.xlsx](/assembly/python-net/_sample_files/developer-guide/advanced-usage/working-with-image-reports-common-master-detail/common-master-detail-image-in-spreadsheet-document/common-master-detail.xlsx)
{{< /tab-text >}}
{{< /tab >}}
{{< tab "customers.json" >}}
{{< tab-text >}}
The following sample file is used in this example: [customers.json](/assembly/python-net/_sample_files/developer-guide/advanced-usage/working-with-image-reports-common-master-detail/common-master-detail-image-in-spreadsheet-document/customers.json)
{{< /tab-text >}}
{{< /tab >}}
{{< tab "pictures" >}}
{{< tab-text >}}
The following sample files are used in this example: [quayside-bistro.png](/assembly/python-net/_sample_files/developer-guide/advanced-usage/working-with-image-reports-common-master-detail/common-master-detail-image-in-spreadsheet-document/quayside-bistro.png), [lantern-street-cafe.png](/assembly/python-net/_sample_files/developer-guide/advanced-usage/working-with-image-reports-common-master-detail/common-master-detail-image-in-spreadsheet-document/lantern-street-cafe.png), [saltmarsh-deli.png](/assembly/python-net/_sample_files/developer-guide/advanced-usage/working-with-image-reports-common-master-detail/common-master-detail-image-in-spreadsheet-document/saltmarsh-deli.png), [pier-nine-kitchen.png](/assembly/python-net/_sample_files/developer-guide/advanced-usage/working-with-image-reports-common-master-detail/common-master-detail-image-in-spreadsheet-document/pier-nine-kitchen.png)
{{< /tab-text >}}
{{< /tab >}}
{{< tab "common-master-detail-report.xlsx" >}}  
```text
Binary file (XLSX, 43 KB)
```
[Download full output](/assembly/python-net/_output_files/developer-guide/advanced-usage/working-with-image-reports-common-master-detail/common-master-detail-image-in-spreadsheet-document/generating_the_report/common-master-detail-report.xlsx)
{{< /tab >}}
{{< /tabs >}}

## Common Master-Detail in OpenOffice Spreadsheet Document

### Creating the Template

OpenDocument Spreadsheet (ODS) is a spreadsheet document format which can be used as an alternative to Microsoft Excel Document (XLS/XLSX) formats. Since ODS is not a Microsoft Proprietary format, there are multiple software (including Microsoft Office and Apache OpenOffice) available to create, open, edit and save this format. For more information on the available software to work with ODS, please visit wikipedia article.

In this topic, we'll not reinvent the wheel to recreate a template for generating an 'Common Master-Detail' report in ODS format. Instead, we'll save the existing template to ODS format using Microsoft Office. In order to achieve this; assuming you are using Microsoft Office 2010, please follow below steps:

1.  Open existing template we created in previous topic.
2.  Click "File" and select "Save As".
3.  Select "OpenDocument Spreadsheet" from "Save As Type" drop down.
4.  Click "Save".

### Download Template

### Generating the Report

### ODS Template and Report in Apache OpenOffice

In order to check compatibility of ODS between Microsoft Office 2010 and Apache OpenOffice 4.1.2, we performed below tests:

*   We opened the ODS template created through Microsoft Office 2010 in Apache OpenOffice 4.1.2. The template opened successfully in Apache OpenOffice without any issues or formatting losses.
*   We opened the ODS report generated through GroupDocs.Assembly in Apache OpenOffice 4.1.2. The report opened successfully in Apache OpenOffice without any issues or formatting losses.
