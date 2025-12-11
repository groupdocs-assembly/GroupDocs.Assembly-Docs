---
id: assembly-basic-usage-generate-tables
url: assembly/net/basic-usage-generate-tables
title: Generate Tables from Collection Data in C#
weight: 15
description: "Create dynamic tables in documents by iterating over collections and displaying data in table rows using GroupDocs.Assembly for .NET."
keywords: generate tables, table reports, foreach data band, table rows, collection data, tabular data, dynamic tables
productName: GroupDocs.Assembly for .NET
hideChildren: False
---

## Overview

Tables are one of the most common ways to display structured data in documents. GroupDocs.Assembly for .NET makes it easy to generate dynamic tables by iterating over collections and populating table rows with data.

The main classes involved are:
- [DocumentAssembler](https://reference.groupdocs.com/assembly/net/groupdocs.assembly/documentassembler/) - assembles documents
- [DataSourceInfo](https://reference.groupdocs.com/assembly/net/groupdocs.assembly/datasourceinfo/) - wraps data sources

Here are the steps to generate tables from collections:

* Create a table in your template document with a header row
* Add a data band row using `<<foreach>>` syntax to iterate over your collection
* Reference collection item properties in table cells
* Close the data band with `<<foreach>>`
* Assemble the document with your collection data

{{< alert style="info" >}}
Table-row data bands automatically repeat the table row for each item in the collection, creating a complete table with all data rows.
{{< /alert >}}

## Generate Table from .NET Object Collection

Create a table from a list of custom objects:

```csharp
using GroupDocs.Assembly;
using System.Collections.Generic;

public class Product
{
    public string Name { get; set; }
    public decimal Price { get; set; }
    public int Quantity { get; set; }
}

public static void GenerateTableFromCollection()
{
    // Create sample data
    List<Product> products = new List<Product>
    {
        new Product { Name = "Laptop", Price = 999.99m, Quantity = 5 },
        new Product { Name = "Mouse", Price = 29.99m, Quantity = 20 },
        new Product { Name = "Keyboard", Price = 79.99m, Quantity = 15 }
    };
    
    // Assemble document
    DocumentAssembler assembler = new DocumentAssembler();
    assembler.AssembleDocument("TableTemplate.docx", "TableOutput.docx", 
        new DataSourceInfo(products, "products"));
    
    Console.WriteLine("Table generated successfully.");
}
```

## Template Structure for Tables

In your template document (TableTemplate.docx), create a table with this structure:

| Product Name | Price | Quantity |
|--------------|-------|----------|
| `<<foreach [in products]>>` | | |
| `<<[Name]>>` | `<<[Price]>>` | `<<[Quantity]>>` |
| `<<foreach>>` | | |

The `<<foreach>>` tags should span the entire data row. After assembly, you'll get:

| Product Name | Price | Quantity |
|--------------|-------|----------|
| Laptop | 999.99 | 5 |
| Mouse | 29.99 | 20 |
| Keyboard | 79.99 | 15 |

## Generate Table with Formatting

You can format table cell values using format strings:

```csharp
using GroupDocs.Assembly;
using System.Collections.Generic;

public static void GenerateFormattedTable()
{
    List<Product> products = new List<Product>
    {
        new Product { Name = "Laptop", Price = 999.99m, Quantity = 5 },
        new Product { Name = "Mouse", Price = 29.99m, Quantity = 20 }
    };
    
    DocumentAssembler assembler = new DocumentAssembler();
    assembler.AssembleDocument("TableTemplate.docx", "FormattedTable.docx", 
        new DataSourceInfo(products, "products"));
}
```

Template with formatting:

| Product Name | Price | Quantity |
|--------------|-------|----------|
| `<<foreach [in products]>>` | | |
| `<<[Name]>>` | `<<[Price]:"C">>` | `<<[Quantity]>>` |
| `<<foreach>>` | | |

The `:"C"` format string formats the price as currency.

## Generate Table from DataTable

You can also generate tables from ADO.NET DataTable:

```csharp
using GroupDocs.Assembly;
using System.Data;

public static void GenerateTableFromDataTable()
{
    // Create DataTable
    DataTable productsTable = new DataTable("Products");
    productsTable.Columns.Add("Name", typeof(string));
    productsTable.Columns.Add("Price", typeof(decimal));
    productsTable.Columns.Add("Quantity", typeof(int));
    
    // Add rows
    productsTable.Rows.Add("Laptop", 999.99m, 5);
    productsTable.Rows.Add("Mouse", 29.99m, 20);
    productsTable.Rows.Add("Keyboard", 79.99m, 15);
    
    DocumentAssembler assembler = new DocumentAssembler();
    assembler.AssembleDocument("TableTemplate.docx", "DataTableOutput.docx", 
        new DataSourceInfo(productsTable, "products"));
    
    Console.WriteLine("Table generated from DataTable successfully.");
}
```

## Generate Table with Totals

Add a total row after the data rows:

```csharp
using GroupDocs.Assembly;
using System.Collections.Generic;

public static void GenerateTableWithTotals()
{
    List<Product> products = new List<Product>
    {
        new Product { Name = "Laptop", Price = 999.99m, Quantity = 5 },
        new Product { Name = "Mouse", Price = 29.99m, Quantity = 20 },
        new Product { Name = "Keyboard", Price = 79.99m, Quantity = 15 }
    };
    
    DocumentAssembler assembler = new DocumentAssembler();
    assembler.AssembleDocument("TableWithTotalsTemplate.docx", "TableWithTotals.docx", 
        new DataSourceInfo(products, "products"));
    
    Console.WriteLine("Table with totals generated successfully.");
}
```

Template structure:

| Product Name | Price | Quantity |
|--------------|-------|----------|
| `<<foreach [in products]>>` | | |
| `<<[Name]>>` | `<<[Price]:"C">>` | `<<[Quantity]>>` |
| `<<foreach>>` | | |
| **Total** | `<<[products.Sum(p => p.Price)]:"C">>` | `<<[products.Sum(p => p.Quantity)]>>` |

## Generate Table in Spreadsheet

Tables work similarly in spreadsheet templates:

```csharp
using GroupDocs.Assembly;
using System.Collections.Generic;

public static void GenerateTableInSpreadsheet()
{
    List<Product> products = new List<Product>
    {
        new Product { Name = "Laptop", Price = 999.99m, Quantity = 5 },
        new Product { Name = "Mouse", Price = 29.99m, Quantity = 20 }
    };
    
    DocumentAssembler assembler = new DocumentAssembler();
    assembler.AssembleDocument("TableTemplate.xlsx", "TableOutput.xlsx", 
        new DataSourceInfo(products, "products"));
    
    Console.WriteLine("Table generated in spreadsheet successfully.");
}
```

{{< alert style="warning" >}}
In spreadsheet templates, the data band row must be within a table structure. Select the range and create a table in Excel before adding the foreach syntax.
{{< /alert >}}

### Advanced Usage Topics

To learn more about filtering, sorting, grouping table data, conditional table rows, and advanced table formatting, please refer to the [advanced usage section]({{< ref "assembly/net/developer-guide/advanced-usage/_index.md" >}}).

## More resources

### GitHub Examples

You may easily run the code above and see the feature in action in our GitHub examples:

* [GroupDocs.Assembly for .NET examples, plugins, and showcase](https://github.com/groupdocs-assembly/GroupDocs.Assembly-for-.NET)
* [GroupDocs.Assembly for Java examples, plugins, and showcase](https://github.com/groupdocs-assembly/GroupDocs.Assembly-for-Java)
* [GroupDocs.Assembly for Python via .NET examples, plugins, and showcase](https://github.com/groupdocs-assembly/GroupDocs.Assembly-for-Python-via-.NET)

### Free Online Apps

Along with the full-featured .NET library, we provide simple but powerful free online apps.

To assemble documents from templates and data sources, you can use the online apps from the **[GroupDocs.Assembly App Product Family](https://products.groupdocs.app/assembly/family)**.

