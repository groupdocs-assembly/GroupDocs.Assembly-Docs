---
id: bubble-chart-in-word-processing-document
url: assembly/java/bubble-chart-in-word-processing-document
title: Bubble Chart in Word Processing Document
weight: 1
description: ""
keywords: 
productName: GroupDocs.Assembly for Java
hideChildren: False
---
{{< alert style="info" >}}In this article, we will use GroupDocs.Assembly to generate a Bubble Chart report in Word Processing Document format.{{< /alert >}}{{< alert style="info" >}}The code uses some of the objects defined in [The Business Layer](https://docs.groupdocs.com/assembly/java/the-business-layer/).{{< /alert >}}

## Bubble Chart in Microsoft Word Document

### Creating a Bubble Chart

Please follow below steps to create bubble chart in MS Word 2013:

1.  Click in the document where you want to insert the chart, click the "Insert" tab, and then click "Chart" in the illustrations group to open the "Insert Chart" dialog box.
2.  Select "X Y(Scatter)" in the sidebar, you will see a gallery of charts.
3.  Select the "Bubble" and press "OK" to insert the chart and Worksheet template to your document.
4.  Right click chart and select 'Edit Data' to provide chart data. See [Chart Data (Excel)](https://docs.groupdocs.com/assembly/java/bubble-chart-in-word-processing-document/#adding-syntax-to-be-evaluated-by-groupdocsassembly-engine).
5.  Save your Document.

### Reporting Requirement

As a report developer, you are required to share your sales/orders dynamically with the following key requirements:

*   Retrieve total Contract Prices by Months.
*   Report must be generated in the Word Processing Document.

### Adding Syntax to be evaluated by GroupDocs.Assembly Engine

#### Chart Title

```java
Total Contract Prices by Months<<foreach [in getContracts()
.groupBy(c => c.getDate().getMonth())]>><<x [key + 1]>>
```

#### Chart Data (Excel)

<table class="MsoTableGrid" border="1" cellspacing="0" cellpadding="0" width="623" style="width: 467.5pt; border-collapse: collapse; border-top-color: initial; border-top-style: none; border-top-width: initial; border-right-color: initial; border-right-style: none; border-right-width: initial; border-bottom-color: initial; border-bottom-style: none; border-bottom-width: initial; border-left-color: initial; border-left-style: none; border-left-width: initial;"><tbody><tr><td width="108" valign="top" style="width: 80.75pt; border-top-color: windowtext; border-top-style: solid; border-top-width: 1pt; border-right-color: windowtext; border-right-style: solid; border-right-width: 1pt; border-bottom-color: windowtext; border-bottom-style: solid; border-bottom-width: 1pt; border-left-color: windowtext; border-left-style: solid; border-left-width: 1pt; padding-top: 0in; padding-right: 5.4pt; padding-bottom: 0in; padding-left: 5.4pt;"><p class="MsoNormal" style="margin-bottom: 0.0001pt; line-height: normal;"><span style="color: black;">X-Values</span></p></td><td width="438" valign="top" style="width: 328.5pt; border-top-color: windowtext; border-top-style: solid; border-top-width: 1pt; border-right-color: windowtext; border-right-style: solid; border-right-width: 1pt; border-bottom-color: windowtext; border-bottom-style: solid; border-bottom-width: 1pt; border-left-color: initial; border-left-style: none; border-left-width: initial; padding-top: 0in; padding-right: 5.4pt; padding-bottom: 0in; padding-left: 5.4pt;"><p class="MsoNormal" style="margin-bottom: 0.0001pt; line-height: normal;"><span style="color: black;">Total Contract Price&lt;&lt;y [sum(c =&gt; c.getPrice())]&gt;&gt;&lt;&lt;size[count()]&gt;&gt;</span></p></td><td width="78" valign="top" style="width: 58.25pt; border-top-color: windowtext; border-top-style: solid; border-top-width: 1pt; border-right-color: windowtext; border-right-style: solid; border-right-width: 1pt; border-bottom-color: windowtext; border-bottom-style: solid; border-bottom-width: 1pt; border-left-color: initial; border-left-style: none; border-left-width: initial; padding-top: 0in; padding-right: 5.4pt; padding-bottom: 0in; padding-left: 5.4pt;"><p class="MsoNormal" style="margin-bottom: 0.0001pt; line-height: normal;"><span style="color: black;">Size</span></p></td></tr><tr><td width="108" valign="top" style="width: 80.75pt; border-top-color: initial; border-top-style: none; border-top-width: initial; border-right-color: windowtext; border-right-style: solid; border-right-width: 1pt; border-bottom-color: windowtext; border-bottom-style: solid; border-bottom-width: 1pt; border-left-color: windowtext; border-left-style: solid; border-left-width: 1pt; padding-top: 0in; padding-right: 5.4pt; padding-bottom: 0in; padding-left: 5.4pt;"><p class="MsoNormal" align="right" style="margin-bottom: 0.0001pt; text-align: right; line-height: normal;"><span style="color: black;">0.7</span></p></td><td width="438" valign="top" style="width: 328.5pt; border-top-color: initial; border-top-style: none; border-top-width: initial; border-left-color: initial; border-left-style: none; border-left-width: initial; border-bottom-color: windowtext; border-bottom-style: solid; border-bottom-width: 1pt; border-right-color: windowtext; border-right-style: solid; border-right-width: 1pt; padding-top: 0in; padding-right: 5.4pt; padding-bottom: 0in; padding-left: 5.4pt;"><p class="MsoNormal" align="right" style="margin-bottom: 0.0001pt; text-align: right; line-height: normal;"><span style="color: black;">2.7</span></p></td><td width="78" valign="top" style="width: 58.25pt; border-top-color: initial; border-top-style: none; border-top-width: initial; border-left-color: initial; border-left-style: none; border-left-width: initial; border-bottom-color: windowtext; border-bottom-style: solid; border-bottom-width: 1pt; border-right-color: windowtext; border-right-style: solid; border-right-width: 1pt; padding-top: 0in; padding-right: 5.4pt; padding-bottom: 0in; padding-left: 5.4pt;"><p class="MsoNormal" align="right" style="margin-bottom: 0.0001pt; text-align: right; line-height: normal;"><span style="color: black;">10</span></p></td></tr><tr><td width="108" valign="top" style="width: 80.75pt; border-top-color: initial; border-top-style: none; border-top-width: initial; border-right-color: windowtext; border-right-style: solid; border-right-width: 1pt; border-bottom-color: windowtext; border-bottom-style: solid; border-bottom-width: 1pt; border-left-color: windowtext; border-left-style: solid; border-left-width: 1pt; padding-top: 0in; padding-right: 5.4pt; padding-bottom: 0in; padding-left: 5.4pt;"><p class="MsoNormal" align="right" style="margin-bottom: 0.0001pt; text-align: right; line-height: normal;"><span style="color: black;">1.8</span></p></td><td width="438" valign="top" style="width: 328.5pt; border-top-color: initial; border-top-style: none; border-top-width: initial; border-left-color: initial; border-left-style: none; border-left-width: initial; border-bottom-color: windowtext; border-bottom-style: solid; border-bottom-width: 1pt; border-right-color: windowtext; border-right-style: solid; border-right-width: 1pt; padding-top: 0in; padding-right: 5.4pt; padding-bottom: 0in; padding-left: 5.4pt;"><p class="MsoNormal" align="right" style="margin-bottom: 0.0001pt; text-align: right; line-height: normal;"><span style="color: black;">3.2</span></p></td><td width="78" valign="top" style="width: 58.25pt; border-top-color: initial; border-top-style: none; border-top-width: initial; border-left-color: initial; border-left-style: none; border-left-width: initial; border-bottom-color: windowtext; border-bottom-style: solid; border-bottom-width: 1pt; border-right-color: windowtext; border-right-style: solid; border-right-width: 1pt; padding-top: 0in; padding-right: 5.4pt; padding-bottom: 0in; padding-left: 5.4pt;"><p class="MsoNormal" align="right" style="margin-bottom: 0.0001pt; text-align: right; line-height: normal;"><span style="color: black;">4</span></p></td></tr><tr><td width="108" valign="top" style="width: 80.75pt; border-top-color: initial; border-top-style: none; border-top-width: initial; border-right-color: windowtext; border-right-style: solid; border-right-width: 1pt; border-bottom-color: windowtext; border-bottom-style: solid; border-bottom-width: 1pt; border-left-color: windowtext; border-left-style: solid; border-left-width: 1pt; padding-top: 0in; padding-right: 5.4pt; padding-bottom: 0in; padding-left: 5.4pt;"><p class="MsoNormal" align="right" style="margin-bottom: 0.0001pt; text-align: right; line-height: normal;"><span style="color: black;">2.6</span></p></td><td width="438" valign="top" style="width: 328.5pt; border-top-color: initial; border-top-style: none; border-top-width: initial; border-left-color: initial; border-left-style: none; border-left-width: initial; border-bottom-color: windowtext; border-bottom-style: solid; border-bottom-width: 1pt; border-right-color: windowtext; border-right-style: solid; border-right-width: 1pt; padding-top: 0in; padding-right: 5.4pt; padding-bottom: 0in; padding-left: 5.4pt;"><p class="MsoNormal" align="right" style="margin-bottom: 0.0001pt; text-align: right; line-height: normal;"><span style="color: black;">0.8</span></p></td><td width="78" valign="top" style="width: 58.25pt; border-top-color: initial; border-top-style: none; border-top-width: initial; border-left-color: initial; border-left-style: none; border-left-width: initial; border-bottom-color: windowtext; border-bottom-style: solid; border-bottom-width: 1pt; border-right-color: windowtext; border-right-style: solid; border-right-width: 1pt; padding-top: 0in; padding-right: 5.4pt; padding-bottom: 0in; padding-left: 5.4pt;"><p class="MsoNormal" align="right" style="margin-bottom: 0.0001pt; text-align: right; line-height: normal;"><span style="color: black;">8</span></p></td></tr></tbody></table>
### Download Bubble Chart Template

Please download the sample Bubble Chart document we created in this article:

*   [Bubble Chart.docx](https://github.com/groupdocs-assembly/GroupDocs.Assembly-for-Java/blob/master/Examples/GroupDocs.Assembly.Examples.Java/Data/Storage/Word%20Templates/Bubble%20Chart.docx?raw=true)

### Generating The Report

{{< gist GroupDocsGists 25ca4f457bde680504eb2c9cfbb2b8db >}}

## Bubble Chart in OpenOffice Document

To be investigated.
