---
id: in-table-list-in-spreadsheet-document
url: assembly/java/in-table-list-in-spreadsheet-document
title: In-Table List in Spreadsheet Document
weight: 2
description: ""
keywords: 
productName: GroupDocs.Assembly for Java
hideChildren: False
---
{{< alert style="info" >}}In this article, we will use GroupDocs.Assembly to generate a In-TableList report in Spreadsheet format.{{< /alert >}}{{< alert style="info" >}}The code uses some of the objects defined in [The Business Layer](https://docs.groupdocs.com/assembly/java/the-business-layer/).{{< /alert >}}

## In-Table List in Microsoft Excel Document

### Creating a In-Table List

Practising the following steps you can create In-Table List Template in MS Excel 2013.

1.  Add a new Workbook.
2.  Select the range of cells that you want to include in the table.
3.  On the Insert tab, in the Tables group, click Table.
4.  Save your Document.

### Reporting Requirement

As a report developer, you are required to represent the information of the managers with the following key requirements:

*   Report must show managers' name.
*   It must show the sum of contract prices against each manager.
*   It must sum up all the contract prices for all the managers.
*   All the representation must be in tabular form.
*   Report must be generated in the Spreadsheet Document.

### Adding Syntax to be evaluated by GroupDocs.Assembly Engine

| **Manager**                                       | **Contract Price**                                           |
| ------------------------------------------------- | ------------------------------------------------------------ |
| **<<foreach [in getManagers()]>><<[getName()]>>** | <<[getContracts().sum(<br />   c => c.getPrice())]>><</foreach>> |
| **Total:**                                        | <<[getManagers().sum(<br />   m => m.getContracts().sum(<br />     c => c.getPrice()))]>> |

### Download In-Table List Template

Please download the sample In-Table List document we created in this article:

*   [In-Table List.xlsx](https://github.com/groupdocs-assembly/GroupDocs.Assembly-for-Java/blob/master/Examples/GroupDocs.Assembly.Examples.Java/Data/Storage/Spreadsheet%20Templates/In-Table%20List.xlsx?raw=true)

### Generating The Report

{{< gist GroupDocsGists a85a917d5602e18168b0f98f7de9f1bd >}}

### ODS Template and Report in Apache OpenOffice

In order to check compatibility of ODS between Microsoft Office 2010 and Apache OpenOffice 4.1.2, we performed below tests:

*   We opened the ODS template created through Microsoft Office 2010 in Apache OpenOffice 4.1.2. The template opened successfully in Apache OpenOffice without any issues or formatting losses.
*   We opened the ODS report generated through GroupDocs.Assembly in Apache OpenOffice 4.1.2. The report opened successfully in Apache OpenOffice without any issues or formatting losses.
