---
id: in-paragraph-list-in-email-document
url: assembly/java/in-paragraph-list-in-email-document
title: In-Paragraph List in Email Document
weight: 6
description: ""
keywords: 
productName: GroupDocs.Assembly for Java
hideChildren: False
---
{{< alert style="info" >}}In this article, we will use GroupDocs.Assembly to generate a In-Paragraph List report in Email Document format.{{< /alert >}}

## In-Paragraph List in Email Document

### Reporting Requirement

As a report developer, you are required to share the following key requirements:

*   Report must be in .eml or .msg format.
*   It must add email recipient, css and subject of the email.
*   A descriptive or informative line like "We provide support for the following clients:".
*   Show all the clients along with the above sentence.

### Adding Syntax to be evaluated by GroupDocs.Assembly Engine

```java
We provide support for the following clients: <<foreach [in getClients()]>><<[indexOf() != 0 ? ", " : ""]>><<[getName()]>><</foreach>>
```

### Download In-Paragraph List Template

Please download the sample Common List document we created in this article:

*   [In-Paragraph List.eml](https://raw.githubusercontent.com/groupdocs-assembly/GroupDocs.Assembly-for-Java/master/Examples/GroupDocs.Assembly.Examples.Java/Data/Storage/Email%20Templates/Bulleted%20List.eml?raw=true)

### Generating The Report

{{< alert style="info" >}}The code uses some of the objects defined in: [The Business Layer](https://docs.groupdocs.com/assembly/java/the-business-layer/){{< /alert >}}{{< gist samicheemagroupdocs 3ff4323ee0af247c4d071c002294dff6 >}}
