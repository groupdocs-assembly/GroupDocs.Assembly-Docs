---
id: bulleted-list-in-spreadsheet-document
url: assembly/java/bulleted-list-in-spreadsheet-document
title: Bulleted List in Spreadsheet Document
weight: 2
description: ""
keywords: 
productName: GroupDocs.Assembly for Java
hideChildren: False
---
{{< alert style="info" >}}In this article, we will use GroupDocs.Assembly to generate a Bulleted List report in Spreadsheet Document format.{{< /alert >}}{{< alert style="info" >}}The code uses some of the objects defined in [The Business Layer](https://docs.groupdocs.com/assembly/java/the-business-layer/).{{< /alert >}}

## Bulleted List in Microsoft Excel Document

### Creating a Bulleted List

Practising the following steps you can insert Bulleted List in MS Excel 2013.  
Adding a bulleted list in Microsoft Excel is different than Microsoft Word. Moreover, there are two ways to apply bulleted list in Microsoft Excel:

*   In-Cell List
*   Multiple-Cell List

Apply the following steps to build the In-Cell template

1.  Add a new Workbook.
2.  Press Insert Tab (at the top-bar).
3.  Add bullet symbol by clicking on Symbol icon.
4.  Save the Document.

### Reporting Requirement

As a report developer, you are required to share the following key requirements:

*   Report must show all the clients in a bulleted list format.
*   Report must be generated in the Spreadsheet Document.

### Adding Syntax to be evaluated by GroupDocs.Assembly Engine

**In-Cell List**

```java
We provide support for the following clients:
<<foreach [in getClients()]>>
-          <<[getName()]>><</foreach>>
```

**Multiple-Cell List**

```java
We provide support for the following products:
<<foreach [in getClients()]>>-          <<[getName()]>>
```

close the foreach loop in next column

```java
<</foreach>>
```

### Download Bulleted List Template

Please download the sample Bulleted List document we created in this article:

*   [Bulleted List.xlsx](https://github.com/groupdocs-assembly/GroupDocs.Assembly-for-Java/blob/master/Examples/GroupDocs.Assembly.Examples.Java/Data/Storage/Spreadsheet%20Templates/Bulleted%20List.xlsx?raw=true)

### Generating The Report

{{< gist GroupDocsGists 3c2c2bfddda742a41fb86345a768415e >}}

### ODS Template and Report in Apache OpenOffice

In order to check compatibility of ODS between Microsoft Office 2010 and Apache OpenOffice 4.1.2, we performed below tests:

*   We opened the ODS template created through Microsoft Office 2010 in Apache OpenOffice 4.1.2. The template opened successfully in Apache OpenOffice without any issues or formatting losses.
*   We opened the ODS report generated through GroupDocs.Assembly in Apache OpenOffice 4.1.2. The report opened successfully in Apache OpenOffice without any issues or formatting losses.
