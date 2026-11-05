---
id: generating-report-using-multiple-data-sources-in-spreadsheet-document
url: assembly/python-net/generating-report-using-multiple-data-sources-in-spreadsheet-document
title: Generating Report using Multiple Data Sources in Spreadsheet Document
weight: 2
description: "Generating Report using Multiple Data Sources in Spreadsheet Document with GroupDocs.Assembly for Python via .NET: the template, the Python data and the code."
keywords: generating report using multiple data sources in spreadsheet document, GroupDocs.Assembly, Python, report generation
productName: GroupDocs.Assembly for Python via .NET
hideChildren: False
---
{{< alert style="info" >}}In this article, we will use GroupDocs.Assembly to generate a report. This report will fetch data from multiple data sources.{{< /alert >}}{{< alert style="info" >}}The example reads the shop data described in [The Business Layer]({{< ref "assembly/python-net/developer-guide/basic-usage/working-with-a-business-case/the-business-layer.md" >}}).{{< /alert >}}

## Generating Report in Microsoft Excel Document

### Creating a Template

1.  Insert a desired shape to display image in it.
2.  Go to Insert Tab and select shape by clicking on Shape Icon.
3.  Add a bullet list at the place where you want it
4.  Save your Document

### Reporting Requirement

As a report developer, you are required to generate a report that fetches data from two different data sources (e:g XML, JSON). Report must show following information:

*   Customer name and picture
*   List of products

### Adding Syntax to be evaluated by GroupDocs.Assembly Engine

<table class="gd-assembly">
	<tbody>
		<tr>
			<td colspan="3">&lt;&lt;foreach [in customers]>></td>
			<td></td>
			<td></td>
		</tr>
		<tr style="vertical-align: top">
			<td colspan="3" rowspan="8">&lt;&lt;image[customer.Photo]>></td>
			<td></td>
			<td></td>
		</tr>
		<tr>
			<td></td>
			<td></td>
		</tr>
		<tr>
			<td></td>
			<td></td>
		</tr>
		<tr>
			<td></td>
			<td></td>
		</tr>
		<tr>
			<td></td>
			<td></td>
		</tr>
		<tr>
			<td></td>
			<td></td>
		</tr>
		<tr>
			<td></td>
			<td></td>
		</tr>
		<tr>
			<td></td>
			<td></td>
		</tr>
		<tr>
			<td colspan="3">&lt;&lt;[CustomerName]>></td>
			<td colspan="2">&lt;&lt;/foreach>></td>
		</tr>
	</tbody>
</table>

**In-Cell List**

```text
We provide support for the following products:
<<foreach [in products]>>
-          <<[ProductName]>><</foreach>>
```

{{< alert style="success" >}}For detailed technical information about syntax,expressions and report generation by the engine, please visit: [Working with GroupDocs.Assembly Engine]({{< ref "assembly/python-net/developer-guide/basic-usage/working-with-groupdocs.assembly-engine/_index.md" >}}){{< /alert >}}

### Download Template

Get template from here.

*   [multiple-data-source.ods](/assembly/python-net/_sample_files/developer-guide/advanced-usage/working-with-multiple-data-sources/generating-report-using-multiple-data-sources-in-spreadsheet-document/multiple-data-source.ods)

### Generating the Report

{{< tabs "example1" >}}
{{< tab "Python" >}}
```python
import json

from groupdocs.assembly import DataSourceInfo, DocumentAssembler

with open("customers.json", encoding="utf-8") as f:
    customers = json.load(f)

with open("products.json", encoding="utf-8") as f:
    products = json.load(f)

assembler = DocumentAssembler()
assembler.assemble_document("multiple-data-source.ods", "multiple-data-source-report.ods", [
    DataSourceInfo(customers, "customers"),
    DataSourceInfo(products, "products"),
])
```
{{< /tab >}}
{{< tab "multiple-data-source.ods" >}}
{{< tab-text >}}
The following sample file is used in this example: [multiple-data-source.ods](/assembly/python-net/_sample_files/developer-guide/advanced-usage/working-with-multiple-data-sources/generating-report-using-multiple-data-sources-in-spreadsheet-document/multiple-data-source.ods)
{{< /tab-text >}}
{{< /tab >}}
{{< tab "customers.json" >}}
{{< tab-text >}}
The following sample file is used in this example: [customers.json](/assembly/python-net/_sample_files/developer-guide/advanced-usage/working-with-multiple-data-sources/generating-report-using-multiple-data-sources-in-spreadsheet-document/customers.json)
{{< /tab-text >}}
{{< /tab >}}
{{< tab "products.json" >}}
{{< tab-text >}}
The following sample file is used in this example: [products.json](/assembly/python-net/_sample_files/developer-guide/advanced-usage/working-with-multiple-data-sources/generating-report-using-multiple-data-sources-in-spreadsheet-document/products.json)
{{< /tab-text >}}
{{< /tab >}}
{{< tab "pictures" >}}
{{< tab-text >}}
The following sample files are used in this example: [quayside-bistro.png](/assembly/python-net/_sample_files/developer-guide/advanced-usage/working-with-multiple-data-sources/generating-report-using-multiple-data-sources-in-spreadsheet-document/quayside-bistro.png), [lantern-street-cafe.png](/assembly/python-net/_sample_files/developer-guide/advanced-usage/working-with-multiple-data-sources/generating-report-using-multiple-data-sources-in-spreadsheet-document/lantern-street-cafe.png), [saltmarsh-deli.png](/assembly/python-net/_sample_files/developer-guide/advanced-usage/working-with-multiple-data-sources/generating-report-using-multiple-data-sources-in-spreadsheet-document/saltmarsh-deli.png), [pier-nine-kitchen.png](/assembly/python-net/_sample_files/developer-guide/advanced-usage/working-with-multiple-data-sources/generating-report-using-multiple-data-sources-in-spreadsheet-document/pier-nine-kitchen.png)
{{< /tab-text >}}
{{< /tab >}}
{{< tab "multiple-data-source-report.ods" >}}  
```text
Binary file (ODS, 22 KB)
```
[Download full output](/assembly/python-net/_output_files/developer-guide/advanced-usage/working-with-multiple-data-sources/generating-report-using-multiple-data-sources-in-spreadsheet-document/generating_the_report/multiple-data-source-report.ods)
{{< /tab >}}
{{< /tabs >}}

## Generating Report in OpenOffice Spreadsheet Document

### Creating the Template

OpenDocument Text (ODT) is a word processing document format which can be used as an alternative to Microsoft Word Document (DOC/DOCX) formats. Since ODT is not a Microsoft Proprietary format, there are multiple software (including Microsoft Office and Apache OpenOffice) available to create, open, edit and save this format. For more information on the available software to work with ODT, please visit [wikipedia article](https://en.wikipedia.org/wiki/OpenDocument#Software).

In this topic, we'll not reinvent the wheel to recreate a template for generating a report in ODT format. Instead, we'll save the existing template to ODT format using Microsoft Office. In order to achieve this; assuming you are using Microsoft Office 2010, please follow below steps:

1.  Open existing template we created in previous topic.
2.  Click "File" and select "Save As".
3.  Select "OpenDocument Text" from "Save As Type" drop down.
4.  Click "Save".

### Download Template

Get template from here.
