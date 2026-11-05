---
id: in-table-master-detail-in-word-processing-document
url: assembly/python-net/in-table-master-detail-in-word-processing-document
title: In-Table Master-Detail in Word Processing Document
weight: 1
description: "In-Table Master-Detail in Word Processing Document with GroupDocs.Assembly for Python via .NET: the template, the Python data and the code."
keywords: in-table master-detail in word processing document, GroupDocs.Assembly, Python, report generation
productName: GroupDocs.Assembly for Python via .NET
hideChildren: False
---
{{< alert style="info" >}}In this article, we will use GroupDocs.Assembly to generate an In-Table Master-Detail report in Word Processing Document format based on the use case: [Working with a Business Case]({{< ref "assembly/python-net/developer-guide/basic-usage/working-with-a-business-case/_index.md" >}}).{{< /alert >}}{{< alert style="info" >}}The example reads the shop data described in [The Business Layer]({{< ref "assembly/python-net/developer-guide/basic-usage/working-with-a-business-case/the-business-layer.md" >}}).{{< /alert >}}

## In-Table Master-Detail in Microsoft Word Document

### Creating a In-Table Master-Detail

Practising the following steps you can create In-Table Master-Detail Template in MS Word 2013.

1.  Click the document where you want to add the table.
2.  Press "Insert" tab to insert the table.
3.  Insert a 2x4 table.
4.  Save the template.

### Reporting Requirement

As a report developer, you are required to represent customers' total orders prices and price of each product separately with the following key requirements:

*   A report must show each customer along with his total orders prices.
*   It must also show each individual product ordered by the customers.
*   It must show the sum of the order prices.
*   It must represent all the information in tabular form.
*   A report must be generated in the Word Processing Document.

### Adding Syntax to be evaluated by GroupDocs.Assembly Engine

<table cellspacing="0" cellpadding="0" style="border-collapse: collapse; margin-left: 0pt;"><tbody><tr><td style="border-bottom-color: rgb(191, 191, 191); border-bottom-style: solid; border-bottom-width: 0.75pt; border-left-color: rgb(191, 191, 191); border-left-style: solid; border-left-width: 0.75pt; border-right-color: rgb(191, 191, 191); border-right-style: solid; border-right-width: 0.75pt; border-top-color: rgb(191, 191, 191); border-top-style: solid; border-top-width: 0.75pt; padding-left: 5.03pt; padding-right: 5.03pt; vertical-align: top; width: 456.45pt;"><p style="margin-top: 0pt; margin-right: 0pt; margin-bottom: 0pt; margin-left: 0pt;"><span style="font-family: Calibri; font-size: 11pt;">&nbsp;</span></p><table cellspacing="0" cellpadding="0" style="border-collapse: collapse; margin-left: 0pt;"><tbody><tr><td style="border-bottom-color: rgb(102, 102, 102); border-bottom-style: solid; border-bottom-width: 1.5pt; border-left-color: rgb(153, 153, 153); border-left-style: solid; border-left-width: 0.75pt; border-right-color: rgb(153, 153, 153); border-right-style: solid; border-right-width: 0.75pt; border-top-color: rgb(153, 153, 153); border-top-style: solid; border-top-width: 0.75pt; padding-left: 5.03pt; padding-right: 5.03pt; vertical-align: top; width: 266.8pt;"><p style="margin-top: 0pt; margin-right: 0pt; margin-bottom: 0pt; margin-left: 0pt;"><span style="font-family: Calibri; font-size: 11pt; font-weight: bold;">Customer</span></p></td><td style="border-bottom-color: rgb(102, 102, 102); border-bottom-style: solid; border-bottom-width: 1.5pt; border-left-color: rgb(153, 153, 153); border-left-style: solid; border-left-width: 0.75pt; border-right-color: rgb(153, 153, 153); border-right-style: solid; border-right-width: 0.75pt; border-top-color: rgb(153, 153, 153); border-top-style: solid; border-top-width: 0.75pt; padding-left: 5.03pt; padding-right: 5.03pt; vertical-align: top; width: 167.55pt;"><p style="margin-top: 0pt; margin-right: 0pt; margin-bottom: 0pt; margin-left: 0pt;"><span style="font-family: Calibri; font-size: 11pt; font-weight: bold;">Order</span><span style="font-family: Calibri; font-size: 11pt; font-weight: bold;"> Price</span></p></td></tr><tr><td style="border-bottom-color: rgb(153, 153, 153); border-bottom-style: solid; border-bottom-width: 0.75pt; border-left-color: rgb(153, 153, 153); border-left-style: solid; border-left-width: 0.75pt; border-right-color: rgb(153, 153, 153); border-right-style: solid; border-right-width: 0.75pt; border-top-color: rgb(153, 153, 153); border-top-style: solid; border-top-width: 0.75pt; padding-left: 5.03pt; padding-right: 5.03pt; vertical-align: top; width: 266.8pt;"><p style="margin-top: 0pt; margin-right: 0pt; margin-bottom: 0pt; margin-left: 0pt;"><span style="font-family: Calibri; font-size: 11pt; font-weight: bold;">&lt;&lt;foreach [in </span><span style="font-family: Calibri; font-size: 11pt; font-weight: bold;">customers</span><span style="font-family: Calibri; font-size: 11pt; font-weight: bold;">]&gt;&gt;&lt;&lt;[</span><span style="font-family: Calibri; font-size: 11pt; font-weight: bold;">Customer</span><span style="font-family: Calibri; font-size: 11pt; font-weight: bold;">Name</span><span style="font-family: Calibri; font-size: 11pt; font-weight: bold;">]&gt;&gt;</span></p></td><td style="border-bottom-color: rgb(153, 153, 153); border-bottom-style: solid; border-bottom-width: 0.75pt; border-left-color: rgb(153, 153, 153); border-left-style: solid; border-left-width: 0.75pt; border-right-color: rgb(153, 153, 153); border-right-style: solid; border-right-width: 0.75pt; border-top-color: rgb(153, 153, 153); border-top-style: solid; border-top-width: 0.75pt; padding-left: 5.03pt; padding-right: 5.03pt; vertical-align: top; width: 167.55pt;"><p style="margin-top: 0pt; margin-right: 0pt; margin-bottom: 0pt; margin-left: 0pt;"><span style="font-family: Calibri; font-size: 11pt;">&lt;&lt;[</span><span style="font-family: Calibri; font-size: 11pt;">Order</span><span style="font-family: Calibri; font-size: 11pt;">.</span><span style="font-family: Calibri; font-size: 11pt;">Sum</span><span style="font-family: Calibri; font-size: 11pt;">(</span></p><p style="margin-top: 0pt; margin-right: 0pt; margin-bottom: 0pt; margin-left: 0pt;"><span style="font-family: Calibri; font-size: 11pt;">c =&gt; c.</span><span style="font-family: Calibri; font-size: 11pt;">Price</span><span style="font-family: Calibri; font-size: 11pt;">)]&gt;&gt;</span></p></td></tr><tr><td style="border-bottom-color: rgb(153, 153, 153); border-bottom-style: solid; border-bottom-width: 0.75pt; border-left-color: rgb(153, 153, 153); border-left-style: solid; border-left-width: 0.75pt; border-right-color: rgb(153, 153, 153); border-right-style: solid; border-right-width: 0.75pt; border-top-color: rgb(153, 153, 153); border-top-style: solid; border-top-width: 0.75pt; padding-left: 5.03pt; padding-right: 5.03pt; vertical-align: top; width: 266.8pt;"><p style="margin-top: 0pt; margin-right: 0pt; margin-bottom: 0pt; margin-left: 0pt;"><span style="font-family: Calibri; font-size: 11pt; font-style: italic; font-weight: normal;">&lt;&lt;foreach [in </span><span style="font-family: Calibri; font-size: 11pt; font-style: italic; font-weight: normal;">Order</span><span style="font-family: Calibri; font-size: 11pt; font-style: italic; font-weight: normal;">]&gt;&gt; &lt;&lt;[</span><span style="font-family: Calibri; font-size: 11pt; font-style: italic; font-weight: normal;">Product.ProductName</span><span style="font-family: Calibri; font-size: 11pt; font-style: italic; font-weight: normal;">]&gt;&gt;</span></p></td><td style="border-bottom-color: rgb(153, 153, 153); border-bottom-style: solid; border-bottom-width: 0.75pt; border-left-color: rgb(153, 153, 153); border-left-style: solid; border-left-width: 0.75pt; border-right-color: rgb(153, 153, 153); border-right-style: solid; border-right-width: 0.75pt; border-top-color: rgb(153, 153, 153); border-top-style: solid; border-top-width: 0.75pt; padding-left: 5.03pt; padding-right: 5.03pt; vertical-align: top; width: 167.55pt;"><p style="margin-top: 0pt; margin-right: 0pt; margin-bottom: 0pt; margin-left: 0pt;"><span style="font-family: Calibri; font-size: 11pt;">&lt;&lt;[</span><span style="font-family: Calibri; font-size: 11pt;">Price</span><span style="font-family: Calibri; font-size: 11pt;">]&gt;&gt;&lt;&lt;/foreach&gt;&gt;&lt;&lt;</span></p><p style="margin-top: 0pt; margin-right: 0pt; margin-bottom: 0pt; margin-left: 0pt;"><span style="font-family: Calibri; font-size: 11pt;">/foreach&gt;&gt;</span></p></td></tr><tr><td style="border-bottom-color: rgb(153, 153, 153); border-bottom-style: solid; border-bottom-width: 0.75pt; border-left-color: rgb(153, 153, 153); border-left-style: solid; border-left-width: 0.75pt; border-right-color: rgb(153, 153, 153); border-right-style: solid; border-right-width: 0.75pt; border-top-color: rgb(153, 153, 153); border-top-style: solid; border-top-width: 0.75pt; padding-left: 5.03pt; padding-right: 5.03pt; vertical-align: top; width: 266.8pt;"><p style="margin-top: 0pt; margin-right: 0pt; margin-bottom: 0pt; margin-left: 0pt;"><span style="font-family: Calibri; font-size: 11pt; font-weight: bold;">Total:</span></p></td><td style="border-bottom-color: rgb(153, 153, 153); border-bottom-style: solid; border-bottom-width: 0.75pt; border-left-color: rgb(153, 153, 153); border-left-style: solid; border-left-width: 0.75pt; border-right-color: rgb(153, 153, 153); border-right-style: solid; border-right-width: 0.75pt; border-top-color: rgb(153, 153, 153); border-top-style: solid; border-top-width: 0.75pt; padding-left: 5.03pt; padding-right: 5.03pt; vertical-align: top; width: 167.55pt;"><p style="margin-top: 0pt; margin-right: 0pt; margin-bottom: 0pt; margin-left: 0pt;"><span style="font-family: Calibri; font-size: 11pt;">&lt;&lt;[</span><span style="font-family: Calibri; font-size: 11pt;">Sum</span><span style="font-family: Calibri; font-size: 11pt;">(</span></p><p style="margin-top: 0pt; margin-right: 0pt; margin-bottom: 0pt; margin-left: 0pt;"><span style="font-family: Calibri; font-size: 11pt;">m =&gt; m.</span><span style="font-family: Calibri; font-size: 11pt;">Order</span><span style="font-family: Calibri; font-size: 11pt;">.</span><span style="font-family: Calibri; font-size: 11pt;">Sum</span><span style="font-family: Calibri; font-size: 11pt;">(</span></p><p style="margin-top: 0pt; margin-right: 0pt; margin-bottom: 0pt; margin-left: 0pt;"><span style="font-family: Calibri; font-size: 11pt;">c =&gt; c.</span><span style="font-family: Calibri; font-size: 11pt;">Price</span><span style="font-family: Calibri; font-size: 11pt;">))]&gt;&gt;</span></p></td></tr></tbody></table><p style="margin-top: 0pt; margin-right: 0pt; margin-bottom: 0pt; margin-left: 0pt;"><span style="font-family: Calibri; font-size: 11pt;">&nbsp;</span></p><p style="margin-top: 0pt; margin-right: 0pt; margin-bottom: 0pt; margin-left: 0pt;"><span style="font-family: Calibri; font-size: 11pt;">&nbsp;</span></p></td></tr></tbody></table>
{{< alert style="success" >}}For detailed technical information about syntax, expressions and report generation by the engine, please visit: [Working with GroupDocs.Assembly Engine]({{< ref "assembly/python-net/developer-guide/basic-usage/working-with-groupdocs.assembly-engine/_index.md" >}}).{{< /alert >}}

### Download In-Table Master-Detail Template

Please download the sample In-Table Master-Detail document we created in this article:

*   [in-table-master-detail.odt](/assembly/python-net/_sample_files/developer-guide/advanced-usage/working-with-table-reports-master-detail/in-table-master-detail-in-word-processing-document/in-table-master-detail.odt)

### Generating The Report 

{{< tabs "example1" >}}
{{< tab "Python" >}}
```python
import json

from groupdocs.assembly import DataSourceInfo, DocumentAssembler

with open("customers.json", encoding="utf-8") as f:
    customers = json.load(f)

assembler = DocumentAssembler()
assembler.assemble_document("in-table-master-detail.odt", "in-table-master-detail-report.odt", DataSourceInfo(customers, "customers"))
```
{{< /tab >}}
{{< tab "in-table-master-detail.odt" >}}
{{< tab-text >}}
The following sample file is used in this example: [in-table-master-detail.odt](/assembly/python-net/_sample_files/developer-guide/advanced-usage/working-with-table-reports-master-detail/in-table-master-detail-in-word-processing-document/in-table-master-detail.odt)
{{< /tab-text >}}
{{< /tab >}}
{{< tab "customers.json" >}}
{{< tab-text >}}
The following sample file is used in this example: [customers.json](/assembly/python-net/_sample_files/developer-guide/advanced-usage/working-with-table-reports-master-detail/in-table-master-detail-in-word-processing-document/customers.json)
{{< /tab-text >}}
{{< /tab >}}
{{< tab "in-table-master-detail-report.odt" >}}  
```text
Binary file (ODT, 6 KB)
```
[Download full output](/assembly/python-net/_output_files/developer-guide/advanced-usage/working-with-table-reports-master-detail/in-table-master-detail-in-word-processing-document/generating_the_report/in-table-master-detail-report.odt)
{{< /tab >}}
{{< /tabs >}}

## In-Table Master-Detail in OpenOffice Document

### Creating the Template

OpenDocument Text (ODT) is a word processing document format which can be used as an alternative to Microsoft Word Document (DOC/DOCX) formats. Since ODT is not a Microsoft Proprietary format, there are multiple software (including Microsoft Office and Apache OpenOffice) available to create, open, edit and save this format. For more information on the available software to work with ODT, please visit [Wikipedia article](https://en.wikipedia.org/wiki/OpenDocument#Software).

In this topic, we 'll not reinvent the wheel to recreate a template for generating an 'In-Table Master-Detail' report in ODT format. Instead, we'll save the existing template to ODT format using Microsoft Office. In order to achieve this; assuming you are using Microsoft Office 2010, please follow below steps:

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
