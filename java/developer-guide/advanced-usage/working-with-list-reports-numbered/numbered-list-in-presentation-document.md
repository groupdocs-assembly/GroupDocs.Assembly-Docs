---
id: numbered-list-in-presentation-document
url: assembly/java/numbered-list-in-presentation-document
title: Numbered List in Presentation Document
weight: 3
description: ""
keywords: 
productName: GroupDocs.Assembly for Java
hideChildren: False
---
{{< alert style="info" >}}In this article, we will use GroupDocs.Assembly to generate a Numbered List report in Presentation Document format.{{< /alert >}}{{< alert style="info" >}}The code uses some of the objects defined in [The Business Layer](https://docs.groupdocs.com/assembly/java/the-business-layer/).{{< /alert >}}

## Numbered List in Microsoft PowerPoint Document

### Creating a Numbered List

Practising the following steps you can create Numbered List Template in MS PowerPoint 2013.

1.  Add a new presentation slide.
2.  Write a sentence like "We provide support for the following clients:".
3.  Start numbered list.
4.  Save the template.

### Reporting Requirement

As a report developer, you are required to represent the following key requirements:

*   Report must show the client names in a numbered list.
*   Report must be generated in the Presentation Document.

### Adding Syntax to be evaluated by GroupDocs.Assembly Engine

```java
We provide support for the following clients:
1<<foreach [in getClients()]>><<[getName()]>>
<</foreach>>
```

### Download Numbered List Template

Please download the sample Numbered List document we created in this article:

*   [Numbered List.pptx](https://github.com/groupdocs-assembly/GroupDocs.Assembly-for-Java/blob/master/Examples/GroupDocs.Assembly.Examples.Java/Data/Storage/Presentation%20Templates/Numbered%20List.pptx?raw=true)

### Generating The Report

{{< gist GroupDocsGists 284dcf48c48ab542fcb196cff290ac51 >}}

### ODP Template and Report in Apache OpenOffice

In order to check compatibility of ODP between Microsoft Office 2010 and Apache OpenOffice 4.1.2, we performed below tests:

*   We opened the ODP template created through Microsoft Office 2010 in Apache OpenOffice 4.1.2. The template opened successfully in Apache OpenOffice without any issues or formatting losses.
*   We opened the ODP report generated through GroupDocs.Assembly in Apache OpenOffice 4.1.2. The report opened successfully in Apache OpenOffice without any issues or formatting losses.
