---
id: barcode-image-generation-in-presentation-document
url: assembly/java/barcode-image-generation-in-presentation-document
title: Barcode Image Generation in Presentation Document
weight: 4
description: ""
keywords: 
productName: GroupDocs.Assembly for Java
hideChildren: False
---
{{< alert style="info" >}}The code uses some of the objects defined in [The Business Layer](https://docs.groupdocs.com/assembly/java/the-business-layer/).{{< /alert >}}

## Barcode Generation in Microsoft PowerPoint

### Template Syntax

*   Add a textbox to your template at the place where you want a barcode image to be inserted.
*   Add the following syntax:

```java
<<barcode [value] -itf6>>
```

### Download Template

Get the template from here.

*   [Barcode.pptx](https://github.com/groupdocs-assembly/GroupDocs.Assembly-for-Java/blob/master/Examples/GroupDocs.Assembly.Examples.Java/Data/Storage/Presentation%20Templates/Barcode.pptx?raw=true)

### The Code

{{< gist GroupDocsGists e6892938d4cad17c877cafb4b6ce2997 >}}


