---
id: multicolored-numbered-list-in-html-document
url: assembly/java/multicolored-numbered-list-in-html-document
title: Multicolored Numbered List in HTML Document
weight: 4
description: ""
keywords: 
productName: GroupDocs.Assembly for Java
hideChildren: False
---
{{< alert style="info" >}}In this article, we will use GroupDocs.Assembly to generate a Multicolored Numbered List report in HTML Document format.{{< /alert >}}

## Multicolored Numbered List in HTML Document

### Reporting Requirement

As a report developer, you are required to represent the following key requirements:

*   Report must show the clients in numbered list.
*   It must highlight the products.
*   Report must be generated in the HTML Document.

### Adding Syntax to be evaluated by GroupDocs.Assembly Engine

```java
We provide support for the following clients:
<ol>
&lt;&lt;foreach [in getClients()]&gt;&gt;
<li &lt;&lt;if [indexOf() % 2 == 0]&gt;&gt;style="background-color:#FFF8DC"&lt;&lt;/if&gt;&gt;>&lt;&lt;[getName()]&gt;&gt;</li>
&lt;&lt;/foreach&gt;&gt;
</ol>
```

### Download Multicolored Numbered List Template

Please download the sample template we created in this article:

*   [Multicolored Numbered List.html](https://github.com/groupdocs-assembly/GroupDocs.Assembly-for-Java/blob/master/Examples/GroupDocs.Assembly.Examples.Java/Data/Storage/Html%20Templates/Multicolored%20Numbered%20List.html?raw=true)

### Generating The Report

{{< alert style="info" >}}The code uses some of the objects defined in: [The Business Layer](https://docs.groupdocs.com/assembly/java/the-business-layer/){{< /alert >}}{{< gist atirtahirgroupdocs c511abcfb4a85dba94fb95091a6e014a >}}


