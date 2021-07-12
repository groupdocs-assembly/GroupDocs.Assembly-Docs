---
id: common-master-detail-image-in-text-document
url: assembly/java/common-master-detail-image-in-text-document
title: Common Master-Detail Image in Text Document
weight: 5
description: ""
keywords: 
productName: GroupDocs.Assembly for Java
hideChildren: False
---
{{< alert style="info" >}}In this article, we will use GroupDocs.Assembly to generate a Common Master-Detail report in Text Document format.{{< /alert >}}{{< alert style="info" >}}The code uses some of the objects defined in [The Business Layer](https://docs.groupdocs.com/assembly/java/the-business-layer/).{{< /alert >}}

## Common Master-Detail Image in Text Document

### Reporting Requirement

As a report developer, you are required to represent the information of the managers and clients with the following key requirements:

*   Report must show managers' picture and name.
*   It must associate the managers with their clients.
*   Report must be generated in the Text Document.

### Adding Syntax to be evaluated by GroupDocs.Assembly Engine

{{< alert style="warning" >}}Inserting Images Dynamically is not Supported yet{{< /alert >}}

```java
<<foreach [in getManagers()]>><<[getName()]>>
Clients: <<foreach [in getContracts()]>><<[indexOf() != 0 ? ", " : ""]>><<[getClient().getName()]>><</foreach>>
<</foreach>>
```

### Download Common Master-Detail Template

Please download the sample Common master-detail document we created in this article:

*   [Common Master-Detail.txt](https://github.com/groupdocs-assembly/GroupDocs.Assembly-for-Java/blob/master/Examples/GroupDocs.Assembly.Examples.Java/Data/Storage/Text%20Templates/Common%20Master-Detail.txt?raw=true)

### Generating The Report

{{< gist GroupDocsGists d4a29bbe5042d0da99c3de6117bc1c77 >}}


