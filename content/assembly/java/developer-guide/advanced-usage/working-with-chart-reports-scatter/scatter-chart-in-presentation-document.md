---
id: scatter-chart-in-presentation-document
url: assembly/java/scatter-chart-in-presentation-document
title: Scatter Chart in Presentation Document
weight: 3
description: ""
keywords: 
productName: GroupDocs.Assembly for Java
hideChildren: False
---
{{< alert style="info" >}}In this article, we will use GroupDocs.Assembly to generate a Scatter Chart report in Presentation Document format.{{< /alert >}}{{< alert style="info" >}}The code uses some of the objects defined in [The Business Layer](https://docs.groupdocs.com/assembly/java/the-business-layer/).{{< /alert >}}

## Scatter Chart in Microsoft PowerPoint Document

### Creating a Scatter Chart

Please following below steps to create Scatter Chart in MS PowerPoint 2013:

1.  Click in the document where you want to insert the chart, click the "Insert" tab, and then click "Chart" in the illustrations group to open the "Insert Chart" dialog box.
2.  Select "XY (Scatter)".
3.  Preview "Scatter" and press OK to insert the chart and Worksheet template to your document.
4.  Edit the Worksheet with your data to update the chart. See [Chart Data (Excel)](https://docs.groupdocs.com/assembly/java/scatter-chart-in-presentation-document/#adding-syntax-to-be-evaluated-by-groupdocsassembly-engine).
5.  Save the template.

### Reporting Requirement

As a report developer, you are required to show contract prices by month with the following key requirements:

*   Report must show information on a Scatter Chart.
*   It must indicate total contract prices by month.
*   Report must be generated in the Presentation Document.

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

*   [Scatter Chart.pptx](https://github.com/groupdocs-assembly/GroupDocs.Assembly-for-Java/blob/master/Examples/GroupDocs.Assembly.Examples.Java/Data/Storage/Presentation%20Templates/Scatter%20Chart.pptx?raw=true)

### Generating The Report

{{< gist GroupDocsGists 12dbe91a8a8ad4f7e05521faa308c512 >}}

## Scatter Chart in OpenOffice Presentation Document

To be investigated.
