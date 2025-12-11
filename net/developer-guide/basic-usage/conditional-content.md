---
id: assembly-basic-usage-conditional-content
url: assembly/net/basic-usage-conditional-content
title: Add Conditional Content with If/Else in C#
weight: 23
description: "Display content conditionally in templates using if/elseif/else blocks based on data values."
keywords: conditional content, if else, conditional blocks, conditional display, conditional formatting, if elseif
productName: GroupDocs.Assembly for .NET
hideChildren: False
---

## Overview

Conditional blocks allow you to display different content in your documents based on data values. GroupDocs.Assembly for .NET supports if/elseif/else syntax similar to C#, enabling you to create dynamic documents that adapt their content based on conditions.

The main syntax elements are:
- `<<if [condition]>>` - display content if condition is true
- `<<elseif [condition]>>` - display content if previous conditions are false and this condition is true
- `<<else>>` - display content if all conditions are false
- `<<if>>` - closing tag

Here are the steps to use conditional content:

* Create a template with conditional blocks
* Define conditions using C# expressions that return boolean values
* Provide content for each condition branch
* Assemble the document with your data

{{< alert style="info" >}}
Conditional expressions must return boolean values. You can use comparison operators (==, !=, <, >, <=, >=), logical operators (&&, ||, !), and method calls that return bool.
{{< /alert >}}

## Simple If/Else Block

Display content based on a simple condition:

```csharp
using GroupDocs.Assembly;

public class Customer
{
    public string Name { get; set; }
    public decimal Balance { get; set; }
}

public static void SimpleConditional()
{
    var customer = new Customer
    {
        Name = "John Doe",
        Balance = 1500.00m
    };
    
    DocumentAssembler assembler = new DocumentAssembler();
    assembler.AssembleDocument("ConditionalTemplate.docx", "ConditionalOutput.docx", 
        new DataSourceInfo(customer, "customer"));
    
    Console.WriteLine("Conditional content generated successfully.");
}
```

## Template Example for Simple If/Else

In your template (ConditionalTemplate.docx):

```
Customer: <<[customer.Name]>>

<<if [customer.Balance > 1000]>>
Status: Premium Customer
You have a high balance and qualify for special benefits.
<<else>>
Status: Standard Customer
Thank you for your business.
<<if>>
```

## If/Elseif/Else Block

Use multiple conditions with elseif:

```csharp
using GroupDocs.Assembly;

public class Order
{
    public decimal Amount { get; set; }
}

public static void MultipleConditions()
{
    var order = new Order
    {
        Amount = 750.00m
    };
    
    DocumentAssembler assembler = new DocumentAssembler();
    assembler.AssembleDocument("ConditionalTemplate.docx", "ConditionalOutput.docx", 
        new DataSourceInfo(order, "order"));
    
    Console.WriteLine("Multiple conditions processed successfully.");
}
```

Template with elseif:

```
Order Amount: <<[order.Amount]:"C">>

<<if [order.Amount > 1000]>>
Discount: 10% (Large order discount)
<<elseif [order.Amount > 500]>>
Discount: 5% (Medium order discount)
<<else>>
Discount: No discount available
<<if>>
```

## Conditional Content with Collections

Check if collections have items:

```csharp
using GroupDocs.Assembly;
using System.Collections.Generic;

public class Report
{
    public List<string> Items { get; set; }
}

public static void ConditionalWithCollections()
{
    var report = new Report
    {
        Items = new List<string> { "Item 1", "Item 2", "Item 3" }
    };
    
    DocumentAssembler assembler = new DocumentAssembler();
    assembler.AssembleDocument("ConditionalTemplate.docx", "ConditionalOutput.docx", 
        new DataSourceInfo(report, "report"));
    
    Console.WriteLine("Conditional content with collections generated successfully.");
}
```

Template:

```
<<if [report.Items.Any()]>>
Items:
<<foreach [in report.Items]>>
- <<[report.Items_Text]>>
<</foreach>>
<<else>>
No items available.
<<if>>
```

## Conditional Content in Data Bands

Use conditional blocks within foreach loops:

```csharp
using GroupDocs.Assembly;
using System.Collections.Generic;

public class Product
{
    public string Name { get; set; }
    public decimal Price { get; set; }
    public bool InStock { get; set; }
}

public static void ConditionalInDataBand()
{
    List<Product> products = new List<Product>
    {
        new Product { Name = "Laptop", Price = 999.99m, InStock = true },
        new Product { Name = "Mouse", Price = 29.99m, InStock = false },
        new Product { Name = "Keyboard", Price = 79.99m, InStock = true }
    };
    
    DocumentAssembler assembler = new DocumentAssembler();
    assembler.AssembleDocument("ConditionalTemplate.docx", "ConditionalOutput.docx", 
        new DataSourceInfo(products, "products"));
    
    Console.WriteLine("Conditional content in data band generated successfully.");
}
```

Template:

```
<<foreach [in products]>>
<<[Name]>> - <<[Price]:"C">>
<<if [InStock]>>
✓ In Stock
<<else>>
✗ Out of Stock
<<if>>

<</foreach>>
```

## Complex Conditions

Use logical operators for complex conditions:

```csharp
using GroupDocs.Assembly;

public class Employee
{
    public int YearsOfService { get; set; }
    public decimal Salary { get; set; }
    public string Department { get; set; }
}

public static void ComplexConditions()
{
    var employee = new Employee
    {
        YearsOfService = 5,
        Salary = 75000m,
        Department = "Engineering"
    };
    
    DocumentAssembler assembler = new DocumentAssembler();
    assembler.AssembleDocument("ConditionalTemplate.docx", "ConditionalOutput.docx", 
        new DataSourceInfo(employee, "employee"));
    
    Console.WriteLine("Complex conditions processed successfully.");
}
```

Template with complex conditions:

```
<<if [employee.YearsOfService >= 5 && employee.Salary > 70000]>>
Eligible for promotion
<<elseif [employee.Department == "Engineering"]>>
Consider for technical leadership
<<else>>
Standard review process
<<if>>
```

## Conditional Formatting

Apply different formatting based on conditions:

```csharp
using GroupDocs.Assembly;

public class Invoice
{
    public decimal Amount { get; set; }
    public bool IsPaid { get; set; }
}

public static void ConditionalFormatting()
{
    var invoice = new Invoice
    {
        Amount = 1500.00m,
        IsPaid = false
    };
    
    DocumentAssembler assembler = new DocumentAssembler();
    assembler.AssembleDocument("ConditionalTemplate.docx", "ConditionalOutput.docx", 
        new DataSourceInfo(invoice, "invoice"));
    
    Console.WriteLine("Conditional formatting applied successfully.");
}
```

Template:

```
Amount: <<[invoice.Amount]:"C">>

<<if [invoice.IsPaid]>>
Status: PAID
<<else>>
Status: UNPAID - Payment Required
<<if>>
```

## Using Methods in Conditions

Call methods that return boolean values:

```csharp
using GroupDocs.Assembly;
using System.Collections.Generic;

public class Order
{
    public List<OrderItem> Items { get; set; }
    
    public bool HasItems()
    {
        return Items != null && Items.Count > 0;
    }
}

public class OrderItem
{
    public string Name { get; set; }
}

public static void ConditionalWithMethods()
{
    var order = new Order
    {
        Items = new List<OrderItem> { new OrderItem { Name = "Product" } }
    };
    
    DocumentAssembler assembler = new DocumentAssembler();
    assembler.AssembleDocument("ConditionalTemplate.docx", "ConditionalOutput.docx", 
        new DataSourceInfo(order, "order"));
    
    Console.WriteLine("Conditional with methods processed successfully.");
}
```

Template:

```
<<if [order.HasItems()]>>
Order contains items.
<<else>>
Order is empty.
<<if>>
```

{{< alert style="warning" >}}
Conditional blocks must be properly closed with `<<if>>`. Nested conditional blocks are supported, but ensure proper nesting and closing of all blocks.
{{< /alert >}}

### Advanced Usage Topics

To learn more about table-row conditional blocks, conditional formatting in different document types, and advanced conditional scenarios, please refer to the [advanced usage section]({{< ref "assembly/net/developer-guide/advanced-usage/_index.md" >}}).

## More resources

### GitHub Examples

You may easily run the code above and see the feature in action in our GitHub examples:

* [GroupDocs.Assembly for .NET examples, plugins, and showcase](https://github.com/groupdocs-assembly/GroupDocs.Assembly-for-.NET)
* [GroupDocs.Assembly for Java examples, plugins, and showcase](https://github.com/groupdocs-assembly/GroupDocs.Assembly-for-Java)
* [GroupDocs.Assembly for Python via .NET examples, plugins, and showcase](https://github.com/groupdocs-assembly/GroupDocs.Assembly-for-Python-via-.NET)

### Free Online Apps

Along with the full-featured .NET library, we provide simple but powerful free online apps.

To assemble documents from templates and data sources, you can use the online apps from the **[GroupDocs.Assembly App Product Family](https://products.groupdocs.app/assembly/family)**.

