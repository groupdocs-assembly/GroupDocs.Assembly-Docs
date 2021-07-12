---
id: numbered-list-in-text-document
url: assembly/java/numbered-list-in-text-document
title: Numbered List in Text Document
weight: 5
description: ""
keywords: 
productName: GroupDocs.Assembly for Java
hideChildren: False
---
{{< alert style="info" >}}In this article, we will use GroupDocs.Assembly to generate a Numbered List report in Text Document format.{{< /alert >}}{{< alert style="info" >}}The code uses some of the objects defined in The Business Layer.{{< /alert >}}

## Numbered List in Text Document

### Reporting Requirement

As a report developer, you are required to represent the following key requirements:

*   Report must show the client names in a numbered list.
*   Report must be generated in the Text document.

### Adding Syntax to be evaluated by GroupDocs.Assembly Engine

```java
We provide support for the following clients:
<<foreach [in getClients()]>><<[numberOf()]>>. <<[getName()]>>
<</foreach>>
```

### Download Numbered List Template

Please download the sample template we created in this article:

*   [Numbered List.txt](https://github.com/groupdocs-assembly/GroupDocs.Assembly-for-Java/blob/master/Examples/GroupDocs.Assembly.Examples.Java/Data/Storage/Text%20Templates/Numbered%20List.txt?raw=true)

### Generating The Report

{{< gist GroupDocsGists d25321fd5b1fe937a42fc607c3ad0c00 >}}


