---
id: assembly-basic-usage-first-document-java
url: assembly/java/basic-usage-first-document
linktitle: Generate Your First Document
title: Generate Your First Document from Java Object
weight: 2
description: "Create your first document by generating a simple report from an in-memory Java object using GroupDocs.Assembly for Java."
keywords: generate document, create report, first example, Java object, POJO, Java, assemble, compose, build document
productName: GroupDocs.Assembly for Java
hideChildren: False
---

## Overview

This guide walks you through creating your first document with GroupDocs.Assembly for Java. You'll generate a simple document from an in-memory Java object, demonstrating the basic workflow of template-based document assembly.

The main classes involved are:
- [DocumentAssembler](https://reference.groupdocs.com/assembly/java/com.groupdocs.assembly/documentassembler/) - the main class for assembling documents
- [DataSourceInfo](https://reference.groupdocs.com/assembly/java/com.groupdocs.assembly/datasourceinfo/) - wraps data source objects with optional names

Here are the steps to generate your first document:

* Create a simple public Java class with getters to represent your data
* Instantiate the class and populate it with sample data
* Create a template document (DOCX) with expression tags calling the object's getters
* Use DocumentAssembler to assemble the template with your data object
* Save the assembled document to a file

## Define a Simple Data Class

First, create a simple class to hold your data:

```java
public class Person
{
    private String name;
    private int age;
    private String email;

    public String getName() { return name; }
    public void setName(String value) { this.name = value; }
    public int getAge() { return age; }
    public void setAge(int value) { this.age = value; }
    public String getEmail() { return email; }
    public void setEmail(String value) { this.email = value; }
}
```

{{< alert style="info" >}}
The data class must be public. Otherwise, the engine rejects it as a data source with the "A data source object must be of a visible type" error.
{{< /alert >}}

## Generate Document from Object

Now, create a method to generate a document from this object:

```java
import com.groupdocs.assembly.*;

public static void generateFirstDocument() throws Exception
{
    // Create sample data
    Person person = new Person();
    person.setName("John Doe");
    person.setAge(30);
    person.setEmail("john.doe@example.com");

    // Paths for template and output
    String templatePath = "Template.docx";
    String outputPath = "Output.docx";

    // Assemble the document
    DocumentAssembler assembler = new DocumentAssembler();
    assembler.assembleDocument(templatePath, outputPath,
        new DataSourceInfo(person, "person"));

    System.out.println("Document generated successfully: " + outputPath);
}
```

## Template Document Example

Your template document (Template.docx) should contain expression tags like this:

```
Name: <<[person.getName()]>>
Age: <<[person.getAge()]>>
Email: <<[person.getEmail()]>>
```

After assembly, the output will be:

```
Name: John Doe
Age: 30
Email: john.doe@example.com
```

{{< alert style="info" >}}
Members of Java objects are accessed in templates by calling their public methods, such as getters (`person.getName()`). A property-like reference such as `person.Name` does not work for Java objects.
{{< /alert >}}

## Using Contextual Object Member Access

You can also use contextual member access, which allows you to omit the data source name in simple scenarios:

```java
public static void generateDocumentWithContextualAccess() throws Exception
{
    Person person = new Person();
    person.setName("Jane Smith");
    person.setAge(28);
    person.setEmail("jane.smith@example.com");

    DocumentAssembler assembler = new DocumentAssembler();
    // When using contextual access, you can omit the data source name
    assembler.assembleDocument("Template.docx", "Output.docx",
        new DataSourceInfo(person));
}
```

With contextual access, your template can use:

```
Name: <<[getName()]>>
Age: <<[getAge()]>>
Email: <<[getEmail()]>>
```

{{< alert style="info" >}}
When using contextual object member access, the template expressions can call the object's methods directly without the data source name prefix. This is useful for simple, single-object scenarios.
{{< /alert >}}

### Advanced Usage Topics

To learn more about working with complex data structures, multiple data sources, and advanced template syntax, please refer to the [advanced usage section]({{< ref "assembly/java/developer-guide/advanced-usage/_index.md" >}}).

## More resources

### GitHub Examples

You may easily run the code above and see the feature in action in our GitHub examples:

* [GroupDocs.Assembly for Java examples, plugins, and showcase](https://github.com/groupdocs-assembly/GroupDocs.Assembly-for-Java)
* [GroupDocs.Assembly for .NET examples, plugins, and showcase](https://github.com/groupdocs-assembly/GroupDocs.Assembly-for-.NET)
* [GroupDocs.Assembly for Python via .NET examples, plugins, and showcase](https://github.com/groupdocs-assembly/GroupDocs.Assembly-for-Python-via-.NET)

### Free Online Apps

Along with the full-featured Java library, we provide simple but powerful free online apps.

To assemble documents from templates and data sources, you can use the online apps from the **[GroupDocs.Assembly App Product Family](https://products.groupdocs.app/assembly/family)**.
