---
id: common-list-image-in-text-document
url: assembly/java/common-list-image-in-text-document
title: Common List Image in Text Document
weight: 5
description: ""
keywords: 
productName: GroupDocs.Assembly for Java
hideChildren: False
---
{{< alert style="info" >}}In this article, we will use GroupDocs.Assembly to generate a Common List report in Text Document format.{{< /alert >}}{{< alert style="info" >}}The code uses some of the objects defined in [The Business Laye](https://docs.groupdocs.com/assembly/java/the-business-layer/)r.{{< /alert >}}

## Common List in Text Document

### Reporting Requirement

As a report developer, you are required to share the following key requirements:

*   Report must show multiple managers' picture and name.
*   Report must be generated in the Text Document format.

### Adding Syntax to be evaluated by GroupDocs.Assembly Engine

{{< alert style="warning" >}}Inserting Images Dynamically is not Supported yet{{< /alert >}}

```java
<<foreach [in getManagers()]>><<[getName()]>>
<</foreach>>
```

### Download Common List Template

Please download the sample Common List document we created in this article:

*   [Common List.txt](https://github.com/groupdocs-assembly/GroupDocs.Assembly-for-Java/blob/master/Examples/GroupDocs.Assembly.Examples.Java/Data/Storage/Text%20Templates/Common%20List.txt?raw=true)

### Generating The Report

{{< gist GroupDocsGists d0cefcf2965923335faed6d91207a1af >}}


