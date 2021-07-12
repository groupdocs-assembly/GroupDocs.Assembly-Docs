---
id: in-table-list-with-filtering-grouping-and-ordering-in-word-processing-document
url: assembly/java/in-table-list-with-filtering-grouping-and-ordering-in-word-processing-document
title: In-Table List with Filtering Grouping and Ordering in Word Processing Document
weight: 1
description: ""
keywords: 
productName: GroupDocs.Assembly for Java
hideChildren: False
---
{{< alert style="info" >}}In this article, we will use GroupDocs.Assembly to generate In-TableList with Filtering, Grouping, and Ordering report in Word Processing Document format.{{< /alert >}}{{< alert style="info" >}}The code uses some of the objects defined in [The Business Layer](https://docs.groupdocs.com/assembly/java/the-business-layer/).{{< /alert >}}

## In-Table List with Filtering, Grouping, and Ordering in Microsoft Word Document

### Creating a In-Table List with Filtering, Grouping, and Ordering

Practicing the following steps you can create In-Table List with Filtering, Grouping, and Ordering Template in MS Word 2013.

1.  Click the document where you want to add the table.
2.  Press "Insert" tab to insert the table.
3.  Insert a 2x2 table.
4.  Save the template.

### Reporting Requirement

As a report developer, you are required to represent managers' contract information with the following key requirements:

*   Report must show each manager along with sum of prices of his contracts.
*   It must represent all the information in tabular form.
*   Report must be generated in the Word Processing Document.

### Adding Syntax to be evaluated by GroupDocs.Assembly Engine

| **Manager**                                                  | **Contract Price**                       |
| ------------------------------------------------------------ | ---------------------------------------- |
| **<<foreach [in getContracts()<br />    .where(c => c.getDate().getYear() + 1900 == 2015)<br />    .groupBy(c => c.getManager())<br />    .orderBy(g => g.key.getName())]>><br /><<[key.getName()]>>** | <<[sum(c => c.getPrice())]>><</foreach>> |

### Download In-Table List with Filtering, Grouping, and Ordering Template

Please download the sample In-Table List with Filtering, Grouping, and Ordering document we created in this article:

*   [In-Table List with Filtering, Grouping, and Ordering.docx](https://github.com/groupdocs-assembly/GroupDocs.Assembly-for-Java/blob/master/Examples/GroupDocs.Assembly.Examples.Java/Data/Storage/Word%20Templates/In-Table%20List%20with%20Filtering%2C%20Grouping%2C%20and%20Ordering.docx?raw=true)

### Generating The Report

{{< gist GroupDocsGists 729c3fe954b072ffea852e64521ecca4 >}}

### ODT Template and Report in Apache OpenOffice

In order to check compatibility of ODT between Microsoft Office 2010 and Apache OpenOffice 4.1.2, we performed below tests:

*   We opened the ODT template created through Microsoft Office 2010 in Apache OpenOffice 4.1.2. The template opened successfully in Apache OpenOffice without any issues or formatting losses.
*   We opened the ODT report generated through GroupDocs.Assembly in Apache OpenOffice 4.1.2. The report opened successfully in Apache OpenOffice without any issues or formatting losses.
