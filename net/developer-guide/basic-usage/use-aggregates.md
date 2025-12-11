---
id: assembly-basic-usage-aggregates
url: assembly/net/basic-usage-aggregates
title: Use Simple Aggregates (Sum, Count, Average) in C#
weight: 24
description: "Calculate and display aggregate values like sums, counts, and averages from data collections in templates."
keywords: aggregates, sum, count, average, totals, calculations, aggregate functions, LINQ aggregates
productName: GroupDocs.Assembly for .NET
toc: True
---

## Overview

GroupDocs.Assembly for .NET supports LINQ-based aggregate functions that allow you to calculate sums, counts, averages, and other aggregate values directly in templates. These functions work with collections and enable you to display totals, summaries, and statistical information in your documents.

The main aggregate functions are:
- `Sum()` - calculate sum of numeric values
- `Count()` - count number of items
- `Average()` - calculate average of numeric values
- `Min()` - find minimum value
- `Max()` - find maximum value

Here are the steps to use aggregates:

* Create a template with aggregate expressions
* Use LINQ aggregate methods on collections
* Reference aggregate results in your template
* Assemble the document with your data

{{< alert style="info" >}}
Aggregate functions use LINQ syntax and work with any collection type, including lists, arrays, DataTables, and other enumerable collections.
{{< /alert >}}

## Calculate Sum

Calculate the sum of values in a collection:

```csharp
using GroupDocs.Assembly;
using System.Collections.Generic;

public class OrderItem
{
    public string ProductName { get; set; }
    public decimal Price { get; set; }
    public int Quantity { get; set; }
}

public static void CalculateSum()
{
    List<OrderItem> items = new List<OrderItem>
    {
        new OrderItem { ProductName = "Laptop", Price = 999.99m, Quantity = 1 },
        new OrderItem { ProductName = "Mouse", Price = 29.99m, Quantity = 2 },
        new OrderItem { ProductName = "Keyboard", Price = 79.99m, Quantity = 1 }
    };
    
    DocumentAssembler assembler = new DocumentAssembler();
    assembler.AssembleDocument("AggregatesTemplate.docx", "AggregatesOutput.docx", 
        new DataSourceInfo(items, "items"));
    
    Console.WriteLine("Sum calculated successfully.");
}
```

## Template Example for Sum

In your template (AggregatesTemplate.docx):

```
Items:
<<foreach [in items]>>
<<[ProductName]>> - <<[Price]:"C">> x <<[Quantity]>>
<</foreach>>

Total: <<[items.Sum(i => i.Price * i.Quantity)]:"C">>
```

## Calculate Count

Count the number of items in a collection:

```csharp
using GroupDocs.Assembly;
using System.Collections.Generic;

public static void CalculateCount()
{
    List<string> products = new List<string> 
    { 
        "Laptop", 
        "Mouse", 
        "Keyboard", 
        "Monitor" 
    };
    
    DocumentAssembler assembler = new DocumentAssembler();
    assembler.AssembleDocument("AggregatesTemplate.docx", "AggregatesOutput.docx", 
        new DataSourceInfo(products, "products"));
    
    Console.WriteLine("Count calculated successfully.");
}
```

Template:

```
Products:
<<foreach [in products]>>
- <<[products_Text]>>
<</foreach>>

Total Products: <<[products.Count()]>>
```

## Calculate Average

Calculate the average of numeric values:

```csharp
using GroupDocs.Assembly;
using System.Collections.Generic;

public class Sale
{
    public decimal Amount { get; set; }
}

public static void CalculateAverage()
{
    List<Sale> sales = new List<Sale>
    {
        new Sale { Amount = 1000.00m },
        new Sale { Amount = 1500.00m },
        new Sale { Amount = 800.00m },
        new Sale { Amount = 1200.00m }
    };
    
    DocumentAssembler assembler = new DocumentAssembler();
    assembler.AssembleDocument("AggregatesTemplate.docx", "AggregatesOutput.docx", 
        new DataSourceInfo(sales, "sales"));
    
    Console.WriteLine("Average calculated successfully.");
}
```

Template:

```
Sales:
<<foreach [in sales]>>
<<[Amount]:"C">>
<</foreach>>

Average Sale: <<[sales.Average(s => s.Amount)]:"C">>
```

## Calculate Min and Max

Find minimum and maximum values:

```csharp
using GroupDocs.Assembly;
using System.Collections.Generic;

public static void CalculateMinMax()
{
    List<Sale> sales = new List<Sale>
    {
        new Sale { Amount = 1000.00m },
        new Sale { Amount = 1500.00m },
        new Sale { Amount = 800.00m }
    };
    
    DocumentAssembler assembler = new DocumentAssembler();
    assembler.AssembleDocument("AggregatesTemplate.docx", "AggregatesOutput.docx", 
        new DataSourceInfo(sales, "sales"));
    
    Console.WriteLine("Min and max calculated successfully.");
}
```

Template:

```
Minimum Sale: <<[sales.Min(s => s.Amount)]:"C">>
Maximum Sale: <<[sales.Max(s => s.Amount)]:"C">>
```

## Multiple Aggregates

Use multiple aggregates in the same template:

```csharp
using GroupDocs.Assembly;
using System.Collections.Generic;

public static void MultipleAggregates()
{
    List<OrderItem> items = new List<OrderItem>
    {
        new OrderItem { ProductName = "Laptop", Price = 999.99m, Quantity = 1 },
        new OrderItem { ProductName = "Mouse", Price = 29.99m, Quantity = 2 },
        new OrderItem { ProductName = "Keyboard", Price = 79.99m, Quantity = 1 }
    };
    
    DocumentAssembler assembler = new DocumentAssembler();
    assembler.AssembleDocument("AggregatesTemplate.docx", "AggregatesOutput.docx", 
        new DataSourceInfo(items, "items"));
    
    Console.WriteLine("Multiple aggregates calculated successfully.");
}
```

Template:

```
Items:
<<foreach [in items]>>
<<[ProductName]>> - <<[Price]:"C">> x <<[Quantity]>>
<</foreach>>

Summary:
Total Items: <<[items.Count()]>>
Total Quantity: <<[items.Sum(i => i.Quantity)]>>
Total Amount: <<[items.Sum(i => i.Price * i.Quantity)]:"C">>
Average Price: <<[items.Average(i => i.Price)]:"C">>
```

## Aggregates with Conditions

Use aggregates with filtered data:

```csharp
using GroupDocs.Assembly;
using System.Collections.Generic;

public static void AggregatesWithConditions()
{
    List<OrderItem> items = new List<OrderItem>
    {
        new OrderItem { ProductName = "Laptop", Price = 999.99m, Quantity = 1 },
        new OrderItem { ProductName = "Mouse", Price = 29.99m, Quantity = 2 },
        new OrderItem { ProductName = "Keyboard", Price = 79.99m, Quantity = 1 }
    };
    
    DocumentAssembler assembler = new DocumentAssembler();
    assembler.AssembleDocument("AggregatesTemplate.docx", "AggregatesOutput.docx", 
        new DataSourceInfo(items, "items"));
    
    Console.WriteLine("Conditional aggregates calculated successfully.");
}
```

Template:

```
High-value items (Price > 100):
<<foreach [in items.Where(i => i.Price > 100)]>>
<<[ProductName]>> - <<[Price]:"C">>
<</foreach>>

Total High-value: <<[items.Where(i => i.Price > 100).Sum(i => i.Price)]:"C">>
```

## Aggregates in Master-Detail Reports

Calculate aggregates for detail records within master records:

```csharp
using GroupDocs.Assembly;
using System.Collections.Generic;

public class Order
{
    public int OrderId { get; set; }
    public List<OrderItem> Items { get; set; }
}

public static void AggregatesInMasterDetail()
{
    List<Order> orders = new List<Order>
    {
        new Order
        {
            OrderId = 1001,
            Items = new List<OrderItem>
            {
                new OrderItem { ProductName = "Laptop", Price = 999.99m, Quantity = 1 },
                new OrderItem { ProductName = "Mouse", Price = 29.99m, Quantity = 2 }
            }
        }
    };
    
    DocumentAssembler assembler = new DocumentAssembler();
    assembler.AssembleDocument("AggregatesTemplate.docx", "AggregatesOutput.docx", 
        new DataSourceInfo(orders, "orders"));
    
    Console.WriteLine("Master-detail aggregates calculated successfully.");
}
```

Template:

```
<<foreach [in orders]>>
Order #<<[OrderId]>>
Items:
<<foreach [in Items]>>
  <<[ProductName]>> - <<[Price]:"C">> x <<[Quantity]>>
<</foreach>>
Order Total: <<[Items.Sum(i => i.Price * i.Quantity)]:"C">>
<</foreach>>
```

{{< alert style="warning" >}}
Aggregate functions require collections. Ensure your data source is a collection type (List, Array, DataTable, etc.) when using aggregates.
{{< /alert >}}

### Advanced Usage Topics

To learn more about grouping, filtering with aggregates, custom aggregate functions, and performance optimization, please refer to the [advanced usage section]({{< ref "assembly/net/developer-guide/advanced-usage/_index.md" >}}).

## More resources

### GitHub Examples

You may easily run the code above and see the feature in action in our GitHub examples:

* [GroupDocs.Assembly for .NET examples, plugins, and showcase](https://github.com/groupdocs-assembly/GroupDocs.Assembly-for-.NET)
* [GroupDocs.Assembly for Java examples, plugins, and showcase](https://github.com/groupdocs-assembly/GroupDocs.Assembly-for-Java)
* [GroupDocs.Assembly for Python via .NET examples, plugins, and showcase](https://github.com/groupdocs-assembly/GroupDocs.Assembly-for-Python-via-.NET)

### Free Online Apps

Along with the full-featured .NET library, we provide simple but powerful free online apps.

To assemble documents from templates and data sources, you can use the online apps from the **[GroupDocs.Assembly App Product Family](https://products.groupdocs.app/assembly/family)**.

