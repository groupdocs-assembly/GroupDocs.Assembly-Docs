---
id: single-row-image-in-spreadsheet-document
url: assembly/java/single-row-image-in-spreadsheet-document
title: Single Row Image in Spreadsheet Document
weight: 2
description: ""
keywords: 
productName: GroupDocs.Assembly for Java
hideChildren: False
---
{{< alert style="info" >}}In this article, we will use GroupDocs.Assembly to generate a Single Row Image report in Spreadsheet Document format.{{< /alert >}}{{< alert style="info" >}}The code uses some of the objects defined in [The Business Layer](https://docs.groupdocs.com/assembly/java/the-business-layer/).{{< /alert >}}

## Single Row in Microsoft Excel Document

### Creating a Single Row

Please follow below steps to create Single Row Image in MS Excel 2013:

1.  Create a new Workbook.
2.  Insert a desired shape to display image in it.
3.  Go to Insert Tab and select shape by clicking on Shape Icon.
4.  Write "Name" and "Age" to show name and age info of the customer.
5.  Save the template.

### Reporting Requirement

As a report developer, you are required to represent information of first single manager with the following key requirements:

*   Report must show image of the manager
*   It must show Name and age of manager
*   Report must be generated in the Spreadsheet Document.

### Adding Syntax to be evaluated by GroupDocs.Assembly Engine

<table class="MsoTableGrid" border="1" cellspacing="0" cellpadding="0" style="border-collapse: collapse; border-top-color: initial; border-top-style: none; border-top-width: initial; border-right-color: initial; border-right-style: none; border-right-width: initial; border-bottom-color: initial; border-bottom-style: none; border-bottom-width: initial; border-left-color: initial; border-left-style: none; border-left-width: initial;"><tbody><tr><td width="172" valign="top" style="width: 129.05pt; border-top-color: initial; border-top-style: none; border-top-width: initial; border-right-color: initial; border-right-style: none; border-right-width: initial; border-bottom-color: initial; border-bottom-style: none; border-bottom-width: initial; border-left-color: initial; border-left-style: none; border-left-width: initial; padding-top: 0in; padding-right: 5.4pt; padding-bottom: 0in; padding-left: 5.4pt;"><p class="MsoNormal" style="margin-bottom: 0.0001pt; line-height: normal;"><img width="153" height="142" src="" alt="<<image [manager.getPhoto()]>>"></p></td><td width="436" valign="top" style="width: 326.9pt; border-top-color: initial; border-top-style: none; border-top-width: initial; border-right-color: initial; border-right-style: none; border-right-width: initial; border-bottom-color: initial; border-bottom-style: none; border-bottom-width: initial; border-left-color: initial; border-left-style: none; border-left-width: initial; padding-top: 0in; padding-right: 5.4pt; padding-bottom: 0in; padding-left: 5.4pt;"><table class="MsoTable15Plain2" border="0" cellspacing="0" cellpadding="0" style="border-collapse: collapse; border-top-color: initial; border-top-style: none; border-top-width: initial; border-right-color: initial; border-right-style: none; border-right-width: initial; border-bottom-color: initial; border-bottom-style: none; border-bottom-width: initial; border-left-color: initial; border-left-style: none; border-left-width: initial;"><tbody><tr><td width="116" valign="top" style="width: 86.7pt; padding-top: 0in; padding-right: 5.4pt; padding-bottom: 0in; padding-left: 5.4pt;"><p class="MsoNormal" style="margin-bottom: 0.0001pt; line-height: normal;"><b><span style="font-size: 16pt;">Name:</span></b></p></td><td width="305" valign="top" style="width: 228.9pt; padding-top: 0in; padding-right: 5.4pt; padding-bottom: 0in; padding-left: 5.4pt;"><p class="MsoNormal" style="margin-bottom: 0.0001pt; line-height: normal;"><b><span style="font-size: 16pt;">&lt;&lt;[manager.getName()]&gt;&gt;</span></b></p></td></tr><tr><td width="116" valign="top" style="width: 86.7pt; padding-top: 0in; padding-right: 5.4pt; padding-bottom: 0in; padding-left: 5.4pt;"><p class="MsoNormal" style="margin-bottom: 0.0001pt; line-height: normal;"><b><span style="font-size: 16pt;">Age:</span></b></p></td><td width="305" valign="top" style="width: 228.9pt; padding-top: 0in; padding-right: 5.4pt; padding-bottom: 0in; padding-left: 5.4pt;"><p class="MsoNormal" style="margin-bottom: 0.0001pt; line-height: normal;"><span style="font-size: 16pt;">&lt;&lt;[manager.getAge()]&gt;&gt;</span></p></td></tr></tbody></table><p class="MsoNormal" style="margin-bottom: 0.0001pt; line-height: normal;"></p></td></tr></tbody></table>
### Download Single Row Template

Please download the sample Single Row document we created in this article:

*   [Single Row.xlsx](https://github.com/groupdocs-assembly/GroupDocs.Assembly-for-Java/blob/master/Examples/GroupDocs.Assembly.Examples.Java/Data/Storage/Spreadsheet%20Templates/Single%20Row.xlsx?raw=true)

### Generating The Report

{{< gist GroupDocsGists 7d0baf2bd25fa3d626e93d540a9395b4 >}}

### ODS Template and Report in Apache OpenOffice

In order to check compatibility of ODS between Microsoft Office 2010 and Apache OpenOffice 4.1.2, we performed below tests:

*   We opened the ODS template created through Microsoft Office 2010 in Apache OpenOffice 4.1.2. The template opened successfully in Apache OpenOffice without any issues or formatting losses.

*   We opened the ODS report generated through GroupDocs.Assembly in Apache OpenOffice 4.1.2. The report opened successfully in Apache OpenOffice without any issues or formatting losses.
