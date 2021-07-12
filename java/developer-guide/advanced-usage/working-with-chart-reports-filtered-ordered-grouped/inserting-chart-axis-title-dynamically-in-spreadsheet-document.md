---
id: inserting-chart-axis-title-dynamically-in-spreadsheet-document
url: assembly/java/inserting-chart-axis-title-dynamically-in-spreadsheet-document
title: Inserting Chart Axis Title Dynamically in Spreadsheet Document
weight: 7
description: ""
keywords: 
productName: GroupDocs.Assembly for Java
hideChildren: False
---
{{< alert style="info" >}}This feature is supported by version 18.1 or greater.{{< /alert >}}{{< alert style="info" >}}The code uses some of the objects defined in [The Business Layer](https://docs.groupdocs.com/assembly/java/the-business-layer/).{{< /alert >}}

## Column Chart in Microsoft Excel Document

### Creating a Column Chart

Following steps, you can create a column chart in MS Excel 2013:

1.  Create a new Workbook
2.  Click the "Insert" tab, and then click "Insert Column Chart" icon in the Charts group to view the drop-down list
3.  Select the "100% Stacked Column" and press "OK" to insert the chart and Worksheet template to your Worksheet
4.  Edit the Worksheet with your data to update the chart
5.  Save your Document

### Reporting Requirement

As a report developer, you are required to share orders quantity of the customers dynamically with the following key requirements:

*   A report must show the quantity of sales/orders
*   Sales/orders quantity must be represented by Quarters
*   It must associate order quantity with the corresponding customer
*   A report must be generated in the Spreadsheet Document

### Adding Syntax to be Evaluated by GroupDocs.Assembly Engine

#### Chart Title

```java
<<[title]>><<foreach [in getContracts()
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

#### Download Template

Please download the sample Chart with Filtering, Grouping, and Ordering with Dynamic Title document we created in this article:

*   [Chart Template.xlsx](https://github.com/groupdocs-assembly/GroupDocs.Assembly-for-Java/blob/master/Examples/GroupDocs.Assembly.Examples.Java/Data/Storage/Spreadsheet%20Templates/Chart%20with%20Filtering%2C%20Grouping%2C%20and%20Ordering_Dynamic_Title.xlsx) (Template for CustomObject and JSON examples) 

### Generating The Report

{{< gist GroupDocsGists 2f73ae9a61cddc1c34067925ce1d0f1c >}}


