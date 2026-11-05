---
id: in-table-master-detail-in-spreadsheet-document
url: assembly/python-net/in-table-master-detail-in-spreadsheet-document
title: In-Table Master-Detail in Spreadsheet Document
weight: 2
description: "In-Table Master-Detail in Spreadsheet Document with GroupDocs.Assembly for Python via .NET: the template, the Python data and the code."
keywords: in-table master-detail in spreadsheet document, GroupDocs.Assembly, Python, report generation
productName: GroupDocs.Assembly for Python via .NET
hideChildren: False
---
{{< alert style="info" >}}In this article, we will use GroupDocs.Assembly to generate an In-Table Master-Detail report in Spreadsheet Document format based on the use case: [Working with a Business Case]({{< ref "assembly/python-net/developer-guide/basic-usage/working-with-a-business-case/_index.md" >}}).{{< /alert >}}{{< alert style="info" >}}The example reads the shop data described in [The Business Layer]({{< ref "assembly/python-net/developer-guide/basic-usage/working-with-a-business-case/the-business-layer.md" >}}).{{< /alert >}}

## In-Table Master-Detail in Microsoft Excel Document

### Creating a In-Table Master-Detail

Practising the following steps you can create In-Table Master-Detail Template in MS Excel 2013.

1.  Add a new Workbook.
2.  Select the range of cells that you want to include in the table.
3.  On the Insert tab, in the Tables group, click Table.
4.  Insert a 2x4 table.
5.  Save the template.

### Reporting Requirement

As a report developer, you are required to represent customers' total orders prices and price of each product separately with the following key requirements:

*   The report must show each customer along with his total orders prices.
*   It must also show each individual product ordered by the customers.
*   It must show the sum of the order prices.
*   It must represent all the information in tabular form.
*   The report must be generated in the Spreadsheet Document.

### Adding Syntax to be evaluated by GroupDocs.Assembly Engine

<table cellspacing="0" cellpadding="0" style="border-collapse: collapse; margin-left: 0pt;"><tbody><tr style="height: 15.25pt;"><td style="border-bottom-color: rgb(128, 128, 128); border-bottom-style: solid; border-bottom-width: 2.25pt; border-left-color: rgb(150, 150, 150); border-left-style: solid; border-left-width: 1.5pt; border-right-color: rgb(150, 150, 150); border-right-style: solid; border-right-width: 1.5pt; border-top-color: rgb(150, 150, 150); border-top-style: solid; border-top-width: 1.5pt; padding-left: 0.75pt; padding-right: 0.75pt; vertical-align: top; width: 254.9pt;"><p style="margin-top: 0pt; margin-right: 0pt; margin-bottom: 0pt; margin-left: 0pt;"><span style="font-family: Calibri; font-size: 11pt; font-weight: bold;">Customer</span></p></td><td style="border-bottom-color: rgb(128, 128, 128); border-bottom-style: solid; border-bottom-width: 2.25pt; border-right-color: rgb(150, 150, 150); border-right-style: solid; border-right-width: 1.5pt; border-top-color: rgb(150, 150, 150); border-top-style: solid; border-top-width: 1.5pt; padding-left: 1.5pt; padding-right: 0.75pt; vertical-align: top; width: 151.65pt;"><p style="margin-top: 0pt; margin-right: 0pt; margin-bottom: 0pt; margin-left: 0pt;"><span style="font-family: Calibri; font-size: 11pt; font-weight: bold;">Order Price</span></p></td></tr><tr style="height: 30.5pt;"><td style="border-bottom-color: rgb(150, 150, 150); border-bottom-style: solid; border-bottom-width: 1.5pt; border-left-color: rgb(150, 150, 150); border-left-style: solid; border-left-width: 1.5pt; border-right-color: rgb(150, 150, 150); border-right-style: solid; border-right-width: 1.5pt; padding-left: 0.75pt; padding-right: 0.75pt; vertical-align: top; width: 254.9pt;"><p style="margin-top: 0pt; margin-right: 0pt; margin-bottom: 0pt; margin-left: 0pt;"><span style="font-family: Calibri; font-size: 11pt; font-weight: bold;">&lt;&lt;</span><span style="font-family: Calibri; font-size: 11pt; font-weight: bold;">foreach</span><span style="font-family: Calibri; font-size: 11pt; font-weight: bold;"> [in customers]&gt;&gt;&lt;&lt;[</span><span style="font-family: Calibri; font-size: 11pt; font-weight: bold;">CustomerName</span><span style="font-family: Calibri; font-size: 11pt; font-weight: bold;">]&gt;&gt;</span></p></td><td style="border-bottom-color: rgb(150, 150, 150); border-bottom-style: solid; border-bottom-width: 1.5pt; border-right-color: rgb(150, 150, 150); border-right-style: solid; border-right-width: 1.5pt; padding-left: 1.5pt; padding-right: 0.75pt; vertical-align: top; width: 151.65pt;"><p style="margin-top: 0pt; margin-right: 0pt; margin-bottom: 0pt; margin-left: 0pt;"><span style="font-family: Calibri; font-size: 11pt;">&lt;&lt;[</span><span style="font-family: Calibri; font-size: 11pt;">Order.Sum</span><span style="font-family: Calibri; font-size: 11pt;">(</span></p><p style="margin-top: 0pt; margin-right: 0pt; margin-bottom: 0pt; margin-left: 0pt;"><span style="font-family: Calibri; font-size: 11pt;">c =&gt; </span><span style="font-family: Calibri; font-size: 11pt;">c.Price</span><span style="font-family: Calibri; font-size: 11pt;">)]&gt;&gt;</span></p></td></tr><tr style="height: 29.75pt;"><td style="border-bottom-color: rgb(150, 150, 150); border-bottom-style: solid; border-bottom-width: 1.5pt; border-left-color: rgb(150, 150, 150); border-left-style: solid; border-left-width: 1.5pt; border-right-color: rgb(150, 150, 150); border-right-style: solid; border-right-width: 1.5pt; padding-left: 0.75pt; padding-right: 0.75pt; vertical-align: top; width: 254.9pt;"><p style="margin-top: 0pt; margin-right: 0pt; margin-bottom: 0pt; margin-left: 0pt;"><span style="font-family: Calibri; font-size: 11pt; font-style: italic;">&lt;&lt;</span><span style="font-family: Calibri; font-size: 11pt; font-style: italic;">foreach</span><span style="font-family: Calibri; font-size: 11pt; font-style: italic;"> [in Order]&gt;&gt; &lt;&lt;[</span><span style="font-family: Calibri; font-size: 11pt; font-style: italic;">Product.ProductName</span><span style="font-family: Calibri; font-size: 11pt; font-style: italic;">]&gt;&gt;</span></p></td><td style="border-bottom-color: rgb(150, 150, 150); border-bottom-style: solid; border-bottom-width: 1.5pt; border-right-color: rgb(150, 150, 150); border-right-style: solid; border-right-width: 1.5pt; padding-left: 1.5pt; padding-right: 0.75pt; vertical-align: top; width: 151.65pt;"><p style="margin-top: 0pt; margin-right: 0pt; margin-bottom: 0pt; margin-left: 0pt;"><span style="font-family: Calibri; font-size: 11pt;">&lt;&lt;[Price]&gt;&gt;&lt;&lt;/</span><span style="font-family: Calibri; font-size: 11pt;">foreach</span><span style="font-family: Calibri; font-size: 11pt;">&gt;&gt;&lt;&lt;/</span></p><p style="margin-top: 0pt; margin-right: 0pt; margin-bottom: 0pt; margin-left: 0pt;"><span style="font-family: Calibri; font-size: 11pt;">foreach</span><span style="font-family: Calibri; font-size: 11pt;">&gt;&gt;</span></p></td></tr><tr style="height: 44.3pt;"><td style="border-bottom-color: rgb(150, 150, 150); border-bottom-style: solid; border-bottom-width: 1.5pt; border-left-color: rgb(150, 150, 150); border-left-style: solid; border-left-width: 1.5pt; border-right-color: rgb(150, 150, 150); border-right-style: solid; border-right-width: 1.5pt; padding-left: 0.75pt; padding-right: 0.75pt; vertical-align: top; width: 254.9pt;"><p style="margin-top: 0pt; margin-right: 0pt; margin-bottom: 0pt; margin-left: 0pt;"><span style="font-family: Calibri; font-size: 11pt; font-weight: bold;">Total:</span></p></td><td style="border-bottom-color: rgb(150, 150, 150); border-bottom-style: solid; border-bottom-width: 1.5pt; border-right-color: rgb(150, 150, 150); border-right-style: solid; border-right-width: 1.5pt; padding-left: 1.5pt; padding-right: 0.75pt; vertical-align: top; width: 151.65pt;"><p style="margin-top: 0pt; margin-right: 0pt; margin-bottom: 0pt; margin-left: 0pt;"><span style="font-family: Calibri; font-size: 11pt;">&lt;&lt;[Sum(</span></p><p style="margin-top: 0pt; margin-right: 0pt; margin-bottom: 0pt; margin-left: 0pt;"><span style="font-family: Calibri; font-size: 11pt;">m =&gt; </span><span style="font-family: Calibri; font-size: 11pt;">m.Order.Sum</span><span style="font-family: Calibri; font-size: 11pt;">(</span></p><p style="margin-top: 0pt; margin-right: 0pt; margin-bottom: 0pt; margin-left: 0pt;"><span style="font-family: Calibri; font-size: 11pt;">c =&gt; </span><span style="font-family: Calibri; font-size: 11pt;">c.Price</span><span style="font-family: Calibri; font-size: 11pt;">))]&gt;&gt;</span></p></td></tr></tbody></table>
{{< alert style="success" >}}For detailed technical information about syntax, expressions and report generation by the engine, please visit: [Working with GroupDocs.Assembly Engine]({{< ref "assembly/python-net/developer-guide/basic-usage/working-with-groupdocs.assembly-engine/_index.md" >}}).{{< /alert >}}

### Download In-Table Master-Detail Template

Please download the sample In-Table Master-Detail document we created in this article:

*   [in-table-master-detail.ods](/assembly/python-net/_sample_files/developer-guide/advanced-usage/working-with-table-reports-master-detail/in-table-master-detail-in-spreadsheet-document/in-table-master-detail.ods)

### Generating The Report

{{< tabs "example1" >}}
{{< tab "Python" >}}
```python
import json

from groupdocs.assembly import DataSourceInfo, DocumentAssembler

with open("customers.json", encoding="utf-8") as f:
    customers = json.load(f)

assembler = DocumentAssembler()
assembler.assemble_document("in-table-master-detail.ods", "in-table-master-detail-report.ods", DataSourceInfo(customers, "customers"))
```
{{< /tab >}}
{{< tab "in-table-master-detail.ods" >}}
{{< tab-text >}}
The following sample file is used in this example: [in-table-master-detail.ods](/assembly/python-net/_sample_files/developer-guide/advanced-usage/working-with-table-reports-master-detail/in-table-master-detail-in-spreadsheet-document/in-table-master-detail.ods)
{{< /tab-text >}}
{{< /tab >}}
{{< tab "customers.json" >}}
{{< tab-text >}}
The following sample file is used in this example: [customers.json](/assembly/python-net/_sample_files/developer-guide/advanced-usage/working-with-table-reports-master-detail/in-table-master-detail-in-spreadsheet-document/customers.json)
{{< /tab-text >}}
{{< /tab >}}
{{< tab "in-table-master-detail-report.ods" >}}  
```text
Binary file (ODS, 6 KB)
```
[Download full output](/assembly/python-net/_output_files/developer-guide/advanced-usage/working-with-table-reports-master-detail/in-table-master-detail-in-spreadsheet-document/generating_the_report/in-table-master-detail-report.ods)
{{< /tab >}}
{{< /tabs >}}

## In-Table Master-Detail in OpenOffice Spreadsheet Document

### Creating the Template

OpenDocument Spreadsheet (ODS) is a spreadsheet document format which can be used as an alternative to Microsoft Excel Document (XLS/XLSX) formats. Since ODS is not a Microsoft Proprietary format, there are multiple software (including Microsoft Office and Apache OpenOffice) available to create, open, edit and save this format. For more information on the available software to work with ODS, please visit [wikipedia article](https://en.wikipedia.org/wiki/OpenDocument#Software).

In this topic, we 'll not reinvent the wheel to recreate a template for generating an 'In-Table Master-Detail' report in ODS format. Instead, we'll save the existing template to ODS format using Microsoft Office. In order to achieve this; assuming you are using Microsoft Office 2010, please follow below steps:

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
