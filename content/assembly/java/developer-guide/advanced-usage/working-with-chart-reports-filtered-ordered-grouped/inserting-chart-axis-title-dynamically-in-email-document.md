---
id: inserting-chart-axis-title-dynamically-in-email-document
url: assembly/java/inserting-chart-axis-title-dynamically-in-email-document
title: Inserting Chart Axis Title Dynamically in Email Document
weight: 9
description: ""
keywords: 
productName: GroupDocs.Assembly for Java
hideChildren: False
---
{{< alert style="info" >}}This feature is supported by version 18.1 or greater{{< /alert >}}{{< alert style="info" >}}The code uses some of the objects defined in [The Business Layer](https://docs.groupdocs.com/assembly/java/the-business-layer/).{{< /alert >}}

## Column Chart in Email Document

### Creating a Column Chart

Please follow below steps to create a column chart in MS Outlook 2013:

1.  Create a new Email
2.  Click the "Insert" tab, and then click "Chart" in the illustrations group to open the "Insert Chart" dialogue box
3.  Select "Column" in the sidebar, you will see a gallery of charts
4.  Select the "100% Stacked Column" and press "OK" to insert the chart and Worksheet template to your email
5.  Edit the Worksheet with your data to update the chart
6.  Save your Email

### Reporting Requirement

As a report developer, you are required to share orders quantity of the customers dynamically with the following key requirements:

*   A report must be in .eml or .msg format
*   It must add email recipient, CSS and subject of the email
*   Report must show total Order Quantity by Quarters

### Adding Syntax to be evaluated by GroupDocs.Assembly Engine

#### Chart Title

```java
<<[title]>><<foreach [in getContracts()
.where(c => c.getDate().getYear() + 1900 == 2015)
.groupBy(c => c.getManager())
.orderBy(g => g.key.getName())]>><<x [key.getName()]>>
```

#### Chart Data (Excel)

|            | 1st Quarter<<y [where(c => c.getDate().getMonth() >= 0 && c.getDate().getMonth() <= 2).sum(c => c.getPrice())]>> | 2nd Quarter<<y [where(c => c.getDate().getMonth() >= 3 && c.getDate().getMonth() <= 5).sum(c => c.getPrice())]>> | 3rd Quarter<<y [where(c => c.getDate().getMonth() >= 6 && c.getDate().getMonth() <= 8).sum(c => c.getPrice())]>> | 4th Quarter<<y [where(c => c.getDate().getMonth() >= 9 && c.getDate().getMonth() <= 11).sum(c => c.getPrice())]>> |
| ---------- | ------------------------------------------------------------ | ------------------------------------------------------------ | ------------------------------------------------------------ | ------------------------------------------------------------ |
| Category 1 | 4.3                                                          | 2.4                                                          | 2                                                            | 3                                                            |
| Category 2 | 2.5                                                          | 4.4                                                          | 2                                                            | 2                                                            |
| Category 3 | 3.5                                                          | 1.8                                                          | 3                                                            | 5                                                            |
| Category 4 | 4.5                                                          | 2.8                                                          | 5                                                            | 2                                                            |

### Download Template

Please download the sample Chart Template we created in this article:

*   [Chart Template.msg](https://github.com/groupdocs-assembly/GroupDocs.Assembly-for-Java/blob/master/Examples/GroupDocs.Assembly.Examples.Java/Data/Storage/Email%20Templates/Chart%20with%20Filtering%2C%20Grouping%2C%20and%20Ordering_Dynamic_Title.msg)

### Generating The Report

{{< gist GroupDocsGists 10096bac56029ef28eed87add3a237a0 >}}


