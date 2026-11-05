---
id: chart-series-coloring-in-spreadsheet-document
url: assembly/python-net/chart-series-coloring-in-spreadsheet-document
title: Chart Series Coloring in Spreadsheet Document
weight: 3
description: "Chart Series Coloring in Spreadsheet Document with GroupDocs.Assembly for Python via .NET: the template, the Python data and the code."
keywords: chart series coloring in spreadsheet document, GroupDocs.Assembly, Python, report generation
productName: GroupDocs.Assembly for Python via .NET
hideChildren: False
---
{{< alert style="info" >}}The example reads the shop data described in [The Business Layer]({{< ref "assembly/python-net/developer-guide/basic-usage/working-with-a-business-case/the-business-layer.md" >}}).{{< /alert >}}

## Chart Series Coloring in Spreadsheet Document 

### Creating a Column Chart

Practising the following steps, you can insert a Column Chart in  MS Excel 2013:

1.  Create a new Workbook.
2.  Click the "Insert" tab, and then click "Insert Column Chart" icon in the Charts group to view the drop-down list.
3.  Select the "100% Stacked Column" and press "OK" to insert the chart and Worksheet template to your Worksheet.
4.  Edit the Worksheet with your data to update the chart. See [Chart Data]({{< ref "assembly/python-net/developer-guide/advanced-usage/working-with-chart-series-coloring/chart-series-coloring-in-spreadsheet-document.md#adding-syntax-to-be-evaluated-by-groupdocsassembly-engine" >}}).
5.  Save your Document.

### Reporting Requirement

As a report developer, you are required to share contract price by manager dynamically with the following key requirements:

*   The report must show the  name of the manager
*   The report must show the total contract price for each manager 
*   Series color to be used in chart series 
*   The report must be generated in the Spreadsheet Document

### Adding Syntax to be evaluated by GroupDocs.Assembly Engine

#### Chart Title

```text
<Total Contract Prices by Managers<<foreach [m in
managers]>><<x [m.Manager]>>
```

#### Legend Entries

```text
="Total Contract Price<<y [m.Total_Contract_Price]>><<seriesColor [color]>>"
```

{{< alert style="success" >}}For detailed technical information about syntax, expressions and report generation by the engine, please visit: [Working with GroupDocs.Assembly Engine]({{< ref "assembly/python-net/developer-guide/basic-usage/working-with-groupdocs.assembly-engine/_index.md" >}}){{< /alert >}}

### Download Template

Please download the sample Dynamic Chart Series Color document we created in this article:

*   [dynamic-chart-series-color.xlsx](/assembly/python-net/_sample_files/developer-guide/advanced-usage/working-with-chart-series-coloring/chart-series-coloring-in-spreadsheet-document/dynamic-chart-series-color.xlsx)

### Generating The Report

For a chart with dynamic data, you can set colors of chart series dynamically based upon expressions. To use the feature, do the following steps:

*   Declare a chart with dynamic data in the usual way
*   For chart series to be colored dynamically, define corresponding color expressions in names of these series using **seriesColor** tags having the following syntax:
  
    ```text
    <<seriesColor [color_expression]>>
    ```
    

A color expression must return a value of one of the following types:

*   A string containing the name of a known color, that is, the case-insensitive name of a member of the [KnownColor](https://msdn.microsoft.com/en-us/library/system.drawing.knowncolor(v=vs.110).aspx) enumeration such as "red"
*   An integer value defining RGB (red, green, blue) components of the color such as 0xFFFF00 (yellow)
*   A value of the [Color](http://msdn.microsoft.com/en-us/library/system.drawing.color(v=vs.110).aspx) type

Following code snippet generates the report:

{{< tabs "example1" >}}
{{< tab "Python" >}}
```python
from groupdocs.assembly import DataSourceInfo, DocumentAssembler
from groupdocs.assembly.data import DocumentTable, DocumentTableOptions

options = DocumentTableOptions()
options.first_row_contains_column_names = True
table = DocumentTable("managers.docx", 1, options)
table.columns["Total_Contract_Price"].type = float

assembler = DocumentAssembler()
assembler.assemble_document("dynamic-chart-series-color.xlsx", "dynamic-chart-series-color-report.xlsx", [
    DataSourceInfo(table, "managers"),
    DataSourceInfo("Coral", "color"),
])
```
{{< /tab >}}
{{< tab "dynamic-chart-series-color.xlsx" >}}
{{< tab-text >}}
The following sample file is used in this example: [dynamic-chart-series-color.xlsx](/assembly/python-net/_sample_files/developer-guide/advanced-usage/working-with-chart-series-coloring/chart-series-coloring-in-spreadsheet-document/dynamic-chart-series-color.xlsx)
{{< /tab-text >}}
{{< /tab >}}
{{< tab "managers.docx" >}}
{{< tab-text >}}
The following sample file is used in this example: [managers.docx](/assembly/python-net/_sample_files/developer-guide/advanced-usage/working-with-chart-series-coloring/chart-series-coloring-in-spreadsheet-document/managers.docx)
{{< /tab-text >}}
{{< /tab >}}
{{< tab "dynamic-chart-series-color-report.xlsx" >}}  
```text
Binary file (XLSX, 13 KB)
```
[Download full output](/assembly/python-net/_output_files/developer-guide/advanced-usage/working-with-chart-series-coloring/chart-series-coloring-in-spreadsheet-document/generating_the_report/dynamic-chart-series-color-report.xlsx)
{{< /tab >}}
{{< /tabs >}}
