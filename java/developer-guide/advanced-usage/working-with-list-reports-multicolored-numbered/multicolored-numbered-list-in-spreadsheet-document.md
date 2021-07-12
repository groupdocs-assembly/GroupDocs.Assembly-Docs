---
id: multicolored-numbered-list-in-spreadsheet-document
url: assembly/java/multicolored-numbered-list-in-spreadsheet-document
title: Multicolored Numbered List in Spreadsheet Document
weight: 2
description: ""
keywords: 
productName: GroupDocs.Assembly for Java
hideChildren: False
---
{{< alert style="info" >}}In this article, we will use GroupDocs.Assembly to generate a Multicolored Numbered List report in Spreadsheet Document format.{{< /alert >}}

## Multicolored Numbered List in Microsoft Excel Document

### Creating a Multicolored Numbered List

Practicing the following steps you can create Multicolored Numbered List Template in MS Excel 2013.

1.  Add a new Workbook.
2.  In one cell, write a sentence like "We provide support for the following clients:".
3.  Select the cell, and assign a color by pressing "Cell Styles" in Styles group.
4.  Save the template.

### Reporting Requirement

As a report developer, you are required to represent the following key requirements:

*   Report must show the clients in numbered list.
*   It must highlight the products.
*   Report must be generated in the Spreadsheet Document.

### Adding Syntax to be evaluated by GroupDocs.Assembly Engine

We provide support for the following clients:

<ol>
<li>&lt;&lt;foreach [in getClients()]>>&lt;&lt;if [indexOf() % 2 == 0]>>&lt;&lt;[getName()]>></li>
<li style="background-color: #ceffbc">&lt;&lt;else>>&lt;&lt;[getName()]>></li>
</ol>

​		<</if>><</foreach>>

### Download Multicolored Numbered List Template

Please download the sample Multicolored Numbered List document we created in this article:

*   [Multicolored Numbered List.xlsx](https://github.com/groupdocs-assembly/GroupDocs.Assembly-for-Java/blob/master/Examples/GroupDocs.Assembly.Examples.Java/Data/Storage/Spreadsheet%20Templates/Multicolored%20Numbered%20List.xlsx?raw=true)

### Generating The Report

{{< alert style="info" >}}The code uses some of the objects defined in: [The Business Layer](https://docs.groupdocs.com/assembly/java/the-business-layer/){{< /alert >}}{{< gist atirtahirgroupdocs d6c0fde163b9edd0cc9dda4bcd01843a >}}

### ODS Template and Report in Apache OpenOffice

In order to check compatibility of ODS between Microsoft Office 2010 and Apache OpenOffice 4.1.2, we performed below tests:

*   We opened the ODS template created through Microsoft Office 2010 in Apache OpenOffice 4.1.2. The template opened successfully in Apache OpenOffice without any issues or formatting losses.
*   We opened the ODS report generated through GroupDocs.Assembly in Apache OpenOffice 4.1.2. The report opened successfully in Apache OpenOffice without any issues or formatting losses.
