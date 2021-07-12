---
id: bulleted-list-in-email-document
url: assembly/java/bulleted-list-in-email-document
title: Bulleted List in Email Document
weight: 6
description: ""
keywords: 
productName: GroupDocs.Assembly for Java
hideChildren: False
---
{{< alert style="info" >}}In this article, we will use GroupDocs.Assembly to generate a Bulleted List report in Email format.{{< /alert >}}

## Reporting Requirement

As a report developer, you are required to share the following key requirements:

*   Report must be in .eml or .msg format.
*   It must add email recipient, css and subject of the email.
*   Report must show all the clients in a bulleted list format.

## Adding Syntax to be evaluated by GroupDocs.Assembly Engine

### Recipients, Cc and Subject

```java
<<foreach [r in recipients]>><<[r]>>; <</foreach>>
<<[cc]>>
<<[subject]>>
```

### Body

```java
We provide support for the following clients:
<<foreach [in getClients()]>>•	<<[getName()]>>
<</foreach>>
```

## Download Bulleted List Template

Please download the sample Bulleted List document we created in this article:

*   [Bulleted List.eml](https://raw.githubusercontent.com/groupdocs-assembly/GroupDocs.Assembly-for-Java/master/Examples/GroupDocs.Assembly.Examples.Java/Data/Storage/Email%20Templates/Bulleted%20List.eml?raw=true)

## Generating The Report

{{< alert style="info" >}}The code uses some of the objects defined in: The Business Layer{{< /alert >}}{{< gist samicheemagroupdocs e61f2df361bc042a989380c1fdc20435 >}}


