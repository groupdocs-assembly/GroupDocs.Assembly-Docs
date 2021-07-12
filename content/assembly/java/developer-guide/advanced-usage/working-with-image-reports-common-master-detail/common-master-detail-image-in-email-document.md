---
id: common-master-detail-image-in-email-document
url: assembly/java/common-master-detail-image-in-email-document
title: Common Master-Detail Image in Email Document
weight: 6
description: ""
keywords: 
productName: GroupDocs.Assembly for Java
hideChildren: False
---
{{< alert style="info" >}}In this article, we will use GroupDocs.Assembly to generate a Common Master-Detail report in Email Document format.{{< /alert >}}

## Common Master-Detail in Email Document

### Creating a Common Master-Detail

Please follow below steps to create Common Master-Detail Template in MS Outlook 2013:

1.  Create a new Email.
2.  Insert two shapes, one for holding image and other for holding other details.
3.  Save the Email.

### Reporting Requirement

As a report developer, you are required to represent the information of the managers and clients with the following key requirements:

*   Report must be in .eml or .msg format.
*   It must add email recipient, css and subject of the email.
*   Report must show manager's picture and name.
*   It must associate the managers with their clients.

### Adding Syntax to be evaluated by GroupDocs.Assembly Engine

{{< alert style="warning" >}}NOTE: Dynamic inserting of images is not supported yet.{{< /alert >}}

```java
<<foreach [in getManagers()]>>Manager: <<[getName()]>>
Clients: <<foreach [in getContracts()]>><<[indexOf() != 0 ? ", " : ""]>>
<<[getClient().getName()]>><</foreach>>
<</foreach>>
```

### Download Common Master-Detail Template

Please download the sample Common Master-Detail document we created in this article:

*   [Common Master-Detail.eml](https://raw.githubusercontent.com/groupdocs-assembly/GroupDocs.Assembly-for-Java/master/Examples/GroupDocs.Assembly.Examples.Java/Data/Storage/Email%20Templates/Bulleted%20List.eml?raw=true)

### Generating The Report

{{< alert style="info" >}}The code uses some of the objects defined in: [The Business Layer](https://docs.groupdocs.com/assembly/java/the-business-layer/){{< /alert >}}{{< gist samicheemagroupdocs c55506d4b7d27cd6d0d29db308fe9d54 >}}
