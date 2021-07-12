---
id: scatter-chart-in-spreadsheet-document
url: assembly/java/scatter-chart-in-spreadsheet-document
title: Scatter Chart in Spreadsheet Document
weight: 2
description: ""
keywords: 
productName: GroupDocs.Assembly for Java
hideChildren: False
---
{{< alert style="info" >}}In this article, we will use GroupDocs.Assembly to generate a Scatter Chart report in Spreadsheet Document format.{{< /alert >}}{{< alert style="info" >}}The code uses some of the objects defined in [The Business Layer](https://docs.groupdocs.com/assembly/java/the-business-layer/).{{< /alert >}}

## Scatter Chart in Microsoft Excel Document

### Creating a Scatter Chart

Please follow below steps to create Scatter Chart in MS Excel 2013:

1.  Add a new Workbook.
2.  Click in the workbook where you want to insert the chart, click the "Insert" tab, and then click "Insert Scatter Chart Icon" in the charts group.
3.  A drop-down with charts will appear, select the "Scatter" and press "OK" to insert the chart.
4.  Click on the chart you just inserted, then click the "Change Data" icon in Data group.
5.  Now add legend entries. See [Chart Data](https://docs.groupdocs.com/assembly/java/scatter-chart-in-spreadsheet-document/#adding-syntax-to-be-evaluated-by-groupdocsassembly-engine).
6.  Save your Document.

### Reporting Requirement

As a report developer, you are required to show contract prices by month with the following key requirements:

*   Report must show information on a Scatter Chart.
*   It must indicate total contract prices by month.
*   Report must be generated in the Spreadsheet Document.

### Adding Syntax to be evaluated by GroupDocs.Assembly Engine

#### Chart Title

```java
Total Contract Prices by Months<<foreach [in getContracts()
.groupBy(c => c.getDate().getMonth())]>>
```

#### Chart Data

**Legend Entries**

```java
="Total Contract Price<<x [key + 1]>><<y [sum(c => c.getPrice())]>>"
```

### Download Scatter Chart Template

Please download the sample Scatter Chart document we created in this article:

*   [Scatter Chart.xlsx](https://github.com/groupdocs-assembly/GroupDocs.Assembly-for-Java/blob/master/Examples/GroupDocs.Assembly.Examples.Java/Data/Storage/Spreadsheet%20Templates/Scatter%20Chart.xlsx?raw=true)

### Generating The Report

{{< gist GroupDocsGists 9f23eb8da0d619df8b7c873b6bbd482c >}}

## Scatter Chart in OpenOffice Spreadsheet Document

To be investigated.
