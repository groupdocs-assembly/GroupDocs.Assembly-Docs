---
id: assembly-basic-usage-generate-tables-java
url: assembly/java/basic-usage-generate-tables
linktitle: Generate Tables
title: Generate Tables from Collection Data
weight: 15
description: "Create dynamic tables in documents by iterating over collections and displaying data in table rows using GroupDocs.Assembly for Java."
keywords: generate tables, table reports, foreach data band, table rows, collection data, tabular data, dynamic tables
productName: GroupDocs.Assembly for Java
hideChildren: False
---

## Overview

Tables are one of the most common ways to display structured data in documents. GroupDocs.Assembly for Java makes it easy to generate dynamic tables by iterating over collections and populating table rows with data.

The main classes involved are:
- [DocumentAssembler](https://reference.groupdocs.com/assembly/java/com.groupdocs.assembly/documentassembler/) - assembles documents
- [DataSourceInfo](https://reference.groupdocs.com/assembly/java/com.groupdocs.assembly/datasourceinfo/) - wraps data sources

Here are the steps to generate tables from collections:

* Create a table in your template document with a header row
* Add a data band row using `<<foreach>>` syntax to iterate over your collection
* Reference collection item members in table cells
* Close the data band with `<</foreach>>`
* Assemble the document with your collection data

{{< alert style="info" >}}
Table-row data bands automatically repeat the table row for each item in the collection, creating a complete table with all data rows.
{{< /alert >}}

## Generate Table from Java Object Collection

Create a table from a collection of custom objects:

```java
import com.groupdocs.assembly.*;

public class Product
{
    private final String name;
    private final double price;
    private final int quantity;

    public Product(String name, double price, int quantity)
    {
        this.name = name;
        this.price = price;
        this.quantity = quantity;
    }

    public String getName() { return name; }
    public double getPrice() { return price; }
    public int getQuantity() { return quantity; }
}

public static void generateTableFromCollection() throws Exception
{
    // Create sample data
    Product[] products =
    {
        new Product("Laptop", 999.99, 5),
        new Product("Mouse", 29.99, 20),
        new Product("Keyboard", 79.99, 15)
    };

    // Assemble document
    DocumentAssembler assembler = new DocumentAssembler();
    assembler.assembleDocument("TableTemplate.docx", "TableOutput.docx",
        new DataSourceInfo(products, "products"));

    System.out.println("Table generated successfully.");
}
```

{{< alert style="info" >}}
Because of Java type erasure, the engine cannot determine the item type of a `java.util.List` passed directly as a data source, so calling item methods such as `getName()` fails. Pass an array (as shown above), or expose the list through a getter of a wrapper object (for example, `public List<Product> getProducts()`) and iterate over it in the template: `<<foreach [in data.getProducts()]>>`.
{{< /alert >}}

## Template Structure for Tables

In your template document (TableTemplate.docx), create a table with this structure:

| Product Name | Price | Quantity |
|--------------|-------|----------|
| `<<foreach [in products]>><<[getName()]>>` | `<<[getPrice()]>>` | `<<[getQuantity()]>><</foreach>>` |

The opening `<<foreach>>` tag must be placed at the beginning of the first cell of the data row, and the closing `<</foreach>>` tag at the end of the last cell, so that the data band spans the entire row. Members of Java objects are accessed through their getter methods. After assembly, you'll get:

| Product Name | Price | Quantity |
|--------------|-------|----------|
| Laptop | 999.99 | 5 |
| Mouse | 29.99 | 20 |
| Keyboard | 79.99 | 15 |

## Generate Table with Formatting

You can format table cell values using format strings:

```java
import com.groupdocs.assembly.*;

public static void generateFormattedTable() throws Exception
{
    Product[] products =
    {
        new Product("Laptop", 999.99, 5),
        new Product("Mouse", 29.99, 20)
    };

    DocumentAssembler assembler = new DocumentAssembler();
    assembler.assembleDocument("TableTemplate.docx", "FormattedTable.docx",
        new DataSourceInfo(products, "products"));
}
```

Template with formatting:

| Product Name | Price | Quantity |
|--------------|-------|----------|
| `<<foreach [in products]>><<[getName()]>>` | `<<[getPrice()]:"$#,##0.00">>` | `<<[getQuantity()]>><</foreach>>` |

The `:"$#,##0.00"` format string formats the price as currency (for example, `$999.99`). Number format strings follow the `java.text.DecimalFormat` pattern syntax, and the decimal and grouping separators depend on the current locale.

## Generate Table from DataTable

You can also generate tables from a [DataTable](https://reference.groupdocs.com/assembly/java/com.groupdocs.assembly.system.data/datatable/):

```java
import com.groupdocs.assembly.*;
import com.groupdocs.assembly.system.data.*;

public static void generateTableFromDataTable() throws Exception
{
    // Create DataTable
    DataTable productsTable = new DataTable("Products");
    productsTable.getColumns().add("Name", String.class);
    productsTable.getColumns().add("Price", Double.class);
    productsTable.getColumns().add("Quantity", Integer.class);

    // Add rows
    productsTable.getRows().add("Laptop", 999.99, 5);
    productsTable.getRows().add("Mouse", 29.99, 20);
    productsTable.getRows().add("Keyboard", 79.99, 15);

    DocumentAssembler assembler = new DocumentAssembler();
    assembler.assembleDocument("DataTableTemplate.docx", "DataTableOutput.docx",
        new DataSourceInfo(productsTable, "products"));

    System.out.println("Table generated from DataTable successfully.");
}
```

DataTable columns are referenced by name rather than through getters, so the template (DataTableTemplate.docx) looks as follows:

| Product Name | Price | Quantity |
|--------------|-------|----------|
| `<<foreach [in products]>><<[Name]>>` | `<<[Price]>>` | `<<[Quantity]>><</foreach>>` |

## Generate Table with Totals

Add a total row after the data rows:

```java
import com.groupdocs.assembly.*;

public static void generateTableWithTotals() throws Exception
{
    Product[] products =
    {
        new Product("Laptop", 999.99, 5),
        new Product("Mouse", 29.99, 20),
        new Product("Keyboard", 79.99, 15)
    };

    DocumentAssembler assembler = new DocumentAssembler();
    assembler.assembleDocument("TableWithTotalsTemplate.docx", "TableWithTotals.docx",
        new DataSourceInfo(products, "products"));

    System.out.println("Table with totals generated successfully.");
}
```

Template structure:

| Product Name | Price | Quantity |
|--------------|-------|----------|
| `<<foreach [in products]>><<[getName()]>>` | `<<[getPrice()]:"$#,##0.00">>` | `<<[getQuantity()]>><</foreach>>` |
| **Total** | `<<[products.sum(p => p.getPrice())]:"$#,##0.00">>` | `<<[products.sum(p => p.getQuantity())]>>` |

## Generate Table in Spreadsheet

Tables work similarly in spreadsheet templates:

```java
import com.groupdocs.assembly.*;

public static void generateTableInSpreadsheet() throws Exception
{
    Product[] products =
    {
        new Product("Laptop", 999.99, 5),
        new Product("Mouse", 29.99, 20)
    };

    DocumentAssembler assembler = new DocumentAssembler();
    assembler.assembleDocument("TableTemplate.xlsx", "TableOutput.xlsx",
        new DataSourceInfo(products, "products"));

    System.out.println("Table generated in spreadsheet successfully.");
}
```

{{< alert style="warning" >}}
In spreadsheet templates, the data band is a row of cells: put the opening `<<foreach>>` tag at the beginning of the first cell of the row and the closing `<</foreach>>` tag at the end of the last cell of the row. The row is repeated for each item in the collection.
{{< /alert >}}

### Advanced Usage Topics

To learn more about filtering, sorting, grouping table data, conditional table rows, and advanced table formatting, please refer to the [advanced usage section]({{< ref "assembly/java/developer-guide/advanced-usage/_index.md" >}}).

## More resources

### GitHub Examples

You may easily run the code above and see the feature in action in our GitHub examples:

* [GroupDocs.Assembly for Java examples, plugins, and showcase](https://github.com/groupdocs-assembly/GroupDocs.Assembly-for-Java)
* [GroupDocs.Assembly for .NET examples, plugins, and showcase](https://github.com/groupdocs-assembly/GroupDocs.Assembly-for-.NET)
* [GroupDocs.Assembly for Python via .NET examples, plugins, and showcase](https://github.com/groupdocs-assembly/GroupDocs.Assembly-for-Python-via-.NET)

### Free Online Apps

Along with the full-featured Java library, we provide simple but powerful free online apps.

To assemble documents from templates and data sources, you can use the online apps from the **[GroupDocs.Assembly App Product Family](https://products.groupdocs.app/assembly/family)**.
