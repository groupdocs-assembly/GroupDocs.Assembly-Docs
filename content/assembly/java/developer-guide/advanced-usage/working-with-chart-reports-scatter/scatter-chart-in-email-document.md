---
id: scatter-chart-in-email-document
url: assembly/java/scatter-chart-in-email-document
title: Scatter Chart in Email Document
weight: 4
description: ""
keywords: 
productName: GroupDocs.Assembly for Java
hideChildren: False
---
{{< alert style="info" >}}In this article, we will use GroupDocs.Assembly to generate a Scatter Chart report in Email Document format.{{< /alert >}}

## Scatter Chart in Microsoft PowerPoint Document

### Creating a Scatter Chart

Please following below steps to create Scatter Chart in MS Outlook 2013:

1.  Create a new Email.
2.  Click in the email where you want to insert the chart, click the "Insert" tab, and then click "Chart" in the illustrations group to open the "Insert Chart" dialog box.
3.  Select "XY (Scatter)".
4.  Preview "Scatter" and press OK to insert the chart and Worksheet template to your email.
5.  Edit the Worksheet with your data to update the chart.
6.  Save the template.

### Reporting Requirement

As a report developer, you are required to show contract prices by month with the following key requirements:

*   Report must be in .eml or .msg format.
*   It must add email recipient, css and subject of the email.
*   Report must show information on a Scatter Chart.
*   It must indicate total contract prices by month.

### Adding Syntax to be evaluated by GroupDocs.Assembly Engine

#### Chart Title

```java
Total Contract Prices by Months<<foreach [in getContracts()
.groupBy(c => c.getDate().getMonth())]>>
```

#### Chart Data (Email)

| X-Values | Total Contract Price<<x [key + 1]>><<y [sum(c => c.getPrice())]>> |
| -------- | ------------------------------------------------------------ |
| 0.7      | 2.7                                                          |
| 1.8      | 3.2                                                          |
| 2.6      | 0.8                                                          |

### Download Scatter Chart Template

Please download the sample Scatter Chart document we created in this article:

*   [Scatter Chart.eml](https://raw.githubusercontent.com/groupdocs-assembly/GroupDocs.Assembly-for-Java/master/Examples/GroupDocs.Assembly.Examples.Java/Data/Storage/Email%20Templates/Bulleted%20List.eml?raw=true)

### Generating The Report

{{< alert style="info" >}}The code uses some of the objects defined in: [The Business Layer](https://docs.groupdocs.com/assembly/java/the-business-layer/){{< /alert >}}{{< gist samicheemagroupdocs 0127601c204a7ff3449fd2dae98eb7d6 >}}


