---
id: single-row-image-in-text-document
url: assembly/java/single-row-image-in-text-document
title: Single Row Image in Text Document
weight: 5
description: ""
keywords: 
productName: GroupDocs.Assembly for Java
hideChildren: False
---
{{< alert style="info" >}}In this article, we will use GroupDocs.Assembly to generate a Single Row Image report in Text Document format.{{< /alert >}}{{< alert style="info" >}}The code uses some of the objects defined in [The Business Layer](https://docs.groupdocs.com/assembly/java/the-business-layer/).{{< /alert >}}

## Single Row Image in Text Document

### Reporting Requirement

As a report developer, you are required to represent information of first single manager with the following key requirements:

*   Report must show image of the manager
*   It must show Name and age of manager
*   Report must be generated in the Text Document.

### Adding Syntax to be evaluated by GroupDocs.Assembly Engine

{{< alert style="warning" >}}Inserting Images Dynamically is not Supported yet{{< /alert >}}

```java
Name:	<<[manager.getName()]>>
Age:	<<[manager.getAge()]>>
```

### Download Single Row Image Template

Please download the sample template we created in this article:

*   [Single Row Image.txt](https://github.com/groupdocs-assembly/GroupDocs.Assembly-for-Java/blob/master/Examples/GroupDocs.Assembly.Examples.Java/Data/Storage/Text%20Templates/Single%20Row.txt?raw=true)

### Generating The Report

{{< gist GroupDocsGists c87f4a581ae7d23c97ee3a2c08c8087e >}}


