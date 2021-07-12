---
id: in-table-list-with-alternate-content-in-word-processing-document
url: assembly/java/in-table-list-with-alternate-content-in-word-processing-document
title: In-Table List With Alternate Content in Word Processing Document
weight: 1
description: ""
keywords: 
productName: GroupDocs.Assembly for Java
hideChildren: False
---
{{< alert style="info" >}}In this article, we will use GroupDocs.Assembly to generate In-TableList WithAlternateContent report in Word Processing Document format.{{< /alert >}}{{< alert style="info" >}}The code uses some of the objects defined in [The Business Layer](https://docs.groupdocs.com/assembly/java/the-business-layer/).{{< /alert >}}

## In-Table List With Alternate Content in Microsoft Word Document

### Creating a In-Table List With Alternate Content

Practising the following steps you can create In-Table List With Alternate Content Template in MS Word 2013.

1.  Click the document where you want to add the table.
2.  Press "Insert" tab to insert the table.
3.  Insert a 2X3 table.
4.  Save the template.

### Reporting Requirement

As a report developer, you are required to represent your clients and their prices with the following key requirements:

*   Report must show each client along with its price.
*   It must show sum of all the prices.
*   It must represent all the information in tabular form.
*   Report must be generated in the Word Processing Document.

### Adding Syntax to be evaluated by GroupDocs.Assembly Engine

<table class="MsoNormalTable" border="0" cellspacing="0" cellpadding="0" width="571" style="width: 428pt; border-collapse: collapse;"><tbody><tr style="height: 15.75pt;"><td width="380" style="width: 285pt; border-top-color: rgb(153, 153, 153); border-top-style: solid; border-top-width: 1pt; border-right-color: rgb(153, 153, 153); border-right-style: solid; border-right-width: 1pt; border-bottom-color: rgb(102, 102, 102); border-bottom-style: solid; border-bottom-width: 1.5pt; border-left-color: rgb(153, 153, 153); border-left-style: solid; border-left-width: 1pt; padding-top: 0in; padding-right: 5.4pt; padding-bottom: 0in; padding-left: 5.4pt; height: 15.75pt;"><p class="MsoNormal" style="margin-bottom: 0.0001pt; line-height: normal;"><b><span style="color: black;">Client</span></b></p></td><td width="191" style="width: 143pt; border-top-color: rgb(153, 153, 153); border-top-style: solid; border-top-width: 1pt; border-left-color: initial; border-left-style: none; border-left-width: initial; border-bottom-color: rgb(102, 102, 102); border-bottom-style: solid; border-bottom-width: 1.5pt; border-right-color: rgb(153, 153, 153); border-right-style: solid; border-right-width: 1pt; padding-top: 0in; padding-right: 5.4pt; padding-bottom: 0in; padding-left: 5.4pt; height: 15.75pt;"><p class="MsoNormal" style="margin-bottom: 0.0001pt; line-height: normal;"><b><span style="color: black;">Contract Price</span></b></p></td></tr><tr style="height: 16.5pt;"><td width="571" colspan="2" style="width: 428pt; border-top-color: initial; border-top-style: none; border-top-width: initial; border-right-color: rgb(153, 153, 153); border-right-style: solid; border-right-width: 1pt; border-bottom-color: rgb(153, 153, 153); border-bottom-style: solid; border-bottom-width: 1pt; border-left-color: rgb(153, 153, 153); border-left-style: solid; border-left-width: 1pt; padding-top: 0in; padding-right: 5.4pt; padding-bottom: 0in; padding-left: 5.4pt; height: 16.5pt;"><p class="MsoNormal" align="center" style="margin-bottom: 0.0001pt; text-align: center; line-height: normal;"><b><span style="color: black;">&lt;&lt;if [!getContracts().any()]&gt;&gt;No data</span></b></p></td></tr><tr style="height: 30.75pt;"><td width="380" style="width: 285pt; border-top-color: initial; border-top-style: none; border-top-width: initial; border-right-color: rgb(153, 153, 153); border-right-style: solid; border-right-width: 1pt; border-bottom-color: rgb(153, 153, 153); border-bottom-style: solid; border-bottom-width: 1pt; border-left-color: rgb(153, 153, 153); border-left-style: solid; border-left-width: 1pt; padding-top: 0in; padding-right: 5.4pt; padding-bottom: 0in; padding-left: 5.4pt; height: 30.75pt;"><p class="MsoNormal" style="margin-bottom: 0.0001pt; line-height: normal;"><b><span style="color: black;">&lt;&lt;else&gt;&gt;&lt;&lt;foreach [in getContracts()]&gt;&gt;&lt;&lt;[getClient().getName()]&gt;&gt;</span></b></p></td><td width="191" style="width: 143pt; border-top-color: initial; border-top-style: none; border-top-width: initial; border-left-color: initial; border-left-style: none; border-left-width: initial; border-bottom-color: rgb(153, 153, 153); border-bottom-style: solid; border-bottom-width: 1pt; border-right-color: rgb(153, 153, 153); border-right-style: solid; border-right-width: 1pt; padding-top: 0in; padding-right: 5.4pt; padding-bottom: 0in; padding-left: 5.4pt; height: 30.75pt;"><p class="MsoNormal" style="margin-bottom: 0.0001pt; line-height: normal;"><span style="color: black;">&lt;&lt;[getPrice()]&gt;&gt;&lt;&lt;/foreach&gt;&gt;</span></p></td></tr><tr style="height: 30.75pt;"><td width="380" style="width: 285pt; border-top-color: initial; border-top-style: none; border-top-width: initial; border-right-color: rgb(153, 153, 153); border-right-style: solid; border-right-width: 1pt; border-bottom-color: rgb(153, 153, 153); border-bottom-style: solid; border-bottom-width: 1pt; border-left-color: rgb(153, 153, 153); border-left-style: solid; border-left-width: 1pt; padding-top: 0in; padding-right: 5.4pt; padding-bottom: 0in; padding-left: 5.4pt; height: 30.75pt;"><p class="MsoNormal" style="margin-bottom: 0.0001pt; line-height: normal;"><b><span style="color: black;">Total:</span></b></p></td><td width="191" style="width: 143pt; border-top-color: initial; border-top-style: none; border-top-width: initial; border-left-color: initial; border-left-style: none; border-left-width: initial; border-bottom-color: rgb(153, 153, 153); border-bottom-style: solid; border-bottom-width: 1pt; border-right-color: rgb(153, 153, 153); border-right-style: solid; border-right-width: 1pt; padding-top: 0in; padding-right: 5.4pt; padding-bottom: 0in; padding-left: 5.4pt; height: 30.75pt;"><p class="MsoNormal" style="margin-bottom: 0.0001pt; line-height: normal;"><span style="color: black;">&lt;&lt;[getContracts().sum(<br>&nbsp; c =&gt; c.getPrice())]&gt;&gt;&lt;&lt;/if&gt;&gt;</span></p></td></tr></tbody></table>

### Download In-Table List With Alternate Content Template

Please download the sample In-Table List With Alternate Content document we created in this article:

*   [In-Table List With Alternate Content.docx](https://github.com/groupdocs-assembly/GroupDocs.Assembly-for-Java/blob/master/Examples/GroupDocs.Assembly.Examples.Java/Data/Storage/Word%20Templates/In-Table%20List%20with%20Alternate%20Content.docx?raw=true)

### Generating The Report

{{< gist GroupDocsGists 53b3177d14f48335422fe6e762e9d57e >}}

### ODT Template and Report in Apache OpenOffice

In order to check compatibility of ODT between Microsoft Office 2010 and Apache OpenOffice 4.1.2, we performed below tests:

*   We opened the ODT template created through Microsoft Office 2010 in Apache OpenOffice 4.1.2. The template opened successfully in Apache OpenOffice without any issues or formatting losses.
*   We opened the ODT report generated through GroupDocs.Assembly in Apache OpenOffice 4.1.2. The report opened successfully in Apache OpenOffice without any issues or formatting losses.
