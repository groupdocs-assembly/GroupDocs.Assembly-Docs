---
id: multicolored-numbered-list-in-presentation-document
url: assembly/java/multicolored-numbered-list-in-presentation-document
title: Multicolored Numbered List in Presentation Document
weight: 3
description: ""
keywords: 
productName: GroupDocs.Assembly for Java
hideChildren: False
---
{{< alert style="info" >}}In this article, we will use GroupDocs.Assembly to generate a Multicolored Numbered List report in Presentation Document format.{{< /alert >}}

## Multicolored Numbered List in Microsoft PowerPoint Document

### Creating a Multicolored Numbered List

Practicing the following steps you can create Multicolored Numbered List Template in MS PowerPoint 2013.

1.  In your document, write a sentence like "We provide support for the following clients:".
2.  Start numbered list.
3.  Go to the "Design" tab and select color to make it colored list.
4.  Save the template.

### Reporting Requirement

As a report developer, you are required to represent the following key requirements:

*   Report must show the clients in numbered list.
*   It must highlight the products.
*   Report must be generated in the Presentation Document.

### Adding Syntax to be evaluated by GroupDocs.Assembly Engine

We provide support for the following clients:

<ol>
<li>&lt;&lt;foreach [in getClients()]>>&lt;&lt;if [indexOf() % 2 == 0]>>&lt;&lt;[getName()]>></li>
<li style="background-color: #ceffbc">&lt;&lt;else>>&lt;&lt;[getName()]>></li>
</ol>

​		<</if>><</foreach>>

### Download Multicolored Numbered List Template

Please download the sample Multicolored Numbered List document we created in this article:

*   [Multicolored Numbered List.pptx](https://github.com/groupdocs-assembly/GroupDocs.Assembly-for-Java/blob/master/Examples/GroupDocs.Assembly.Examples.Java/Data/Storage/Presentation%20Templates/Multicolored%20Numbered%20List.pptx?raw=true)

### Generating The Report

{{< alert style="info" >}}The code uses some of the objects defined in: [The Business Layer](){{< /alert >}}{{< gist atirtahirgroupdocs 12b6ec3b323811a352fe887de98e37b7 >}}



### ODP Template and Report in Apache OpenOffice

In order to check compatibility of ODP between Microsoft Office 2010 and Apache OpenOffice 4.1.2, we performed below tests:

*   We opened the ODP template created through Microsoft Office 2010 in Apache OpenOffice 4.1.2. The template opened successfully in Apache OpenOffice without any issues or formatting losses.
*   We opened the ODP report generated through GroupDocs.Assembly in Apache OpenOffice 4.1.2. The report opened successfully in Apache OpenOffice without any issues or formatting losses.
