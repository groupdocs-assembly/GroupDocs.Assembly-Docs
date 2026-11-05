---
id: chart-series-coloring-in-email-document
url: assembly/python-net/chart-series-coloring-in-email-document
title: Chart Series Coloring in Email Document
weight: 4
description: "Chart Series Coloring in Email Document with GroupDocs.Assembly for Python via .NET: the template, the Python data and the code."
keywords: chart series coloring in email document, GroupDocs.Assembly, Python, report generation
productName: GroupDocs.Assembly for Python via .NET
hideChildren: False
---
{{< alert style="info" >}}The example reads the shop data described in [The Business Layer]({{< ref "assembly/python-net/developer-guide/basic-usage/working-with-a-business-case/the-business-layer.md" >}}).{{< /alert >}}

## Chart Series Coloring in Email Document

### Creating a Column Chart

Please follow below steps to create a column chart in MS Outlook 2013:

1.  Create a new Email
2.  Click the "Insert" tab, and then click "Chart" in the illustrations group to open the "Insert Chart" dialog box
3.  Select "Column" in the sidebar, you will see a gallery of charts
4.  Select the "100% Stacked Column" and press "OK" to insert the chart and Worksheet template to your email
5.  Edit the Worksheet with your data to update the chart
6.  Save your Email

### Reporting Requirement

As a report developer, you are required to share contract price by manager dynamically with the following key requirements:

*   The report must show the  name of the manager
*   The report must show the total contract price for each manager 
*   Series color to be used in chart series 
*   The Report must be generated in the Email Document

### Adding Syntax to be evaluated by GroupDocs.Assembly Engine

#### Chart Title

```text
<Total Contract Prices by Managers<<foreach [m in
managers]>><<x [m.Manager]>>
```

#### Chart Data (Excel)

|   | Total Contract Price<<y [m.Total_Contract_Price]>><<seriesColor [color]>> |
| --- | --- |
| Category 1 | 4.3 |
| Category 2 | 2.5 |
| Category 3 | 3.5 |
| Category 4 | 4.5 |

{{< alert style="success" >}}For detailed technical information about syntax, expressions and report generation by the engine, please visit: [Working with GroupDocs.Assembly Engine]({{< ref "assembly/python-net/developer-guide/basic-usage/working-with-groupdocs.assembly-engine/_index.md" >}}){{< /alert >}}

### Download Template

Please download the sample Dynamic Chart Series Color document we created in this article:

*   [dynamic-chart-series-color.msg](/assembly/python-net/_sample_files/developer-guide/advanced-usage/working-with-chart-series-coloring/chart-series-coloring-in-email-document/dynamic-chart-series-color.msg)

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
assembler.assemble_document("dynamic-chart-series-color.msg", "dynamic-chart-series-color-report.msg", [
    DataSourceInfo(table, "managers"),
    DataSourceInfo("Coral", "color"),
    DataSourceInfo("Harbor Lane Provisions <orders@harborlane.example>", "sender"),
    DataSourceInfo(["Quayside Bistro <orders@quaysidebistro.example>", "jonas.weber@harborlane.example"], "recipients"),
    DataSourceInfo("amara.osei@harborlane.example", "cc"),
    DataSourceInfo("Dynamic chart series color", "subject"),
])
```
{{< /tab >}}
{{< tab "dynamic-chart-series-color.msg" >}}
{{< tab-text >}}
The following sample file is used in this example: [dynamic-chart-series-color.msg](/assembly/python-net/_sample_files/developer-guide/advanced-usage/working-with-chart-series-coloring/chart-series-coloring-in-email-document/dynamic-chart-series-color.msg)
{{< /tab-text >}}
{{< /tab >}}
{{< tab "managers.docx" >}}
{{< tab-text >}}
The following sample file is used in this example: [managers.docx](/assembly/python-net/_sample_files/developer-guide/advanced-usage/working-with-chart-series-coloring/chart-series-coloring-in-email-document/managers.docx)
{{< /tab-text >}}
{{< /tab >}}
{{< tab "dynamic-chart-series-color-report.msg" >}}  
```text
Binary file (MSG, 40 KB)
```
[Download full output](/assembly/python-net/_output_files/developer-guide/advanced-usage/working-with-chart-series-coloring/chart-series-coloring-in-email-document/generating_the_report/dynamic-chart-series-color-report.msg)
{{< /tab >}}
{{< /tabs >}}
