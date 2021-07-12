---
id: bulleted-list-in-html-document
url: assembly/java/bulleted-list-in-html-document
title: Bulleted List in HTML Document
weight: 4
description: ""
keywords: 
productName: GroupDocs.Assembly for Java
hideChildren: False
---
{{< alert style="info" >}}In this article, we will use GroupDocs.Assembly to generate a Bulleted List report in HTML Document format.{{< /alert >}}{{< alert style="info" >}}The code uses some of the objects defined in [The Business Layer](https://docs.groupdocs.com/assembly/java/the-business-layer/).{{< /alert >}}

## Bulleted List in HTML Document

### Reporting Requirement

As a report developer, you are required to share the following key requirements:

*   Report must show all the clients in a bulleted list format.
*   Report must be generated in the HTML Document.

### Adding Syntax to be evaluated by GroupDocs.Assembly Engine

```java
We provide support for the following clients:
<ul>
&lt;&lt;foreach [in getClients()]&gt;&gt;
<li>&lt;&lt;[getName()]&gt;&gt;</li>
&lt;&lt;/foreach&gt;&gt;
</ul>
Regular text. <span style="background-color:orange">Highlighted text.</span>
```

### Download Bulleted List Template

Please download the sample Bulleted List document we created in this article:

*   [Bulleted List.html](https://github.com/groupdocs-assembly/GroupDocs.Assembly-for-Java/blob/master/Examples/GroupDocs.Assembly.Examples.Java/Data/Storage/Html%20Templates/Bulleted%20List.html?raw=true)

### Generating The Report

{{< gist GroupDocsGists b42b6ec6de4351826d7886fe3e701a0d >}}


