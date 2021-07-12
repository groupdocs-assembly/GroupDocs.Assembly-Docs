---
id: common-master-detail-image-in-html-document
url: assembly/java/common-master-detail-image-in-html-document
title: Common Master-Detail Image in HTML Document
weight: 4
description: ""
keywords: 
productName: GroupDocs.Assembly for Java
hideChildren: False
---
{{< alert style="info" >}}In this article, we will use GroupDocs.Assembly to generate a Common Master-Detail report in HTML Document format.{{< /alert >}}{{< alert style="info" >}}The code uses some of the objects defined in [The Business Layer](https://docs.groupdocs.com/assembly/java/the-business-layer/).{{< /alert >}}

## Common Master-Detail Image in HTML Document

### Reporting Requirement

As a report developer, you are required to represent the information of the managers and clients with the following key requirements:

*   Report must show managers' picture and name.
*   It must associate the managers with their clients.
*   Report must be generated in the HTML Document.

### Adding Syntax to be evaluated by GroupDocs.Assembly Engine

```java
<<foreach [in getManagers()]
>> 
<<[getName()]>>
Clients: <<foreach [in getContracts()]>><<[indexOf() != 0 ? ", " : ""]>><<[getClient().getName()]>><</foreach>>
<</foreach>>
```

### Download Common Master-Detail Template

Please download the sample Common master-detail document we created in this article:

*   [Common Master-Detail.html](https://github.com/groupdocs-assembly/GroupDocs.Assembly-for-Java/blob/master/Examples/GroupDocs.Assembly.Examples.Java/Data/Storage/Html%20Templates/Common%20Master-Detail.html?raw=true)

### Generating The Report

{{< gist GroupDocsGists 4ac39db9865f7602818752db5e01a57e >}}


