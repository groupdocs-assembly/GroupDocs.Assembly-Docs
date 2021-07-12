---
id: single-row-image-in-html-document
url: assembly/java/single-row-image-in-html-document
title: Single Row Image in HTML Document
weight: 4
description: ""
keywords: 
productName: GroupDocs.Assembly for Java
hideChildren: False
---
{{< alert style="info" >}}In this article, we will use GroupDocs.Assembly to generate a Single Row Image report in HTML Document format.{{< /alert >}}{{< alert style="info" >}}The code uses some of the objects defined in [The Business Layer](https://docs.groupdocs.com/assembly/java/the-business-layer/).{{< /alert >}}

## Single Row Image in HTML Document

### Reporting Requirement

As a report developer, you are required to represent information of first single manager with the following key requirements:

*   Report must show image of the manager
*   It must show Name and age of manager
*   Report must be generated in the HTML Document.

### Adding Syntax to be evaluated by GroupDocs.Assembly Engine

<table><tbody><tr><td><img height="100" width="100" src="data:image/jpeg;base64,<<[FileUtil.getBytesAsBase64(manager.getPhoto())]>>"></td><td><table><tbody><tr><td><b>Name:</b></td><td><b>&lt;&lt;[manager.getName()]&gt;&gt;</b></td></tr><tr><td><b>Age:</b></td><td>&lt;&lt;[manager.getAge()]&gt;&gt;</td></tr></tbody></table></td></tr></tbody></table>
### Download Single Row Image Template

Please download the sample template we created in this article:

*   [Single Row Image.html](https://github.com/groupdocs-assembly/GroupDocs.Assembly-for-Java/blob/master/Examples/GroupDocs.Assembly.Examples.Java/Data/Storage/Html%20Templates/Single%20Row.html?raw=true)

### Generating The Report

{{< gist GroupDocsGists ea903857e3ebcd9ad615f829caa0feb5 >}}


