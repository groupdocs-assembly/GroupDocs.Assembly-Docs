---
id: pie-chart-in-email-document
url: assembly/java/pie-chart-in-email-document
title: Pie Chart in Email Document
weight: 4
description: ""
keywords: 
productName: GroupDocs.Assembly for Java
hideChildren: False
---
{{< alert style="info" >}}In this article, we will use GroupDocs.Assembly to generate a Pie Chart report in Presentation Document format.{{< /alert >}}

## Pie Chart in Email Document

### Creating a Pie Chart

Please follow below steps to create Pie Chart in MS Outlook 2013:

1.  Create a new Email.
2.  Click the "Insert" tab, and then click "Chart" in the illustrations group to open the "Insert Chart" dialog box.
3.  Select "Pie".
4.  Preview "Pie" and press OK to insert the chart and Worksheet template to your email.
5.  Edit the Worksheet with your data to update the chart.

### Reporting Requirement

As a report developer, you are required to share managers' contract prices dynamically with the following key requirements:

*   Report must be in .eml or .msg format.
*   It must add email recipient, css and subject of the email.
*   Report must show information on a Pie Chart.
*   It must indicate manager name with value (price of the contract).

### Adding Syntax to be evaluated by GroupDocs.Assembly Engine

#### Chart Title

```java
Total Contract Price<<foreach [in getManagers()]>><<x [getName()]>>
```

#### Chart Data (Email)

<table border="1" cellspacing="0" cellpadding="0" style="border-collapse: collapse; border-top-color: initial; border-top-style: none; border-top-width: initial; border-right-color: initial; border-right-style: none; border-right-width: initial; border-bottom-color: initial; border-bottom-style: none; border-bottom-width: initial; border-left-color: initial; border-left-style: none; border-left-width: initial;"><tbody><tr><td width="312" valign="top" style="width: 233.75pt; border-top-color: windowtext; border-top-style: solid; border-top-width: 1pt; border-right-color: windowtext; border-right-style: solid; border-right-width: 1pt; border-bottom-color: windowtext; border-bottom-style: solid; border-bottom-width: 1pt; border-left-color: windowtext; border-left-style: solid; border-left-width: 1pt; padding-top: 0in; padding-right: 5.4pt; padding-bottom: 0in; padding-left: 5.4pt;"><p style="margin-bottom: 0.0001pt; line-height: normal;">&nbsp;</p></td><td width="312" valign="bottom" style="width: 233.75pt; border-top-color: windowtext; border-top-style: solid; border-top-width: 1pt; border-right-color: windowtext; border-right-style: solid; border-right-width: 1pt; border-bottom-color: windowtext; border-bottom-style: solid; border-bottom-width: 1pt; border-left-color: initial; border-left-style: none; border-left-width: initial; padding-top: 0in; padding-right: 5.4pt; padding-bottom: 0in; padding-left: 5.4pt;"><p style="margin-bottom: 0.0001pt; line-height: normal;"><span style="color: black;">Total Contract Price&lt;&lt;y [getContracts().sum(c =&gt; c.getPrice())]&gt;&gt;</span></p></td></tr><tr><td width="312" valign="top" style="width: 233.75pt; border-top-color: initial; border-top-style: none; border-top-width: initial; border-right-color: windowtext; border-right-style: solid; border-right-width: 1pt; border-bottom-color: windowtext; border-bottom-style: solid; border-bottom-width: 1pt; border-left-color: windowtext; border-left-style: solid; border-left-width: 1pt; padding-top: 0in; padding-right: 5.4pt; padding-bottom: 0in; padding-left: 5.4pt;"><p style="margin-bottom: 0.0001pt; line-height: normal;">A</p></td><td width="312" valign="top" style="width: 233.75pt; border-top-color: initial; border-top-style: none; border-top-width: initial; border-left-color: initial; border-left-style: none; border-left-width: initial; border-bottom-color: windowtext; border-bottom-style: solid; border-bottom-width: 1pt; border-right-color: windowtext; border-right-style: solid; border-right-width: 1pt; padding-top: 0in; padding-right: 5.4pt; padding-bottom: 0in; padding-left: 5.4pt;"><p style="margin-bottom: 0.0001pt; line-height: normal;">8.2</p></td></tr><tr><td width="312" valign="top" style="width: 233.75pt; border-top-color: initial; border-top-style: none; border-top-width: initial; border-right-color: windowtext; border-right-style: solid; border-right-width: 1pt; border-bottom-color: windowtext; border-bottom-style: solid; border-bottom-width: 1pt; border-left-color: windowtext; border-left-style: solid; border-left-width: 1pt; padding-top: 0in; padding-right: 5.4pt; padding-bottom: 0in; padding-left: 5.4pt;"><p style="margin-bottom: 0.0001pt; line-height: normal;">B</p></td><td width="312" valign="top" style="width: 233.75pt; border-top-color: initial; border-top-style: none; border-top-width: initial; border-left-color: initial; border-left-style: none; border-left-width: initial; border-bottom-color: windowtext; border-bottom-style: solid; border-bottom-width: 1pt; border-right-color: windowtext; border-right-style: solid; border-right-width: 1pt; padding-top: 0in; padding-right: 5.4pt; padding-bottom: 0in; padding-left: 5.4pt;"><p style="margin-bottom: 0.0001pt; line-height: normal;">3.2</p></td></tr><tr><td width="312" valign="top" style="width: 233.75pt; border-top-color: initial; border-top-style: none; border-top-width: initial; border-right-color: windowtext; border-right-style: solid; border-right-width: 1pt; border-bottom-color: windowtext; border-bottom-style: solid; border-bottom-width: 1pt; border-left-color: windowtext; border-left-style: solid; border-left-width: 1pt; padding-top: 0in; padding-right: 5.4pt; padding-bottom: 0in; padding-left: 5.4pt;"><p style="margin-bottom: 0.0001pt; line-height: normal;">C</p></td><td width="312" valign="top" style="width: 233.75pt; border-top-color: initial; border-top-style: none; border-top-width: initial; border-left-color: initial; border-left-style: none; border-left-width: initial; border-bottom-color: windowtext; border-bottom-style: solid; border-bottom-width: 1pt; border-right-color: windowtext; border-right-style: solid; border-right-width: 1pt; padding-top: 0in; padding-right: 5.4pt; padding-bottom: 0in; padding-left: 5.4pt;"><p style="margin-bottom: 0.0001pt; line-height: normal;">1.4</p></td></tr><tr><td width="312" valign="top" style="width: 233.75pt; border-top-color: initial; border-top-style: none; border-top-width: initial; border-right-color: windowtext; border-right-style: solid; border-right-width: 1pt; border-bottom-color: windowtext; border-bottom-style: solid; border-bottom-width: 1pt; border-left-color: windowtext; border-left-style: solid; border-left-width: 1pt; padding-top: 0in; padding-right: 5.4pt; padding-bottom: 0in; padding-left: 5.4pt;"><p style="margin-bottom: 0.0001pt; line-height: normal;">D</p></td><td width="312" valign="top" style="width: 233.75pt; border-top-color: initial; border-top-style: none; border-top-width: initial; border-left-color: initial; border-left-style: none; border-left-width: initial; border-bottom-color: windowtext; border-bottom-style: solid; border-bottom-width: 1pt; border-right-color: windowtext; border-right-style: solid; border-right-width: 1pt; padding-top: 0in; padding-right: 5.4pt; padding-bottom: 0in; padding-left: 5.4pt;"><p style="margin-bottom: 0.0001pt; line-height: normal;">1.2</p></td></tr></tbody></table>
### Download Pie Chart Template

Please download the sample Pie Chart document we created in this article:

*   [Pie Chart.eml](https://raw.githubusercontent.com/groupdocs-assembly/GroupDocs.Assembly-for-Java/master/Examples/GroupDocs.Assembly.Examples.Java/Data/Storage/Email%20Templates/Bulleted%20List.eml?raw=true)

### Generating The Report

{{< alert style="info" >}}The code uses some of the objects defined in: [The Business Layer](https://docs.groupdocs.com/assembly/java/the-business-layer/){{< /alert >}}{{< gist samicheemagroupdocs d260234be58124a0318f6a76f2ad4dca >}}


