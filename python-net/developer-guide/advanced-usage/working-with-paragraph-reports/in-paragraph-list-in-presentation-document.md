---
id: in-paragraph-list-in-presentation-document
url: assembly/python-net/in-paragraph-list-in-presentation-document
title: In-Paragraph List in Presentation Document
weight: 3
description: "In-Paragraph List in Presentation Document with GroupDocs.Assembly for Python via .NET: the template, the Python data and the code."
keywords: in-paragraph list in presentation document, GroupDocs.Assembly, Python, report generation
productName: GroupDocs.Assembly for Python via .NET
hideChildren: False
---
{{< alert style="info" >}}In this article, we will use GroupDocs.Assembly to generate a In-Paragraph List report in Presentation Document format based on the use case: [Working with a Business Case]({{< ref "assembly/python-net/developer-guide/basic-usage/working-with-a-business-case/_index.md" >}}).{{< /alert >}}

## In-Paragraph List in Microsoft PowerPoint Document

### Creating a In-Paragraph List

Practicing the following steps you can create In-Paragraph List Template in MS PowerPoint 2013.

1.  Add a new presentation slide.
2.  Write a sentence, for example "We provide support for the following products:".
3.  Save the template.

### Reporting Requirement

As a report developer, you are required to describe the services you are providing with the following key requirements:

*   A descriptive or informative line like "We provide support for the following products:".
*   Show all the products along with the above sentence.
*   Report must be generated in the Presentation Document.

### Adding Syntax to be evaluated by GroupDocs.Assembly Engine

```text
We provide support for the following products:
<<foreach [in products]>><<[IndexOf() != 0 ? ", " : ""]>>
<<[ProductName]>>
<</foreach>>
```

{{< alert style="success" >}}For detailed technical information about syntax, expressions and report generation by the engine, please visit: [Working with GroupDocs.Assembly Engine]({{< ref "assembly/python-net/developer-guide/basic-usage/working-with-groupdocs.assembly-engine/_index.md" >}}).{{< /alert >}}

### Download In-Paragraph List Template

Please download the sample In-Paragraph List document we created in this article:

*   [in-paragraph-list.odp](/assembly/python-net/_sample_files/developer-guide/advanced-usage/working-with-paragraph-reports/in-paragraph-list-in-presentation-document/in-paragraph-list.odp)

### Generating The Report

{{< alert style="info" >}}The example reads the shop data described in [The Business Layer]({{< ref "assembly/python-net/developer-guide/basic-usage/working-with-a-business-case/the-business-layer.md" >}}).{{< /alert >}}

{{< tabs "example1" >}}
{{< tab "Python" >}}
```python
import json

from groupdocs.assembly import DataSourceInfo, DocumentAssembler

with open("products.json", encoding="utf-8") as f:
    products = json.load(f)

assembler = DocumentAssembler()
assembler.assemble_document("in-paragraph-list.odp", "in-paragraph-list-report.odp", DataSourceInfo(products, "products"))
```
{{< /tab >}}
{{< tab "in-paragraph-list.odp" >}}
{{< tab-text >}}
The following sample file is used in this example: [in-paragraph-list.odp](/assembly/python-net/_sample_files/developer-guide/advanced-usage/working-with-paragraph-reports/in-paragraph-list-in-presentation-document/in-paragraph-list.odp)
{{< /tab-text >}}
{{< /tab >}}
{{< tab "products.json" >}}
{{< tab-text >}}
The following sample file is used in this example: [products.json](/assembly/python-net/_sample_files/developer-guide/advanced-usage/working-with-paragraph-reports/in-paragraph-list-in-presentation-document/products.json)
{{< /tab-text >}}
{{< /tab >}}
{{< tab "in-paragraph-list-report.odp" >}}  
```text
Binary file (ODP, 7 KB)
```
[Download full output](/assembly/python-net/_output_files/developer-guide/advanced-usage/working-with-paragraph-reports/in-paragraph-list-in-presentation-document/generating_the_report/in-paragraph-list-report.odp)
{{< /tab >}}
{{< /tabs >}}

## In-Paragraph List in OpenOffice Presentation Document

### Creating the Template

OpenDocument Presentation (ODP) is a presentation document format which can be used as an alternative to Microsoft PowerPoint Document (PPT/PPTX) formats. Since ODP is not a Microsoft Proprietary format, there are multiple software (including Microsoft Office and Apache OpenOffice) available to create, open, edit and save this format. For more information on the available software to work with ODP, please visit [wikipedia article](https://en.wikipedia.org/wiki/OpenDocument#Software).

In this topic, we'll not reinvent the wheel to recreate a template for generating an 'In-Paragraph List' report in ODP format. Instead, we'll save the existing template to ODP format using Microsoft Office. In order to achieve this; assuming you are using Microsoft Office 2010, please follow below steps:

1.  Open existing template we created in previous topic.
2.  Click "File" and select "Save As".
3.  Select "OpenDocument Presentation" from "Save As Type" drop down.
4.  Click "Save".

### Download Template

### Generating the Report

### ODP Template and Report in Apache OpenOffice

In order to check compatibility of ODP between Microsoft Office 2010 and Apache OpenOffice 4.1.2, we performed below tests:

*   We opened the ODP template created through Microsoft Office 2010 in Apache OpenOffice 4.1.2. The template opened successfully in Apache OpenOffice without any issues or formatting losses.
*   We opened the ODP report generated through GroupDocs.Assembly in Apache OpenOffice 4.1.2. The report opened successfully in Apache OpenOffice without any issues or formatting losses.
