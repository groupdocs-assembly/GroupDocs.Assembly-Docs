---
id: single-row-image-in-word-processing-document
url: assembly/python-net/single-row-image-in-word-processing-document
title: Single Row Image in Word Processing Document
weight: 1
description: "Single Row Image in Word Processing Document with GroupDocs.Assembly for Python via .NET: the template, the Python data and the code."
keywords: single row image in word processing document, GroupDocs.Assembly, Python, report generation
productName: GroupDocs.Assembly for Python via .NET
hideChildren: False
---
{{< alert style="info" >}}In this article, we will use GroupDocs.Assembly to generate a Single Row Image report in Word Processing Document format based on the use case: [Working with a Business Case]({{< ref "assembly/python-net/developer-guide/basic-usage/working-with-a-business-case/_index.md" >}}).{{< /alert >}}{{< alert style="info" >}}The example reads the shop data described in [The Business Layer]({{< ref "assembly/python-net/developer-guide/basic-usage/working-with-a-business-case/the-business-layer.md" >}}).{{< /alert >}}

## Single Row Image in Microsoft Word Document

### Creating a Single Row Image

Please follow below steps to create a Single Row Image in MS Word 2013:

1.  Insert the desired shape to display image in it.
2.  Go to Insert Tab and select shape by clicking on Shape Icon.
3.  Write "Name" and "Contact Number" to show name and contact info of the customer.
4.  Save the template.

### Reporting Requirement

As a report developer, you are required to represent information of first single customer with the following key requirements:

*   The report must show image of the customer
*   It must show Name and Contact Number of the customer
*   The report must be generated in the Word Processing Document.

{{< alert style="info" >}}See how to use images in MS Word [here](https://www.youtube.com/watch?v=vTef7N7NAvg&index=3&list=PLoVseBOSg-uQ2pLcb_hyZO2KRl0fKBQlE).{{< /alert >}}

### Adding Syntax to be evaluated by GroupDocs.Assembly Engine

<table cellspacing="0" cellpadding="0" style="border-collapse: collapse; margin-left: 0pt;"><tbody><tr><td style="padding-left: 5.4pt; padding-right: 5.4pt; vertical-align: top; width: 118.25pt;"><table cellspacing="0" cellpadding="0" style="border-collapse: collapse; float: left; margin-top: 0pt; margin-right: 9pt; margin-bottom: 0pt; margin-left: 9pt; width: 122pt;"><tbody><tr style="height: 112pt;"><td style="border-bottom-color: rgb(0, 0, 0); border-bottom-style: solid; border-bottom-width: 0.75pt; border-left-color: rgb(0, 0, 0); border-left-style: solid; border-left-width: 0.75pt; border-right-color: rgb(0, 0, 0); border-right-style: solid; border-right-width: 0.75pt; border-top-color: rgb(0, 0, 0); border-top-style: solid; border-top-width: 0.75pt; padding-left: 5.03pt; padding-right: 5.03pt; vertical-align: top; width: 110.45pt;"><p style="font-size: 11pt; line-height: 108%; margin-top: 0pt; margin-right: 0pt; margin-bottom: 8pt; margin-left: 0pt;"><span style="font-family: Calibri; font-size: 11pt;">&lt;&lt;image [</span><span style="font-family: Calibri; font-size: 11pt;">customer.</span><span style="font-family: Calibri; font-size: 11pt;">Photo</span><span style="font-family: Calibri; font-size: 11pt;">]&gt;&gt;</span></p></td></tr></tbody></table><p style="margin-top: 0pt; margin-right: 0pt; margin-bottom: 0pt; margin-left: 0pt;"></p></td><td style="padding-left: 5.4pt; padding-right: 5.4pt; vertical-align: top; width: 316.1pt;"><p style="margin-top: 0pt; margin-right: 0pt; margin-bottom: 0pt; margin-left: 0pt;"><span style="font-family: Calibri; font-size: 11pt;">&nbsp;</span></p><table cellspacing="0" cellpadding="0" style="border-collapse: collapse; margin-left: 0pt;"><tbody><tr><td style="padding-left: 5.4pt; padding-right: 5.4pt; vertical-align: top; width: 43.95pt;"><p style="margin-top: 0pt; margin-right: 0pt; margin-bottom: 0pt; margin-left: 0pt;"><span style="font-family: Calibri; font-size: 14pt; font-weight: bold;">Name:</span></p></td><td style="padding-left: 5.4pt; padding-right: 5.4pt; vertical-align: top; width: 274.6pt;"><p style="margin-top: 0pt; margin-right: 0pt; margin-bottom: 0pt; margin-left: 0pt;"><span style="font-family: Calibri; font-size: 16pt; font-weight: bold;">&lt;&lt;[</span><span style="font-family: Calibri; font-size: 16pt; font-weight: bold;">customer</span><span style="font-family: Calibri; font-size: 16pt; font-weight: bold;">.</span><span style="font-family: Calibri; font-size: 16pt; font-weight: bold;">Customer</span><span style="font-family: Calibri; font-size: 16pt; font-weight: bold;">Name</span><span style="font-family: Calibri; font-size: 16pt; font-weight: bold;">]&gt;&gt;</span></p></td></tr><tr><td style="padding-left: 5.4pt; padding-right: 5.4pt; vertical-align: top; width: 75.9pt;"><p style="margin-top: 0pt; margin-right: 0pt; margin-bottom: 0pt; margin-left: 0pt;"><span style="font-family: Calibri; font-size: 16pt; font-weight: bold;">Contact Number</span><span style="font-family: Calibri; font-size: 16pt; font-weight: bold;">:</span></p></td><td style="padding-left: 5.4pt; padding-right: 5.4pt; vertical-align: top; width: 218.1pt;"><p style="margin-top: 0pt; margin-right: 0pt; margin-bottom: 0pt; margin-left: 0pt;"><span style="font-family: Calibri; font-size: 16pt;">&lt;&lt;[</span><span style="font-family: Calibri; font-size: 16pt;">customer</span><span style="font-family: Calibri; font-size: 16pt;">.</span><span style="font-family: Calibri; font-size: 16pt;">CustomerContactNumber</span><span style="font-family: Calibri; font-size: 16pt;">]&gt;&gt;</span></p></td></tr></tbody></table><p style="margin-top: 0pt; margin-right: 0pt; margin-bottom: 0pt; margin-left: 0pt;"></p></td></tr></tbody></table>
{{< alert style="success" >}}For detailed technical information about syntax, expressions and report generation by the engine, please visit: [Working with GroupDocs.Assembly Engine]({{< ref "assembly/python-net/developer-guide/basic-usage/working-with-groupdocs.assembly-engine/_index.md" >}}).{{< /alert >}}

### Download Single Row Template

Please download the sample Single Row document we created in this article:

*   [single-row.docx](/assembly/python-net/_sample_files/developer-guide/advanced-usage/working-with-image-reports-single-row/single-row-image-in-word-processing-document/single-row.docx)

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
assembler.assemble_document("single-row.docx", "single-row-report.docx", DataSourceInfo(customer, "customer"))
```
{{< /tab >}}
{{< tab "single-row.docx" >}}
{{< tab-text >}}
The following sample file is used in this example: [single-row.docx](/assembly/python-net/_sample_files/developer-guide/advanced-usage/working-with-image-reports-single-row/single-row-image-in-word-processing-document/single-row.docx)
{{< /tab-text >}}
{{< /tab >}}
{{< tab "customer.json" >}}
{{< tab-text >}}
The following sample file is used in this example: [customer.json](/assembly/python-net/_sample_files/developer-guide/advanced-usage/working-with-image-reports-single-row/single-row-image-in-word-processing-document/customer.json)
{{< /tab-text >}}
{{< /tab >}}
{{< tab "pictures" >}}
{{< tab-text >}}
The following sample files are used in this example: [quayside-bistro.png](/assembly/python-net/_sample_files/developer-guide/advanced-usage/working-with-image-reports-single-row/single-row-image-in-word-processing-document/quayside-bistro.png), [lantern-street-cafe.png](/assembly/python-net/_sample_files/developer-guide/advanced-usage/working-with-image-reports-single-row/single-row-image-in-word-processing-document/lantern-street-cafe.png), [saltmarsh-deli.png](/assembly/python-net/_sample_files/developer-guide/advanced-usage/working-with-image-reports-single-row/single-row-image-in-word-processing-document/saltmarsh-deli.png), [pier-nine-kitchen.png](/assembly/python-net/_sample_files/developer-guide/advanced-usage/working-with-image-reports-single-row/single-row-image-in-word-processing-document/pier-nine-kitchen.png)
{{< /tab-text >}}
{{< /tab >}}
{{< tab "single-row-report.docx" >}}  
```text
Binary file (DOCX, 16 KB)
```
[Download full output](/assembly/python-net/_output_files/developer-guide/advanced-usage/working-with-image-reports-single-row/single-row-image-in-word-processing-document/generating_the_report/single-row-report.docx)
{{< /tab >}}
{{< /tabs >}}

## Single Row in OpenOffice Document

### Creating the Template

OpenDocument Text (ODT) is a word processing document format which can be used as an alternative to Microsoft Word Document (DOC/DOCX) formats. Since ODT is not a Microsoft Proprietary format, there are multiple software (including Microsoft Office and Apache OpenOffice) available to create, open, edit and save this format. For more information on the available software to work with ODT, please visit [wikipedia article](https://en.wikipedia.org/wiki/OpenDocument#Software).

In this topic, we'll not reinvent the wheel to recreate a template for generating an 'Single Row' report in ODT format. Instead, we'll save the existing template to ODT format using Microsoft Office. In order to achieve this; assuming you are using Microsoft Office 2010, please follow below steps:

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
