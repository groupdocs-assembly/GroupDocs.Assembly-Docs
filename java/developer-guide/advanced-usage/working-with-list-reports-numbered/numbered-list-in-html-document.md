---
id: numbered-list-in-html-document
url: assembly/java/numbered-list-in-html-document
title: Numbered List in HTML Document
weight: 4
description: ""
keywords: 
productName: GroupDocs.Assembly for Java
hideChildren: False
---
{{< alert style="info" >}}In this article, we will use GroupDocs.Assembly to generate a Numbered List report in HTML Document format.{{< /alert >}}{{< alert style="info" >}}The code uses some of the objects defined in [The Business Layer](https://docs.groupdocs.com/assembly/java/the-business-layer/).{{< /alert >}}

## Numbered List in HTML Document

### Reporting Requirement

As a report developer, you are required to represent the following key requirements:

*   Report must show the client names in a numbered list.
*   Report must be generated in the HTML document.

### Adding Syntax to be evaluated by GroupDocs.Assembly Engine

We provide support for the following clients:
```
   <<foreach \[in getClients()\]>>
1.  <<\[getName()\]>>
   <</foreach>>
```

### Download Numbered List Template

Please download the sample template we created in this article:

*   [Numbered List.html](https://github.com/groupdocs-assembly/GroupDocs.Assembly-for-Java/blob/master/Examples/GroupDocs.Assembly.Examples.Java/Data/Storage/Html%20Templates/Numbered%20List.html?raw=true)

### Generating The Report

{{< gist GroupDocsGists c5f6caf241562d1ad4a58ccd708adfae >}}


