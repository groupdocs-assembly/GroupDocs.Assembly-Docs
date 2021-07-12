---
id: common-list-image-in-html-document
url: assembly/java/common-list-image-in-html-document
title: Common List Image in HTML Document
weight: 4
description: ""
keywords: 
productName: GroupDocs.Assembly for Java
hideChildren: False
---
{{< alert style="info" >}}In this article, we will use GroupDocs.Assembly to generate a Common List report in HTML Document format.{{< /alert >}}{{< alert style="info" >}}The code uses some of the objects defined in [The Business Layer](https://docs.groupdocs.com/assembly/java/the-business-layer/).{{< /alert >}}

## Common List in HTML Document

### Reporting Requirement

As a report developer, you are required to share the following key requirements:

*   Report must show multiple managers' picture and name.
*   Report must be generated in the HTML Document format.

### Adding Syntax to be evaluated by GroupDocs.Assembly Engine

```java
<<foreach [in getManagers()]>> <<image [getPhoto()]>>
<<[getName()]>>
<</foreach>>
```

### Download Common List Template

Please download the sample Common List document we created in this article:

*   [Common List.html](https://github.com/groupdocs-assembly/GroupDocs.Assembly-for-Java/blob/master/Examples/GroupDocs.Assembly.Examples.Java/Data/Storage/Html%20Templates/Common%20List.html?raw=true)

### Generating The Report

{{< gist GroupDocsGists 729966c553a7ce2b543d244a2183018d >}}


