---
id: adding-next-field-into-template-syntax
url: assembly/java/adding-next-field-into-template-syntax
title: Adding NEXT Field into Template Syntax
weight: 30
description: ""
keywords: 
productName: GroupDocs.Assembly for Java
hideChildren: False
---
{{< alert style="info" >}}The code uses some of the objects defined in [The Business Layer](https://docs.groupdocs.com/assembly/java/the-business-layer/).{{< /alert >}}

## Adding Syntax to be evaluated by GroupDocs.Assembly Engine

**Template Syntax**

```java
We provide support for the following clients:
•	<<foreach [in getClients()]>><<next>><<[getName()]>>
<</foreach>>
```

## The Recipe

*   Set up the source document template path
*   Set up destination report path
*   Instantiate DocumentAssembler class
*   Generate report

### Download Template

Get the template from here:

*   [Using next.docx](https://github.com/groupdocs-assembly/GroupDocs.Assembly-for-Java/blob/master/Examples/GroupDocs.Assembly.Examples.Java/Data/Storage/Word%20Templates/Using%20next.docx?raw=true)

### The Code

{{< gist GroupDocsGists f5bf95c52059f408b60bd47c1f9c4d7d >}}


