---
id: single-row-image-in-presentation-document
url: assembly/java/single-row-image-in-presentation-document
title: Single Row Image in Presentation Document
weight: 3
description: ""
keywords: 
productName: GroupDocs.Assembly for Java
hideChildren: False
---
{{< alert style="info" >}}In this article, we will use GroupDocs.Assembly to generate a Single Row Image report in Presentation Document format.{{< /alert >}}{{< alert style="info" >}}The code uses some of the objects defined in [The Business Layer](https://docs.groupdocs.com/assembly/java/the-business-layer/).{{< /alert >}}

## Single Row in Microsoft PowerPoint Document

### Creating a Single Row

Please follow below steps to create Single Row Image in MS PowerPoint 2013:

1.  Creat a new presentation slide.
2.  Insert a desired shape to display image in it.
3.  Go to Insert Tab and select shape by clicking on Shape Icon.
4.  Write "Name" and "Age" to show name and age info of the customer.
5.  Save the template.

### Reporting Requirement

As a report developer, you are required to represent information of first single manager with the following key requirements:

*   Report must show image of the manager
*   It must show Name and age of manager
*   Report must be generated in the Presentation Document.

### Adding Syntax to be evaluated by GroupDocs.Assembly Engine

{{< alert style="warning" >}}At the moment, GroupDocs.Assembly does not support images in PowerPoint Presentation.{{< /alert >}}

```java
Name:	<<[manager.getName()]>>
Age:	<<[manager.getAge()]>>
```

### Download Single Row Template

Please download the sample Single Row document we created in this article:

*   [Single Row.pptx](https://github.com/groupdocs-assembly/GroupDocs.Assembly-for-Java/blob/master/Examples/GroupDocs.Assembly.Examples.Java/Data/Storage/Presentation%20Templates/Single%20Row.pptx?raw=true)

### Generating The Report

{{< gist GroupDocsGists f20a9bbba651eb9e04988200853531e1 >}}

### ODP Template and Report in Apache OpenOffice

In order to check compatibility of ODP between Microsoft Office 2010 and Apache OpenOffice 4.1.2, we performed below tests:

*   We opened the ODP template created through Microsoft Office 2010 in Apache OpenOffice 4.1.2. The template opened successfully in Apache OpenOffice without any issues or formatting losses.
*   We opened the ODP report generated through GroupDocs.Assembly in Apache OpenOffice 4.1.2. The report opened successfully in Apache OpenOffice without any issues or formatting losses.
