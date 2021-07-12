---
id: common-list-image-in-presentation-document
url: assembly/java/common-list-image-in-presentation-document
title: Common List Image in Presentation Document
weight: 3
description: ""
keywords: 
productName: GroupDocs.Assembly for Java
hideChildren: False
---
{{< alert style="info" >}}In this article, we will use GroupDocs.Assembly to generate a Common List Image report in Presentation Document format.{{< /alert >}}{{< alert style="info" >}}The code uses some of the objects defined in [The Business Layer](https://docs.groupdocs.com/assembly/java/the-business-layer/).{{< /alert >}}

## Common List in Microsoft PowerPoint Document

### Creating a Common List Image

Please follow below steps to create Common List Template in MS PowerPoint 2013:

1.  Create a new presentation slide.
2.  Add two shapes to hold pictures and name.
3.  Save your Document.

### Reporting Requirement

As a report developer, you are required to represent the following key requirements:

*   Report must show multiple managers' name.
*   Report must be generated in the Presentation Document.

### Adding Syntax to be evaluated by GroupDocs.Assembly Engine

{{< alert style="warning" >}}There is no way to use image inside a foreach tag in Microsoft PowerPoint.{{< /alert >}}

```java
<<foreach [in getManagers()]>><<[getName()]>>
<</foreach>>
```

### Download Template

Please download the sample Common List document we created in this article:

*   [Common List.pptx](https://github.com/groupdocs-assembly/GroupDocs.Assembly-for-Java/blob/master/Examples/GroupDocs.Assembly.Examples.Java/Data/Storage/Presentation%20Templates/Common%20List.pptx?raw=true)

### Generating The Report

{{< gist GroupDocsGists 4e08200953c3248b654b62ce0b72ad56 >}}

### ODP Template and Report in Apache OpenOffice

In order to check compatibility of ODP between Microsoft Office 2010 and Apache OpenOffice 4.1.2, we performed below tests:

*   We opened the ODP template created through Microsoft Office 2010 in Apache OpenOffice 4.1.2. The template opened successfully in Apache OpenOffice without any issues or formatting losses.

*   We opened the ODP report generated through GroupDocs.Assembly in Apache OpenOffice 4.1.2. The report opened successfully in Apache OpenOffice without any issues or formatting losses.
