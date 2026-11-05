---
id: pie-chart-in-spreadsheet-document
url: assembly/python-net/pie-chart-in-spreadsheet-document
title: Pie Chart in Spreadsheet Document
weight: 2
description: "Pie Chart in Spreadsheet Document with GroupDocs.Assembly for Python via .NET: the template, the Python data and the code."
keywords: pie chart in spreadsheet document, GroupDocs.Assembly, Python, report generation
productName: GroupDocs.Assembly for Python via .NET
hideChildren: False
---
{{< alert style="info" >}}In this article, we will use GroupDocs.Assembly to generate a Pie Chart report in Spreadsheet Document format based on the use case: [Working with a Business Case]({{< ref "assembly/python-net/developer-guide/basic-usage/working-with-a-business-case/_index.md" >}}).{{< /alert >}}{{< alert style="info" >}}The example reads the shop data described in [The Business Layer]({{< ref "assembly/python-net/developer-guide/basic-usage/working-with-a-business-case/the-business-layer.md" >}}).{{< /alert >}}

## Pie Chart in Microsoft Excel Document

### Creating a Pie Chart

Please follow below steps to create Pie Chart in MS Excel 2013.

1.  Add a new Workbook.
2.  Click in the workbook where you want to insert the chart, click the "Insert" tab, and then click "Pie Chart Icon" in the charts group.
3.  A drop-down with charts will appear, select the "Pie" and press "OK" to insert the chart.
4.  Click on the chart you just inserted, then click the "Change Data" icon in Data group.
5.  Now add legend entries. See [Chart Data]({{< ref "assembly/python-net/developer-guide/advanced-usage/working-with-chart-reports-pie/pie-chart-in-spreadsheet-document.md#adding-syntax-to-be-evaluated-by-groupdocsassembly-engine" >}})
6.  Save your Document.

### Reporting Requirement

As a report developer, you are required to share your customers' orders details dynamically with the following key requirements:

*   The report must show information on a Pie Chart.
*   It must indicate customer name with value (price of the orders purchased).
*   The report must be generated in the Spreadsheet Document.

### Adding Syntax to be evaluated by GroupDocs.Assembly Engine

#### Chart Title

```text
Total Order Price<<foreach [in customers]>>
<<x [CustomerName]>>
```

#### Chart Data

**Legend Entries**

```text
="Total Order Price<<y [Order.Sum(c => c.Price)]>>"
```

{{< alert style="success" >}}For detailed technical information about syntax, expressions and report generation by the engine, please visit: [Working with GroupDocs.Assembly Engine]({{< ref "assembly/python-net/developer-guide/basic-usage/working-with-groupdocs.assembly-engine/_index.md" >}}).{{< /alert >}}

### Download Pie Chart Template

Please download the sample Pie Chart document we created in this article:

*   [pie-chart.xlsx](/assembly/python-net/_sample_files/developer-guide/advanced-usage/working-with-chart-reports-pie/pie-chart-in-spreadsheet-document/pie-chart.xlsx)

### Generating The Report

{{< tabs "example1" >}}
{{< tab "Python" >}}
```python
import json

from groupdocs.assembly import DataSourceInfo, DocumentAssembler

with open("customers.json", encoding="utf-8") as f:
    customers = json.load(f)

assembler = DocumentAssembler()
assembler.assemble_document("pie-chart.xlsx", "pie-chart-report.xlsx", DataSourceInfo(customers, "customers"))
```
{{< /tab >}}
{{< tab "pie-chart.xlsx" >}}
{{< tab-text >}}
The following sample file is used in this example: [pie-chart.xlsx](/assembly/python-net/_sample_files/developer-guide/advanced-usage/working-with-chart-reports-pie/pie-chart-in-spreadsheet-document/pie-chart.xlsx)
{{< /tab-text >}}
{{< /tab >}}
{{< tab "customers.json" >}}
{{< tab-text >}}
The following sample file is used in this example: [customers.json](/assembly/python-net/_sample_files/developer-guide/advanced-usage/working-with-chart-reports-pie/pie-chart-in-spreadsheet-document/customers.json)
{{< /tab-text >}}
{{< /tab >}}
{{< tab "pie-chart-report.xlsx" >}}  
```text
Binary file (XLSX, 12 KB)
```
[Download full output](/assembly/python-net/_output_files/developer-guide/advanced-usage/working-with-chart-reports-pie/pie-chart-in-spreadsheet-document/generating_the_report/pie-chart-report.xlsx)
{{< /tab >}}
{{< /tabs >}}

## Pie Chart in OpenOffice Spreadsheet Document

To be investigated.
