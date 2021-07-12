---
id: single-row-image-in-email-document
url: assembly/java/single-row-image-in-email-document
title: Single Row Image in Email Document
weight: 6
description: ""
keywords: 
productName: GroupDocs.Assembly for Java
hideChildren: False
---
{{< alert style="info" >}}In this article, we will use GroupDocs.Assembly to generate a Single Row Image report in Email Document format.{{< /alert >}}

## Single Row Image in Email Document

### Reporting Requirement

As a report developer, you are required to represent information of first single manager with the following key requirements:

*   Report must be in .eml or .msg format.
*   It must add email recipient, css and subject of the email.
*   Report must show image of the manager
*   It must show Name and age of manager

### Adding Syntax to be evaluated by GroupDocs.Assembly Engine

{{< alert style="warning" >}}Inserting Images Dynamically is not Supported yet{{< /alert >}}

```java
Name:	<<[manager.getName()]>>
Age:	<<[manager.getAge()]>>
```

### Download Single Row Image Template

Please download the sample template we created in this article:

*   [Single Row Image.eml](https://raw.githubusercontent.com/groupdocs-assembly/GroupDocs.Assembly-for-Java/master/Examples/GroupDocs.Assembly.Examples.Java/Data/Storage/Email%20Templates/Bulleted%20List.eml?raw=true)

### Generating The Report

{{< alert style="info" >}}The code uses some of the objects defined in: [The Business Layer](https://docs.groupdocs.com/assembly/java/the-business-layer/){{< /alert >}}{{< gist samicheemagroupdocs e39e429b95be8b91f06b1a7716d748e1 >}}


