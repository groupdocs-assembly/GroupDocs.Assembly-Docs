---
id: multicolored-numbered-list-in-presentation-document
url: assembly/python-net/multicolored-numbered-list-in-presentation-document
title: Multicolored Numbered List in Presentation Document
weight: 3
description: "Multicolored Numbered List in Presentation Document with GroupDocs.Assembly for Python via .NET: the template, the Python data and the code."
keywords: multicolored numbered list in presentation document, GroupDocs.Assembly, Python, report generation
productName: GroupDocs.Assembly for Python via .NET
hideChildren: False
---
{{< alert style="info" >}}In this article, we will use GroupDocs.Assembly to generate a Multicolored Numbered List report in Presentation Document format based on the use case: [Working with a Business Case]({{< ref "assembly/python-net/developer-guide/basic-usage/working-with-a-business-case/_index.md" >}}).{{< /alert >}}{{< alert style="info" >}}The example reads the shop data described in [The Business Layer]({{< ref "assembly/python-net/developer-guide/basic-usage/working-with-a-business-case/the-business-layer.md" >}}).{{< /alert >}}

## Multicolored Numbered List in Microsoft PowerPoint Document

### Creating a Multicolored Numbered List

Practising the following steps you can create Multicolored Numbered List Template in MS PowerPoint 2013.

1.  In your document, write a sentence like "We provide support for the following products:".
2.  Start numbered list.
3.  Go to the "Design" tab and select color to make it colored list.
4.  Save the template.

### Reporting Requirement

As a report developer, you are required to describe the services you are providing with the following key requirements:

*   The report must show the products in numbered list.
*   It must highlight the products.
*   The report must be generated in the Presentation Document.

### Adding Syntax to be evaluated by GroupDocs.Assembly Engine

<table cellspacing="0" cellpadding="0" style="border-collapse: collapse; margin-left: 0pt; width: 457pt;"><tbody><tr><td style="background-color: rgb(91, 155, 213); border-bottom-color: rgb(255, 255, 255); border-bottom-style: solid; border-bottom-width: 3pt; border-left-color: rgb(255, 255, 255); border-left-style: solid; border-left-width: 1pt; border-right-color: rgb(255, 255, 255); border-right-style: solid; border-right-width: 1pt; border-top-color: rgb(255, 255, 255); border-top-style: solid; border-top-width: 1pt; padding-left: 4.9pt; padding-right: 4.9pt; padding-top: 0.25pt; vertical-align: top; width: 267.2pt;"><p style="font-size: 11pt; line-height: 108%; margin-top: 0pt; margin-right: 0pt; margin-bottom: 8pt; margin-left: 0pt;"><span style="font-family: Calibri; font-size: 11pt; font-weight: bold;">Customer</span></p></td><td style="background-color: rgb(91, 155, 213); border-bottom-color: rgb(255, 255, 255); border-bottom-style: solid; border-bottom-width: 3pt; border-left-color: rgb(255, 255, 255); border-left-style: solid; border-left-width: 1pt; border-right-color: rgb(255, 255, 255); border-right-style: solid; border-right-width: 1pt; border-top-color: rgb(255, 255, 255); border-top-style: solid; border-top-width: 1pt; padding-left: 4.9pt; padding-right: 4.9pt; padding-top: 0.25pt; vertical-align: top; width: 167.2pt;"><p style="font-size: 11pt; line-height: 108%; margin-top: 0pt; margin-right: 0pt; margin-bottom: 8pt; margin-left: 0pt;"><span style="font-family: Calibri; font-size: 11pt; font-weight: bold;">Order Price</span></p></td></tr><tr><td style="background-color: rgb(244, 177, 131); border-bottom-color: rgb(255, 255, 255); border-bottom-style: solid; border-bottom-width: 1pt; border-left-color: rgb(255, 255, 255); border-left-style: solid; border-left-width: 1pt; border-right-color: rgb(255, 255, 255); border-right-style: solid; border-right-width: 1pt; border-top-color: rgb(255, 255, 255); border-top-style: solid; border-top-width: 3pt; padding-left: 4.9pt; padding-right: 4.9pt; vertical-align: top; width: 267.2pt;"><p style="font-size: 11pt; line-height: 108%; margin-top: 0pt; margin-right: 0pt; margin-bottom: 8pt; margin-left: 0pt;"><span style="font-family: Calibri; font-size: 11pt; font-weight: bold;">&lt;&lt;foreach [in orders]&gt;&gt;&lt;&lt;if [Price &gt;= 400]&gt;&gt;&lt;&lt;[Customer.CustomerName]&gt;&gt;</span></p></td><td style="background-color: rgb(244, 177, 131); border-bottom-color: rgb(255, 255, 255); border-bottom-style: solid; border-bottom-width: 1pt; border-left-color: rgb(255, 255, 255); border-left-style: solid; border-left-width: 1pt; border-right-color: rgb(255, 255, 255); border-right-style: solid; border-right-width: 1pt; border-top-color: rgb(255, 255, 255); border-top-style: solid; border-top-width: 3pt; padding-left: 4.9pt; padding-right: 4.9pt; vertical-align: top; width: 167.2pt;"><p style="font-size: 11pt; line-height: 108%; margin-top: 0pt; margin-right: 0pt; margin-bottom: 8pt; margin-left: 0pt;"><span style="font-family: Calibri; font-size: 11pt;">&lt;&lt;[Price]&gt;&gt;</span></p></td></tr><tr><td style="background-color: rgb(91, 155, 213); border-bottom-color: rgb(255, 255, 255); border-bottom-style: solid; border-bottom-width: 1pt; border-left-color: rgb(255, 255, 255); border-left-style: solid; border-left-width: 1pt; border-right-color: rgb(255, 255, 255); border-right-style: solid; border-right-width: 1pt; border-top-color: rgb(255, 255, 255); border-top-style: solid; border-top-width: 1pt; padding-left: 4.9pt; padding-right: 4.9pt; padding-top: 0.25pt; vertical-align: top; width: 267.2pt;"><p style="font-size: 11pt; line-height: 108%; margin-top: 0pt; margin-right: 0pt; margin-bottom: 8pt; margin-left: 0pt;"><span style="font-family: Calibri; font-size: 11pt; font-weight: bold;">&lt;&lt;else&gt;&gt;&lt;&lt;[Customer.CustomerName]&gt;&gt;</span></p></td><td style="background-color: rgb(234, 239, 247); border-bottom-color: rgb(255, 255, 255); border-bottom-style: solid; border-bottom-width: 1pt; border-left-color: rgb(255, 255, 255); border-left-style: solid; border-left-width: 1pt; border-right-color: rgb(255, 255, 255); border-right-style: solid; border-right-width: 1pt; border-top-color: rgb(255, 255, 255); border-top-style: solid; border-top-width: 1pt; padding-left: 4.9pt; padding-right: 4.9pt; padding-top: 0.25pt; vertical-align: top; width: 167.2pt;"><p style="font-size: 11pt; line-height: 108%; margin-top: 0pt; margin-right: 0pt; margin-bottom: 8pt; margin-left: 0pt;"><span style="font-family: Calibri; font-size: 11pt;">&lt;&lt;[Price]&gt;&gt;&lt;&lt;/if&gt;&gt;&lt;&lt;/foreach&gt;&gt;</span></p></td></tr><tr><td style="background-color: rgb(91, 155, 213); border-bottom-color: rgb(255, 255, 255); border-bottom-style: solid; border-bottom-width: 1pt; border-left-color: rgb(255, 255, 255); border-left-style: solid; border-left-width: 1pt; border-right-color: rgb(255, 255, 255); border-right-style: solid; border-right-width: 1pt; border-top-color: rgb(255, 255, 255); border-top-style: solid; border-top-width: 1pt; padding-left: 4.9pt; padding-right: 4.9pt; padding-top: 0.25pt; vertical-align: top; width: 267.2pt;"><p style="font-size: 11pt; line-height: 108%; margin-top: 0pt; margin-right: 0pt; margin-bottom: 8pt; margin-left: 0pt;"><span style="font-family: Calibri; font-size: 11pt; font-weight: bold;">Total:</span></p></td><td style="background-color: rgb(210, 222, 239); border-bottom-color: rgb(255, 255, 255); border-bottom-style: solid; border-bottom-width: 1pt; border-left-color: rgb(255, 255, 255); border-left-style: solid; border-left-width: 1pt; border-right-color: rgb(255, 255, 255); border-right-style: solid; border-right-width: 1pt; border-top-color: rgb(255, 255, 255); border-top-style: solid; border-top-width: 1pt; padding-left: 4.9pt; padding-right: 4.9pt; padding-top: 0.25pt; vertical-align: top; width: 167.2pt;"><p style="font-size: 11pt; line-height: 108%; margin-top: 0pt; margin-right: 0pt; margin-bottom: 8pt; margin-left: 0pt;"><span style="font-family: Calibri; font-size: 11pt;">&lt;&lt;[Sum(c =&gt; c.Price)]&gt;&gt;</span></p></td></tr></tbody></table>
{{< alert style="success" >}}For detailed technical information about syntax, expressions and report generation by the engine, please visit: [Working with GroupDocs.Assembly Engine]({{< ref "assembly/python-net/developer-guide/basic-usage/working-with-groupdocs.assembly-engine/_index.md" >}}).{{< /alert >}}

Download Multicolored Numbered List Template

Please download the sample Multicolored Numbered List document we created in this article:

*   [multicolored-numbered-list.pptx](/assembly/python-net/_sample_files/developer-guide/advanced-usage/working-with-list-reports-multicolored-numbered/multicolored-numbered-list-in-presentation-document/multicolored-numbered-list.pptx)

### Generating The Report

{{< tabs "example1" >}}
{{< tab "Python" >}}
```python
import json

from groupdocs.assembly import DataSourceInfo, DocumentAssembler

with open("products.json", encoding="utf-8") as f:
    products = json.load(f)

assembler = DocumentAssembler()
assembler.assemble_document("multicolored-numbered-list.pptx", "multicolored-numbered-list-report.pptx", DataSourceInfo(products, "products"))
```
{{< /tab >}}
{{< tab "multicolored-numbered-list.pptx" >}}
{{< tab-text >}}
The following sample file is used in this example: [multicolored-numbered-list.pptx](/assembly/python-net/_sample_files/developer-guide/advanced-usage/working-with-list-reports-multicolored-numbered/multicolored-numbered-list-in-presentation-document/multicolored-numbered-list.pptx)
{{< /tab-text >}}
{{< /tab >}}
{{< tab "products.json" >}}
{{< tab-text >}}
The following sample file is used in this example: [products.json](/assembly/python-net/_sample_files/developer-guide/advanced-usage/working-with-list-reports-multicolored-numbered/multicolored-numbered-list-in-presentation-document/products.json)
{{< /tab-text >}}
{{< /tab >}}
{{< tab "multicolored-numbered-list-report.pptx" >}}  
```text
Binary file (PPTX, 38 KB)
```
[Download full output](/assembly/python-net/_output_files/developer-guide/advanced-usage/working-with-list-reports-multicolored-numbered/multicolored-numbered-list-in-presentation-document/generating_the_report/multicolored-numbered-list-report.pptx)
{{< /tab >}}
{{< /tabs >}}

## Multicolored Numbered List in OpenOffice Presentation Document

### Creating the Template

OpenDocument Presentation (ODP) is a presentation document format which can be used as an alternative to Microsoft PowerPoint Document (PPT/PPTX) formats. Since ODP is not a Microsoft Proprietary format, there are multiple software (including Microsoft Office and Apache OpenOffice) available to create, open, edit and save this format. For more information on the available software to work with ODP, please visit [wikipedia article](https://en.wikipedia.org/wiki/OpenDocument#Software).

In this topic, we'll not reinvent the wheel to recreate a template for generating an 'Multicolored Numbered List' report in ODP format. Instead, we'll save the existing template to ODP format using Microsoft Office. In order to achieve this; assuming you are using Microsoft Office 2010, please follow below steps:

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
