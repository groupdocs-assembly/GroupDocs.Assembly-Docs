---
id: single-row-image-in-presentation-document
url: assembly/python-net/single-row-image-in-presentation-document
title: Single Row Image in Presentation Document
weight: 3
description: "Single Row Image in Presentation Document with GroupDocs.Assembly for Python via .NET: the template, the Python data and the code."
keywords: single row image in presentation document, GroupDocs.Assembly, Python, report generation
productName: GroupDocs.Assembly for Python via .NET
hideChildren: False
---
{{< alert style="info" >}}In this article, we will use GroupDocs.Assembly to generate a Single Row Image report in Presentation Document format based on the use case: [Working with a Business Case]({{< ref "assembly/python-net/developer-guide/basic-usage/working-with-a-business-case/_index.md" >}}).{{< /alert >}}

## Single Row in Microsoft PowerPoint Document

### Creating a Single Row

Please follow below steps to create Single Row Image in MS PowerPoint 2013:

1.  Create a new presentation slide.
2.  Insert the desired shape to display the image in it.
3.  Go to Insert Tab and select shape by clicking on Shape Icon.
4.  Write "Name" and "Contact Number" to show the name and contact info of the customer.
5.  Save the template.

### Reporting Requirement

As a report developer, you are required to represent information of first single customer with the following key requirements:

*   Report must show image of the customer.
*   It must show Name and Contact Number of the customer.
*   Report must be generated in the Presentation Document.

### Adding Syntax to be evaluated by GroupDocs.Assembly Engine

{{< alert style="warning" >}}At the moment, GroupDocs.Assembly does not support images in PowerPoint Presentation.{{< /alert >}}

<table class="iksweb">
	<tbody>
		<tr>
			<td rowspan="2" style="font-size: 44pt">Click to<br> add title</td>
			<td>Name:</td>
			<td><<[customer.CustomerName]>></td>
		</tr>
		<tr>
			<td>Contact Details:</td>
			<td><<[customer. CustomerContactNumber]>></td>
		</tr>
	</tbody>
</table>

{{< alert style="success" >}}For detailed technical information about syntax, expressions and report generation by the engine, please visit: [Working with GroupDocs.Assembly Engine]({{< ref "assembly/python-net/developer-guide/basic-usage/working-with-groupdocs.assembly-engine/_index.md" >}}).{{< /alert >}}

### Download Single Row Template

Please download the sample Single Row document we created in this article:

*   [single-row.pptx](/assembly/python-net/_sample_files/developer-guide/advanced-usage/working-with-image-reports-single-row/single-row-image-in-presentation-document/single-row.pptx)

{{< alert style="warning" >}}Use this template for DB, Dataset, JSON and XML examples also.{{< /alert >}}

### Generating The Report

{{< tabs "example1" >}}
{{< tab "Python" >}}
```python
import json

from groupdocs.assembly import DataSourceInfo, DocumentAssembler

with open("customer.json", encoding="utf-8") as f:
    customer = json.load(f)

assembler = DocumentAssembler()
assembler.assemble_document("single-row.pptx", "single-row-report.pptx", DataSourceInfo(customer, "customer"))
```
{{< /tab >}}
{{< tab "single-row.pptx" >}}
{{< tab-text >}}
The following sample file is used in this example: [single-row.pptx](/assembly/python-net/_sample_files/developer-guide/advanced-usage/working-with-image-reports-single-row/single-row-image-in-presentation-document/single-row.pptx)
{{< /tab-text >}}
{{< /tab >}}
{{< tab "customer.json" >}}
{{< tab-text >}}
The following sample file is used in this example: [customer.json](/assembly/python-net/_sample_files/developer-guide/advanced-usage/working-with-image-reports-single-row/single-row-image-in-presentation-document/customer.json)
{{< /tab-text >}}
{{< /tab >}}
{{< tab "pictures" >}}
{{< tab-text >}}
The following sample files are used in this example: [quayside-bistro.png](/assembly/python-net/_sample_files/developer-guide/advanced-usage/working-with-image-reports-single-row/single-row-image-in-presentation-document/quayside-bistro.png), [lantern-street-cafe.png](/assembly/python-net/_sample_files/developer-guide/advanced-usage/working-with-image-reports-single-row/single-row-image-in-presentation-document/lantern-street-cafe.png), [saltmarsh-deli.png](/assembly/python-net/_sample_files/developer-guide/advanced-usage/working-with-image-reports-single-row/single-row-image-in-presentation-document/saltmarsh-deli.png), [pier-nine-kitchen.png](/assembly/python-net/_sample_files/developer-guide/advanced-usage/working-with-image-reports-single-row/single-row-image-in-presentation-document/pier-nine-kitchen.png)
{{< /tab-text >}}
{{< /tab >}}
{{< tab "single-row-report.pptx" >}}  
```text
Binary file (PPTX, 32 KB)
```
[Download full output](/assembly/python-net/_output_files/developer-guide/advanced-usage/working-with-image-reports-single-row/single-row-image-in-presentation-document/generating_the_report/single-row-report.pptx)
{{< /tab >}}
{{< /tabs >}}

## Single Row in OpenOffice Presentation Document

### Creating the Template

OpenDocument Presentation (ODP) is a presentation document format which can be used as an alternative to Microsoft PowerPoint Document (PPT/PPTX) formats. Since ODP is not a Microsoft Proprietary format, there are multiple software (including Microsoft Office and Apache OpenOffice) available to create, open, edit and save this format. For more information on the available software to work with ODP, please visit [wikipedia article](https://en.wikipedia.org/wiki/OpenDocument#Software).

In this topic, we'll not reinvent the wheel to recreate a template for generating an 'Single Row' report in ODP format. Instead, we'll save the existing template to ODP format using Microsoft Office. In order to achieve this; assuming you are using Microsoft Office 2010, please follow below steps:

1.  Open existing template we created in previous topic.
2.  Click "File" and select "Save As".
3.  Select "OpenDocument Text" from "Save As Type" drop down.
4.  Click "Save".

### Download Template

### Generating the report

### ODP Template and Report in Apache OpenOffice

In order to check compatibility of ODP between Microsoft Office 2010 and Apache OpenOffice 4.1.2, we performed below tests:

*   We opened the ODP template created through Microsoft Office 2010 in Apache OpenOffice 4.1.2. The template opened successfully in Apache OpenOffice without any issues or formatting losses.
*   We opened the ODP report generated through GroupDocs.Assembly in Apache OpenOffice 4.1.2. The report opened successfully in Apache OpenOffice without any issues or formatting losses.
