---
id: email-reports
url: assembly/python-net/email-reports
title: Generate email report with common list.
weight: 2
description: ""
keywords: 
productName: GroupDocs.Assembly for Python via .NET
hideChildren: False
---

## Adding Syntax to be evaluated by GroupDocs.Assembly Engine

**Template Syntax**

```python
assembler = ga.DocumentAssembler()
dataSource = ga.data.JsonDataSource("datasource.json")
DataSourceInfo = ga.DataSourceInfo(dataSource, "customers")
array = [DataSourceInfo, ga.DataSourceInfo(["test@test.mail", "groupdocs@groupdocs.mail"], "recipients"), ga.DataSourceInfo("sender@sender.mail", "sender"), ga.DataSourceInfo("cc@example.com", "cc"), ga.DataSourceInfo("groupdocs", "subject")]
print(assembler.assemble_document("input.msg", "output.msg", array))
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
