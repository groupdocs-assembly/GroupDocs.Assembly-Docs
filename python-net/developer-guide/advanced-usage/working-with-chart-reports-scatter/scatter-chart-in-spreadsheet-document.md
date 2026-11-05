---
id: scatter-chart-in-spreadsheet-document
url: assembly/python-net/scatter-chart-in-spreadsheet-document
title: Scatter Chart in Spreadsheet Document
weight: 2
description: "Scatter Chart in Spreadsheet Document with GroupDocs.Assembly for Python via .NET: the template, the Python data and the code."
keywords: scatter chart in spreadsheet document, GroupDocs.Assembly, Python, report generation
productName: GroupDocs.Assembly for Python via .NET
hideChildren: False
---
{{< alert style="info" >}}In this article, we will use GroupDocs.Assembly to generate a Scatter Chart report in Spreadsheet Document format based on the use case: [Working with a Business Case]({{< ref "assembly/python-net/developer-guide/basic-usage/working-with-a-business-case/_index.md" >}}).{{< /alert >}}{{< alert style="info" >}}The example reads the shop data described in [The Business Layer]({{< ref "assembly/python-net/developer-guide/basic-usage/working-with-a-business-case/the-business-layer.md" >}}).{{< /alert >}}

## Scatter Chart in Microsoft Excel Document

### Creating a Scatter Chart

Please follow below steps to create Scatter Chart in MS Excel 2013:

1.  Add a new Workbook.
2.  Click in the workbook where you want to insert the chart, click the "Insert" tab, and then click "Insert Scatter Chart Icon" in the charts group.
3.  A drop-down with charts will appear, select the "Scatter" and press "OK" to insert the chart.
4.  Click on the chart you just inserted, then click the "Change Data" icon in Data group.
5.  Now add legend entries. See [Chart Data]({{< ref "assembly/python-net/developer-guide/advanced-usage/working-with-chart-reports-scatter/scatter-chart-in-spreadsheet-document.md#adding-syntax-to-be-evaluated-by-groupdocsassembly-engine" >}}).
6.  Save your Document.

### Reporting Requirement

As a report developer, you are required to show your customers' orders prices by month with the following key requirements:

*   Report must show information on a Scatter Chart.
*   It must indicate Price of each order by month.
*   Report must be generated in the Spreadsheet Document.

### Adding Syntax to be evaluated by GroupDocs.Assembly Engine

#### Chart Title

```text
Total Order Prices by Months<<foreach [in orders
.GroupBy(c => c.OrderDate.Month)]>>
```

#### Chart Data

**Legend Entries**

```text
="Total Order Price<<x [Key]>><<y [Sum(c => c.Price)]>>"
```

{{< alert style="success" >}}For detailed technical information about syntax, expressions and report generation by the engine, please visit: [Working with GroupDocs.Assembly Engine]({{< ref "assembly/python-net/developer-guide/basic-usage/working-with-groupdocs.assembly-engine/_index.md" >}}).{{< /alert >}}

### Download Scatter Chart Template

Please download the sample Scatter Chart document we created in this article:

*   [scatter-chart.xlsx](/assembly/python-net/_sample_files/developer-guide/advanced-usage/working-with-chart-reports-scatter/scatter-chart-in-spreadsheet-document/scatter-chart.xlsx)

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
assembler.assemble_document("scatter-chart.xlsx", "scatter-chart-report.xlsx", DataSourceInfo(orders, "orders"))
```
{{< /tab >}}
{{< tab "scatter-chart.xlsx" >}}
{{< tab-text >}}
The following sample file is used in this example: [scatter-chart.xlsx](/assembly/python-net/_sample_files/developer-guide/advanced-usage/working-with-chart-reports-scatter/scatter-chart-in-spreadsheet-document/scatter-chart.xlsx)
{{< /tab-text >}}
{{< /tab >}}
{{< tab "orders.json" >}}
{{< tab-text >}}
The following sample file is used in this example: [orders.json](/assembly/python-net/_sample_files/developer-guide/advanced-usage/working-with-chart-reports-scatter/scatter-chart-in-spreadsheet-document/orders.json)
{{< /tab-text >}}
{{< /tab >}}
{{< tab "scatter-chart-report.xlsx" >}}  
```text
Binary file (XLSX, 13 KB)
```
[Download full output](/assembly/python-net/_output_files/developer-guide/advanced-usage/working-with-chart-reports-scatter/scatter-chart-in-spreadsheet-document/generating_the_report/scatter-chart-report.xlsx)
{{< /tab >}}
{{< /tabs >}}

## Scatter Chart in OpenOffice Spreadsheet Document

To be investigated.
