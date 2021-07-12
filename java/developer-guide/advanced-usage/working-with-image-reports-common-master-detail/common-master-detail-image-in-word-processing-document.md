---
id: common-master-detail-image-in-word-processing-document
url: assembly/java/common-master-detail-image-in-word-processing-document
title: Common Master-Detail Image in Word Processing Document
weight: 1
description: ""
keywords: 
productName: GroupDocs.Assembly for Java
hideChildren: False
---
{{< alert style="info" >}}In this article, we will use GroupDocs.Assembly to generate a Common Master-Detail Image report in Word Processing Document format.{{< /alert >}}{{< alert style="info" >}}The code uses some of the objects defined in [The Business Layer](https://docs.groupdocs.com/assembly/java/the-business-layer/).{{< /alert >}}

## Common Master-Detail Image in Microsoft Word Document

### Creating a Common Master-Detail Image

Please follow below steps you can create Common Master-Detail Template in MS Word 2013.

1.  Insert a desired shape to display image in it.
2.  Go to Insert Tab and select shape by clicking on Shape Icon.
3.  Save your Document.

### Reporting Requirement

As a report developer, you are required to represent the information of the managers and clients with the following key requirements:

*   Report must show managers' picture and name.
*   It must associate the managers with their clients.
*   Report must be generated in the Word Processing Document.

### Adding Syntax to be evaluated by GroupDocs.Assembly Engine

```java
<<foreach [in getManagers()]
>> >" style="outline: 0px !important;">
<<[getName()]>>
Clients: <<foreach [in getContracts()]>><<[indexOf() != 0 ? ", " : ""]>><<[getClient().getName()]>><</foreach>>
 
<</foreach>>
```

### Download Common Master-DetailTemplate

Please download the sample Common Master-Detail document we created in this article:

*   [Common Master-Detail.docx](https://github.com/groupdocs-assembly/GroupDocs.Assembly-for-Java/blob/master/Examples/GroupDocs.Assembly.Examples.Java/Data/Storage/Word%20Templates/Common%20Master-Detail.docx?raw=true)

### Generating The Report

{{< gist GroupDocsGists ba824939d097cefaa3ba6ee6de30f9d5 >}}

### ODT Template and Report in Apache OpenOffice

In order to check compatibility of ODT between Microsoft Office 2010 and Apache OpenOffice 4.1.2, we performed below tests:

*   We opened the ODT template created through Microsoft Office 2010 in Apache OpenOffice 4.1.2. The template opened successfully in Apache OpenOffice without any issues or formatting losses.
*   We opened the ODT report generated through GroupDocs.Assembly in Apache OpenOffice 4.1.2. The report opened successfully in Apache OpenOffice without any issues or formatting losses.
