---
id: inserting-chart-axis-title-dynamically-in-spreadsheet-document
url: assembly/python-net/inserting-chart-axis-title-dynamically-in-spreadsheet-document
title: Inserting Chart Axis Title Dynamically in Spreadsheet Document
weight: 7
description: "Inserting Chart Axis Title Dynamically in Spreadsheet Document with GroupDocs.Assembly for Python via .NET: the template, the Python data and the code."
keywords: inserting chart axis title dynamically in spreadsheet document, GroupDocs.Assembly, Python, report generation
productName: GroupDocs.Assembly for Python via .NET
hideChildren: False
---
{{< alert style="info" >}}The example reads the shop data described in [The Business Layer]({{< ref "assembly/python-net/developer-guide/basic-usage/working-with-a-business-case/the-business-layer.md" >}}).{{< /alert >}}

## Column Chart in Microsoft Excel Document

### Creating a Column Chart

Following steps, you can create a column chart in MS Excel 2013:

1.  Create a new Workbook
2.  Click the "Insert" tab, and then click "Insert Column Chart" icon in the Charts group to view the drop-down list
3.  Select the "100% Stacked Column" and press "OK" to insert the chart and Worksheet template to your Worksheet
4.  Edit the Worksheet with your data to update the chart
5.  Save your Document

### Reporting Requirement

As a report developer, you are required to share orders quantity of the customers dynamically with the following key requirements:

*   A report must show the quantity of sales/orders
*   Sales/orders quantity must be represented by Quarters
*   It must associate order quantity with the corresponding customer
*   A report must be generated in the Spreadsheet Document

### Adding Syntax to be Evaluated by GroupDocs.Assembly Engine

#### Chart Title

```text
<<[title]>><<foreach [in orders
.Where(c => c.OrderDate.Year == 2015)
.GroupBy(c => c.Customer)
.OrderBy(g => g.Key.CustomerName)]>><<x [Key.CustomerName]>>
```

#### Chart Data

**Legend Entries**

```text
="1st Quarter<<y [Where(c => c.OrderDate.Month >= 1 && c.OrderDate.Month <= 3).Sum(c => c.ProductQuantity)]>>"
="2nd Quarter<<y [Where(c => c.OrderDate.Month >= 4 && c.OrderDate.Month <= 6).Sum(c => c.ProductQuantity)]>>"
="3rd Quarter<<y [Where(c => c.OrderDate.Month >= 7 && c.OrderDate.Month <= 9).Sum(c => c.ProductQuantity)]>>"
="4th Quarter<<y [Where(c => c.OrderDate.Month >= 10 && c.OrderDate.Month <= 12).Sum(c => c.ProductQuantity)]>>"
```

### Download Template

Please download the sample Chart with Filtering, Grouping, and Ordering with Dynamic Title document we created in this article:

*   [chart-with-filtering-and-dynamic-title.xlsx](/assembly/python-net/_sample_files/developer-guide/advanced-usage/working-with-chart-reports-filtered-ordered-grouped/inserting-chart-axis-title-dynamically-in-spreadsheet-document/chart-with-filtering-and-dynamic-title.xlsx)

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
assembler.assemble_document("chart-with-filtering-and-dynamic-title.xlsx", "chart-with-filtering-and-dynamic-title-report.xlsx", [
    DataSourceInfo(orders, "orders"),
    DataSourceInfo("Harbor Lane orders by customer, 2015", "title"),
])
```
{{< /tab >}}
{{< tab "chart-with-filtering-and-dynamic-title.xlsx" >}}
{{< tab-text >}}
The following sample file is used in this example: [chart-with-filtering-and-dynamic-title.xlsx](/assembly/python-net/_sample_files/developer-guide/advanced-usage/working-with-chart-reports-filtered-ordered-grouped/inserting-chart-axis-title-dynamically-in-spreadsheet-document/chart-with-filtering-and-dynamic-title.xlsx)
{{< /tab-text >}}
{{< /tab >}}
{{< tab "orders.json" >}}
{{< tab-text >}}
The following sample file is used in this example: [orders.json](/assembly/python-net/_sample_files/developer-guide/advanced-usage/working-with-chart-reports-filtered-ordered-grouped/inserting-chart-axis-title-dynamically-in-spreadsheet-document/orders.json)
{{< /tab-text >}}
{{< /tab >}}
{{< tab "chart-with-filtering-and-dynamic-title-report.xlsx" >}}  
```text
Binary file (XLSX, 13 KB)
```
[Download full output](/assembly/python-net/_output_files/developer-guide/advanced-usage/working-with-chart-reports-filtered-ordered-grouped/inserting-chart-axis-title-dynamically-in-spreadsheet-document/generating_the_report/chart-with-filtering-and-dynamic-title-report.xlsx)
{{< /tab >}}
{{< /tabs >}}
