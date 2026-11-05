---
id: bulleted-list-in-word-processing-document
url: assembly/python-net/bulleted-list-in-word-processing-document
title: Bulleted List in Word Processing Document
weight: 1
description: "Bulleted List in Word Processing Document with GroupDocs.Assembly for Python via .NET: the template, the Python data and the code."
keywords: bulleted list in word processing document, GroupDocs.Assembly, Python, report generation
productName: GroupDocs.Assembly for Python via .NET
hideChildren: False
---
{{< alert style="info" >}}In this article, we will use GroupDocs.Assembly to generate a Bulleted List report in Word Processing Document format based on the use case: [Working with a Business Case]({{< ref "assembly/python-net/developer-guide/basic-usage/working-with-a-business-case/_index.md" >}}).{{< /alert >}}{{< alert style="info" >}}The example reads the shop data described in [The Business Layer]({{< ref "assembly/python-net/developer-guide/basic-usage/working-with-a-business-case/the-business-layer.md" >}}).{{< /alert >}}

## Bulleted List in Microsoft Word Document

### Creating a Bulleted List

Practising the following steps you can insert Bulleted List in MS Word 2013.

1.  Add a bullet list at the place where you want it.
2.  Save your Document.

### Reporting Requirement

As a report developer, you are required to share the information of the products with the following key requirements:

*   Report must show all the products in a bulleted list format.
*   Report must be generated in the Word Processing Document.

### Adding Syntax to be evaluated by GroupDocs.Assembly Engine

**Template Syntax**

```text
We provide support for the following products:
. <<foreach [in products]>><<[ProductName]>>
<</foreach>>
```

{{< alert style="success" >}}For detailed technical information about syntax, expressions and report generation by the engine, please visit: [Working with GroupDocs.Assembly Engine]({{< ref "assembly/python-net/developer-guide/basic-usage/working-with-groupdocs.assembly-engine/_index.md" >}}).{{< /alert >}}

### Download Bulleted List Template

Please download the sample Bulleted List document we created in this article:

*   [bulleted-list.odt](/assembly/python-net/_sample_files/developer-guide/advanced-usage/working-with-list-reports-bulleted/bulleted-list-in-word-processing-document/bulleted-list.odt)

### Generating The Report

{{< tabs "example1" >}}
{{< tab "Python" >}}
```python
import json

from groupdocs.assembly import DataSourceInfo, DocumentAssembler

with open("products.json", encoding="utf-8") as f:
    products = json.load(f)

assembler = DocumentAssembler()
assembler.assemble_document("bulleted-list.odt", "bulleted-list-report.odt", DataSourceInfo(products, "product"))
```
{{< /tab >}}
{{< tab "bulleted-list.odt" >}}
{{< tab-text >}}
The following sample file is used in this example: [bulleted-list.odt](/assembly/python-net/_sample_files/developer-guide/advanced-usage/working-with-list-reports-bulleted/bulleted-list-in-word-processing-document/bulleted-list.odt)
{{< /tab-text >}}
{{< /tab >}}
{{< tab "products.json" >}}
{{< tab-text >}}
The following sample file is used in this example: [products.json](/assembly/python-net/_sample_files/developer-guide/advanced-usage/working-with-list-reports-bulleted/bulleted-list-in-word-processing-document/products.json)
{{< /tab-text >}}
{{< /tab >}}
{{< tab "bulleted-list-report.odt" >}}  
```text
Binary file (ODT, 5 KB)
```
[Download full output](/assembly/python-net/_output_files/developer-guide/advanced-usage/working-with-list-reports-bulleted/bulleted-list-in-word-processing-document/generating_the_report/bulleted-list-report.odt)
{{< /tab >}}
{{< /tabs >}}

## Bulleted List in OpenOffice Document

### Creating the Template

OpenDocument Text (ODT) is a word processing document format which can be used as an alternative to Microsoft Word Document (DOC/DOCX) formats. Since ODT is not a Microsoft Proprietary format, there are multiple software (including Microsoft Office and Apache OpenOffice) available to create, open, edit and save this format. For more information on the available software to work with ODT, please visit [wikipedia article](https://en.wikipedia.org/wiki/OpenDocument#Software).

In this topic, we'll not reinvent the wheel to recreate a template for generating an 'Bulleted List' report in ODT format. Instead, we'll save the existing template to ODT format using Microsoft Office. In order to achieve this; assuming you are using Microsoft Office 2010, please follow below steps:

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
