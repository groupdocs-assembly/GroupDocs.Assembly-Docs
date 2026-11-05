---
id: numbered-list-in-word-processing-document
url: assembly/python-net/numbered-list-in-word-processing-document
title: Numbered List in Word Processing Document
weight: 1
description: "Numbered List in Word Processing Document with GroupDocs.Assembly for Python via .NET: the template, the Python data and the code."
keywords: numbered list in word processing document, GroupDocs.Assembly, Python, report generation
productName: GroupDocs.Assembly for Python via .NET
hideChildren: False
---
{{< alert style="info" >}}In this article, we will use GroupDocs.Assembly to generate a Numbered List report in Word Processing Document format based on the use case: [Working with a Business Case]({{< ref "assembly/python-net/developer-guide/basic-usage/working-with-a-business-case/_index.md" >}}).{{< /alert >}}{{< alert style="info" >}}The example reads the shop data described in [The Business Layer]({{< ref "assembly/python-net/developer-guide/basic-usage/working-with-a-business-case/the-business-layer.md" >}}).{{< /alert >}}

## Numbered List in Microsoft Word Document

### Creating a Numbered List

Practising the following steps you can create Numbered List Template in MS Word 2013.

1.  In your document, write a sentence like "We provide support for the following products:".
2.  Start numbered list.
3.  Save the template.

### Reporting Requirement

As a report developer, you are required to describe the services you are providing with the following key requirements:

*   The report must show the products in the numbered list.
*   The report must be generated in the Word Processing Document.

### Adding Syntax to be evaluated by GroupDocs.Assembly Engine

```text
We provide support for the following products:
1.	<<foreach [in products]>><<[ProductName]>>
<</foreach>>
```

{{< alert style="success" >}}For detailed technical information about syntax, expressions and report generation by the engine, please visit: [Working with GroupDocs.Assembly Engine]({{< ref "assembly/python-net/developer-guide/basic-usage/working-with-groupdocs.assembly-engine/_index.md" >}}).{{< /alert >}}

Download Numbered List Template

Please download the sample Numbered List document we created in this article:

*   [numbered-list.odt](/assembly/python-net/_sample_files/developer-guide/advanced-usage/working-with-list-reports-numbered/numbered-list-in-word-processing-document/numbered-list.odt)
*   [numbered-list-with-restartnum.docx](/assembly/python-net/_sample_files/developer-guide/advanced-usage/working-with-list-reports-numbered/numbered-list-in-word-processing-document/numbered-list-with-restartnum.docx)

### Generating The Report

{{< tabs "example1" >}}
{{< tab "Python" >}}
```python
import json

from groupdocs.assembly import DataSourceInfo, DocumentAssembler

with open("products.json", encoding="utf-8") as f:
    products = json.load(f)

assembler = DocumentAssembler()
assembler.assemble_document("numbered-list.odt", "numbered-list-report.odt", DataSourceInfo(products, "products"))
```
{{< /tab >}}
{{< tab "numbered-list.odt" >}}
{{< tab-text >}}
The following sample file is used in this example: [numbered-list.odt](/assembly/python-net/_sample_files/developer-guide/advanced-usage/working-with-list-reports-numbered/numbered-list-in-word-processing-document/numbered-list.odt)
{{< /tab-text >}}
{{< /tab >}}
{{< tab "products.json" >}}
{{< tab-text >}}
The following sample file is used in this example: [products.json](/assembly/python-net/_sample_files/developer-guide/advanced-usage/working-with-list-reports-numbered/numbered-list-in-word-processing-document/products.json)
{{< /tab-text >}}
{{< /tab >}}
{{< tab "numbered-list-report.odt" >}}  
```text
Binary file (ODT, 4 KB)
```
[Download full output](/assembly/python-net/_output_files/developer-guide/advanced-usage/working-with-list-reports-numbered/numbered-list-in-word-processing-document/generating_the_report/numbered-list-report.odt)
{{< /tab >}}
{{< /tabs >}}

{{< tabs "example2" >}}
{{< tab "Python" >}}
```python
import json

from groupdocs.assembly import DataSourceInfo, DocumentAssembler

with open("orders.json", encoding="utf-8") as f:
    orders = json.load(f)

assembler = DocumentAssembler()
assembler.assemble_document("numbered-list-with-restartnum.docx", "numbered-list-with-restartnum-report.docx", DataSourceInfo(orders, "orders"))
```
{{< /tab >}}
{{< tab "numbered-list-with-restartnum.docx" >}}
{{< tab-text >}}
The following sample file is used in this example: [numbered-list-with-restartnum.docx](/assembly/python-net/_sample_files/developer-guide/advanced-usage/working-with-list-reports-numbered/numbered-list-in-word-processing-document/numbered-list-with-restartnum.docx)
{{< /tab-text >}}
{{< /tab >}}
{{< tab "orders.json" >}}
{{< tab-text >}}
The following sample file is used in this example: [orders.json](/assembly/python-net/_sample_files/developer-guide/advanced-usage/working-with-list-reports-numbered/numbered-list-in-word-processing-document/orders.json)
{{< /tab-text >}}
{{< /tab >}}
{{< tab "numbered-list-with-restartnum-report.docx" >}}  
```text
Binary file (DOCX, 13 KB)
```
[Download full output](/assembly/python-net/_output_files/developer-guide/advanced-usage/working-with-list-reports-numbered/numbered-list-in-word-processing-document/generating_the_report_2/numbered-list-with-restartnum-report.docx)
{{< /tab >}}
{{< /tabs >}}

## Numbered List in OpenOffice Document

### Creating the Template

OpenDocument Text (ODT) is a word processing document format which can be used as an alternative to Microsoft Word Document (DOC/DOCX) formats. Since ODT is not a Microsoft Proprietary format, there are multiple software (including Microsoft Office and Apache OpenOffice) available to create, open, edit and save this format. For more information on the available software to work with ODT, please visit [wikipedia article](https://en.wikipedia.org/wiki/OpenDocument#Software).

In this topic, we'll not reinvent the wheel to recreate a template for generating an 'Numbered List' report in ODT format. Instead, we'll save the existing template to ODT format using Microsoft Office. In order to achieve this; assuming you are using Microsoft Office 2010, please follow below steps:

1.  Open existing template we created in previous topic.
2.  Click "File" and select "Save As".
3.  Select "OpenDocument Text" from "Save As Type" drop down.
4.  Click "Save".

### Download Template

### Generating the Report

### ODT Template and Report in Apache OpenOffice

In order to check compatibility of ODT between Microsoft Office 2010 and Apache OpenOffice 4.1.2, we performed below tests:

*   We opened the ODT template created through Microsoft Office 2010 in Apache OpenOffice 4.1.2. The template opened successfully in Apache OpenOffice without any issues or formatting losses.
*   We opened the ODT report generated through GroupDocs.Assembly in Apache OpenOffice 4.1.2. The report opened successfully in Apache OpenOffice without any issues or formatting losses.

## Numbering Restart in Nested Numbered List 

The GroupDocs.Assembly engine allows restart list numbering within your documents dynamically using *<<restartNum>>* tags. In particular, this feature is useful when working with a nested numbered list within a data band.  

Assume that we are picking *Order* and *Service* classes as defined in the following *Custom Objects* of our business use case.

Given that orders is an enumeration of Order instances, you could try to use the following template to output information on several orders in one document.

```text
<<foreach [in orders]>><<[Customer.CustomerName]>> (<<[Customer.CustomerContactNumber]>>)
1.	<<foreach [in Services]>><<[ServiceName]>>
<</foreach>><</foreach>>
```

The generated report will look as follows:

```
Jane Doe (+9211874)
	1.	Regular Cleaning
	2.	Oven Cleaning
John Smith (+458789)
	3.	Regular Cleaning
	4.	Oven Cleaning
	5.	Carpet Cleaning
John Smith (+458789)
	6.	Regular Cleaning
	7.	Carpet Cleaning
John Smith (+458789)
	8.	Oven Cleaning
```

However, there would be a single numbered list across all orders, which is not applicable for this scenario. Hence, you can make the list numbering to restart for every order by putting a *<<restartNum>>* tag into your template before a corresponding *<<foreach>>* tag as follows:

```text
<<foreach [in orders]>><<[ Customer.CustomerName]>> (<<[Customer.CustomerContactNumber]>>)
1.	<<restartNum>><<foreach [in Services]>><<[ServiceName]>>
<</foreach>><</foreach>>
```

 Then, the generated report will look as follows:

```
Jane Doe (+9211874)
	1.	Regular Cleaning
	2.	Oven Cleaning
John Smith (+458789)
	1.	Regular Cleaning
	2.	Oven Cleaning
	3.	Carpet Cleaning
John Smith (+458789)
	1.	Regular Cleaning
	2.	Carpet Cleaning
John Smith (+458789)
	1.	Oven Cleaning
```
