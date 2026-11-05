---
id: in-table-list-in-presentation-document
url: assembly/python-net/in-table-list-in-presentation-document
title: In-Table List in Presentation Document
weight: 3
description: "In-Table List in Presentation Document with GroupDocs.Assembly for Python via .NET: the template, the Python data and the code."
keywords: in-table list in presentation document, GroupDocs.Assembly, Python, report generation
productName: GroupDocs.Assembly for Python via .NET
hideChildren: False
---
{{< alert style="info" >}}In this article, we will use GroupDocs.Assembly to generate a In-TableList report in Presentationformat based on the use case: [Working with a Business Case]({{< ref "assembly/python-net/developer-guide/basic-usage/working-with-a-business-case/_index.md" >}}).{{< /alert >}}{{< alert style="info" >}}The example reads the shop data described in [The Business Layer]({{< ref "assembly/python-net/developer-guide/basic-usage/working-with-a-business-case/the-business-layer.md" >}}).{{< /alert >}}

## In-Table List in Microsoft PowerPoint Document

### Creating a In-Table List

Practicing the following steps you can create In-Table List Template in MS PowerPoint 2013.

1.  Add a new presentation slide.
2.  Press "Insert" tab.
3.  Add a 2x3 table.
4.  Save your Document.

### Reporting Requirement

As a report developer, you are required to represent the information of the customers and the total order prices with the following key requirements:

*   Report must show customers' name.
*   It must show the sum of orders prices against each customer.
*   It must sum up all the order prices for all the customers.
*   All the representation must be in tabular form.
*   Report must be generated in the PowerPoint Document.

### Adding Syntax to be evaluated by GroupDocs.Assembly Engine

<table cellspacing="0" cellpadding="0" style="border-collapse: collapse; margin-left: 0pt; width: 457pt;"><tbody><tr><td style="background-color: rgb(91, 155, 213); border-bottom-color: rgb(255, 255, 255); border-bottom-style: solid; border-bottom-width: 3pt; border-left-color: rgb(255, 255, 255); border-left-style: solid; border-left-width: 1pt; border-right-color: rgb(255, 255, 255); border-right-style: solid; border-right-width: 1pt; border-top-color: rgb(255, 255, 255); border-top-style: solid; border-top-width: 1pt; padding-left: 4.9pt; padding-right: 4.9pt; padding-top: 0.25pt; vertical-align: top; width: 267.2pt;"><p style="font-size: 11pt; line-height: 107%; margin-top: 0pt; margin-right: 0pt; margin-bottom: 0pt; margin-left: 0pt;"><span style="color: rgb(255, 255, 255); font-family: Calibri; font-size: 11pt; font-weight: bold;">Customer</span></p></td><td style="background-color: rgb(91, 155, 213); border-bottom-color: rgb(255, 255, 255); border-bottom-style: solid; border-bottom-width: 3pt; border-left-color: rgb(255, 255, 255); border-left-style: solid; border-left-width: 1pt; border-right-color: rgb(255, 255, 255); border-right-style: solid; border-right-width: 1pt; border-top-color: rgb(255, 255, 255); border-top-style: solid; border-top-width: 1pt; padding-left: 4.9pt; padding-right: 4.9pt; padding-top: 0.25pt; vertical-align: top; width: 167.2pt;"><p style="font-size: 11pt; line-height: 107%; margin-top: 0pt; margin-right: 0pt; margin-bottom: 0pt; margin-left: 0pt;"><span style="color: rgb(255, 255, 255); font-family: Calibri; font-size: 11pt; font-weight: bold;">Order Price</span></p></td></tr><tr><td style="background-color: rgb(91, 155, 213); border-bottom-color: rgb(255, 255, 255); border-bottom-style: solid; border-bottom-width: 1pt; border-left-color: rgb(255, 255, 255); border-left-style: solid; border-left-width: 1pt; border-right-color: rgb(255, 255, 255); border-right-style: solid; border-right-width: 1pt; border-top-color: rgb(255, 255, 255); border-top-style: solid; border-top-width: 3pt; padding-left: 4.9pt; padding-right: 4.9pt; vertical-align: top; width: 267.2pt;"><p style="font-size: 11pt; line-height: 107%; margin-top: 0pt; margin-right: 0pt; margin-bottom: 0pt; margin-left: 0pt;"><span style="color: rgb(255, 255, 255); font-family: Calibri; font-size: 11pt; font-weight: bold;">&lt;&lt;</span><span style="color: rgb(255, 255, 255); font-family: Calibri; font-size: 11pt; font-weight: bold;">foreach</span><span style="color: rgb(255, 255, 255); font-family: Calibri; font-size: 11pt; font-weight: bold;"> [in customers]&gt;&gt;&lt;&lt;[</span><span style="color: rgb(255, 255, 255); font-family: Calibri; font-size: 11pt; font-weight: bold;">CustomerName</span><span style="color: rgb(255, 255, 255); font-family: Calibri; font-size: 11pt; font-weight: bold;">]&gt;&gt;</span></p></td><td style="background-color: rgb(210, 222, 239); border-bottom-color: rgb(255, 255, 255); border-bottom-style: solid; border-bottom-width: 1pt; border-left-color: rgb(255, 255, 255); border-left-style: solid; border-left-width: 1pt; border-right-color: rgb(255, 255, 255); border-right-style: solid; border-right-width: 1pt; border-top-color: rgb(255, 255, 255); border-top-style: solid; border-top-width: 3pt; padding-left: 4.9pt; padding-right: 4.9pt; vertical-align: top; width: 167.2pt;"><p style="font-size: 11pt; line-height: 107%; margin-top: 0pt; margin-right: 0pt; margin-bottom: 0pt; margin-left: 0pt;"><span style="font-family: Calibri; font-size: 11pt;">&lt;&lt;[</span><span style="font-family: Calibri; font-size: 11pt;">Order.Sum</span><span style="font-family: Calibri; font-size: 11pt;">(</span></p><p style="font-size: 11pt; line-height: 107%; margin-top: 0pt; margin-right: 0pt; margin-bottom: 0pt; margin-left: 0pt;"><span style="font-family: Calibri; font-size: 11pt;">c =&gt; </span><span style="font-family: Calibri; font-size: 11pt;">c.Price</span><span style="font-family: Calibri; font-size: 11pt;">)]&gt;&gt;&lt;&lt;/</span><span style="font-family: Calibri; font-size: 11pt;">foreach</span><span style="font-family: Calibri; font-size: 11pt;">&gt;&gt;</span></p></td></tr><tr><td style="background-color: rgb(91, 155, 213); border-bottom-color: rgb(255, 255, 255); border-bottom-style: solid; border-bottom-width: 1pt; border-left-color: rgb(255, 255, 255); border-left-style: solid; border-left-width: 1pt; border-right-color: rgb(255, 255, 255); border-right-style: solid; border-right-width: 1pt; border-top-color: rgb(255, 255, 255); border-top-style: solid; border-top-width: 1pt; padding-left: 4.9pt; padding-right: 4.9pt; padding-top: 0.25pt; vertical-align: top; width: 267.2pt;"><p style="font-size: 11pt; line-height: 107%; margin-top: 0pt; margin-right: 0pt; margin-bottom: 0pt; margin-left: 0pt;"><span style="color: rgb(255, 255, 255); font-family: Calibri; font-size: 11pt; font-weight: bold;">Total:</span></p></td><td style="background-color: rgb(234, 239, 247); border-bottom-color: rgb(255, 255, 255); border-bottom-style: solid; border-bottom-width: 1pt; border-left-color: rgb(255, 255, 255); border-left-style: solid; border-left-width: 1pt; border-right-color: rgb(255, 255, 255); border-right-style: solid; border-right-width: 1pt; border-top-color: rgb(255, 255, 255); border-top-style: solid; border-top-width: 1pt; padding-left: 4.9pt; padding-right: 4.9pt; padding-top: 0.25pt; vertical-align: top; width: 167.2pt;"><p style="font-size: 11pt; line-height: 107%; margin-top: 0pt; margin-right: 0pt; margin-bottom: 0pt; margin-left: 0pt;"><span style="font-family: Calibri; font-size: 11pt;">&lt;&lt;[Sum(</span></p><p style="font-size: 11pt; line-height: 107%; margin-top: 0pt; margin-right: 0pt; margin-bottom: 0pt; margin-left: 0pt;"><span style="font-family: Calibri; font-size: 11pt;">m =&gt; </span><span style="font-family: Calibri; font-size: 11pt;">m.Order.Sum</span><span style="font-family: Calibri; font-size: 11pt;">(</span></p><p style="font-size: 11pt; line-height: 107%; margin-top: 0pt; margin-right: 0pt; margin-bottom: 0pt; margin-left: 0pt;"><span style="font-family: Calibri; font-size: 11pt;">c =&gt; </span><span style="font-family: Calibri; font-size: 11pt;">c.Price</span><span style="font-family: Calibri; font-size: 11pt;">))]&gt;&gt;</span></p></td></tr></tbody></table>
{{< alert style="success" >}}For detailed technical information about syntax,expressions and report generation by the engine, please visit: [Working with GroupDocs.Assembly Engine]({{< ref "assembly/python-net/developer-guide/basic-usage/working-with-groupdocs.assembly-engine/_index.md" >}}).{{< /alert >}}

### Download In-Table List Template

Please download the sample In-Table List document we created in this article:

*   [in-table-list.pptx](/assembly/python-net/_sample_files/developer-guide/advanced-usage/working-with-table-reports/in-table-list-in-presentation-document/in-table-list.pptx)

### Generating The Report

{{< tabs "example1" >}}
{{< tab "Python" >}}
```python
import json

from groupdocs.assembly import DataSourceInfo, DocumentAssembler

with open("customers.json", encoding="utf-8") as f:
    customers = json.load(f)

assembler = DocumentAssembler()
assembler.assemble_document("in-table-list.pptx", "in-table-list-report.pptx", DataSourceInfo(customers, "customers"))
```
{{< /tab >}}
{{< tab "in-table-list.pptx" >}}
{{< tab-text >}}
The following sample file is used in this example: [in-table-list.pptx](/assembly/python-net/_sample_files/developer-guide/advanced-usage/working-with-table-reports/in-table-list-in-presentation-document/in-table-list.pptx)
{{< /tab-text >}}
{{< /tab >}}
{{< tab "customers.json" >}}
{{< tab-text >}}
The following sample file is used in this example: [customers.json](/assembly/python-net/_sample_files/developer-guide/advanced-usage/working-with-table-reports/in-table-list-in-presentation-document/customers.json)
{{< /tab-text >}}
{{< /tab >}}
{{< tab "in-table-list-report.pptx" >}}  
```text
Binary file (PPTX, 33 KB)
```
[Download full output](/assembly/python-net/_output_files/developer-guide/advanced-usage/working-with-table-reports/in-table-list-in-presentation-document/generating_the_report/in-table-list-report.pptx)
{{< /tab >}}
{{< /tabs >}}

## In-Table List in OpenOffice Presentation Document

### Creating the Template

OpenDocument Presentation (ODP) is a presentation document format which can be used as an alternative to Microsoft PowerPoint Document (PPT/PPTX) formats. Since ODP is not a Microsoft Proprietary format, there are multiple software (including Microsoft Office and Apache OpenOffice) available to create, open, edit and save this format. For more information on the available software to work with ODP, please visit [wikipedia article](https://en.wikipedia.org/wiki/OpenDocument#Software).

In this topic, we 'll not reinvent the wheel to recreate a template for generating an 'In-Table List' report in ODP format. Instead, we'll save the existing template to ODP format using Microsoft Office. In order to achieve this; assuming you are using Microsoft Office 2010, please follow below steps:

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
