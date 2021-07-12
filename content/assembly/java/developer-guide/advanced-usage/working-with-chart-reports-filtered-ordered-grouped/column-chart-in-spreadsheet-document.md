---
id: column-chart-in-spreadsheet-document
url: assembly/java/column-chart-in-spreadsheet-document
title: Column Chart in Spreadsheet Document
weight: 2
description: ""
keywords: 
productName: GroupDocs.Assembly for Java
hideChildren: False
---
{{< alert style="info" >}}In this article, we will use GroupDocs.Assembly to generate a Column Chart Report with Filtered, Ordered and Grouped Data in Spreadsheet Document format.{{< /alert >}}{{< alert style="info" >}}The code uses some of the objects defined in [The Business Layer](https://docs.groupdocs.com/assembly/java/the-business-layer/).{{< /alert >}}

## Column Chart in Microsoft Excel Document

### Creating a Column Chart

Following below steps, you can create column chart in MS Excel 2013:

1.  Create a new Workbook.
2.  Click the "Insert" tab, and then click "Insert Column Chart" icon in the Charts group to view the drop-down list.
3.  Select the "100% Stacked Column" and press "OK" to insert the chart and Worksheet template to your Worksheet.
4.  Edit the Worksheet with your data to update the chart. See [Chart Data](https://docs.groupdocs.com/assembly/java/column-chart-in-spreadsheet-document/#adding-syntax-to-be-evaluated-by-groupdocsassembly-engine).
5.  Save your Document.

### Reporting Requirement

As a report developer, you are required to share orders quantity of the customers dynamically with the following key requirements:

*   Report must show total Contract Prices by Quarters
*   Report must be generated in the Spreadsheet Document.

### Adding Syntax to be evaluated by GroupDocs.Assembly Engine

#### Chart Title

```java
Total Contract Prices by Quarters<<foreach [in getContracts()
.where(c => c.getDate().getYear() + 1900 == 2015)
.groupBy(c => c.getManager())
.orderBy(g => g.key.getName())]>><<x [key.getName()]>>
```

#### Chart Data

**Legend Entries**

```java
="1st Quarter<<y [where(c => c.getDate().getMonth() >= 0 && c.getDate().getMonth() <= 2).sum(c => c.getPrice())]>>"
="2nd Quarter<<y [where(c => c.getDate().getMonth() >= 3 && c.getDate().getMonth() <= 5).sum(c => c.getPrice())]>>"
="3rd Quarter<<y [where(c => c.getDate().getMonth() >= 6 && c.getDate().getMonth() <= 8).sum(c => c.getPrice())]>>"
="4th Quarter<<y [where(c => c.getDate().getMonth() >= 9 && c.getDate().getMonth() <= 11).sum(c => c.getPrice())]>>"
```

### Download Template

Please download the sample Chart with Filtering, Grouping, and Ordering document we created in this article:

*   [Chart Template.xlsx](https://github.com/groupdocs-assembly/GroupDocs.Assembly-for-Java/blob/master/Examples/GroupDocs.Assembly.Examples.Java/Data/Storage/Spreadsheet%20Templates/Chart%20with%20Filtering%2C%20Grouping%2C%20and%20Ordering.xlsx?raw=true)

### Generating The Report

{{< gist GroupDocsGists 90f1cfd555c77ca915ba4284903bc892 >}}

## Column Chart in OpenOffice Spreadsheet Document

To be investigated.
