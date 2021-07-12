---
id: in-table-list-with-highlighted-rows-in-spreadsheet-document
url: assembly/java/in-table-list-with-highlighted-rows-in-spreadsheet-document
title: In-Table List with Highlighted Rows in Spreadsheet Document
weight: 2
description: ""
keywords: 
productName: GroupDocs.Assembly for Java
hideChildren: False
---
{{< alert style="info" >}}In this article, we will use GroupDocs.Assembly to generate In-TableList with Highlighted Rows report in Spreadsheet Document format.{{< /alert >}}{{< alert style="info" >}}The code uses some of the objects defined in [The Business Laye](https://docs.groupdocs.com/assembly/java/the-business-layer/)r.{{< /alert >}}

## In-Table List with Highlighted Rows in Microsoft Excel Document

### Creating a In-Table List with Highlighted Rows

Practising the following steps you can create In-Table List with Highlighted Rows Template in MS Excel 2013.

1.  Add a new Workbook.
2.  Select the range of cells that you want to include in the table.
3.  On the Insert tab, in the Tables group, click Table.
4.  Insert a 2x4 table.
5.  Click the cell you want to highlight.
6.  Click "Cell Styles" in Styles group.
7.  Save the template.

### Reporting Requirement

As a report developer, you are required to represent the following key requirements:

*   Report must show all the client names with price.
*   Show single client and his single contract price in a single row.
*   It must highlight the record with contract price more than or equal to 1000000.
*   It must show sum of the contract prices.
*   It must represent all the information in tabular form.
*   Report must be generated in the Spreadsheet Document.

### Adding Syntax to be evaluated by GroupDocs.Assembly Engine

<table class="MsoTableGridLight" border="1" cellspacing="0" cellpadding="0" style="border-collapse: collapse; border-top-color: initial; border-top-style: none; border-top-width: initial; border-right-color: initial; border-right-style: none; border-right-width: initial; border-bottom-color: initial; border-bottom-style: none; border-bottom-width: initial; border-left-color: initial; border-left-style: none; border-left-width: initial;"><tbody><tr><td width="623" valign="top" style="width: 467.25pt; border-top-color: rgb(191, 191, 191); border-top-style: solid; border-top-width: 1pt; border-right-color: rgb(191, 191, 191); border-right-style: solid; border-right-width: 1pt; border-bottom-color: rgb(191, 191, 191); border-bottom-style: solid; border-bottom-width: 1pt; border-left-color: rgb(191, 191, 191); border-left-style: solid; border-left-width: 1pt; padding-top: 0in; padding-right: 5.4pt; padding-bottom: 0in; padding-left: 5.4pt;"><p class="MsoNormal" style="margin-bottom: 0.0001pt; line-height: normal;">&nbsp;</p><table class="MsoTable15Grid1Light" border="1" cellspacing="0" cellpadding="0" style="border-collapse: collapse; border-top-color: initial; border-top-style: none; border-top-width: initial; border-right-color: initial; border-right-style: none; border-right-width: initial; border-bottom-color: initial; border-bottom-style: none; border-bottom-width: initial; border-left-color: initial; border-left-style: none; border-left-width: initial;"><tbody><tr><td width="370" valign="top" style="width: 277.6pt; border-top-color: rgb(153, 153, 153); border-top-style: solid; border-top-width: 1pt; border-right-color: rgb(153, 153, 153); border-right-style: solid; border-right-width: 1pt; border-bottom-color: rgb(102, 102, 102); border-bottom-style: solid; border-bottom-width: 1.5pt; border-left-color: rgb(153, 153, 153); border-left-style: solid; border-left-width: 1pt; padding-top: 0in; padding-right: 5.4pt; padding-bottom: 0in; padding-left: 5.4pt;"><p class="MsoNormal" style="margin-bottom: 0.0001pt; line-height: normal;"><b>Client</b></p></td><td width="238" valign="top" style="width: 178.35pt; border-top-color: rgb(153, 153, 153); border-top-style: solid; border-top-width: 1pt; border-left-color: initial; border-left-style: none; border-left-width: initial; border-bottom-color: rgb(102, 102, 102); border-bottom-style: solid; border-bottom-width: 1.5pt; border-right-color: rgb(153, 153, 153); border-right-style: solid; border-right-width: 1pt; padding-top: 0in; padding-right: 5.4pt; padding-bottom: 0in; padding-left: 5.4pt;"><p class="MsoNormal" style="margin-bottom: 0.0001pt; line-height: normal;"><b>Contract Price</b></p></td></tr><tr><td width="370" valign="top" style="width: 277.6pt; border-top-color: initial; border-top-style: none; border-top-width: initial; border-right-color: rgb(153, 153, 153); border-right-style: solid; border-right-width: 1pt; border-bottom-color: rgb(153, 153, 153); border-bottom-style: solid; border-bottom-width: 1pt; border-left-color: rgb(153, 153, 153); border-left-style: solid; border-left-width: 1pt; background-color: rgb(255, 242, 204); background-image: initial; padding-top: 0in; padding-right: 5.4pt; padding-bottom: 0in; padding-left: 5.4pt;"><p class="MsoNormal" style="margin-bottom: 0.0001pt; line-height: normal;"><b>&lt;&lt;foreach [in getContracts()]&gt;&gt;&lt;&lt;if [getPrice() &gt;= 1000000]&gt;&gt;&lt;&lt;[getClient().getName()]&gt;&gt;</b></p></td><td width="238" valign="top" style="width: 178.35pt; border-top-color: initial; border-top-style: none; border-top-width: initial; border-left-color: initial; border-left-style: none; border-left-width: initial; border-bottom-color: rgb(153, 153, 153); border-bottom-style: solid; border-bottom-width: 1pt; border-right-color: rgb(153, 153, 153); border-right-style: solid; border-right-width: 1pt; background-color: rgb(255, 242, 204); background-image: initial; padding-top: 0in; padding-right: 5.4pt; padding-bottom: 0in; padding-left: 5.4pt;"><p class="MsoNormal" style="margin-bottom: 0.0001pt; line-height: normal;">&lt;&lt;[getPrice()]&gt;&gt;</p></td></tr><tr><td width="370" valign="top" style="width: 277.6pt; border-top-color: initial; border-top-style: none; border-top-width: initial; border-right-color: rgb(153, 153, 153); border-right-style: solid; border-right-width: 1pt; border-bottom-color: rgb(153, 153, 153); border-bottom-style: solid; border-bottom-width: 1pt; border-left-color: rgb(153, 153, 153); border-left-style: solid; border-left-width: 1pt; padding-top: 0in; padding-right: 5.4pt; padding-bottom: 0in; padding-left: 5.4pt;"><p class="MsoNormal" style="margin-bottom: 0.0001pt; line-height: normal;"><b>&lt;&lt;else&gt;&gt;&lt;&lt;[getClient().getName()]&gt;&gt;</b></p></td><td width="238" valign="top" style="width: 178.35pt; border-top-color: initial; border-top-style: none; border-top-width: initial; border-left-color: initial; border-left-style: none; border-left-width: initial; border-bottom-color: rgb(153, 153, 153); border-bottom-style: solid; border-bottom-width: 1pt; border-right-color: rgb(153, 153, 153); border-right-style: solid; border-right-width: 1pt; padding-top: 0in; padding-right: 5.4pt; padding-bottom: 0in; padding-left: 5.4pt;"><p class="MsoNormal" style="margin-bottom: 0.0001pt; line-height: normal;">&lt;&lt;[getPrice()]&gt;&gt;&lt;&lt;/if&gt;&gt;&lt;&lt;/foreach&gt;&gt;</p></td></tr><tr><td width="370" valign="top" style="width: 277.6pt; border-top-color: initial; border-top-style: none; border-top-width: initial; border-right-color: rgb(153, 153, 153); border-right-style: solid; border-right-width: 1pt; border-bottom-color: rgb(153, 153, 153); border-bottom-style: solid; border-bottom-width: 1pt; border-left-color: rgb(153, 153, 153); border-left-style: solid; border-left-width: 1pt; padding-top: 0in; padding-right: 5.4pt; padding-bottom: 0in; padding-left: 5.4pt;"><p class="MsoNormal" style="margin-bottom: 0.0001pt; line-height: normal;"><b>Total:</b></p></td><td width="238" valign="top" style="width: 178.35pt; border-top-color: initial; border-top-style: none; border-top-width: initial; border-left-color: initial; border-left-style: none; border-left-width: initial; border-bottom-color: rgb(153, 153, 153); border-bottom-style: solid; border-bottom-width: 1pt; border-right-color: rgb(153, 153, 153); border-right-style: solid; border-right-width: 1pt; padding-top: 0in; padding-right: 5.4pt; padding-bottom: 0in; padding-left: 5.4pt;"><p class="MsoNormal" style="margin-bottom: 0.0001pt; line-height: normal;">&lt;&lt;[getContracts().sum(</p><p class="MsoNormal" style="margin-bottom: 0.0001pt; line-height: normal;">&nbsp; c =&gt; c.getPrice())]&gt;&gt;</p></td></tr></tbody></table><p class="MsoNormal" style="margin-bottom: 0.0001pt; line-height: normal;">&nbsp;</p><p class="MsoNormal" style="margin-bottom: 0.0001pt; line-height: normal;">&nbsp;</p></td></tr></tbody></table>
### Download In-Table List with Highlighted Rows Template

Please download the sample In-Table List with Highlighted Rows document we created in this article:

*   [In-Table List with Highlighted Rows.xlsx](https://github.com/groupdocs-assembly/GroupDocs.Assembly-for-Java/blob/master/Examples/GroupDocs.Assembly.Examples.Java/Data/Storage/Spreadsheet%20Templates/In-Table%20List%20with%20Highlighted%20Rows.xlsx?raw=true)

### Generating The Report

{{< gist GroupDocsGists 46c41d0904f70c013c0427c89757d29e >}}



### ODS Template and Report in Apache OpenOffice

In order to check compatibility of ODS between Microsoft Office 2010 and Apache OpenOffice 4.1.2, we performed below tests:

*   We opened the ODS template created through Microsoft Office 2010 in Apache OpenOffice 4.1.2. The template opened successfully in Apache OpenOffice without any issues or formatting losses.
*   We opened the ODS report generated through GroupDocs.Assembly in Apache OpenOffice 4.1.2. The report opened successfully in Apache OpenOffice without any issues or formatting losses.
