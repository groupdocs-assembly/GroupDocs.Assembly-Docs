---
id: assembly-basic-usage-first-document
url: assembly/python-net/basic-usage-first-document
linktitle: Generate Your First Document
title: Generate Your First Document from a Python Dict
weight: 2
description: "Create your first document with GroupDocs.Assembly for Python via .NET by generating a simple report from an in-memory Python dict."
keywords: generate document, create report, first example, Python dict, Python, assemble, compose, build document
productName: GroupDocs.Assembly for Python via .NET
hideChildren: False
---

## Overview

This guide walks you through creating your first document with GroupDocs.Assembly for Python via .NET. You'll generate a simple document from an in-memory Python dict, demonstrating the basic workflow of template-based document assembly.

The main classes involved are:
- [DocumentAssembler](https://reference.groupdocs.com/assembly/python-net/groupdocs.assembly/documentassembler/) - the main class for assembling documents
- [DataSourceInfo](https://reference.groupdocs.com/assembly/python-net/groupdocs.assembly/datasourceinfo/) - wraps data source objects with optional names

Here are the steps to generate your first document:

* Describe your data as a Python dict whose keys are the names the template reads
* Populate the dict with sample data
* Create a template document (DOCX) with expression tags referencing the dict's keys
* Use DocumentAssembler to assemble the template with your data
* Save the assembled document to a file

## Describe the Data as a Dict

In Python you do not declare a class for the data. A dict is enough: each key becomes a member the template can read, and the value's Python type decides what the template sees (`str`, `int`, `float`, `decimal.Decimal`, `bool`, `datetime`, nested dicts and lists).

```python
person = {
    "Name": "Amara Osei",
    "Age": 41,
    "Email": "amara.osei@harborlane.example",
}
```

## Generate Document from a Dict

Now, pass the dict to the assembler together with the name the template uses for it:

{{< tabs "example1" >}}
{{< tab "Python" >}}
```python
from groupdocs.assembly import DataSourceInfo, DocumentAssembler

# Create sample data
person = {
    "Name": "Amara Osei",
    "Age": 41,
    "Email": "amara.osei@harborlane.example",
}

# Paths for template and output
template_path = "person-card.docx"
output_path = "person-card-report.docx"

# Assemble the document
assembler = DocumentAssembler()
assembler.assemble_document(template_path, output_path, DataSourceInfo(person, "person"))

print("Document generated successfully:", output_path)
```
{{< /tab >}}
{{< tab "person-card.docx" >}}
{{< tab-text >}}
The following sample file is used in this example: [person-card.docx](/assembly/python-net/_sample_files/developer-guide/basic-usage/generate-first-document/person-card.docx)
{{< /tab-text >}}
{{< /tab >}}
{{< tab "person-card-report.docx" >}}  
```text
Binary file (DOCX, 7 KB)
```
[Download full output](/assembly/python-net/_output_files/developer-guide/basic-usage/generate-first-document/generate_document_from_a_dict/person-card-report.docx)
{{< /tab >}}
{{< /tabs >}}

## Template Document Example

Your template document (person-card.docx) should contain expression tags like this:

```text
Name: <<[person.Name]>>
Age: <<[person.Age]>>
Email: <<[person.Email]>>
```

After assembly, the output will be:

```text
Name: Amara Osei
Age: 41
Email: amara.osei@harborlane.example
```

## Using Contextual Object Member Access

You can also use contextual member access, which allows you to omit the data source name in simple scenarios:

{{< tabs "example2" >}}
{{< tab "Python" >}}
```python
from groupdocs.assembly import DataSourceInfo, DocumentAssembler

person = {
    "Name": "Lena Park",
    "Age": 29,
    "Email": "lena.park@harborlane.example",
}

assembler = DocumentAssembler()
# When using contextual access, you can omit the data source name
assembler.assemble_document("person-card-contextual.docx", "person-card-contextual-report.docx",
                            DataSourceInfo(person))
```
{{< /tab >}}
{{< tab "person-card-contextual.docx" >}}
{{< tab-text >}}
The following sample file is used in this example: [person-card-contextual.docx](/assembly/python-net/_sample_files/developer-guide/basic-usage/generate-first-document/person-card-contextual.docx)
{{< /tab-text >}}
{{< /tab >}}
{{< tab "person-card-contextual-report.docx" >}}  
```text
Binary file (DOCX, 7 KB)
```
[Download full output](/assembly/python-net/_output_files/developer-guide/basic-usage/generate-first-document/using_contextual_object_member_access/person-card-contextual-report.docx)
{{< /tab >}}
{{< /tabs >}}

With contextual access, your template can use:

```text
Name: <<[Name]>>
Age: <<[Age]>>
Email: <<[Email]>>
```

{{< alert style="info" >}}
When using contextual object member access, the template expressions can reference the dict's keys directly without the data source name prefix. This is useful for simple, single-object scenarios. A template that still names the source (`<<[person.Name]>>`) fails when the source has no name: the engine looks for a `person` key in the dict.
{{< /alert >}}

### Advanced Usage Topics

To learn more about working with complex data structures, multiple data sources, and advanced template syntax, please refer to the [advanced usage section]({{< ref "assembly/python-net/developer-guide/advanced-usage/_index.md" >}}).

## More resources

### GitHub Examples

You may easily run the code above and see the feature in action in our GitHub examples:

* [GroupDocs.Assembly for .NET examples, plugins, and showcase](https://github.com/groupdocs-assembly/GroupDocs.Assembly-for-.NET)
* [GroupDocs.Assembly for Java examples, plugins, and showcase](https://github.com/groupdocs-assembly/GroupDocs.Assembly-for-Java)
* [GroupDocs.Assembly for Python via .NET examples, plugins, and showcase](https://github.com/groupdocs-assembly/GroupDocs.Assembly-for-Python-via-.NET)

### Free Online Apps

Along with the full-featured library, we provide simple but powerful free online apps.

To assemble documents from templates and data sources, you can use the online apps from the **[GroupDocs.Assembly App Product Family](https://products.groupdocs.app/assembly/family)**.
