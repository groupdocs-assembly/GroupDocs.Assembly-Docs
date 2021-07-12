---
id: numbered-list-in-spreadsheet-document
url: assembly/java/numbered-list-in-spreadsheet-document
title: Numbered List in Spreadsheet Document
weight: 2
description: ""
keywords: 
productName: GroupDocs.Assembly for Java
hideChildren: False
---
{{< alert style="info" >}}In this article, we will use GroupDocs.Assembly to generate a Numbered List report in Spreadsheet Document format.{{< /alert >}}{{< alert style="info" >}}The code uses some of the objects defined in [The Business Layer](https://docs.groupdocs.com/assembly/java/the-business-layer/).{{< /alert >}}

## Numbered List in Microsoft Excel Document

### Creating a Numbered List

Practising the following steps you can create Numbered List Template in MS Excel 2013.  
You can create two kinds of Numbered List in Microsoft Excel.

*   In-cell List
*   Multiple-cell List

Apply the following steps to build the In-Cell template

1.  Add a new Workbook.
2.  Write a sentence, for example "We provide support for the following clients:" in a single cell and add syntax there.
3.  Save the template.

### Reporting Requirement

As a report developer, you are required to represent the following key requirements:

*   Report must show the client names in numbered list.
*   Report must be generated in the Spreadsheet Document.

### Adding Syntax to be evaluated by GroupDocs.Assembly Engine

**In-cell List**

```java
"We provide support for the following clients:
<<foreach [in getClients()]>><<[numberOf()]>>.         <<[getName()]>>
<</foreach>>"
```

**Multiple-cell List**

```java
<<foreach [in getClients()]>><<[numberOf()]>>.         <<[getName()]>>
<</foreach>>
```

### Download Numbered List Template

Please download the sample Numbered List document we created in this article:

*   [Numbered List.xlsx](https://github.com/groupdocs-assembly/GroupDocs.Assembly-for-Java/blob/master/Examples/GroupDocs.Assembly.Examples.Java/Data/Storage/Spreadsheet%20Templates/Numbered%20List.xlsx?raw=true)

### Generating The Report

{{< gist GroupDocsGists 19dd8c9db2f1f07b67608a2caac732cf >}}

### ODS Template and Report in Apache OpenOffice

In order to check compatibility of ODS between Microsoft Office 2010 and Apache OpenOffice 4.1.2, we performed below tests:

*   We opened the ODS template created through Microsoft Office 2010 in Apache OpenOffice 4.1.2. The template opened successfully in Apache OpenOffice without any issues or formatting losses.
*   We opened the ODS report generated through GroupDocs.Assembly in Apache OpenOffice 4.1.2. The report opened successfully in Apache OpenOffice without any issues or formatting losses.
