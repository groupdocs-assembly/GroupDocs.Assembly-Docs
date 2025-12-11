---
id: assembly-basic-usage-generate-bullet-lists
url: assembly/net/basic-usage-generate-bullet-lists
linktitle: Generate Bullet Lists
title: Generate Bullet Lists from Data Source
weight: 16
description: "Create bulleted lists in documents by iterating over data collections and displaying items as bullets."
keywords: bullet lists, bulleted lists, foreach data band, list items, collection iteration, generate bullets
productName: GroupDocs.Assembly for .NET
hideChildren: False
---

## Overview

Bullet lists are a common way to display collections of items in documents. GroupDocs.Assembly for .NET makes it easy to generate bulleted lists by iterating over data collections using foreach data bands within list structures.

The main classes involved are:
- [DocumentAssembler](https://reference.groupdocs.com/assembly/net/groupdocs.assembly/documentassembler/) - assembles documents
- [DataSourceInfo](https://reference.groupdocs.com/assembly/net/groupdocs.assembly/datasourceinfo/) - wraps data sources

Here are the steps to generate bullet lists:

* Create a bullet list in your template document
* Add a foreach data band within the list to iterate over your collection
* Reference collection item properties in list items
* Close the foreach data band
* Assemble the document with your collection data

{{< alert style="info" >}}
The foreach data band automatically repeats list items for each element in the collection, creating a complete bulleted list with all data items.
{{< /alert >}}

## Generate Bullet List from .NET Collection

Create a bullet list from a list of objects:

```csharp
using GroupDocs.Assembly;
using System.Collections.Generic;

public class Product
{
    public string Name { get; set; }
    public string Description { get; set; }
}

public static void GenerateBulletList()
{
    // Create sample data
    List<Product> products = new List<Product>
    {
        new Product { Name = "Laptop", Description = "High-performance laptop" },
        new Product { Name = "Mouse", Description = "Wireless mouse" },
        new Product { Name = "Keyboard", Description = "Mechanical keyboard" }
    };
    
    // Assemble document
    DocumentAssembler assembler = new DocumentAssembler();
    assembler.AssembleDocument("BulletListTemplate.docx", "BulletListOutput.docx", 
        new DataSourceInfo(products, "products"));
    
    Console.WriteLine("Bullet list generated successfully.");
}
```

## Template Structure for Bullet Lists

In your template document (BulletListTemplate.docx), create a bullet list with this structure:

```
We provide the following products:

<<foreach [in products]>>
• <<[Name]>> - <<[Description]>>
<</foreach>>
```

After assembly, you'll get:

```
We provide the following products:

• Laptop - High-performance laptop
• Mouse - Wireless mouse
• Keyboard - Mechanical keyboard
```

## Generate Bullet List from DataTable

You can also generate bullet lists from ADO.NET DataTable:

```csharp
using GroupDocs.Assembly;
using System.Data;

public static void GenerateBulletListFromDataTable()
{
    // Create DataTable
    DataTable productsTable = new DataTable("Products");
    productsTable.Columns.Add("Name", typeof(string));
    productsTable.Columns.Add("Description", typeof(string));
    
    // Add rows
    productsTable.Rows.Add("Laptop", "High-performance laptop");
    productsTable.Rows.Add("Mouse", "Wireless mouse");
    productsTable.Rows.Add("Keyboard", "Mechanical keyboard");
    
    DocumentAssembler assembler = new DocumentAssembler();
    assembler.AssembleDocument("BulletListTemplate.docx", "BulletListOutput.docx", 
        new DataSourceInfo(productsTable, "products"));
    
    Console.WriteLine("Bullet list generated from DataTable successfully.");
}
```

## Simple Bullet List (Name Only)

For simple lists showing only names:

```csharp
using GroupDocs.Assembly;
using System.Collections.Generic;

public static void GenerateSimpleBulletList()
{
    List<string> items = new List<string> 
    { 
        "Item 1", 
        "Item 2", 
        "Item 3" 
    };
    
    DocumentAssembler assembler = new DocumentAssembler();
    assembler.AssembleDocument("SimpleBulletListTemplate.docx", "SimpleBulletListOutput.docx", 
        new DataSourceInfo(items, "items"));
    
    Console.WriteLine("Simple bullet list generated successfully.");
}
```

Template for simple list:

```
Items:
<<foreach [in items]>>
• <<[items_Text]>>
<</foreach>>
```

## Bullet List in Spreadsheet

Bullet lists work in spreadsheet templates too:

```csharp
using GroupDocs.Assembly;
using System.Collections.Generic;

public static void GenerateBulletListInSpreadsheet()
{
    List<Product> products = new List<Product>
    {
        new Product { Name = "Laptop", Description = "High-performance laptop" },
        new Product { Name = "Mouse", Description = "Wireless mouse" }
    };
    
    DocumentAssembler assembler = new DocumentAssembler();
    assembler.AssembleDocument("BulletListTemplate.xlsx", "BulletListOutput.xlsx", 
        new DataSourceInfo(products, "products"));
    
    Console.WriteLine("Bullet list generated in spreadsheet successfully.");
}
```

## Bullet List in Email

Generate bullet lists in email messages:

```csharp
using GroupDocs.Assembly;
using System.Collections.Generic;

public static void GenerateBulletListInEmail()
{
    List<Product> products = new List<Product>
    {
        new Product { Name = "Laptop", Description = "High-performance laptop" },
        new Product { Name = "Mouse", Description = "Wireless mouse" }
    };
    
    DocumentAssembler assembler = new DocumentAssembler();
    assembler.AssembleDocument("BulletListTemplate.msg", "BulletListOutput.msg", 
        new DataSourceInfo(products, "products"));
    
    Console.WriteLine("Bullet list generated in email successfully.");
}
```

{{< alert style="warning" >}}
In Word documents, ensure the bullet list formatting is applied in the template. The foreach data band will repeat the list item format for each collection element.
{{< /alert >}}

### Advanced Usage Topics

To learn more about nested bullet lists, conditional list items, and advanced list formatting, please refer to the [advanced usage section]({{< ref "assembly/net/developer-guide/advanced-usage/_index.md" >}}).

## More resources

### GitHub Examples

You may easily run the code above and see the feature in action in our GitHub examples:

* [GroupDocs.Assembly for .NET examples, plugins, and showcase](https://github.com/groupdocs-assembly/GroupDocs.Assembly-for-.NET)
* [GroupDocs.Assembly for Java examples, plugins, and showcase](https://github.com/groupdocs-assembly/GroupDocs.Assembly-for-Java)
* [GroupDocs.Assembly for Python via .NET examples, plugins, and showcase](https://github.com/groupdocs-assembly/GroupDocs.Assembly-for-Python-via-.NET)

### Free Online Apps

Along with the full-featured .NET library, we provide simple but powerful free online apps.

To assemble documents from templates and data sources, you can use the online apps from the **[GroupDocs.Assembly App Product Family](https://products.groupdocs.app/assembly/family)**.

