---
id: removing-selective-chart-series-dynamically
url: assembly/python-net/removing-selective-chart-series-dynamically
title: Removing Selective Chart Series Dynamically
weight: 5
description: "Removing Selective Chart Series Dynamically with GroupDocs.Assembly for Python via .NET: the template, the Python data and the code."
keywords: removing selective chart series dynamically, GroupDocs.Assembly, Python, report generation
productName: GroupDocs.Assembly for Python via .NET
hideChildren: False
---
{{< alert style="info" >}}The example reads the shop data described in [The Business Layer]({{< ref "assembly/python-net/developer-guide/basic-usage/working-with-a-business-case/the-business-layer.md" >}}).{{< /alert >}}

## Column Chart in Microsoft Word Document

### Creating a Column Chart

Practising the following steps, you can insert a Column Chart in MS Word 2013:

1.  Click in the document where you want to insert the chart, click the "Insert" tab, and then click "Chart" in the illustrations group to open the "Insert Chart" dialog box.
2.  Select "Column" in the sidebar, you will see a gallery of charts.
3.  Select the "100% Stacked Column" and press "OK" to insert the chart and Worksheet template to your document.
4.  Edit the Worksheet with your data to update the chart. See [Chart Data (Excel)]({{< ref "assembly/python-net/developer-guide/advanced-usage/working-with-chart-reports-filtered-ordered-grouped/removing-selective-chart-series-dynamically.md#adding-syntax-to-be-evaluated-by-groupdocsassembly-engine" >}}).
5.  Save your Document.

### Reporting Requirement

As a report developer, you are required to share orders quantity of the customers dynamically with the following key requirements:

*   A report must show the quantity of sales/orders.
*   Sales/orders quantity must represented by Quarters.
*   It must associate order quantity with the corresponding customer.
*   The report must be generated in the Word Processing Document.

### Adding Syntax to be evaluated by GroupDocs.Assembly Engine

#### Chart Title

```text
Total Order Quantity by Quarters<<foreach [in orders
.Where(c => c.OrderDate.Year == 2015)
.GroupBy(c => c.Customer)
.OrderBy(g => g.Key.CustomerName)]>><<x [Key.CustomerName]>>

```

#### Chart Data (Excel)

|   | 1st Quarter<<y[Where(c => c.OrderDate.Month>= 1 && c.OrderDate.Month <= 3).Sum(c => c.ProductQuantity)]>><<removeif [mode== 1]>> | 2nd Quarter<<y[Where(c => c.OrderDate.Month>= 4 && c.OrderDate.Month <= 6).Sum(c => c.ProductQuantity)]>><<removeif [mode==2]>> | 3rd Quarter<<y[Where(c => c.OrderDate.Month>= 7 && c.OrderDate.Month <= 9).Sum(c => c.ProductQuantity)]>> | 4th Quarter<<y[Where(c => c.OrderDate.Month>= 10 && c.OrderDate.Month <= 12).Sum(c => c.ProductQuantity)]>> |
| --- | --- | --- | --- | --- |
| Category 1 | 4.3 | 2.4 | 2 | 3 |
| Category 2 | 2.5 | 4.4 | 2 | 2 |
| Category 3 | 3.5 | 1.8 | 3 | 5 |
| Category 4 | 4.5 | 2.8 | 5 | 2 |

{{< alert style="success" >}}For detailed technical information about syntax, expressions and report generation by the engine, please visit: [Working with GroupDocs.Assembly Engine]({{< ref "assembly/python-net/developer-guide/basic-usage/working-with-groupdocs.assembly-engine/_index.md" >}}).{{< /alert >}}

### Download Template

Please download the sample Chart with Filtering, Grouping, and Ordering document we created in this article:

*   [remove-selective-chart-series.docx](/assembly/python-net/_sample_files/developer-guide/advanced-usage/working-with-chart-reports-filtered-ordered-grouped/removing-selective-chart-series-dynamically/remove-selective-chart-series.docx)

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
assembler.assemble_document("remove-selective-chart-series.docx", "remove-selective-chart-series-report.docx", [
    DataSourceInfo(orders, "orders"),
    DataSourceInfo(1, "mode"),
])
```
{{< /tab >}}
{{< tab "remove-selective-chart-series.docx" >}}
{{< tab-text >}}
The following sample file is used in this example: [remove-selective-chart-series.docx](/assembly/python-net/_sample_files/developer-guide/advanced-usage/working-with-chart-reports-filtered-ordered-grouped/removing-selective-chart-series-dynamically/remove-selective-chart-series.docx)
{{< /tab-text >}}
{{< /tab >}}
{{< tab "orders.json" >}}
{{< tab-text >}}
The following sample file is used in this example: [orders.json](/assembly/python-net/_sample_files/developer-guide/advanced-usage/working-with-chart-reports-filtered-ordered-grouped/removing-selective-chart-series-dynamically/orders.json)
{{< /tab-text >}}
{{< /tab >}}
{{< tab "remove-selective-chart-series-report.docx" >}}  
```text
Binary file (DOCX, 13 KB)
```
[Download full output](/assembly/python-net/_output_files/developer-guide/advanced-usage/working-with-chart-reports-filtered-ordered-grouped/removing-selective-chart-series-dynamically/generating_the_report/remove-selective-chart-series-report.docx)
{{< /tab >}}
{{< /tabs >}}
