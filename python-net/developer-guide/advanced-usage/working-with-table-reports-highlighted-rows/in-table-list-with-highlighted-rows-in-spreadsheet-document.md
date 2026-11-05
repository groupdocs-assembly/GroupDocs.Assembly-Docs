---
id: in-table-list-with-highlighted-rows-in-spreadsheet-document
url: assembly/python-net/in-table-list-with-highlighted-rows-in-spreadsheet-document
title: In-Table List with Highlighted Rows in Spreadsheet Document
weight: 2
description: "In-Table List with Highlighted Rows in Spreadsheet Document with GroupDocs.Assembly for Python via .NET: the template, the Python data and the code."
keywords: in-table list with highlighted rows in spreadsheet document, GroupDocs.Assembly, Python, report generation
productName: GroupDocs.Assembly for Python via .NET
hideChildren: False
---
{{< alert style="info" >}}In this article, we will use GroupDocs.Assembly to generate an In-Table List with Highlighted Rows report in Spreadsheet Document format based on the use case: [Working with a Business Case]({{< ref "assembly/python-net/developer-guide/basic-usage/working-with-a-business-case/_index.md" >}}).{{< /alert >}}{{< alert style="info" >}}The example reads the shop data described in [The Business Layer]({{< ref "assembly/python-net/developer-guide/basic-usage/working-with-a-business-case/the-business-layer.md" >}}).{{< /alert >}}

## In-Table List with Highlighted Rows in Microsoft Excel Document

### Creating a In-Table List with Highlighted Rows

Practising the following steps you can create In-Table List with Highlighted Rows Template in MS Excel 2013.

1.  Add a new Workbook.
2.  Select the range of cells that you want to include in the table.
3.  On the Insert tab, in the Tables group, click Table.
4.  Insert a 2x4 table.
5.  Click the cell you want to highlight.
6.  Click "Cell Styles" in Styles group.
7.  Save the template.

### Reporting Requirement

As a report developer, you are required to represent customers' orders information with a specific filtering condition with the following key requirements:

*   The report must show each customer along with his orders.
*   Show single Customer and his single order price in a single row.
*   It must highlight the record with order price more than or equal to 400.
*   It must show sum of the order prices.
*   It must represent all the information in tabular form.
*   The report must be generated in the Spreadsheet Document.

### Adding Syntax to be evaluated by GroupDocs.Assembly Engine

<table cellspacing="0" cellpadding="0" style="border-collapse: collapse; margin-left: 0pt; width: 397pt;"><tbody><tr style="height: 15.75pt;"><td style="border-bottom-color: rgb(102, 102, 102); border-bottom-style: solid; border-bottom-width: 1.5pt; border-left-color: rgb(153, 153, 153); border-left-style: solid; border-left-width: 1pt; border-right-color: rgb(153, 153, 153); border-right-style: solid; border-right-width: 1pt; border-top-color: rgb(153, 153, 153); border-top-style: solid; border-top-width: 1pt; padding-left: 4.9pt; padding-right: 4.9pt; vertical-align: middle; width: 231.2pt;"><p style="margin-top: 0pt; margin-right: 0pt; margin-bottom: 0pt; margin-left: 0pt;"><span style="font-family: Calibri; font-size: 11pt; font-weight: bold;">Customer</span></p></td><td style="border-bottom-color: rgb(102, 102, 102); border-bottom-style: solid; border-bottom-width: 1.5pt; border-right-color: rgb(153, 153, 153); border-right-style: solid; border-right-width: 1pt; border-top-color: rgb(153, 153, 153); border-top-style: solid; border-top-width: 1pt; padding-left: 5.4pt; padding-right: 4.9pt; vertical-align: middle; width: 143.2pt;"><p style="margin-top: 0pt; margin-right: 0pt; margin-bottom: 0pt; margin-left: 0pt;"><span style="font-family: Calibri; font-size: 11pt; font-weight: bold;">Order Price</span></p></td></tr><tr style="height: 31.5pt;"><td style="background-color: rgb(255, 242, 204); border-bottom-color: rgb(153, 153, 153); border-bottom-style: solid; border-bottom-width: 1pt; border-left-color: rgb(153, 153, 153); border-left-style: solid; border-left-width: 1pt; border-right-color: rgb(153, 153, 153); border-right-style: solid; border-right-width: 1pt; padding-left: 4.9pt; padding-right: 4.9pt; vertical-align: middle; width: 231.2pt;"><p style="margin-top: 0pt; margin-right: 0pt; margin-bottom: 0pt; margin-left: 0pt;"><span style="font-family: Calibri; font-size: 11pt; font-weight: bold;">&lt;&lt;</span><span style="font-family: Calibri; font-size: 11pt; font-weight: bold;">foreach</span><span style="font-family: Calibri; font-size: 11pt; font-weight: bold;"> [in orders]&gt;&gt;&lt;&lt;if [Price &gt;= 400]&gt;&gt;&lt;&lt;[</span><span style="font-family: Calibri; font-size: 11pt; font-weight: bold;">Customer.CustomerName</span><span style="font-family: Calibri; font-size: 11pt; font-weight: bold;">]&gt;&gt;</span></p></td><td style="background-color: rgb(255, 242, 204); border-bottom-color: rgb(153, 153, 153); border-bottom-style: solid; border-bottom-width: 1pt; border-right-color: rgb(153, 153, 153); border-right-style: solid; border-right-width: 1pt; padding-left: 5.4pt; padding-right: 4.9pt; vertical-align: middle; width: 143.2pt;"><p style="margin-top: 0pt; margin-right: 0pt; margin-bottom: 0pt; margin-left: 0pt;"><span style="font-family: Calibri; font-size: 11pt;">&lt;&lt;[Price]&gt;&gt;</span></p></td></tr><tr style="height: 15.75pt;"><td style="border-bottom-color: rgb(153, 153, 153); border-bottom-style: solid; border-bottom-width: 1pt; border-left-color: rgb(153, 153, 153); border-left-style: solid; border-left-width: 1pt; border-right-color: rgb(153, 153, 153); border-right-style: solid; border-right-width: 1pt; padding-left: 4.9pt; padding-right: 4.9pt; vertical-align: middle; width: 231.2pt;"><p style="margin-top: 0pt; margin-right: 0pt; margin-bottom: 0pt; margin-left: 0pt;"><span style="font-family: Calibri; font-size: 11pt; font-weight: bold;">&lt;&lt;else&gt;&gt;&lt;&lt;[</span><span style="font-family: Calibri; font-size: 11pt; font-weight: bold;">Customer.CustomerName</span><span style="font-family: Calibri; font-size: 11pt; font-weight: bold;">]&gt;&gt;</span></p></td><td style="border-bottom-color: rgb(153, 153, 153); border-bottom-style: solid; border-bottom-width: 1pt; border-right-color: rgb(153, 153, 153); border-right-style: solid; border-right-width: 1pt; padding-left: 5.4pt; padding-right: 4.9pt; vertical-align: middle; width: 143.2pt;"><p style="margin-top: 0pt; margin-right: 0pt; margin-bottom: 0pt; margin-left: 0pt;"><span style="font-family: Calibri; font-size: 11pt;">&lt;&lt;[Price]&gt;&gt;&lt;&lt;/if&gt;&gt;&lt;&lt;/</span><span style="font-family: Calibri; font-size: 11pt;">foreach</span><span style="font-family: Calibri; font-size: 11pt;">&gt;&gt;</span></p></td></tr><tr style="height: 15.75pt;"><td style="border-bottom-color: rgb(153, 153, 153); border-bottom-style: solid; border-bottom-width: 1pt; border-left-color: rgb(153, 153, 153); border-left-style: solid; border-left-width: 1pt; border-right-color: rgb(153, 153, 153); border-right-style: solid; border-right-width: 1pt; padding-left: 4.9pt; padding-right: 4.9pt; vertical-align: middle; width: 231.2pt;"><p style="margin-top: 0pt; margin-right: 0pt; margin-bottom: 0pt; margin-left: 0pt;"><span style="font-family: Calibri; font-size: 11pt; font-weight: bold;">Total:</span></p></td><td style="border-bottom-color: rgb(153, 153, 153); border-bottom-style: solid; border-bottom-width: 1pt; border-right-color: rgb(153, 153, 153); border-right-style: solid; border-right-width: 1pt; padding-left: 5.4pt; padding-right: 4.9pt; vertical-align: middle; width: 143.2pt;"><p style="margin-top: 0pt; margin-right: 0pt; margin-bottom: 0pt; margin-left: 0pt;"><span style="font-family: Calibri; font-size: 11pt;">&lt;&lt;[Sum(c =&gt; </span><span style="font-family: Calibri; font-size: 11pt;">c.Price</span><span style="font-family: Calibri; font-size: 11pt;">)]&gt;&gt;</span></p></td></tr></tbody></table>
{{< alert style="success" >}}For detailed technical information about syntax, expressions and report generation by the engine, please visit: [Working with GroupDocs.Assembly Engine]({{< ref "assembly/python-net/developer-guide/basic-usage/working-with-groupdocs.assembly-engine/_index.md" >}}).{{< /alert >}}

### Download In-Table List with Highlighted Rows Template

Please download the sample In-Table List with Highlighted Rows document we created in this article:

*   [in-table-list-with-highlighted-rows.ods](/assembly/python-net/_sample_files/developer-guide/advanced-usage/working-with-table-reports-highlighted-rows/in-table-list-with-highlighted-rows-in-spreadsheet-document/in-table-list-with-highlighted-rows.ods)

### Generating The Report

{{< tabs "example1" >}}
{{< tab "Python" >}}
```python
import json

from groupdocs.assembly import DataSourceInfo, DocumentAssembler

with open("orders.json", encoding="utf-8") as f:
    orders = json.load(f)

assembler = DocumentAssembler()
assembler.assemble_document("in-table-list-with-highlighted-rows.ods", "in-table-list-with-highlighted-rows-report.ods", DataSourceInfo(orders, "orders"))
```
{{< /tab >}}
{{< tab "in-table-list-with-highlighted-rows.ods" >}}
{{< tab-text >}}
The following sample file is used in this example: [in-table-list-with-highlighted-rows.ods](/assembly/python-net/_sample_files/developer-guide/advanced-usage/working-with-table-reports-highlighted-rows/in-table-list-with-highlighted-rows-in-spreadsheet-document/in-table-list-with-highlighted-rows.ods)
{{< /tab-text >}}
{{< /tab >}}
{{< tab "orders.json" >}}
{{< tab-text >}}
The following sample file is used in this example: [orders.json](/assembly/python-net/_sample_files/developer-guide/advanced-usage/working-with-table-reports-highlighted-rows/in-table-list-with-highlighted-rows-in-spreadsheet-document/orders.json)
{{< /tab-text >}}
{{< /tab >}}
{{< tab "in-table-list-with-highlighted-rows-report.ods" >}}  
```text
Binary file (ODS, 6 KB)
```
[Download full output](/assembly/python-net/_output_files/developer-guide/advanced-usage/working-with-table-reports-highlighted-rows/in-table-list-with-highlighted-rows-in-spreadsheet-document/generating_the_report/in-table-list-with-highlighted-rows-report.ods)
{{< /tab >}}
{{< /tabs >}}

## In-Table List with Highlighted Rows in OpenOffice Spreadsheet Document

### Creating the Template

OpenDocument Spreadsheet (ODS) is a spreadsheet document format which can be used as an alternative to Microsoft Excel Document (XLS/XLSX) formats. Since ODS is not a Microsoft Proprietary format, there are multiple software (including Microsoft Office and Apache OpenOffice) available to create, open, edit and save this format. For more information on the available software to work with ODS, please visit [wikipedia article](https://en.wikipedia.org/wiki/OpenDocument#Software).

In this topic, we 'll not reinvent the wheel to recreate a template for generating an 'In-Table List with Highlighted Rows' report in ODS format. Instead, we'll save the existing template to ODS format using Microsoft Office. In order to achieve this; assuming you are using Microsoft Office 2010, please follow below steps:

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
