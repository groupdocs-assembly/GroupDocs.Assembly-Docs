---
id: in-table-list-with-filtering-grouping-and-ordering-in-spreadsheet-document
url: assembly/python-net/in-table-list-with-filtering-grouping-and-ordering-in-spreadsheet-document
title: In-Table List with Filtering Grouping and Ordering in Spreadsheet Document
weight: 2
description: "In-Table List with Filtering Grouping and Ordering in Spreadsheet Document with GroupDocs.Assembly for Python via .NET: the template, the Python data and the code."
keywords: in-table list with filtering grouping and ordering in spreadsheet document, GroupDocs.Assembly, Python, report generation
productName: GroupDocs.Assembly for Python via .NET
hideChildren: False
---
{{< alert style="info" >}}In this article, we will use GroupDocs.Assembly to generate a In-TableList with Filtering, Grouping, and Ordering report in Spreadsheet Document format based on the use case: [Working with a Business Case]({{< ref "assembly/python-net/developer-guide/basic-usage/working-with-a-business-case/_index.md" >}}).{{< /alert >}}{{< alert style="info" >}}The example reads the shop data described in [The Business Layer]({{< ref "assembly/python-net/developer-guide/basic-usage/working-with-a-business-case/the-business-layer.md" >}}).{{< /alert >}}

## In-Table List with Filtering, Grouping, and Ordering in Microsoft Excel Document

### Creating a In-Table List with Filtering, Grouping, and Ordering

Practising the following steps you can create In-Table List with Filtering, Grouping, and Ordering Template in MS Excel 2013.

1.  Add a new Workbook.
2.  Select the range of cells that you want to include in the table.
3.  On the Insert tab, in the Tables group, click Table.
4.  Save your Document.

### Reporting Requirement

As a report developer, you are required to represent customers' orders information with the following key requirements:

*   Report must show each customer along with sum of prices of his orders.
*   It must represent all the information in tabular form.
*   Report must be generated in the Spreadsheet Document.

### Adding Syntax to be evaluated by GroupDocs.Assembly Engine

<table cellspacing="0" cellpadding="0" style="border-collapse: collapse; margin-left: 0pt; width: 456pt;"><tbody><tr style="height: 15.75pt;"><td style="border-bottom-color: rgb(102, 102, 102); border-bottom-style: solid; border-bottom-width: 1.5pt; border-left-color: rgb(153, 153, 153); border-left-style: solid; border-left-width: 1pt; border-right-color: rgb(153, 153, 153); border-right-style: solid; border-right-width: 1pt; border-top-color: rgb(153, 153, 153); border-top-style: solid; border-top-width: 1pt; padding-left: 4.9pt; padding-right: 4.9pt; vertical-align: middle; width: 252.2pt;"><p style="margin-top: 0pt; margin-right: 0pt; margin-bottom: 0pt; margin-left: 0pt;"><span style="font-family: Calibri; font-size: 11pt; font-weight: bold;">Customer</span></p></td><td style="border-bottom-color: rgb(102, 102, 102); border-bottom-style: solid; border-bottom-width: 1.5pt; border-right-color: rgb(153, 153, 153); border-right-style: solid; border-right-width: 1pt; border-top-color: rgb(153, 153, 153); border-top-style: solid; border-top-width: 1pt; padding-left: 5.4pt; padding-right: 4.9pt; vertical-align: middle; width: 181.2pt;"><p style="margin-top: 0pt; margin-right: 0pt; margin-bottom: 0pt; margin-left: 0pt;"><span style="font-family: Calibri; font-size: 11pt; font-weight: bold;">Order Price</span></p></td></tr><tr style="height: 76.5pt;"><td style="border-bottom-color: rgb(153, 153, 153); border-bottom-style: solid; border-bottom-width: 1pt; border-left-color: rgb(153, 153, 153); border-left-style: solid; border-left-width: 1pt; border-right-color: rgb(153, 153, 153); border-right-style: solid; border-right-width: 1pt; padding-left: 4.9pt; padding-right: 4.9pt; vertical-align: middle; width: 252.2pt;"><p style="margin-top: 0pt; margin-right: 0pt; margin-bottom: 0pt; margin-left: 0pt;"><span style="font-family: Calibri; font-size: 11pt; font-weight: bold;">&lt;&lt;</span><span style="font-family: Calibri; font-size: 11pt; font-weight: bold;">foreach</span><span style="font-family: Calibri; font-size: 11pt; font-weight: bold;"> [in orders</span><br><span style="font-family: Calibri; font-size: 11pt; font-weight: bold;">&nbsp;&nbsp;&nbsp; .Where(c =&gt; </span><span style="font-family: Calibri; font-size: 11pt; font-weight: bold;">c.OrderDate.Year</span><span style="font-family: Calibri; font-size: 11pt; font-weight: bold;"> == 2015)</span><br><span style="font-family: Calibri; font-size: 11pt; font-weight: bold;">&nbsp;&nbsp;&nbsp; .</span><span style="font-family: Calibri; font-size: 11pt; font-weight: bold;">GroupBy</span><span style="font-family: Calibri; font-size: 11pt; font-weight: bold;">(c =&gt; </span><span style="font-family: Calibri; font-size: 11pt; font-weight: bold;">c.Customer</span><span style="font-family: Calibri; font-size: 11pt; font-weight: bold;">)</span><br><span style="font-family: Calibri; font-size: 11pt; font-weight: bold;">&nbsp;&nbsp;&nbsp; .</span><span style="font-family: Calibri; font-size: 11pt; font-weight: bold;">OrderBy</span><span style="font-family: Calibri; font-size: 11pt; font-weight: bold;">(g =&gt; </span><span style="font-family: Calibri; font-size: 11pt; font-weight: bold;">g.Key.CustomerName</span><span style="font-family: Calibri; font-size: 11pt; font-weight: bold;">)]&gt;&gt;&lt;&lt;[</span><span style="font-family: Calibri; font-size: 11pt; font-weight: bold;">Key.CustomerName</span><span style="font-family: Calibri; font-size: 11pt; font-weight: bold;">]&gt;&gt;</span></p></td><td style="border-bottom-color: rgb(153, 153, 153); border-bottom-style: solid; border-bottom-width: 1pt; border-right-color: rgb(153, 153, 153); border-right-style: solid; border-right-width: 1pt; padding-left: 5.4pt; padding-right: 4.9pt; vertical-align: middle; width: 181.2pt;"><p style="margin-top: 0pt; margin-right: 0pt; margin-bottom: 0pt; margin-left: 0pt;"><span style="font-family: Calibri; font-size: 11pt;">&lt;&lt;[Sum(c =&gt; </span><span style="font-family: Calibri; font-size: 11pt;">c.Price</span><span style="font-family: Calibri; font-size: 11pt;">)]&gt;&gt;&lt;&lt;/</span><span style="font-family: Calibri; font-size: 11pt;">foreach</span><span style="font-family: Calibri; font-size: 11pt;">&gt;&gt;</span></p></td></tr></tbody></table>
{{< alert style="success" >}}For detailed technical information about syntax, expressions and report generation by the engine, please visit: [Working with GroupDocs.Assembly Engine]({{< ref "assembly/python-net/developer-guide/basic-usage/working-with-groupdocs.assembly-engine/_index.md" >}}){{< /alert >}}

### Download In-Table List with Filtering, Grouping, and Ordering Template

Please download the sample In-Table List with Filtering, Grouping, and Ordering document we created in this article:

*   [in-table-list-with-filtering.ods](/assembly/python-net/_sample_files/developer-guide/advanced-usage/working-with-table-reports-filtered-ordered-grouped/in-table-list-with-filtering-grouping-and-ordering-in-spreadsheet-document/in-table-list-with-filtering.ods)

### Generating The Report

{{< tabs "example1" >}}
{{< tab "Python" >}}
```python
import json
from datetime import datetime

from groupdocs.assembly import DataSourceInfo, DocumentAssembler

def parse_dates(item):
    # JSON has no dates: turn the order dates into datetime objects for the template
    for key in ("OrderDate", "ShippingDate"):
        if key in item:
            item[key] = datetime.strptime(item[key], "%Y-%m-%dT%H:%M:%S")
    return item

with open("orders.json", encoding="utf-8") as f:
    orders = json.load(f, object_hook=parse_dates)

assembler = DocumentAssembler()
assembler.assemble_document("in-table-list-with-filtering.ods", "in-table-list-with-filtering-report.ods", DataSourceInfo(orders, "orders"))
```
{{< /tab >}}
{{< tab "in-table-list-with-filtering.ods" >}}
{{< tab-text >}}
The following sample file is used in this example: [in-table-list-with-filtering.ods](/assembly/python-net/_sample_files/developer-guide/advanced-usage/working-with-table-reports-filtered-ordered-grouped/in-table-list-with-filtering-grouping-and-ordering-in-spreadsheet-document/in-table-list-with-filtering.ods)
{{< /tab-text >}}
{{< /tab >}}
{{< tab "orders.json" >}}
{{< tab-text >}}
The following sample file is used in this example: [orders.json](/assembly/python-net/_sample_files/developer-guide/advanced-usage/working-with-table-reports-filtered-ordered-grouped/in-table-list-with-filtering-grouping-and-ordering-in-spreadsheet-document/orders.json)
{{< /tab-text >}}
{{< /tab >}}
{{< tab "in-table-list-with-filtering-report.ods" >}}  
```text
Binary file (ODS, 6 KB)
```
[Download full output](/assembly/python-net/_output_files/developer-guide/advanced-usage/working-with-table-reports-filtered-ordered-grouped/in-table-list-with-filtering-grouping-and-ordering-in-spreadsheet-document/generating_the_report/in-table-list-with-filtering-report.ods)
{{< /tab >}}
{{< /tabs >}}

## In-Table List with Filtering, Grouping, and Ordering in OpenOffice Spreadsheet Document

### Creating the Template

OpenDocument Spreadsheet (ODS) is a spreadsheet document format which can be used as an alternative to Microsoft Excel Document (XLS/XLSX) formats. Since ODS is not a Microsoft Proprietary format, there are multiple software (including Microsoft Office and Apache OpenOffice) available to create, open, edit and save this format. For more information on the available software to work with ODS, please visit [wikipedia article](https://en.wikipedia.org/wiki/OpenDocument#Software).

In this topic, we 'll not reinvent the wheel to recreate a template for generating an 'In-Table List with Filtering, Grouping, and Ordering' report in ODS format. Instead, we'll save the existing template to ODS format using Microsoft Office. In order to achieve this; assuming you are using Microsoft Office 2010, please follow below steps:

1.  Open existing template we created in previous topic.
2.  Click "File" and select "Save As".
3.  Select "OpenDocument Spreadsheet" from "Save As Type" drop down.
4.  Click "Save".

### Download Template

### Generating the report

### ODS Template and Report in Apache OpenOffice

In order to check compatibility of ODS between Microsoft Office 2010 and Apache OpenOffice 4.1.2, we performed below tests:

*   We opened the ODS template created through Microsoft Office 2010 in Apache OpenOffice 4.1.2. The template opened successfully in Apache OpenOffice without any issues or formatting losses.
*   We opened the ODS report generated through GroupDocs.Assembly in Apache OpenOffice 4.1.2. The report opened successfully in Apache OpenOffice without any issues or formatting losses.
