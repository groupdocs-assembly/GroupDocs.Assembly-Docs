---
id: chart-series-coloring-in-spreadsheet-document
url: assembly/java/chart-series-coloring-in-spreadsheet-document
title: Chart Series Coloring in Spreadsheet Document
weight: 3
description: ""
keywords: 
productName: GroupDocs.Assembly for Java
hideChildren: False
---
{{< alert style="info" >}}This feature is supported by version 18.5 or greater.{{< /alert >}}{{< alert style="info" >}}The code uses some of the objects defined in [The Business Layer](https://docs.groupdocs.com/assembly/java/the-business-layer/).{{< /alert >}}

## Chart Series Coloring in Spreadsheet Document 

### Creating a Column Chart

Practising the following steps, you can insert a Column Chart in  MS Excel 2013:

1.  Create a new Workbook.
2.  Click the "Insert" tab, and then click "Insert Column Chart" icon in the Charts group to view the drop-down list.
3.  Select the "100% Stacked Column" and press "OK" to insert the chart and Worksheet template to your Worksheet.
4.  Edit the Worksheet with your data to update the chart. See [Chart Data](https://docs.groupdocs.com/assembly/java/chart-series-coloring-in-spreadsheet-document/#adding-syntax-to-be-evaluated-by-groupdocsassembly-engine).
5.  Save your Document.
  

### Reporting Requirement

As a report developer, you are required to share contract price by manager dynamically with the following key requirements:

*   The report must show the  name of the manager
*   The report must show the total contract price for each manager 
*   Series color to be used in chart series 
*   The report must be generated in the Spreadsheet Document

### Adding Syntax to be evaluated by GroupDocs.Assembly Engine

#### Chart Title

```java
<Total Contract Prices by Managers<<foreach [m in
managers]>><<x [m.Manager]>>
```

#### Legend Entries

```java
="Total Contract Price<<y [m.Total_Contract_Price]>><<seriesColor [color]>>"
```

{{< alert style="success" >}}For detailed technical information about syntax, expressions and report generation by the engine, please visit: [Working with GroupDocs.Assembly Engine](https://docs.groupdocs.com/assembly/java/working-with-groupdocs-assembly-engine/){{< /alert >}}

### Download Template

Please download the sample Dynamic Chart Series Color document we created in this article:

*   [Chart Template.xlsx](https://github.com/groupdocs-assembly/GroupDocs.Assembly-for-Java/blob/master/Examples/GroupDocs.Assembly.Examples.Java/Data/Storage/Spreadsheet%20Templates/Dynamic%20Chart%20Series%20Color.xlsx) (Template for CustomObject and JSON examples) 

### Generating The Report

For a chart with dynamic data, you can set colors of chart series dynamically based upon expressions. To use the feature, do the following steps:

*   Declare a chart with dynamic data in the usual way
*   For chart series to be colored dynamically, define corresponding color expressions in names of these series using **seriesColor** tags having the following syntax:
  
    ```java
    <<seriesColor [color_expression]>>
    ```
    

A color expression must return a value of one of the following types:

*   A string containing the name of a known color, that is, the case-insensitive name of a member of the [KnownColor](https://msdn.microsoft.com/en-us/library/system.drawing.knowncolor(v=vs.110).aspx) enumeration such as "red"
*   An integer value defining RGB (red, green, blue) components of the color such as 0xFFFF00 (yellow)
*   A value of the [Color](http://msdn.microsoft.com/en-us/library/system.drawing.color(v=vs.110).aspx) type

Following code snippet generates the report:

{{< gist GroupDocsGists e1c86f03ae3aff341f15c3e7d777b91d >}}


