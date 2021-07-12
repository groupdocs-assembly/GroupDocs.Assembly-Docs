---
id: in-table-list-with-highlighted-rows-in-presentation-document
url: assembly/java/in-table-list-with-highlighted-rows-in-presentation-document
title: In-Table List with Highlighted Rows in Presentation Document
weight: 3
description: ""
keywords: 
productName: GroupDocs.Assembly for Java
hideChildren: False
---
{{< alert style="info" >}}In this article, we will use GroupDocs.Assembly to generate In-TableList with Highlighted Rows report in Presentation Document format.{{< /alert >}}{{< alert style="info" >}}The code uses some of the objects defined in [The Business Layer](https://docs.groupdocs.com/assembly/java/the-business-layer/).{{< /alert >}}

## In-Table List with Highlighted Rows in Microsoft PowerPoint Document

### Creating a In-Table List with Highlighted Rows

Practising the following steps you can create In-Table List with Highlighted Rows Template in MS PowerPoint 2013.

1.  Click the document where you want to add the table.
2.  Press "Insert" tab to insert the table.
3.  Insert a 2x4 table.
4.  Click the cell you want to highlight.
5.  Click "Design" tab, and then select Shading.
6.  Save the template.

### Reporting Requirement

As a report developer, you are required to represent the following key requirements:

*   Report must show all the client names with price.
*   Show single client and his single contract price in a single row.
*   It must highlight the record with contract price more than or equal to 1000000.
*   It must show sum of the contract prices.
*   It must represent all the information in tabular form.
*   Report must be generated in the Presentation Document.

### Adding Syntax to be evaluated by GroupDocs.Assembly Engine

<table class="MsoNormalTable" border="0" cellspacing="0" cellpadding="0" width="608" style="width: 456pt; border-collapse: collapse;"><tbody><tr><td width="371" valign="top" style="width: 278pt; border-top-color: white; border-top-style: solid; border-top-width: 1pt; border-right-color: white; border-right-style: solid; border-right-width: 1pt; border-bottom-color: white; border-bottom-style: solid; border-bottom-width: 3pt; border-left-color: white; border-left-style: solid; border-left-width: 1pt; background-color: rgb(91, 155, 213); background-image: initial; padding-top: 0.75pt; padding-right: 5.4pt; padding-bottom: 0in; padding-left: 5.4pt;"><p class="MsoNormal"><b>Client</b></p></td><td width="237" valign="top" style="width: 178pt; border-top-color: white; border-top-style: solid; border-top-width: 1pt; border-left-color: initial; border-left-style: none; border-left-width: initial; border-bottom-color: white; border-bottom-style: solid; border-bottom-width: 3pt; border-right-color: white; border-right-style: solid; border-right-width: 1pt; background-color: rgb(91, 155, 213); background-image: initial; padding-top: 0.75pt; padding-right: 5.4pt; padding-bottom: 0in; padding-left: 5.4pt;"><p class="MsoNormal"><b>Contract Price</b></p></td></tr><tr><td width="371" valign="top" style="width: 278pt; border-top-color: initial; border-top-style: none; border-top-width: initial; border-right-color: white; border-right-style: solid; border-right-width: 1pt; border-bottom-color: white; border-bottom-style: solid; border-bottom-width: 1pt; border-left-color: white; border-left-style: solid; border-left-width: 1pt; background-color: rgb(244, 177, 131); background-image: initial; padding-top: 0.75pt; padding-right: 5.4pt; padding-bottom: 0in; padding-left: 5.4pt;"><p class="MsoNormal"><b>&lt;&lt;foreach [in getContracts()]&gt;&gt;&lt;&lt;if [getPrice() &gt;= 1000000]&gt;&gt;&lt;&lt;[getClient().getName()]&gt;&gt;</b></p></td><td width="237" valign="top" style="width: 178pt; border-top-color: initial; border-top-style: none; border-top-width: initial; border-left-color: initial; border-left-style: none; border-left-width: initial; border-bottom-color: white; border-bottom-style: solid; border-bottom-width: 1pt; border-right-color: white; border-right-style: solid; border-right-width: 1pt; background-color: rgb(244, 177, 131); background-image: initial; padding-top: 0.75pt; padding-right: 5.4pt; padding-bottom: 0in; padding-left: 5.4pt;"><p class="MsoNormal">&lt;&lt;[getPrice()]&gt;&gt;</p></td></tr><tr><td width="371" valign="top" style="width: 278pt; border-top-color: initial; border-top-style: none; border-top-width: initial; border-right-color: white; border-right-style: solid; border-right-width: 1pt; border-bottom-color: white; border-bottom-style: solid; border-bottom-width: 1pt; border-left-color: white; border-left-style: solid; border-left-width: 1pt; background-color: rgb(91, 155, 213); background-image: initial; padding-top: 0.75pt; padding-right: 5.4pt; padding-bottom: 0in; padding-left: 5.4pt;"><p class="MsoNormal"><b>&lt;&lt;else&gt;&gt;&lt;&lt;[getClient().getName()]&gt;&gt;</b></p></td><td width="237" valign="top" style="width: 178pt; border-top-color: initial; border-top-style: none; border-top-width: initial; border-left-color: initial; border-left-style: none; border-left-width: initial; border-bottom-color: white; border-bottom-style: solid; border-bottom-width: 1pt; border-right-color: white; border-right-style: solid; border-right-width: 1pt; background-color: rgb(234, 239, 247); background-image: initial; padding-top: 0.75pt; padding-right: 5.4pt; padding-bottom: 0in; padding-left: 5.4pt;"><p class="MsoNormal">&lt;&lt;[getPrice()]&gt;&gt;&lt;&lt;/if&gt;&gt;&lt;&lt;/foreach&gt;&gt;</p></td></tr><tr><td width="371" valign="top" style="width: 278pt; border-top-color: initial; border-top-style: none; border-top-width: initial; border-right-color: white; border-right-style: solid; border-right-width: 1pt; border-bottom-color: white; border-bottom-style: solid; border-bottom-width: 1pt; border-left-color: white; border-left-style: solid; border-left-width: 1pt; background-color: rgb(91, 155, 213); background-image: initial; padding-top: 0.75pt; padding-right: 5.4pt; padding-bottom: 0in; padding-left: 5.4pt;"><p class="MsoNormal"><b>Total:</b></p></td><td width="237" valign="top" style="width: 178pt; border-top-color: initial; border-top-style: none; border-top-width: initial; border-left-color: initial; border-left-style: none; border-left-width: initial; border-bottom-color: white; border-bottom-style: solid; border-bottom-width: 1pt; border-right-color: white; border-right-style: solid; border-right-width: 1pt; background-color: rgb(210, 222, 239); background-image: initial; padding-top: 0.75pt; padding-right: 5.4pt; padding-bottom: 0in; padding-left: 5.4pt;"><p class="MsoNormal">&lt;&lt;[getContracts().sum(</p><p class="MsoNormal">&nbsp; c =&gt; c.getPrice())]&gt;&gt;</p></td></tr></tbody></table>
### Download In-Table List with Highlighted Rows Template

Please download the sample In-Table List with Highlighted Rows document we created in this article:

*   [In-Table List with Highlighted Rows.pptx](https://github.com/groupdocs-assembly/GroupDocs.Assembly-for-Java/blob/master/Examples/GroupDocs.Assembly.Examples.Java/Data/Storage/Presentation%20Templates/In-Table%20List%20with%20Highlighted%20Rows.pptx?raw=true)

### Generating The Report

{{< gist GroupDocsGists 8e04684db89b558017267c359517e314 >}}



### ODP Template and Report in Apache OpenOffice

In order to check compatibility of ODP between Microsoft Office 2010 and Apache OpenOffice 4.1.2, we performed below tests:

*   We opened the ODP template created through Microsoft Office 2010 in Apache OpenOffice 4.1.2. The template opened successfully in Apache OpenOffice without any issues or formatting losses.
*   We opened the ODP report generated through GroupDocs.Assembly in Apache OpenOffice 4.1.2. The report opened successfully in Apache OpenOffice without any issues or formatting losses.
