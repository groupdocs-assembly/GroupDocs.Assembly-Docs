---
id: barcode-image-generation-in-word-processing-document
url: assembly/java/barcode-image-generation-in-word-processing-document
title: Barcode Image Generation in Word Processing Document
weight: 2
description: ""
keywords: 
productName: GroupDocs.Assembly for Java
hideChildren: False
---
{{< alert style="info" >}}The code uses some of the objects defined in [The Business Layer](https://docs.groupdocs.com/assembly/java/the-business-layer/).{{< /alert >}}

## Barcode Generation in Microsoft Word

### Template Syntax

*   Add a textbox to your template at the place where you want a barcode image to be inserted.
*   Add the following syntax:

```java
<<barcode [value] -itf6>>
```

#### Download Template

Get the template from here.

*   [Barcode.docx](https://github.com/groupdocs-assembly/GroupDocs.Assembly-for-Java/blob/master/Examples/GroupDocs.Assembly.Examples.Java/Data/Storage/Word%20Templates/Barcode.docx?raw=true)

### The Code

{{< gist GroupDocsGists 5a251b4914b8781cff6502c51e3ceb36 >}}


