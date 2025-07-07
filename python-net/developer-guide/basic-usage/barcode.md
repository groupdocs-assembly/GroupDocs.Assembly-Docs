---
id: barcode
url: assembly/python-net/barcode
title: Generate sample report for document with variable
weight: 1
description: ""
keywords: 
productName: GroupDocs.Assembly for Python via .NET
hideChildren: False
---

## Adding Syntax to be evaluated by GroupDocs.Assembly Engine

**Template Syntax**

```python
assembler = ga.DocumentAssembler()
dataSource = ga.data.XmlDataSource("datasource.xml")
DataSourceInfo = ga.DataSourceInfo(dataSource)
array = [DataSourceInfo]
print(assembler.assemble_document(input.ppt, output.ppt, array))
```

**DataSource XML**
```xml
<Product>
    <Discount>0</Discount>
    <ProductID>1</ProductID>
    <ProductName>LG Nexus 5</ProductName>
    <ProductPrice>350</ProductPrice>
    <UnitsInStock>5</UnitsInStock>
	<Barcode>123456789qwertyu0025</Barcode>
  </Product>
```

## The Recipe

*   Set up the source document data path
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
