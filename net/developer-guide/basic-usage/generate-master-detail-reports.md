---
id: assembly-basic-usage-master-detail
url: assembly/net/basic-usage-master-detail
title: Generate Master-Detail Reports in C#
weight: 18
description: "Create parent-child reports with nested data bands to display master records with their detail records."
keywords: master detail, parent child, nested foreach, hierarchical data, orders and items, generate master detail
productName: GroupDocs.Assembly for .NET
hideChildren: False
---

## Overview

Master-detail reports display hierarchical data where each master record (parent) has associated detail records (children). GroupDocs.Assembly for .NET supports master-detail reports through nested foreach data bands, allowing you to display parent records with their related child records.

The main classes involved are:
- [DocumentAssembler](https://reference.groupdocs.com/assembly/net/groupdocs.assembly/documentassembler/) - assembles documents
- [DataSourceInfo](https://reference.groupdocs.com/assembly/net/groupdocs.assembly/datasourceinfo/) - wraps data sources

Here are the steps to generate master-detail reports:

* Define data structures with parent-child relationships
* Create a template with nested foreach data bands
* Outer foreach iterates over master records
* Inner foreach iterates over detail records for each master
* Assemble the document with your hierarchical data

{{< alert style="info" >}}
Nested foreach data bands allow you to create complex hierarchical reports. The outer band processes master records, while inner bands process related detail records.
{{< /alert >}}

## Define Master-Detail Data Structure

Start by defining classes with parent-child relationships:

```csharp
public class Order
{
    public int OrderId { get; set; }
    public DateTime OrderDate { get; set; }
    public string CustomerName { get; set; }
    public List<OrderItem> Items { get; set; }
}

public class OrderItem
{
    public string ProductName { get; set; }
    public int Quantity { get; set; }
    public decimal Price { get; set; }
}
```

## Generate Master-Detail Report

Create a master-detail report from hierarchical data:

```csharp
using GroupDocs.Assembly;
using System.Collections.Generic;

public static void GenerateMasterDetailReport()
{
    // Create sample data with master-detail relationship
    List<Order> orders = new List<Order>
    {
        new Order
        {
            OrderId = 1001,
            OrderDate = new DateTime(2024, 1, 15),
            CustomerName = "John Doe",
            Items = new List<OrderItem>
            {
                new OrderItem { ProductName = "Laptop", Quantity = 1, Price = 999.99m },
                new OrderItem { ProductName = "Mouse", Quantity = 2, Price = 29.99m }
            }
        },
        new Order
        {
            OrderId = 1002,
            OrderDate = new DateTime(2024, 1, 16),
            CustomerName = "Jane Smith",
            Items = new List<OrderItem>
            {
                new OrderItem { ProductName = "Keyboard", Quantity = 1, Price = 79.99m }
            }
        }
    };
    
    // Assemble document
    DocumentAssembler assembler = new DocumentAssembler();
    assembler.AssembleDocument("MasterDetailTemplate.docx", "MasterDetailOutput.docx", 
        new DataSourceInfo(orders, "orders"));
    
    Console.WriteLine("Master-detail report generated successfully.");
}
```

## Template Structure for Master-Detail

In your template (MasterDetailTemplate.docx), use nested foreach data bands:

```
<<foreach [in orders]>>
Order #<<[OrderId]>>
Date: <<[OrderDate]:"yyyy-MM-dd">>
Customer: <<[CustomerName]>>

Items:
<<foreach [in Items]>>
  - <<[ProductName]>> (Qty: <<[Quantity]>>, Price: <<[Price]:"C">>)
<</foreach>>

Total: <<[Items.Sum(i => i.Price * i.Quantity)]:"C">>

<</foreach>>
```

After assembly, you'll get:

```
Order #1001
Date: 2024-01-15
Customer: John Doe

Items:
  - Laptop (Qty: 1, Price: $999.99)
  - Mouse (Qty: 2, Price: $29.99)

Total: $1,059.97

Order #1002
Date: 2024-01-16
Customer: Jane Smith

Items:
  - Keyboard (Qty: 1, Price: $79.99)

Total: $79.99
```

## Master-Detail in Tables

You can also create master-detail reports in table format:

```csharp
using GroupDocs.Assembly;
using System.Collections.Generic;

public static void GenerateMasterDetailTable()
{
    List<Order> orders = new List<Order>
    {
        new Order
        {
            OrderId = 1001,
            CustomerName = "John Doe",
            Items = new List<OrderItem>
            {
                new OrderItem { ProductName = "Laptop", Quantity = 1, Price = 999.99m },
                new OrderItem { ProductName = "Mouse", Quantity = 2, Price = 29.99m }
            }
        }
    };
    
    DocumentAssembler assembler = new DocumentAssembler();
    assembler.AssembleDocument("MasterDetailTableTemplate.docx", "MasterDetailTableOutput.docx", 
        new DataSourceInfo(orders, "orders"));
    
    Console.WriteLine("Master-detail table generated successfully.");
}
```

Template table structure:

| Order ID | Customer | Product | Quantity | Price |
|----------|----------|---------|----------|-------|
| `<<foreach [in orders]>>` | | | | |
| `<<[OrderId]>>` | `<<[CustomerName]>>` | `<<foreach [in Items]>>` | | |
| | | `<<[ProductName]>>` | `<<[Quantity]>>` | `<<[Price]:"C">>` |
| | | `<<foreach>>` | | |
| `<<foreach>>` | | | | |

## Using Aggregates in Master-Detail

Calculate totals and aggregates for each master record:

```csharp
using GroupDocs.Assembly;
using System.Collections.Generic;

public static void GenerateMasterDetailWithAggregates()
{
    List<Order> orders = new List<Order>
    {
        new Order
        {
            OrderId = 1001,
            CustomerName = "John Doe",
            Items = new List<OrderItem>
            {
                new OrderItem { ProductName = "Laptop", Quantity = 1, Price = 999.99m },
                new OrderItem { ProductName = "Mouse", Quantity = 2, Price = 29.99m }
            }
        }
    };
    
    DocumentAssembler assembler = new DocumentAssembler();
    assembler.AssembleDocument("MasterDetailTemplate.docx", "MasterDetailOutput.docx", 
        new DataSourceInfo(orders, "orders"));
    
    Console.WriteLine("Master-detail report with aggregates generated successfully.");
}
```

Template with aggregates:

```
<<foreach [in orders]>>
Order #<<[OrderId]>> - <<[CustomerName]>>

Items:
<<foreach [in Items]>>
  <<[ProductName]>> - <<[Quantity]>> x <<[Price]:"C">> = <<[Quantity * Price]:"C">>
<</foreach>>

Subtotal: <<[Items.Sum(i => i.Price * i.Quantity)]:"C">>
Item Count: <<[Items.Count()]>>
<</foreach>>
```

{{< alert style="warning" >}}
When using nested foreach data bands, ensure proper closing tags. Each opening `<<foreach>>` must have a corresponding closing `<<foreach>>`.
{{< /alert >}}

### Advanced Usage Topics

To learn more about complex hierarchical structures, multiple levels of nesting, and advanced master-detail patterns, please refer to the [advanced usage section]({{< ref "assembly/net/developer-guide/advanced-usage/_index.md" >}}).

## More resources

### GitHub Examples

You may easily run the code above and see the feature in action in our GitHub examples:

* [GroupDocs.Assembly for .NET examples, plugins, and showcase](https://github.com/groupdocs-assembly/GroupDocs.Assembly-for-.NET)
* [GroupDocs.Assembly for Java examples, plugins, and showcase](https://github.com/groupdocs-assembly/GroupDocs.Assembly-for-Java)
* [GroupDocs.Assembly for Python via .NET examples, plugins, and showcase](https://github.com/groupdocs-assembly/GroupDocs.Assembly-for-Python-via-.NET)

### Free Online Apps

Along with the full-featured .NET library, we provide simple but powerful free online apps.

To assemble documents from templates and data sources, you can use the online apps from the **[GroupDocs.Assembly App Product Family](https://products.groupdocs.app/assembly/family)**.

