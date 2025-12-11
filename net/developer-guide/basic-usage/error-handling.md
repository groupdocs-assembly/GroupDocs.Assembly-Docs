---
id: assembly-basic-usage-error-handling
url: assembly/net/basic-usage-error-handling
title: Handle Common Template and Data Errors
weight: 31
description: "Catch and handle common exceptions during document assembly and validate template syntax and data."
keywords: error handling, exceptions, template errors, data errors, validation, error catching, assembly errors
productName: GroupDocs.Assembly for .NET
toc: True
---

## Overview

Error handling is crucial when generating documents from templates and data sources. GroupDocs.Assembly for .NET provides exceptions that help you identify and resolve issues with templates, data sources, or assembly operations. Understanding common error scenarios and how to handle them improves the reliability of your document generation code.

The main exception types are:
- `DocumentAssemblerException` - general assembly errors
- Template syntax errors
- Data source errors
- Missing member errors

Here are the steps to handle errors:

* Wrap assembly operations in try-catch blocks
* Catch specific exception types
* Validate data sources before assembly
* Handle missing members gracefully
* Log errors for debugging

{{< alert style="info" >}}
GroupDocs.Assembly provides detailed error messages that help identify the exact location and cause of template or data errors.
{{< /alert >}}

## Basic Error Handling

Wrap assembly operations in try-catch blocks:

```csharp
using GroupDocs.Assembly;
using System;

public static void BasicErrorHandling()
{
    try
    {
        var data = new { Name = "John Doe", Age = 30 };
        
        DocumentAssembler assembler = new DocumentAssembler();
        assembler.AssembleDocument("Template.docx", "Output.docx", 
            new DataSourceInfo(data, "data"));
        
        Console.WriteLine("Document assembled successfully.");
    }
    catch (Exception ex)
    {
        Console.WriteLine($"Error assembling document: {ex.Message}");
        // Handle error appropriately
    }
}
```

## Handle Template Syntax Errors

Catch and handle template syntax errors:

```csharp
using GroupDocs.Assembly;
using System;

public static void HandleTemplateErrors()
{
    try
    {
        var data = new { Name = "John Doe" };
        
        DocumentAssembler assembler = new DocumentAssembler();
        assembler.AssembleDocument("Template.docx", "Output.docx", 
            new DataSourceInfo(data, "data"));
    }
    catch (DocumentAssemblerException ex)
    {
        Console.WriteLine($"Template error: {ex.Message}");
        Console.WriteLine($"Error details: {ex.InnerException?.Message}");
        // Log error, notify user, or use fallback template
    }
    catch (Exception ex)
    {
        Console.WriteLine($"Unexpected error: {ex.Message}");
    }
}
```

## Handle Missing Data Members

Handle cases where template references missing data members:

```csharp
using GroupDocs.Assembly;
using System;

public static void HandleMissingMembers()
{
    try
    {
        // Data doesn't have all properties referenced in template
        var data = new { Name = "John Doe" };
        // Template might reference data.Email which doesn't exist
        
        DocumentAssembler assembler = new DocumentAssembler();
        
        // Option 1: Allow missing members (returns null/empty)
        assembler.Options |= DocumentAssemblyOptions.AllowMissingMembers;
        
        assembler.AssembleDocument("Template.docx", "Output.docx", 
            new DataSourceInfo(data, "data"));
    }
    catch (Exception ex)
    {
        Console.WriteLine($"Error: {ex.Message}");
    }
}
```

## Validate Data Before Assembly

Validate data sources before assembly:

```csharp
using GroupDocs.Assembly;
using System;
using System.Collections.Generic;

public static void ValidateDataBeforeAssembly()
{
    var products = new List<Product>();
    // products might be empty or null
    
    if (products == null || products.Count == 0)
    {
        Console.WriteLine("Warning: No products to process.");
        return;
    }
    
    try
    {
        DocumentAssembler assembler = new DocumentAssembler();
        assembler.AssembleDocument("Template.docx", "Output.docx", 
            new DataSourceInfo(products, "products"));
        
        Console.WriteLine("Document assembled successfully.");
    }
    catch (Exception ex)
    {
        Console.WriteLine($"Error: {ex.Message}");
    }
}
```

## Handle File Not Found Errors

Check if template file exists:

```csharp
using GroupDocs.Assembly;
using System;
using System.IO;

public static void HandleFileNotFound()
{
    string templatePath = "Template.docx";
    
    if (!File.Exists(templatePath))
    {
        Console.WriteLine($"Template file not found: {templatePath}");
        return;
    }
    
    try
    {
        var data = new { Name = "John Doe" };
        
        DocumentAssembler assembler = new DocumentAssembler();
        assembler.AssembleDocument(templatePath, "Output.docx", 
            new DataSourceInfo(data, "data"));
        
        Console.WriteLine("Document assembled successfully.");
    }
    catch (FileNotFoundException ex)
    {
        Console.WriteLine($"File not found: {ex.FileName}");
    }
    catch (Exception ex)
    {
        Console.WriteLine($"Error: {ex.Message}");
    }
}
```

## Handle Data Type Errors

Validate data types before assembly:

```csharp
using GroupDocs.Assembly;
using System;

public class Invoice
{
    public string CustomerName { get; set; }
    public decimal? Amount { get; set; } // Nullable
}

public static void HandleDataTypeErrors()
{
    var invoice = new Invoice
    {
        CustomerName = "John Doe",
        Amount = null // Might cause issues if template expects non-null
    };
    
    try
    {
        DocumentAssembler assembler = new DocumentAssembler();
        assembler.AssembleDocument("Template.docx", "Output.docx", 
            new DataSourceInfo(invoice, "invoice"));
    }
    catch (Exception ex)
    {
        Console.WriteLine($"Data type error: {ex.Message}");
        // Handle null values or provide defaults
    }
}
```

## Comprehensive Error Handling

Combine multiple error handling strategies:

```csharp
using GroupDocs.Assembly;
using System;
using System.IO;

public static void ComprehensiveErrorHandling()
{
    string templatePath = "Template.docx";
    string outputPath = "Output.docx";
    
    // Validate inputs
    if (string.IsNullOrEmpty(templatePath) || !File.Exists(templatePath))
    {
        Console.WriteLine("Invalid template path.");
        return;
    }
    
    try
    {
        var data = new { Name = "John Doe", Age = 30 };
        
        // Validate data
        if (data == null)
        {
            Console.WriteLine("Data source is null.");
            return;
        }
        
        DocumentAssembler assembler = new DocumentAssembler();
        
        // Configure error handling options
        assembler.Options |= DocumentAssemblyOptions.AllowMissingMembers;
        
        assembler.AssembleDocument(templatePath, outputPath, 
            new DataSourceInfo(data, "data"));
        
        Console.WriteLine("Document assembled successfully.");
    }
    catch (DocumentAssemblerException ex)
    {
        Console.WriteLine($"Assembly error: {ex.Message}");
        if (ex.InnerException != null)
        {
            Console.WriteLine($"Inner exception: {ex.InnerException.Message}");
        }
        // Log detailed error information
    }
    catch (FileNotFoundException ex)
    {
        Console.WriteLine($"File not found: {ex.FileName}");
    }
    catch (UnauthorizedAccessException ex)
    {
        Console.WriteLine($"Access denied: {ex.Message}");
    }
    catch (Exception ex)
    {
        Console.WriteLine($"Unexpected error: {ex.Message}");
        Console.WriteLine($"Stack trace: {ex.StackTrace}");
    }
}
```

## Handle Stream Errors

Properly handle stream-related errors:

```csharp
using GroupDocs.Assembly;
using System;
using System.IO;

public static void HandleStreamErrors()
{
    try
    {
        using (FileStream templateStream = new FileStream("Template.docx", FileMode.Open))
        using (FileStream outputStream = new FileStream("Output.docx", FileMode.Create))
        {
            var data = new { Name = "John Doe" };
            
            DocumentAssembler assembler = new DocumentAssembler();
            assembler.AssembleDocument(templateStream, outputStream, 
                new DataSourceInfo(data, "data"));
        }
    }
    catch (IOException ex)
    {
        Console.WriteLine($"IO error: {ex.Message}");
    }
    catch (Exception ex)
    {
        Console.WriteLine($"Error: {ex.Message}");
    }
}
```

## Error Handling Best Practices

1. **Always use try-catch blocks** around assembly operations
2. **Validate inputs** before assembly (file existence, data null checks)
3. **Use specific exception types** when possible
4. **Enable AllowMissingMembers** option if your data structure is dynamic
5. **Log errors** with sufficient detail for debugging
6. **Provide user-friendly error messages** in production code

{{< alert style="warning" >}}
Some errors might occur during template evaluation. Always test templates with sample data before deploying to production. Consider using template validation tools or test assemblies.
{{< /alert >}}

### Advanced Usage Topics

To learn more about detailed error logging, template validation, custom error handling, and debugging techniques, please refer to the [advanced usage section]({{< ref "assembly/net/developer-guide/advanced-usage/_index.md" >}}).

## More resources

### GitHub Examples

You may easily run the code above and see the feature in action in our GitHub examples:

* [GroupDocs.Assembly for .NET examples, plugins, and showcase](https://github.com/groupdocs-assembly/GroupDocs.Assembly-for-.NET)
* [GroupDocs.Assembly for Java examples, plugins, and showcase](https://github.com/groupdocs-assembly/GroupDocs.Assembly-for-Java)
* [GroupDocs.Assembly for Python via .NET examples, plugins, and showcase](https://github.com/groupdocs-assembly/GroupDocs.Assembly-for-Python-via-.NET)

### Free Online Apps

Along with the full-featured .NET library, we provide simple but powerful free online apps.

To assemble documents from templates and data sources, you can use the online apps from the **[GroupDocs.Assembly App Product Family](https://products.groupdocs.app/assembly/family)**.

