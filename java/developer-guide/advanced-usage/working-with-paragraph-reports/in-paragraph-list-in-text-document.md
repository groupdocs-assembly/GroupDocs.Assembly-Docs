---
id: in-paragraph-list-in-text-document
url: assembly/java/in-paragraph-list-in-text-document
title: In-Paragraph List in Text Document
weight: 5
description: ""
keywords: 
productName: GroupDocs.Assembly for Java
hideChildren: False
---
{{< alert style="info" >}}In this article, we will use GroupDocs.Assembly to generate In-ParagraphList report in Text Document format.{{< /alert >}}{{< alert style="info" >}}The code uses some of the objects defined in [The Business Layer](https://docs.groupdocs.com/assembly/java/the-business-layer/).{{< /alert >}}

## In-Paragraph List in Text Document

### Reporting Requirement

As a report developer, you are required to share the following key requirements:

*   A descriptive or informative line like "We provide support for the following clients:".
*   Show all the clients along with the above sentence.
*   Report must be generated in the Text Document.

### Adding Syntax to be evaluated by GroupDocs.Assembly Engine

```java
We provide support for the following clients: <<foreach [in getClients()]>><<[indexOf() != 0 ? ", " : ""]>><<[getName()]>><</foreach>>
```

### Download In-Paragraph List Template

Please download the sample Common List document we created in this article:

*   [In-Paragraph List.txt](https://github.com/groupdocs-assembly/GroupDocs.Assembly-for-Java/blob/master/Examples/GroupDocs.Assembly.Examples.Java/Data/Storage/Text%20Templates/In-Paragraph%20List.txt?raw=true)

### Generating The Report

{{< gist GroupDocsGists 8e24e27b32ab5037fd289eb89343b9c9 >}}


