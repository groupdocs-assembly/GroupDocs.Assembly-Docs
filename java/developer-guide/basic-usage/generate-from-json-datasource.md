---
id: assembly-basic-usage-json-datasource-java
url: assembly/java/basic-usage-json-datasource
linktitle: Generate from JSON
title: Generate Document from JSON Data Source
weight: 8
description: "Build documents from JSON data sources using JsonDataSource class to load and bind JSON data to templates in Java applications."
keywords: JSON data source, JsonDataSource, JSON binding, parse JSON, generate from JSON, compose JSON, assemble JSON
productName: GroupDocs.Assembly for Java
hideChildren: False
---

## Overview

GroupDocs.Assembly for Java enables you to generate documents directly from JSON data sources. The `JsonDataSource` class automatically parses JSON and makes it available to your templates, supporting both simple and complex JSON structures.

The main classes involved are:
- [JsonDataSource](https://reference.groupdocs.com/assembly/java/com.groupdocs.assembly/jsondatasource/) - loads and parses JSON data
- [DocumentAssembler](https://reference.groupdocs.com/assembly/java/com.groupdocs.assembly/documentassembler/) - assembles documents from templates
- [DataSourceInfo](https://reference.groupdocs.com/assembly/java/com.groupdocs.assembly/datasourceinfo/) - wraps the data source

Here are the steps to generate documents from JSON:

* Create or obtain JSON data (from file, API, or string)
* Instantiate JsonDataSource with the JSON data
* Create a template document with expression tags referencing JSON properties
* Use DocumentAssembler to assemble the template with JsonDataSource
* Save the assembled document

{{< alert style="info" >}}
JsonDataSource automatically recognizes JSON types (numbers, booleans, dates, strings) and makes them available with proper types in templates, enabling numeric operations and date formatting.
{{< /alert >}}

## Generate Document from JSON File

The simplest way to use JSON data is from a file:

```java
import com.groupdocs.assembly.*;

public static void generateFromJsonFile() throws Exception
{
    JsonDataSource jsonDataSource = new JsonDataSource("data.json");

    DocumentAssembler assembler = new DocumentAssembler();
    assembler.assembleDocument("Template.docx", "Output.docx",
        new DataSourceInfo(jsonDataSource, "data"));
}
```

## Generate Document from JSON String

The `String` parameter of the `JsonDataSource` constructor is a file path. To use JSON content held in a string, wrap it into an `InputStream`:

```java
import com.groupdocs.assembly.*;
import java.io.*;
import java.nio.charset.StandardCharsets;

public static void generateFromJsonString() throws Exception
{
    String jsonString = "{"
        + "\"name\": \"John Doe\","
        + "\"age\": 30,"
        + "\"email\": \"john.doe@example.com\","
        + "\"active\": true"
        + "}";

    try (InputStream jsonStream = new ByteArrayInputStream(jsonString.getBytes(StandardCharsets.UTF_8)))
    {
        JsonDataSource jsonDataSource = new JsonDataSource(jsonStream);

        DocumentAssembler assembler = new DocumentAssembler();
        assembler.assembleDocument("Template.docx", "Output.docx",
            new DataSourceInfo(jsonDataSource, "person"));
    }
}
```

## Working with JSON Arrays

When your JSON root is an array, JsonDataSource treats it as a collection:

```java
import com.groupdocs.assembly.*;
import java.io.*;
import java.nio.charset.StandardCharsets;

public static void generateFromJsonArray() throws Exception
{
    String jsonArray = "["
        + "{ \"name\": \"John\", \"age\": 30 },"
        + "{ \"name\": \"Jane\", \"age\": 28 },"
        + "{ \"name\": \"Bob\", \"age\": 35 }"
        + "]";

    try (InputStream jsonStream = new ByteArrayInputStream(jsonArray.getBytes(StandardCharsets.UTF_8)))
    {
        JsonDataSource jsonDataSource = new JsonDataSource(jsonStream);

        DocumentAssembler assembler = new DocumentAssembler();
        assembler.assembleDocument("Template.docx", "Output.docx",
            new DataSourceInfo(jsonDataSource, "people"));
    }
}
```

## Template Example for JSON Object

For a JSON object like `{"name": "John", "age": 30}`, your template can reference properties directly:

```
Name: <<[data.name]>>
Age: <<[data.age]>>
```

## Template Example for JSON Array

For a JSON array, use a foreach data band to iterate:

```
<<foreach [in people]>>
Name: <<[name]>>, Age: <<[age]>>
<</foreach>>
```

## Working with Nested JSON Objects

JsonDataSource handles nested JSON structures automatically:

```java
import com.groupdocs.assembly.*;
import java.io.*;
import java.nio.charset.StandardCharsets;

public static void generateFromNestedJson() throws Exception
{
    String nestedJson = "{"
        + "\"company\": \"ABC Corp\","
        + "\"address\": {"
        + "    \"street\": \"123 Main St\","
        + "    \"city\": \"New York\","
        + "    \"zip\": \"10001\""
        + "},"
        + "\"employees\": ["
        + "    { \"name\": \"John\", \"position\": \"Developer\" },"
        + "    { \"name\": \"Jane\", \"position\": \"Manager\" }"
        + "]"
        + "}";

    try (InputStream jsonStream = new ByteArrayInputStream(nestedJson.getBytes(StandardCharsets.UTF_8)))
    {
        JsonDataSource jsonDataSource = new JsonDataSource(jsonStream);

        DocumentAssembler assembler = new DocumentAssembler();
        assembler.assembleDocument("Template.docx", "Output.docx",
            new DataSourceInfo(jsonDataSource, "company"));
    }
}
```

Template for nested JSON:

```
Company: <<[company.company]>>
Address: <<[company.address.street]>>, <<[company.address.city]>> <<[company.address.zip]>>

Employees:
<<foreach [in company.employees]>>
- <<[name]>>, <<[position]>>
<</foreach>>
```

## Configure JSON Data Load Options

You can configure how JsonDataSource parses JSON:

```java
import com.groupdocs.assembly.*;

public static void generateWithJsonOptions() throws Exception
{
    JsonDataLoadOptions options = new JsonDataLoadOptions();
    options.setAlwaysGenerateRootObject(true); // Always create root object
    options.setSimpleValueParseMode(JsonSimpleValueParseMode.STRICT); // Strict type parsing

    JsonDataSource jsonDataSource = new JsonDataSource("data.json", options);

    DocumentAssembler assembler = new DocumentAssembler();
    assembler.assembleDocument("Template.docx", "Output.docx",
        new DataSourceInfo(jsonDataSource, "data"));
}
```

In the default `JsonSimpleValueParseMode.LOOSE` mode, the types of JSON simple values are determined by parsing their string representations, so a string such as `"42"` becomes a number. In the `STRICT` mode, the types are determined by the JSON notation, so `"42"` remains a string.

{{< alert style="warning" >}}
By default, if a root JSON element is an object with only one property that is an object or array, the engine skips the root object. Call `setAlwaysGenerateRootObject(true)` to always include it.
{{< /alert >}}

### Advanced Usage Topics

To learn more about working with complex JSON structures, date-time parsing, and advanced JsonDataSource options, please refer to the [advanced usage section]({{< ref "assembly/java/developer-guide/advanced-usage/_index.md" >}}).

## More resources

### GitHub Examples

You may easily run the code above and see the feature in action in our GitHub examples:

* [GroupDocs.Assembly for Java examples, plugins, and showcase](https://github.com/groupdocs-assembly/GroupDocs.Assembly-for-Java)
* [GroupDocs.Assembly for .NET examples, plugins, and showcase](https://github.com/groupdocs-assembly/GroupDocs.Assembly-for-.NET)
* [GroupDocs.Assembly for Python via .NET examples, plugins, and showcase](https://github.com/groupdocs-assembly/GroupDocs.Assembly-for-Python-via-.NET)

### Free Online Apps

Along with the full-featured Java library, we provide simple but powerful free online apps.

To assemble documents from templates and data sources, you can use the online apps from the **[GroupDocs.Assembly App Product Family](https://products.groupdocs.app/assembly/family)**.
