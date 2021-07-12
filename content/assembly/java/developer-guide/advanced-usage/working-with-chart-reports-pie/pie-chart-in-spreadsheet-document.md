---
id: pie-chart-in-spreadsheet-document
url: assembly/java/pie-chart-in-spreadsheet-document
title: Pie Chart in Spreadsheet Document
weight: 2
description: ""
keywords: 
productName: GroupDocs.Assembly for Java
hideChildren: False
---
{{< alert style="info" >}}In this article, we will use GroupDocs.Assembly to generate a Pie Chart report in Spreadsheet Document format.{{< /alert >}}{{< alert style="info" >}}The code uses some of the objects defined in [The Business Layer](https://docs.groupdocs.com/assembly/java/the-business-layer/).{{< /alert >}}

## Pie Chart in Microsoft Excel Document

### Creating a Pie Chart

Please follow below steps to create Pie Chart in MS Excel 2013.

1.  Add a new Workbook.
2.  Click in the workbook where you want to insert the chart, click the "Insert" tab, and then click "Pie Chart Icon" in the charts group.
3.  A drop-down with charts will appear, select the "Pie" and press "OK" to insert the chart.
4.  Click on the chart you just inserted, then click the "Change Data" icon in Data group.
5.  Now add legend entries. See [Chart Data](https://docs.groupdocs.com/assembly/java/pie-chart-in-spreadsheet-document/#adding-syntax-to-be-evaluated-by-groupdocsassembly-engine).
6.  Save your Document.

### Reporting Requirement

As a report developer, you are required to share managers' contract prices dynamically with the following key requirements:

*   Report must show information on a Pie Chart.
*   It must indicate manager name with value (price of the contract).
*   Report must be generated in the Spreadsheet Document.

### Adding Syntax to be evaluated by GroupDocs.Assembly Engine

#### Chart Title

```java
Total Contract Price<<foreach [in getManagers()]>><<x [getName()]>>
```

#### Chart Data

**Legend Entries**

```java
="Total Contract Price<<y [getContracts().sum(c => c.getPrice())]>>"
```

### Download Pie Chart Template

Please download the sample Pie Chart document we created in this article:

*   [Pie Chart.xlsx](https://github.com/groupdocs-assembly/GroupDocs.Assembly-for-Java/blob/master/Examples/GroupDocs.Assembly.Examples.Java/Data/Storage/Spreadsheet%20Templates/Pie%20Chart.xlsx?raw=true)

### Generating The Report

{{< gist GroupDocsGists a8997c78d41078faf2b39601411357b8 >}}

## Pie Chart in OpenOffice Spreadsheet Document

To be investigated.
