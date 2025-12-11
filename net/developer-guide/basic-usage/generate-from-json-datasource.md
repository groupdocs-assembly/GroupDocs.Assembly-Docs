---
id: assembly-basic-usage-json-datasource
url: assembly/net/basic-usage-json-datasource
linktitle: Generate from JSON
title: Generate Document from JSON Data Source
weight: 8
description: "Build documents from JSON data sources using JsonDataSource class to load and bind JSON data to templates in .NET applications."
keywords: JSON data source, JsonDataSource, JSON binding, parse JSON, generate from JSON, compose JSON, assemble JSON
productName: GroupDocs.Assembly for .NET
hideChildren: False
---

## Overview

GroupDocs.Assembly for .NET enables you to generate documents directly from JSON data sources. The `JsonDataSource` class automatically parses JSON and makes it available to your templates, supporting both simple and complex JSON structures.

The main classes involved are:
- [JsonDataSource](https://reference.groupdocs.com/assembly/net/groupdocs.assembly/jsondatasource/) - loads and parses JSON data
- [DocumentAssembler](https://reference.groupdocs.com/assembly/net/groupdocs.assembly/documentassembler/) - assembles documents from templates
- [DataSourceInfo](https://reference.groupdocs.com/assembly/net/groupdocs.assembly/datasourceinfo/) - wraps the data source

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

```csharp
using GroupDocs.Assembly;
using GroupDocs.Assembly.Data;

public static void GenerateFromJsonFile()
{
    JsonDataSource jsonDataSource = new JsonDataSource("data.json");

    DocumentAssembler assembler = new DocumentAssembler();
    assembler.AssembleDocument("Template.docx", "Output.docx",
        new DataSourceInfo(jsonDataSource, "data"));
}
```

## Generate Document from JSON String

You can also create JsonDataSource from a JSON string:

```csharp
using GroupDocs.Assembly;
using GroupDocs.Assembly.Data;

public static void GenerateFromJsonString()
{
    string jsonString = @"{
        ""name"": ""John Doe"",
        ""age"": 30,
        ""email"": ""john.doe@example.com"",
        ""active"": true
    }";
    
    JsonDataSource jsonDataSource = new JsonDataSource(jsonString);

    DocumentAssembler assembler = new DocumentAssembler();
    assembler.AssembleDocument("Template.docx", "Output.docx",
        new DataSourceInfo(jsonDataSource, "person"));
}
```

## Working with JSON Arrays

When your JSON root is an array, JsonDataSource treats it as a collection:

```csharp
using GroupDocs.Assembly;
using GroupDocs.Assembly.Data;

public static void GenerateFromJsonArray()
{
    string jsonArray = @"[
        { ""name"": ""John"", ""age"": 30 },
        { ""name"": ""Jane"", ""age"": 28 },
        { ""name"": ""Bob"", ""age"": 35 }
    ]";
    
    JsonDataSource jsonDataSource = new JsonDataSource(jsonArray);

    DocumentAssembler assembler = new DocumentAssembler();
    assembler.AssembleDocument("Template.docx", "Output.docx",
        new DataSourceInfo(jsonDataSource, "people"));
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

```csharp
using GroupDocs.Assembly;
using GroupDocs.Assembly.Data;

public static void GenerateFromNestedJson()
{
    string nestedJson = @"{
        ""company"": ""ABC Corp"",
        ""address"": {
            ""street"": ""123 Main St"",
            ""city"": ""New York"",
            ""zip"": ""10001""
        },
        ""employees"": [
            { ""name"": ""John"", ""position"": ""Developer"" },
            { ""name"": ""Jane"", ""position"": ""Manager"" }
        ]
    }";
    
    JsonDataSource jsonDataSource = new JsonDataSource(nestedJson);

    DocumentAssembler assembler = new DocumentAssembler();
    assembler.AssembleDocument("Template.docx", "Output.docx",
        new DataSourceInfo(jsonDataSource, "company"));
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

```csharp
using GroupDocs.Assembly;
using GroupDocs.Assembly.Data;

public static void GenerateWithJsonOptions()
{
    JsonDataLoadOptions options = new JsonDataLoadOptions();
    options.AlwaysGenerateRootObject = true; // Always create root object
    options.SimpleValueParseMode = JsonSimpleValueParseMode.Strict; // Strict type parsing
    
    JsonDataSource jsonDataSource = new JsonDataSource("data.json", options);

    DocumentAssembler assembler = new DocumentAssembler();
    assembler.AssembleDocument("Template.docx", "Output.docx",
        new DataSourceInfo(jsonDataSource, "data"));
}
```

{{< alert style="warning" >}}
By default, if a root JSON element is an object with only one property that is an object or array, the engine skips the root object. Set `AlwaysGenerateRootObject` to true to always include it.
{{< /alert >}}

### Advanced Usage Topics

To learn more about working with complex JSON structures, date-time parsing, and advanced JsonDataSource options, please refer to the [advanced usage section]({{< ref "assembly/net/developer-guide/advanced-usage/_index.md" >}}).

## More resources

### GitHub Examples

You may easily run the code above and see the feature in action in our GitHub examples:

* [GroupDocs.Assembly for .NET examples, plugins, and showcase](https://github.com/groupdocs-assembly/GroupDocs.Assembly-for-.NET)
* [GroupDocs.Assembly for Java examples, plugins, and showcase](https://github.com/groupdocs-assembly/GroupDocs.Assembly-for-Java)
* [GroupDocs.Assembly for Python via .NET examples, plugins, and showcase](https://github.com/groupdocs-assembly/GroupDocs.Assembly-for-Python-via-.NET)

### Free Online Apps

Along with the full-featured .NET library, we provide simple but powerful free online apps.

To assemble documents from templates and data sources, you can use the online apps from the **[GroupDocs.Assembly App Product Family](https://products.groupdocs.app/assembly/family)**.

