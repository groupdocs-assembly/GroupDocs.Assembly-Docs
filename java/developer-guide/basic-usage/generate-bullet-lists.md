---
id: assembly-basic-usage-generate-bullet-lists-java
url: assembly/java/basic-usage-generate-bullet-lists
linktitle: Generate Bullet Lists
title: Generate Bullet Lists from Data Source
weight: 16
description: "Create bulleted lists in documents by iterating over data collections and displaying items as bullets using GroupDocs.Assembly for Java."
keywords: bullet lists, bulleted lists, foreach data band, list items, collection iteration, generate bullets
productName: GroupDocs.Assembly for Java
hideChildren: False
---

## Overview

Bullet lists are a common way to display collections of items in documents. GroupDocs.Assembly for Java makes it easy to generate bulleted lists by iterating over data collections using foreach data bands within list structures.

The main classes involved are:
- [DocumentAssembler](https://reference.groupdocs.com/assembly/java/com.groupdocs.assembly/documentassembler/) - assembles documents
- [DataSourceInfo](https://reference.groupdocs.com/assembly/java/com.groupdocs.assembly/datasourceinfo/) - wraps data sources

Here are the steps to generate bullet lists:

* Create a bullet list in your template document
* Add a foreach data band within the list to iterate over your collection
* Reference collection item members in list items
* Close the foreach data band
* Assemble the document with your collection data

{{< alert style="info" >}}
The foreach data band automatically repeats list items for each element in the collection, creating a complete bulleted list with all data items.
{{< /alert >}}

## Generate Bullet List from Java Collection

Create a bullet list from a collection of objects:

```java
import com.groupdocs.assembly.*;

public class Product
{
    private final String name;
    private final String description;

    public Product(String name, String description)
    {
        this.name = name;
        this.description = description;
    }

    public String getName() { return name; }
    public String getDescription() { return description; }
}

public static void generateBulletList() throws Exception
{
    // Create sample data
    Product[] products =
    {
        new Product("Laptop", "High-performance laptop"),
        new Product("Mouse", "Wireless mouse"),
        new Product("Keyboard", "Mechanical keyboard")
    };

    // Assemble document
    DocumentAssembler assembler = new DocumentAssembler();
    assembler.assembleDocument("BulletListTemplate.docx", "BulletListOutput.docx",
        new DataSourceInfo(products, "products"));

    System.out.println("Bullet list generated successfully.");
}
```

{{< alert style="info" >}}
Because of Java type erasure, the engine cannot determine the item type of a `java.util.List` passed directly as a data source, so calling item methods such as `getName()` fails. Pass an array (as shown above), or expose the list through a getter of a wrapper object (for example, `public List<Product> getProducts()`) and iterate over it in the template: `<<foreach [in data.getProducts()]>>`.
{{< /alert >}}

## Template Structure for Bullet Lists

In your template document (BulletListTemplate.docx), create a bullet list with this structure:

```
We provide the following products:

<<foreach [in products]>>• <<[getName()]>> - <<[getDescription()]>>
<</foreach>>
```

Put the opening `<<foreach>>` tag at the beginning of the bulleted paragraph and the closing `<</foreach>>` tag at the beginning of the next paragraph. Members of Java objects are accessed through their getter methods. After assembly, you'll get:

```
We provide the following products:

• Laptop - High-performance laptop
• Mouse - Wireless mouse
• Keyboard - Mechanical keyboard
```

## Generate Bullet List from DataTable

You can also generate bullet lists from a [DataTable](https://reference.groupdocs.com/assembly/java/com.groupdocs.assembly.system.data/datatable/):

```java
import com.groupdocs.assembly.*;
import com.groupdocs.assembly.system.data.*;

public static void generateBulletListFromDataTable() throws Exception
{
    // Create DataTable
    DataTable productsTable = new DataTable("Products");
    productsTable.getColumns().add("Name", String.class);
    productsTable.getColumns().add("Description", String.class);

    // Add rows
    productsTable.getRows().add("Laptop", "High-performance laptop");
    productsTable.getRows().add("Mouse", "Wireless mouse");
    productsTable.getRows().add("Keyboard", "Mechanical keyboard");

    DocumentAssembler assembler = new DocumentAssembler();
    assembler.assembleDocument("DataTableBulletListTemplate.docx", "BulletListOutput.docx",
        new DataSourceInfo(productsTable, "products"));

    System.out.println("Bullet list generated from DataTable successfully.");
}
```

DataTable columns are referenced by name rather than through getters, so the template (DataTableBulletListTemplate.docx) looks as follows:

```
We provide the following products:

<<foreach [in products]>>• <<[Name]>> - <<[Description]>>
<</foreach>>
```

## Simple Bullet List (Name Only)

For simple lists showing only names:

```java
import com.groupdocs.assembly.*;
import java.util.*;

public static void generateSimpleBulletList() throws Exception
{
    List<String> items = Arrays.asList(
        "Item 1",
        "Item 2",
        "Item 3"
    );

    DocumentAssembler assembler = new DocumentAssembler();
    assembler.assembleDocument("SimpleBulletListTemplate.docx", "SimpleBulletListOutput.docx",
        new DataSourceInfo(items, "items"));

    System.out.println("Simple bullet list generated successfully.");
}
```

Template for simple list:

```
Items:
<<foreach [item in items]>>• <<[item]>>
<</foreach>>
```

Here, the iteration variable `item` refers to the current string itself.

## Bullet List in Spreadsheet

Bullet lists work in spreadsheet templates too:

```java
import com.groupdocs.assembly.*;

public static void generateBulletListInSpreadsheet() throws Exception
{
    Product[] products =
    {
        new Product("Laptop", "High-performance laptop"),
        new Product("Mouse", "Wireless mouse")
    };

    DocumentAssembler assembler = new DocumentAssembler();
    assembler.assembleDocument("BulletListTemplate.xlsx", "BulletListOutput.xlsx",
        new DataSourceInfo(products, "products"));

    System.out.println("Bullet list generated in spreadsheet successfully.");
}
```

## Bullet List in Email

Generate bullet lists in email messages:

```java
import com.groupdocs.assembly.*;

public static void generateBulletListInEmail() throws Exception
{
    Product[] products =
    {
        new Product("Laptop", "High-performance laptop"),
        new Product("Mouse", "Wireless mouse")
    };

    DocumentAssembler assembler = new DocumentAssembler();
    assembler.assembleDocument("BulletListTemplate.msg", "BulletListOutput.msg",
        new DataSourceInfo(products, "products"));

    System.out.println("Bullet list generated in email successfully.");
}
```

{{< alert style="warning" >}}
In Word documents, ensure the bullet list formatting is applied in the template. The foreach data band will repeat the list item format for each collection element.
{{< /alert >}}

### Advanced Usage Topics

To learn more about nested bullet lists, conditional list items, and advanced list formatting, please refer to the [advanced usage section]({{< ref "assembly/java/developer-guide/advanced-usage/_index.md" >}}).

## More resources

### GitHub Examples

You may easily run the code above and see the feature in action in our GitHub examples:

* [GroupDocs.Assembly for Java examples, plugins, and showcase](https://github.com/groupdocs-assembly/GroupDocs.Assembly-for-Java)
* [GroupDocs.Assembly for .NET examples, plugins, and showcase](https://github.com/groupdocs-assembly/GroupDocs.Assembly-for-.NET)
* [GroupDocs.Assembly for Python via .NET examples, plugins, and showcase](https://github.com/groupdocs-assembly/GroupDocs.Assembly-for-Python-via-.NET)

### Free Online Apps

Along with the full-featured Java library, we provide simple but powerful free online apps.

To assemble documents from templates and data sources, you can use the online apps from the **[GroupDocs.Assembly App Product Family](https://products.groupdocs.app/assembly/family)**.
