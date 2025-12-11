---
id: assembly-basic-usage-first-document
url: assembly/net/basic-usage-first-document
title: Generate Your First Document from .NET Object in C#
weight: 2
description: "Create your first document by generating a simple report from an in-memory .NET object using GroupDocs.Assembly for .NET."
keywords: generate document, create report, first example, .NET object, C#, assemble, compose, build document
productName: GroupDocs.Assembly for .NET
toc: True
---

## Overview

This guide walks you through creating your first document with GroupDocs.Assembly for .NET. You'll generate a simple document from an in-memory .NET object, demonstrating the basic workflow of template-based document assembly.

The main classes involved are:
- [DocumentAssembler](https://reference.groupdocs.com/assembly/net/groupdocs.assembly/documentassembler/) - the main class for assembling documents
- [DataSourceInfo](https://reference.groupdocs.com/assembly/net/groupdocs.assembly/datasourceinfo/) - wraps data source objects with optional names

Here are the steps to generate your first document:

* Create a simple .NET class with properties to represent your data
* Instantiate the class and populate it with sample data
* Create a template document (DOCX) with expression tags referencing the object properties
* Use DocumentAssembler to assemble the template with your data object
* Save the assembled document to a file

## Define a Simple Data Class

First, create a simple class to hold your data:

```csharp
public class Person
{
    public string Name { get; set; }
    public int Age { get; set; }
    public string Email { get; set; }
}
```

## Generate Document from Object

Now, create a method to generate a document from this object:

```csharp
using GroupDocs.Assembly;
using System;

public static void GenerateFirstDocument()
{
    // Create sample data
    Person person = new Person
    {
        Name = "John Doe",
        Age = 30,
        Email = "john.doe@example.com"
    };
    
    // Paths for template and output
    string templatePath = "Template.docx";
    string outputPath = "Output.docx";
    
    // Assemble the document
    DocumentAssembler assembler = new DocumentAssembler();
    assembler.AssembleDocument(templatePath, outputPath, 
        new DataSourceInfo(person, "person"));
    
    Console.WriteLine($"Document generated successfully: {outputPath}");
}
```

## Template Document Example

Your template document (Template.docx) should contain expression tags like this:

```
Name: <<[person.Name]>>
Age: <<[person.Age]>>
Email: <<[person.Email]>>
```

After assembly, the output will be:

```
Name: John Doe
Age: 30
Email: john.doe@example.com
```

## Using Contextual Object Member Access

You can also use contextual member access, which allows you to omit the data source name in simple scenarios:

```csharp
public static void GenerateDocumentWithContextualAccess()
{
    Person person = new Person
    {
        Name = "Jane Smith",
        Age = 28,
        Email = "jane.smith@example.com"
    };
    
    DocumentAssembler assembler = new DocumentAssembler();
    // When using contextual access, you can omit the data source name
    assembler.AssembleDocument("Template.docx", "Output.docx", 
        new DataSourceInfo(person));
}
```

With contextual access, your template can use:

```
Name: <<[Name]>>
Age: <<[Age]>>
Email: <<[Email]>>
```

{{< alert style="info" >}}
When using contextual object member access, the template expressions can reference properties directly without the data source name prefix. This is useful for simple, single-object scenarios.
{{< /alert >}}

### Advanced Usage Topics

To learn more about working with complex data structures, multiple data sources, and advanced template syntax, please refer to the [advanced usage section]({{< ref "assembly/net/developer-guide/advanced-usage/_index.md" >}}).

## More resources

### GitHub Examples

You may easily run the code above and see the feature in action in our GitHub examples:

* [GroupDocs.Assembly for .NET examples, plugins, and showcase](https://github.com/groupdocs-assembly/GroupDocs.Assembly-for-.NET)
* [GroupDocs.Assembly for Java examples, plugins, and showcase](https://github.com/groupdocs-assembly/GroupDocs.Assembly-for-Java)
* [GroupDocs.Assembly for Python via .NET examples, plugins, and showcase](https://github.com/groupdocs-assembly/GroupDocs.Assembly-for-Python-via-.NET)

### Free Online Apps

Along with the full-featured .NET library, we provide simple but powerful free online apps.

To assemble documents from templates and data sources, you can use the online apps from the **[GroupDocs.Assembly App Product Family](https://products.groupdocs.app/assembly/family)**.

