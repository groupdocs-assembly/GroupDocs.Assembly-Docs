---
id: assembly-basic-usage-template-syntax-basics
url: assembly/net/basic-usage-template-syntax-basics
linktitle: Basic Template Syntax
title: Basic Template Syntax - Expression Tags and Fields
weight: 5
description: "Introduction to basic template syntax including expression tags and simple field access in templates."
keywords: template syntax, expression tags, fields, basic syntax, template expressions, assemble, generate
productName: GroupDocs.Assembly for .NET
hideChildren: False
---

## Overview

GroupDocs.Assembly for .NET uses a simple, LINQ-based template syntax that allows you to embed C# expressions directly in your documents. Expression tags are the foundation of template syntax, enabling you to output data values and perform calculations.

The main syntax elements are:
- Expression tags `<<[expression]>>` - output expression results
- Data bands `<<foreach>>` - iterate over collections
- Conditional blocks `<<if>>` - display content conditionally

Here are the steps to use basic template syntax:

* Create a template document in Word, Excel, PowerPoint, or HTML format
* Insert expression tags using `<<[expression]>>` syntax
* Reference data source properties and methods in expressions
* Assemble the document with your data source

{{< alert style="info" >}}
Template syntax is case-sensitive and follows C# language rules. Expression tags are evaluated at runtime and replaced with their computed values.
{{< /alert >}}

## Basic Expression Tags

Expression tags are the simplest way to output data in templates. They use the syntax `<<[expression]>>`:

```csharp
using GroupDocs.Assembly;

public static void BasicExpressionTags()
{
    // Sample data
    var person = new { Name = "John Doe", Age = 30, Email = "john@example.com" };
    
    // Assemble document
    DocumentAssembler assembler = new DocumentAssembler();
    assembler.AssembleDocument("Template.docx", "Output.docx", 
        new DataSourceInfo(person, "person"));
    
    Console.WriteLine("Document assembled with expression tags.");
}
```

## Template Example with Expression Tags

In your template document (Template.docx), use expression tags like this:

```
Name: <<[person.Name]>>
Age: <<[person.Age]>>
Email: <<[person.Email]>>
```

After assembly, the output will be:

```
Name: John Doe
Age: 30
Email: john@example.com
```

## Using Contextual Object Member Access

When using a single data source, you can omit the data source name and use contextual access:

```csharp
using GroupDocs.Assembly;

public static void ContextualAccess()
{
    var product = new { Name = "Laptop", Price = 999.99m, Stock = 50 };
    
    DocumentAssembler assembler = new DocumentAssembler();
    assembler.AssembleDocument("Template.docx", "Output.docx", 
        new DataSourceInfo(product));
    
    Console.WriteLine("Document assembled with contextual access.");
}
```

Template with contextual access:

```
Product: <<[Name]>>
Price: <<[Price]>>
Stock: <<[Stock]>>
```

## Simple Calculations in Expressions

You can perform calculations directly in expression tags:

```csharp
using GroupDocs.Assembly;

public static void CalculationsInExpressions()
{
    var order = new { Quantity = 5, UnitPrice = 29.99m };
    
    DocumentAssembler assembler = new DocumentAssembler();
    assembler.AssembleDocument("Template.docx", "Output.docx", 
        new DataSourceInfo(order, "order"));
    
    Console.WriteLine("Document assembled with calculations.");
}
```

Template with calculations:

```
Quantity: <<[order.Quantity]>>
Unit Price: <<[order.UnitPrice]>>
Total: <<[order.Quantity * order.UnitPrice]>>
```

## Using String Methods

You can use .NET string methods in expressions:

```csharp
using GroupDocs.Assembly;

public static void StringMethods()
{
    var company = new { Name = "ABC Corporation", Website = "www.example.com" };
    
    DocumentAssembler assembler = new DocumentAssembler();
    assembler.AssembleDocument("Template.docx", "Output.docx", 
        new DataSourceInfo(company, "company"));
    
    Console.WriteLine("Document assembled with string methods.");
}
```

Template with string methods:

```
Company: <<[company.Name.ToUpper()]>>
Website: <<[company.Website.ToLower()]>>
```

## Expression Tag Formatting

You can format expression results using format strings:

```csharp
using GroupDocs.Assembly;

public static void FormattedExpressions()
{
    var invoice = new { 
        Amount = 1500.50m, 
        Date = new DateTime(2024, 1, 15),
        Percentage = 0.15
    };
    
    DocumentAssembler assembler = new DocumentAssembler();
    assembler.AssembleDocument("Template.docx", "Output.docx", 
        new DataSourceInfo(invoice, "invoice"));
    
    Console.WriteLine("Document assembled with formatting.");
}
```

Template with formatting:

```
Amount: <<[invoice.Amount]:"C">>
Date: <<[invoice.Date]:"yyyy-MM-dd">>
Percentage: <<[invoice.Percentage]:"P">>
```

{{< alert style="warning" >}}
Format strings follow .NET formatting conventions. Use "C" for currency, "P" for percentage, and standard date/time format strings for dates.
{{< /alert >}}

### Advanced Usage Topics

To learn more about data bands, conditional blocks, LINQ expressions, and advanced template syntax features, please refer to the [advanced usage section]({{< ref "assembly/net/developer-guide/advanced-usage/_index.md" >}}).

## More resources

### GitHub Examples

You may easily run the code above and see the feature in action in our GitHub examples:

* [GroupDocs.Assembly for .NET examples, plugins, and showcase](https://github.com/groupdocs-assembly/GroupDocs.Assembly-for-.NET)
* [GroupDocs.Assembly for Java examples, plugins, and showcase](https://github.com/groupdocs-assembly/GroupDocs.Assembly-for-Java)
* [GroupDocs.Assembly for Python via .NET examples, plugins, and showcase](https://github.com/groupdocs-assembly/GroupDocs.Assembly-for-Python-via-.NET)

### Free Online Apps

Along with the full-featured .NET library, we provide simple but powerful free online apps.

To assemble documents from templates and data sources, you can use the online apps from the **[GroupDocs.Assembly App Product Family](https://products.groupdocs.app/assembly/family)**.

