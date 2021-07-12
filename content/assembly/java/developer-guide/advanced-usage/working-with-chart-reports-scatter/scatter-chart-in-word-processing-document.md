---
id: scatter-chart-in-word-processing-document
url: assembly/java/scatter-chart-in-word-processing-document
title: Scatter Chart in Word Processing Document
weight: 1
description: ""
keywords: 
productName: GroupDocs.Assembly for Java
hideChildren: False
---
{{< alert style="info" >}}In this article, we will use GroupDocs.Assembly to generate a Scatter Chart report in Word Processing Document format.{{< /alert >}}{{< alert style="info" >}}The code uses some of the objects defined in [The Business Layer](https://docs.groupdocs.com/assembly/java/the-business-layer/).{{< /alert >}}

## Scatter Chart in Microsoft Word Document

### Creating a Scatter Chart

Please follow below to create Scatter Chart in MS Word 2013:

1.  Click in the document where you want to insert the chart, click the "Insert" tab, and then click "Chart" in the illustrations group to open the "Insert Chart" dialog box.
2.  Select "XY (Scatter)".
3.  Preview "Scatter" and press OK to insert the chart and Worksheet template to your document.
4.  Edit the Worksheet with your data to update the chart. See [Chart Data (Excel)](https://docs.groupdocs.com/assembly/java/scatter-chart-in-word-processing-document/#adding-syntax-to-be-evaluated-by-groupdocsassembly-engine).
5.  Save the template.

### Reporting Requirement

As a report developer, you are required to show contract prices by month with the following key requirements:

*   Report must show information on a Scatter Chart.
*   It must indicate total contract prices by month.
*   Report must be generated in the Word Processing Document.

### Adding Syntax to be evaluated by GroupDocs.Assembly Engine

#### Chart Title

```java
Total Contract Prices by Months<<foreach [in getContracts()
.groupBy(c => c.getDate().getMonth())]>>
```

#### Chart Data (Excel)

| X-Values | Total Contract Price<<x [key + 1]>><<y [sum(c => c.getPrice())]>> |
| -------- | ------------------------------------------------------------ |
| 0.7      | 2.7                                                          |
| 1.8      | 3.2                                                          |
| 2.6      | 0.8                                                          |

### Download Scatter Chart Template

Please download the sample Scatter Chart document we created in this article:

*   [Scatter Chart.docx](https://github.com/groupdocs-assembly/GroupDocs.Assembly-for-Java/blob/master/Examples/GroupDocs.Assembly.Examples.Java/Data/Storage/Word%20Templates/Scatter%20Chart.docx?raw=true)

### Generating The Report

{{< gist GroupDocsGists 2b9e00fd18299d0e72191eb34c3747ec >}}

## Scatter Chart in OpenOffice Document

To be investigated.
