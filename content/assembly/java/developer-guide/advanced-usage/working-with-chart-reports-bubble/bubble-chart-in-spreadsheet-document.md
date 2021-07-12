---
id: bubble-chart-in-spreadsheet-document
url: assembly/java/bubble-chart-in-spreadsheet-document
title: Bubble Chart in Spreadsheet Document
weight: 2
description: ""
keywords: 
productName: GroupDocs.Assembly for Java
hideChildren: False
---
{{< alert style="info" >}}In this article, we will use GroupDocs.Assembly to generate a Bubble Chart report in Spreadsheet Document format.{{< /alert >}}{{< alert style="info" >}}The code uses some of the objects defined in [The Business Layer](https://docs.groupdocs.com/assembly/java/the-business-layer/).{{< /alert >}}

## Bubble Chart in Microsoft Excel Document

### Creating a Bubble Chart

Please follow below steps to create a Bubble Chart in MS Excel 2013:

1.  Add a new Workbook.
2.  Click in the workbook where you want to insert the chart, click the "Insert" tab, and then click "Insert Scatter Chart Icon" in the charts group.
3.  A drop-down with charts will appear, select the "Bubble" and press "OK" to insert the chart.
4.  Click on the chart you just inserted, then click the "Select Data" icon in Data group.
5.  Add legend entries. See [Chart Data](https://docs.groupdocs.com/assembly/java/bubble-chart-in-spreadsheet-document/#reporting-requirement).
6.  Save your Document.

### Reporting Requirement

As a report developer, you are required to share your sales/orders dynamically with the following key requirements:

*   Retrieve total Contract Prices by Months.
*   Report must be generated in the Spreadsheet Document.

### Adding Syntax to be evaluated by GroupDocs.Assembly Engine

#### Chart Title

```java
Total Contract Prices by Months<<foreach [in getContracts()
.groupBy(c => c.getDate().getMonth())]>><<x [key + 1]>>
```

#### Chart Data

**Legend Entries**

```java
="Total Contract Price<<y [sum(c => c.getPrice())]>><<size [count()]>>"
```

### Download Bubble Chart Template

Please download the sample Bubble Chart document we created in this article:

*   [Bubble Chart.xlsx](https://github.com/groupdocs-assembly/GroupDocs.Assembly-for-Java/blob/master/Examples/GroupDocs.Assembly.Examples.Java/Data/Storage/Spreadsheet%20Templates/Bubble%20Chart.xlsx?raw=true)

### Generating The Report

{{< gist GroupDocsGists 1b76dbc560b5792fec4d6e809896f7d9 >}}

## Bubble Chart in OpenOffice Spreadsheet Document

To be investigated.
