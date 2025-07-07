---
id: adding-next-field-into-template-syntax
url: assembly/python-net/adding-next-field-into-template-syntax
title: Adding NEXT Field into Template Syntax
weight: 32
description: ""
keywords: 
productName: GroupDocs.Assembly for Python via .NET
hideChildren: False
---
{{< alert style="info" >}}This feature is only compatible with GroupDocs.Assembly for Python via .NET 3.3.0 or later releases.{{< /alert >}}

## Adding Syntax to be evaluated by GroupDocs.Assembly Engine

**Template Syntax**

```python
We provide support for the following products:
. <<foreach [in products]>><<next>><<[ProductName]>>
<</foreach>>
```

## The Recipe

*   Set up the source document template path
*   Set up destination report path
*   Instantiate [DocumentAssembler](https://reference.groupdocs.com/python-net/assembly/groupdocs.assembly/documentassembler) class
*   Generate report

## More resources

### Advanced usage topics

To learn more about library features, please refer to the[advanced usage section]({{< ref "assembly/python-net/developer-guide/advanced-usage/_index.md" >}}).

### GitHub examples

You may easily run the code above and see the feature in action in our GitHub examples:

*   [GroupDocs.Assembly for .NET examples](https://github.com/groupdocs-assembly/GroupDocs.Assembly-for-.NET)
    
*   [GroupDocs.Assembly for Java examples](https://github.com/groupdocs-assembly/GroupDocs.Assembly-for-Java)

*   [GroupDocs.Assembly for Python via .NET examples](https://github.com/groupdocs-assembly/GroupDocs.Assembly-for-Python-via-.NET)
    
