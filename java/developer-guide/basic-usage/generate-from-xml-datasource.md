---
id: assembly-basic-usage-xml-datasource-java
url: assembly/java/basic-usage-xml-datasource
linktitle: Generate from XML
title: Generate Document from XML Data Source
weight: 7
description: "Create reports from XML data sources using XmlDataSource class to load and bind XML data to templates in Java applications."
keywords: XML data source, XmlDataSource, XML binding, parse XML, generate from XML, assemble XML, compose from XML
productName: GroupDocs.Assembly for Java
hideChildren: False
---

## Overview

GroupDocs.Assembly for Java provides the `XmlDataSource` class to work with XML data directly in templates. Unlike using DataSet, XmlDataSource automatically recognizes data types (numbers, dates, booleans) from XML, making it easier to perform calculations and formatting.

The main classes involved are:
- [XmlDataSource](https://reference.groupdocs.com/assembly/java/com.groupdocs.assembly/xmldatasource/) - loads and parses XML data
- [DocumentAssembler](https://reference.groupdocs.com/assembly/java/com.groupdocs.assembly/documentassembler/) - assembles documents
- [XmlDataLoadOptions](https://reference.groupdocs.com/assembly/java/com.groupdocs.assembly/xmldataloadoptions/) - configures XML loading behavior

Here are the steps to generate documents from XML:

* Create or obtain XML data (from file, string, or stream)
* Instantiate XmlDataSource with the XML data
* Create a template document with expression tags referencing XML elements
* Use DocumentAssembler to assemble the template with XmlDataSource
* Save the assembled document

{{< alert style="info" >}}
XmlDataSource automatically recognizes integer, floating-point, boolean, and date-time values from XML strings, enabling numeric operations and date formatting in templates without explicit type conversion.
{{< /alert >}}

## Generate Document from XML File

The simplest way to use XML data is from a file:

```java
import com.groupdocs.assembly.*;

public static void generateFromXmlFile() throws Exception
{
    XmlDataSource xmlDataSource = new XmlDataSource("data.xml");

    DocumentAssembler assembler = new DocumentAssembler();
    assembler.assembleDocument("Template.docx", "Output.docx",
        new DataSourceInfo(xmlDataSource, "data"));
}
```

## XML File Example

Your XML file (data.xml) might look like this:

```xml
<Person>
    <Name>John Doe</Name>
    <Age>30</Age>
    <Birth>1989-04-01 4:00:00 pm</Birth>
    <Email>john.doe@example.com</Email>
</Person>
```

## Template Example for XML Object

For the XML above, your template can reference elements directly:

```
Name: <<[data.Name]>>
Age: <<[data.Age]>>
Date of Birth: <<[data.Birth]:"dd.MM.yyyy">>
Email: <<[data.Email]>>
```

## Generate Document from XML String

The `String` parameter of the `XmlDataSource` constructor is a file path. To use XML content held in a string, wrap it into an `InputStream`:

```java
import com.groupdocs.assembly.*;
import java.io.*;
import java.nio.charset.StandardCharsets;

public static void generateFromXmlString() throws Exception
{
    String xmlString = "<Person>"
        + "<Name>Jane Smith</Name>"
        + "<Age>28</Age>"
        + "<Birth>1992-01-31 07:00:00 am</Birth>"
        + "<Email>jane.smith@example.com</Email>"
        + "</Person>";

    try (InputStream xmlStream = new ByteArrayInputStream(xmlString.getBytes(StandardCharsets.UTF_8)))
    {
        XmlDataSource xmlDataSource = new XmlDataSource(xmlStream);

        DocumentAssembler assembler = new DocumentAssembler();
        assembler.assembleDocument("Template.docx", "Output.docx",
            new DataSourceInfo(xmlDataSource, "person"));
    }
}
```

## Working with XML Arrays

When your XML root contains an array of elements, XmlDataSource treats it as a collection:

```java
import com.groupdocs.assembly.*;
import java.io.*;
import java.nio.charset.StandardCharsets;

public static void generateFromXmlArray() throws Exception
{
    String xmlArray = "<Persons>"
        + "<Person><Name>John Doe</Name><Age>30</Age></Person>"
        + "<Person><Name>Jane Smith</Name><Age>28</Age></Person>"
        + "<Person><Name>Bob Johnson</Name><Age>35</Age></Person>"
        + "</Persons>";

    try (InputStream xmlStream = new ByteArrayInputStream(xmlArray.getBytes(StandardCharsets.UTF_8)))
    {
        XmlDataSource xmlDataSource = new XmlDataSource(xmlStream);

        DocumentAssembler assembler = new DocumentAssembler();
        assembler.assembleDocument("Template.docx", "Output.docx",
            new DataSourceInfo(xmlDataSource, "persons"));
    }
}
```

## Template Example for XML Array

For XML arrays, use a foreach data band:

```
<<foreach [in persons]>>
Name: <<[Name]>>, Age: <<[Age]>>
<</foreach>>

Average age: <<[persons.average(p => p.Age)]>>
```

## Working with Nested XML Elements

XmlDataSource handles nested XML structures automatically:

```java
import com.groupdocs.assembly.*;
import java.io.*;
import java.nio.charset.StandardCharsets;

public static void generateFromNestedXml() throws Exception
{
    String nestedXml = "<Company>"
        + "<Name>ABC Corp</Name>"
        + "<Address>"
        + "<Street>123 Main St</Street>"
        + "<City>New York</City>"
        + "<Zip>10001</Zip>"
        + "</Address>"
        + "<Employees>"
        + "<Employee><Name>John Doe</Name><Position>Developer</Position></Employee>"
        + "<Employee><Name>Jane Smith</Name><Position>Manager</Position></Employee>"
        + "</Employees>"
        + "</Company>";

    try (InputStream xmlStream = new ByteArrayInputStream(nestedXml.getBytes(StandardCharsets.UTF_8)))
    {
        XmlDataSource xmlDataSource = new XmlDataSource(xmlStream);

        DocumentAssembler assembler = new DocumentAssembler();
        assembler.assembleDocument("Template.docx", "Output.docx",
            new DataSourceInfo(xmlDataSource, "company"));
    }
}
```

Template for nested XML (only the root element can be skipped, so the `Employee` elements are accessed through their `Employees` parent):

```
Company: <<[company.Name]>>
Address: <<[company.Address.Street]>>, <<[company.Address.City]>> <<[company.Address.Zip]>>

Employees:
<<foreach [in company.Employees.Employee]>>
- <<[Name]>>, <<[Position]>>
<</foreach>>
```

## Configure XML Data Load Options

You can configure how XmlDataSource parses XML:

```java
import com.groupdocs.assembly.*;

public static void generateWithXmlOptions() throws Exception
{
    XmlDataLoadOptions options = new XmlDataLoadOptions();
    options.setAlwaysGenerateRootObject(true); // Always create root object

    XmlDataSource xmlDataSource = new XmlDataSource("data.xml", options);

    DocumentAssembler assembler = new DocumentAssembler();
    assembler.assembleDocument("Template.docx", "Output.docx",
        new DataSourceInfo(xmlDataSource, "data"));
}
```

{{< alert style="warning" >}}
By default, if a root XML element contains only a sequence of elements of one type, the engine skips the root object. Call `setAlwaysGenerateRootObject(true)` to always include it. For example, with this option the persons from the array above are accessed as `<<foreach [in persons.Person]>>` instead of `<<foreach [in persons]>>`.
{{< /alert >}}

### Advanced Usage Topics

To learn more about working with XML schemas, complex XML structures, XML attributes, and advanced XmlDataSource options, please refer to the [advanced usage section]({{< ref "assembly/java/developer-guide/advanced-usage/_index.md" >}}).

## More resources

### GitHub Examples

You may easily run the code above and see the feature in action in our GitHub examples:

* [GroupDocs.Assembly for Java examples, plugins, and showcase](https://github.com/groupdocs-assembly/GroupDocs.Assembly-for-Java)
* [GroupDocs.Assembly for .NET examples, plugins, and showcase](https://github.com/groupdocs-assembly/GroupDocs.Assembly-for-.NET)
* [GroupDocs.Assembly for Python via .NET examples, plugins, and showcase](https://github.com/groupdocs-assembly/GroupDocs.Assembly-for-Python-via-.NET)

### Free Online Apps

Along with the full-featured Java library, we provide simple but powerful free online apps.

To assemble documents from templates and data sources, you can use the online apps from the **[GroupDocs.Assembly App Product Family](https://products.groupdocs.app/assembly/family)**.
