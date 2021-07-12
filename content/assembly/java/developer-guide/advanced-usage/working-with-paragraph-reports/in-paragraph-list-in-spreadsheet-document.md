---
id: in-paragraph-list-in-spreadsheet-document
url: assembly/java/in-paragraph-list-in-spreadsheet-document
title: In-Paragraph List in Spreadsheet Document
weight: 2
description: ""
keywords: 
productName: GroupDocs.Assembly for Java
hideChildren: False
---
{{< alert style="info" >}}In this article, we will use GroupDocs.Assembly to generate a In-ParagraphList report in Spreadsheet Document format.{{< /alert >}}{{< alert style="info" >}}The code uses some of the objects defined in [The Business Layer](https://docs.groupdocs.com/assembly/java/the-business-layer/).{{< /alert >}}

## In-Paragraph List in Microsoft Excel Document

### Creating a In-Paragraph List

Practising the following steps you can create In-Paragraph List Template in MS Excel 2013.

1.  Add a new Workbook.
2.  Write a sentence, for example "We provide support for the following clients:" in a single column.
3.  Save the template.

### Reporting Requirement

As a report developer, you are required to describe about the clients with the following key requirements:

*   A descriptive or informative line like "We provide support for the following clients:".
*   Show all the clients along with the above sentence.
*   Report must be generated in the Spreadsheet Document.

### Adding Syntax to be evaluated by GroupDocs.Assembly Engine

```java
We provide support for the following clients: <<foreach [in getClients()]>>
<<[indexOf() != 0 ? ", " : ""]>><<[getName()]>><</foreach>>
```

### Download In-Paragraph List Template

Please download the sample In-Paragraph List document we created in this article:

*   [In-Paragraph List.xlsx](https://github.com/groupdocs-assembly/GroupDocs.Assembly-for-Java/blob/master/Examples/GroupDocs.Assembly.Examples.Java/Data/Storage/Spreadsheet%20Templates/In-Paragraph%20List.xlsx?raw=true)

### Generating The Report

{{< gist GroupDocsGists 23a45175195f622deb0d16cb59f5d874 >}}

### ODS Template and Report in Apache OpenOffice

In order to check compatibility of ODS between Microsoft Office 2010 and Apache OpenOffice 4.1.2, we performed below tests:

*   We opened the ODS template created through Microsoft Office 2010 in Apache OpenOffice 4.1.2. The template opened successfully in Apache OpenOffice without any issues or formatting losses.
*   We opened the ODS report generated through GroupDocs.Assembly in Apache OpenOffice 4.1.2. The report opened successfully in Apache OpenOffice without any issues or formatting losses.
