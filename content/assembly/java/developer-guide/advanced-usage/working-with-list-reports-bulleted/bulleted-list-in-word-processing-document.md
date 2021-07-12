---
id: bulleted-list-in-word-processing-document
url: assembly/java/bulleted-list-in-word-processing-document
title: Bulleted List in Word Processing Document
weight: 1
description: ""
keywords: 
productName: GroupDocs.Assembly for Java
hideChildren: False
---
{{< alert style="info" >}}In this article, we will use GroupDocs.Assembly to generate a Bulleted List report in Word Processing Document format.{{< /alert >}}{{< alert style="info" >}}The code uses some of the objects defined in [The Business Layer](https://docs.groupdocs.com/assembly/java/the-business-layer/).{{< /alert >}}

## Bulleted List in Microsoft Word Document

### Creating a Bulleted List

Practising the following steps you can insert Bulleted List in MS Word 2013.

1.  Add a bullet list at the place where you want it.
2.  Save your Document.

### Reporting Requirement

As a report developer, you are required to share the following key requirements:

*   Report must show all the clients in a bulleted list format.
*   Report must be generated in the Word Processing Document.

### Adding Syntax to be evaluated by GroupDocs.Assembly Engine

**Template Syntax**

```java
We provide support for the following clients:
•<<foreach [in getClients()]>><<[getName()]>>
<</foreach>>
```

### Download Bulleted List Template

Please download the sample Bulleted List document we created in this article:

*   [Bulleted List.docx](https://github.com/groupdocs-assembly/GroupDocs.Assembly-for-Java/blob/master/Examples/GroupDocs.Assembly.Examples.Java/Data/Storage/Word%20Templates/Bulleted%20List.docx?raw=true)

### Generating The Report

{{< gist GroupDocsGists 0d492aa10208d139d02c698495c6ae63 >}}

### ODT Template and Report in Apache OpenOffice

In order to check compatibility of ODT between Microsoft Office 2010 and Apache OpenOffice 4.1.2, we performed below tests:

*   We opened the ODT template created through Microsoft Office 2010 in Apache OpenOffice 4.1.2. The template opened successfully in Apache OpenOffice without any issues or formatting losses.
*   We opened the ODT report generated through GroupDocs.Assembly in Apache OpenOffice 4.1.2. The report opened successfully in Apache OpenOffice without any issues or formatting losses.
