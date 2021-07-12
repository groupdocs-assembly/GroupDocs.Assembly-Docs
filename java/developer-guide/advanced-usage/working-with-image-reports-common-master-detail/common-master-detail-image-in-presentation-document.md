---
id: common-master-detail-image-in-presentation-document
url: assembly/java/common-master-detail-image-in-presentation-document
title: Common Master-Detail Image in Presentation Document
weight: 3
description: ""
keywords: 
productName: GroupDocs.Assembly for Java
hideChildren: False
---
{{< alert style="info" >}}In this article, we will use GroupDocs.Assembly to generate a Common Master-Detail report in Presentation Document format.{{< /alert >}}{{< alert style="info" >}}The code uses some of the objects defined in [The Business Layer](https://docs.groupdocs.com/assembly/java/the-business-layer/).{{< /alert >}}

## Common Master-Detail in Microsoft PowerPoint Document

### Creating a Common Master-Detail

Please follow below steps to create Common Master-Detail Template in MS PowerPoint 2013:

1.  Create a new Presentation.
2.  Insert two shapes, one for holding image and other for holding other details.  
    
    #Save the document.

### Reporting Requirement

As a report developer, you are required to represent the information of the managers and clients with the following key requirements:

*   Report must show managers' picture and name.
*   It must associate the managers with their clients.
*   Report must be generated in the Presentation Document.

### Adding Syntax to be evaluated by GroupDocs.Assembly Engine

```java
<<foreach [in getManagers()]>>Manager: <<[getName()]>>
Clients: <<foreach [in getContracts()]>><<[indexOf() != 0 ? ", " : ""]>>
<<[getClient().getName()]>><</foreach>>
<</foreach>>
```

### Download Common Master-Detail Template

Please download the sample Common Master-Detail document we created in this article:

*   [Common Master-Detail.pptx](https://github.com/groupdocs-assembly/GroupDocs.Assembly-for-Java/blob/master/Examples/GroupDocs.Assembly.Examples.Java/Data/Storage/Presentation%20Templates/Common%20Master-Detail.pptx?raw=true)

### Generating The Report

{{< gist GroupDocsGists fbe130505d1b084c64b66835338c3688 >}}

### ODP Template and Report in Apache OpenOffice

In order to check compatibility of ODP between Microsoft Office 2010 and Apache OpenOffice 4.1.2, we performed below tests:

*   We opened the ODP template created through Microsoft Office 2010 in Apache OpenOffice 4.1.2. The template opened successfully in Apache OpenOffice without any issues or formatting losses.
*   We opened the ODP report generated through GroupDocs.Assembly in Apache OpenOffice 4.1.2. The report opened successfully in Apache OpenOffice without any issues or formatting losses.
