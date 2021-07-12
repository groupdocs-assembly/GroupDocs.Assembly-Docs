---
id: bulleted-list-in-text-document
url: assembly/java/bulleted-list-in-text-document
title: Bulleted List in Text Document
weight: 5
description: ""
keywords: 
productName: GroupDocs.Assembly for Java
hideChildren: False
---
{{< alert style="info" >}}In this article, we will use GroupDocs.Assembly to generate a Bulleted List report in Text Document format.{{< /alert >}}{{< alert style="info" >}}The code uses some of the objects defined in [The Business Layer](https://docs.groupdocs.com/assembly/java/the-business-layer/).{{< /alert >}}

## Bulleted List in Text Document

### Reporting Requirement

As a report developer, you are required to share the following key requirements:

*   Report must show all the clients in a bulleted list format.
*   Report must be generated in the Text Document.

### Adding Syntax to be evaluated by GroupDocs.Assembly Engine

```java
We provide support for the following clients:
<<foreach [in getClients()]>>•	<<[getName()]>>
<</foreach>>
```

### Download Bulleted List Template

Please download the sample Bulleted List document we created in this article:

*   [Bulleted List.txt](https://raw.githubusercontent.com/groupdocs-assembly/GroupDocs.Assembly-for-Java/master/Examples/GroupDocs.Assembly.Examples.Java/Data/Storage/Text%20Templates/Bulleted%20List.txt?raw=true)

### Generating The Report

{{< gist GroupDocsGists 0117f3b3de47b8d3d417283937eb9caa >}}


