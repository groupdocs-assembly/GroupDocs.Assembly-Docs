---
id: in-paragraph-list-in-word-processing-document
url: assembly/java/in-paragraph-list-in-word-processing-document
title: In-Paragraph List in Word Processing Document
weight: 1
description: ""
keywords: 
productName: GroupDocs.Assembly for Java
hideChildren: False
---
{{< alert style="info" >}}In this article, we will use GroupDocs.Assembly to generate a In-ParagraphList report in Word Processing Document format.{{< /alert >}}{{< alert style="info" >}}The code uses some of the objects defined in [The Business Layer](https://docs.groupdocs.com/assembly/java/the-business-layer/).{{< /alert >}}

## In-Paragraph List in Microsoft Word Document

### Creating a In-Paragraph List

Practising the following steps you can create In-Paragraph List Template in MS Word 2013.

1.  Write a sentence, for example, "We provide support for the following clients:".
2.  Save the template.

### Reporting Requirement

As a report developer, you are required to describe about the clients with the following key requirements:

*   A descriptive or informative line like "We provide support for the following clients:".
*   Show all the clients along with the above sentence.
*   Report must be generated in the Word Processing Document.

### Adding Syntax to be evaluated by GroupDocs.Assembly Engine

```java
We provide support for the following clients: <<foreach [in getClients()]>>
<<[indexOf() != 0 ? ", " : ""]>><<[getName()]>><</foreach>>
```

### Download In-Paragraph List Template

Please download the sample In-Paragraph List document we created in this article:

*   [In-Paragraph List.docx](https://github.com/groupdocs-assembly/GroupDocs.Assembly-for-Java/blob/master/Examples/GroupDocs.Assembly.Examples.Java/Data/Storage/Word%20Templates/In-Paragraph%20List.docx?raw=true)

### Generating The Report

{{< gist GroupDocsGists f3761bb8dd9ededf05862d904c90c2c9 >}}

### ODT Template and Report in Apache OpenOffice

In order to check compatibility of ODT between Microsoft Office 2010 and Apache OpenOffice 4.1.2, we performed below tests:

*   We opened the ODT template created through Microsoft Office 2010 in Apache OpenOffice 4.1.2. The template opened successfully in Apache OpenOffice without any issues or formatting losses.
*   We opened the ODT report generated through GroupDocs.Assembly in Apache OpenOffice 4.1.2. The report opened successfully in Apache OpenOffice without any issues or formatting losses.
