---
id: multicolored-numbered-list-in-email-document
url: assembly/java/multicolored-numbered-list-in-email-document
title: Multicolored Numbered List in Email Document
weight: 5
description: ""
keywords: 
productName: GroupDocs.Assembly for Java
hideChildren: False
---
{{< alert style="info" >}}In this article, we will use GroupDocs.Assembly to generate a Multicolored Numbered List report in Email Document format.{{< /alert >}}

## Multicolored Numbered List in Email Document

### Creating a Multicolored Numbered List

Practicing the following steps you can create Multicolored Numbered List Template in MS Outlook 2013.

1.  In your email, write a sentence like "We provide support for the following clients:".
2.  Start numbered list.
3.  Go to the "Design" tab and select color to make it colored list.
4.  Save the template.

### Reporting Requirement

As a report developer, you are required to represent the following key requirements:

*   Report must be in .eml or .msg format.
*   It must add email recipient, css and subject of the email.
*   Report must show the clients in numbered list.
*   It must highlight the products.
*   Report must be generated in the Presentation Document.

### Adding Syntax to be evaluated by GroupDocs.Assembly Engine

We provide support for the following clients:

<ol>
<li>&lt;&lt;foreach [in getClients()]>>&lt;&lt;if [indexOf() % 2 == 0]>>      &lt;&lt;[numberOf()]>>.    &lt;&lt;[getName()]>></li>
<li style="background-color: #ffff00">&lt;&lt;else>>      &lt;&lt;[numberOf()]>>.   &lt;&lt;[getName()]>></li>
</ol>

​		<</if>><</foreach>>

### Download Multicolored Numbered List Template

Please download the sample Multicolored Numbered List document we created in this article:

*   [Multicolored Numbered List.eml](https://raw.githubusercontent.com/groupdocs-assembly/GroupDocs.Assembly-for-Java/master/Examples/GroupDocs.Assembly.Examples.Java/Data/Storage/Email%20Templates/Bulleted%20List.eml?raw=true)

### Generating The Report

{{< alert style="info" >}}The code uses some of the objects defined in: [The Business Layer](https://docs.groupdocs.com/assembly/java/the-business-layer/){{< /alert >}}{{< gist samicheemagroupdocs 533045e35a5ec69a56e3e94092e301b6 >}}


