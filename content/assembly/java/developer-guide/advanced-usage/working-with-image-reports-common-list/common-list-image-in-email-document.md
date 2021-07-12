---
id: common-list-image-in-email-document
url: assembly/java/common-list-image-in-email-document
title: Common List Image in Email Document
weight: 6
description: ""
keywords: 
productName: GroupDocs.Assembly for Java
hideChildren: False
---
{{< alert style="info" >}}In this article, we will use GroupDocs.Assembly to generate a Common List report in Email Document format.{{< /alert >}}

## Common List in Email Document

### Reporting Requirement

As a report developer, you are required to share the following key requirements:

*   Report must be in .eml or .msg format.
*   It must add email recipient, css and subject of the email.
*   Report must show multiple managers' picture and name.

### Adding Syntax to be evaluated by GroupDocs.Assembly Engine

{{< alert style="warning" >}}Inserting Images Dynamically is not Supported yet{{< /alert >}}

```java
<<foreach [in getManagers()]>><<[getName()]>>
<</foreach>>
```

### Download Common List Template

Please download the sample Common List document we created in this article:

*   [Common List.eml](https://raw.githubusercontent.com/groupdocs-assembly/GroupDocs.Assembly-for-Java/master/Examples/GroupDocs.Assembly.Examples.Java/Data/Storage/Email%20Templates/Bulleted%20List.eml?raw=true)

### Generating The Report

{{< alert style="info" >}}The code uses some of the objects defined in: The Business Layer{{< /alert >}}{{< gist samicheemagroupdocs f35458abe16581d077174c00c505ff1d >}}


