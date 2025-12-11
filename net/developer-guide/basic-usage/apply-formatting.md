---
id: assembly-basic-usage-formatting
url: assembly/net/basic-usage-formatting
linktitle: Apply Formatting for various types
title: Apply Formatting to Numbers, Dates, and Text in C#
weight: 22
description: "Format numeric values, date-time values, and text strings in templates using format strings and functions."
keywords: formatting, number format, date format, text format, format strings, numeric formatting, date formatting
productName: GroupDocs.Assembly for .NET
hideChildren: False
---

## Overview

GroupDocs.Assembly for .NET provides comprehensive formatting capabilities for numbers, dates, and text in templates. You can use format strings (similar to .NET formatting) and built-in text transformation functions to control how data is displayed in your documents.

The main syntax elements are:
- Format strings: `<<[expression]:"format">>` - apply .NET format strings
- Text functions: `upper`, `lower`, `capital`, `firstcap` - transform text case

Here are the steps to apply formatting:

* Use format strings in expression tags for numbers and dates
* Apply text transformation functions for string formatting
* Combine formatting with expressions and calculations
* Test formatting to ensure desired output

{{< alert style="info" >}}
Format strings follow .NET formatting conventions. Use standard numeric format specifiers (C, N, F, etc.) and date/time format strings (yyyy-MM-dd, etc.).
{{< /alert >}}

## Format Numbers

Format numeric values using format strings:

```csharp
using GroupDocs.Assembly;

public class Invoice
{
    public decimal Amount { get; set; }
    public double Percentage { get; set; }
    public int Quantity { get; set; }
}

public static void FormatNumbers()
{
    var invoice = new Invoice
    {
        Amount = 1500.75m,
        Percentage = 0.15,
        Quantity = 25
    };
    
    DocumentAssembler assembler = new DocumentAssembler();
    assembler.AssembleDocument("FormattingTemplate.docx", "FormattingOutput.docx", 
        new DataSourceInfo(invoice, "invoice"));
    
    Console.WriteLine("Numbers formatted successfully.");
}
```

## Template Examples for Number Formatting

In your template, use format strings:

```
Amount: <<[invoice.Amount]:"C">>
Percentage: <<[invoice.Percentage]:"P">>
Quantity: <<[invoice.Quantity]:"N0">>
```

Common numeric format strings:
- `"C"` - Currency (e.g., $1,500.75)
- `"N"` or `"N2"` - Number with decimals (e.g., 1,500.75)
- `"F"` or `"F2"` - Fixed-point (e.g., 1500.75)
- `"P"` - Percentage (e.g., 15.00%)
- `"D"` - Decimal (for integers)

## Format Dates and Times

Format date-time values:

```csharp
using GroupDocs.Assembly;
using System;

public class Report
{
    public DateTime CreatedDate { get; set; }
    public DateTime DueDate { get; set; }
}

public static void FormatDates()
{
    var report = new Report
    {
        CreatedDate = new DateTime(2024, 1, 15, 14, 30, 0),
        DueDate = new DateTime(2024, 2, 15)
    };
    
    DocumentAssembler assembler = new DocumentAssembler();
    assembler.AssembleDocument("FormattingTemplate.docx", "FormattingOutput.docx", 
        new DataSourceInfo(report, "report"));
    
    Console.WriteLine("Dates formatted successfully.");
}
```

## Template Examples for Date Formatting

```
Created: <<[report.CreatedDate]:"yyyy-MM-dd HH:mm">>
Due Date: <<[report.DueDate]:"MMMM dd, yyyy">>
```

Common date format strings:
- `"yyyy-MM-dd"` - 2024-01-15
- `"MM/dd/yyyy"` - 01/15/2024
- `"MMMM dd, yyyy"` - January 15, 2024
- `"dd.MM.yyyy"` - 15.01.2024
- `"HH:mm"` - 14:30

## Format Text (Case Transformation)

Transform text case using built-in functions:

```csharp
using GroupDocs.Assembly;

public class Product
{
    public string Name { get; set; }
    public string Description { get; set; }
}

public static void FormatText()
{
    var product = new Product
    {
        Name = "laptop computer",
        Description = "HIGH-PERFORMANCE DEVICE"
    };
    
    DocumentAssembler assembler = new DocumentAssembler();
    assembler.AssembleDocument("FormattingTemplate.docx", "FormattingOutput.docx", 
        new DataSourceInfo(product, "product"));
    
    Console.WriteLine("Text formatted successfully.");
}
```

## Template Examples for Text Formatting

```
Name: <<[product.Name]:upper>>
Description: <<[product.Description]:lower>>
Title: <<[product.Name]:capital>>
```

Text transformation functions:
- `:upper` - Convert to UPPERCASE
- `:lower` - Convert to lowercase
- `:capital` - Capitalize Each Word
- `:firstcap` - Capitalize First Letter Only

## Combine Formatting with Calculations

Format calculated values:

```csharp
using GroupDocs.Assembly;

public class Order
{
    public int Quantity { get; set; }
    public decimal UnitPrice { get; set; }
}

public static void FormatCalculations()
{
    var order = new Order
    {
        Quantity = 5,
        UnitPrice = 29.99m
    };
    
    DocumentAssembler assembler = new DocumentAssembler();
    assembler.AssembleDocument("FormattingTemplate.docx", "FormattingOutput.docx", 
        new DataSourceInfo(order, "order"));
    
    Console.WriteLine("Calculations formatted successfully.");
}
```

Template:

```
Quantity: <<[order.Quantity]>>
Unit Price: <<[order.UnitPrice]:"C">>
Total: <<[order.Quantity * order.UnitPrice]:"C">>
```

## Custom Numeric Formats

Use custom format strings for specific requirements:

```csharp
using GroupDocs.Assembly;

public static void CustomNumericFormats()
{
    var data = new { 
        Phone = 1234567890,
        Code = 42,
        Rate = 0.1234
    };
    
    DocumentAssembler assembler = new DocumentAssembler();
    assembler.AssembleDocument("FormattingTemplate.docx", "FormattingOutput.docx", 
        new DataSourceInfo(data, "data"));
    
    Console.WriteLine("Custom formats applied successfully.");
}
```

Template with custom formats:

```
Phone: <<[data.Phone]:"(###) ###-####">>
Code: <<[data.Code]:"000">>
Rate: <<[data.Rate]:"0.00%">>
```

## Formatting in Different Document Types

Formatting works consistently across document types:

```csharp
using GroupDocs.Assembly;

public static void FormatInSpreadsheet()
{
    var invoice = new Invoice
    {
        Amount = 1500.75m,
        CreatedDate = DateTime.Now
    };
    
    DocumentAssembler assembler = new DocumentAssembler();
    assembler.AssembleDocument("FormattingTemplate.xlsx", "FormattingOutput.xlsx", 
        new DataSourceInfo(invoice, "invoice"));
    
    Console.WriteLine("Formatting applied in spreadsheet successfully.");
}
```

{{< alert style="warning" >}}
Format strings are case-sensitive. Use uppercase letters for standard format specifiers (C, N, F, P) and follow .NET formatting conventions exactly.
{{< /alert >}}

### Advanced Usage Topics

To learn more about custom format providers, culture-specific formatting, and advanced formatting scenarios, please refer to the [advanced usage section]({{< ref "assembly/net/developer-guide/advanced-usage/_index.md" >}}).

## More resources

### GitHub Examples

You may easily run the code above and see the feature in action in our GitHub examples:

* [GroupDocs.Assembly for .NET examples, plugins, and showcase](https://github.com/groupdocs-assembly/GroupDocs.Assembly-for-.NET)
* [GroupDocs.Assembly for Java examples, plugins, and showcase](https://github.com/groupdocs-assembly/GroupDocs.Assembly-for-Java)
* [GroupDocs.Assembly for Python via .NET examples, plugins, and showcase](https://github.com/groupdocs-assembly/GroupDocs.Assembly-for-Python-via-.NET)

### Free Online Apps

Along with the full-featured .NET library, we provide simple but powerful free online apps.

To assemble documents from templates and data sources, you can use the online apps from the **[GroupDocs.Assembly App Product Family](https://products.groupdocs.app/assembly/family)**.

