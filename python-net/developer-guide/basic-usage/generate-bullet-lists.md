---
id: assembly-basic-usage-generate-bullet-lists
url: assembly/python-net/basic-usage-generate-bullet-lists
linktitle: Generate Bullet Lists
title: Generate Bullet Lists from Data Source
weight: 16
description: "Create bulleted lists in Word, Excel and email documents from Python lists, dicts and database rows by iterating over them with foreach data bands."
keywords: bullet lists, bulleted lists, foreach data band, list items, collection iteration, generate bullets, Python list, sqlite3, Python
productName: GroupDocs.Assembly for Python via .NET
hideChildren: False
---

## Overview

Bullet lists are a common way to display collections of items in documents. GroupDocs.Assembly for Python via .NET makes it easy to generate bulleted lists by iterating over data collections using foreach data bands within list structures.

The main classes involved are:
- [DocumentAssembler](https://reference.groupdocs.com/assembly/python-net/groupdocs.assembly/documentassembler/) - assembles documents
- [DataSourceInfo](https://reference.groupdocs.com/assembly/python-net/groupdocs.assembly/datasourceinfo/) - wraps data sources

Here are the steps to generate bullet lists:

* Create a bullet list in your template document
* Add a foreach data band within the list to iterate over your collection
* Reference collection item properties in list items
* Close the foreach data band
* Assemble the document with your collection data

{{< alert style="info" >}}
The foreach data band automatically repeats list items for each element in the collection, creating a complete bulleted list with all data items.
{{< /alert >}}

## Generate Bullet List from a Python List

Create a bullet list from a list of dicts:

{{< tabs "example1" >}}
{{< tab "Python" >}}
```python
from groupdocs.assembly import DataSourceInfo, DocumentAssembler

# Create sample data
products = [
    {"Name": "Harbor Blend whole bean coffee", "Description": "Medium roast, roasted weekly"},
    {"Name": "Aged harbour cheddar", "Description": "Matured for two years"},
    {"Name": "Cold-pressed olive oil", "Description": "First cold pressing"},
]

# Assemble document
assembler = DocumentAssembler()
assembler.assemble_document("product-bullets.docx", "product-bullets-report.docx",
                            DataSourceInfo(products, "products"))

print("Bullet list generated successfully.")
```
{{< /tab >}}
{{< tab "product-bullets.docx" >}}
{{< tab-text >}}
The following sample file is used in this example: [product-bullets.docx](/assembly/python-net/_sample_files/developer-guide/basic-usage/generate-bullet-lists/product-bullets.docx)
{{< /tab-text >}}
{{< /tab >}}
{{< tab "product-bullets-report.docx" >}}  
```text
Binary file (DOCX, 8 KB)
```
[Download full output](/assembly/python-net/_output_files/developer-guide/basic-usage/generate-bullet-lists/generate_bullet_list_from_a_python_list/product-bullets-report.docx)
{{< /tab >}}
{{< /tabs >}}

## Template Structure for Bullet Lists

In your template document (product-bullets.docx), create a bullet list with this structure:

```text
We provide the following products:

• <<foreach [in products]>><<[Name]>> - <<[Description]>>
<</foreach>>
```

The data band opens inside the bulleted paragraph and closes at the start of the next one, so the band holds the whole list paragraph and each product gets a bullet of its own. After assembly, you'll get:

```text
We provide the following products:

• Harbor Blend whole bean coffee - Medium roast, roasted weekly
• Aged harbour cheddar - Matured for two years
• Cold-pressed olive oil - First cold pressing
```

## Generate Bullet List from Database Rows

ADO.NET's `DataTable` has no Python counterpart. Rows read from a database become a list of dicts, which the template reads the same way. This example reads the products from an SQLite table with Python's `sqlite3` module:

{{< tabs "example2" >}}
{{< tab "Python" >}}
```python
import sqlite3

from groupdocs.assembly import DataSourceInfo, DocumentAssembler

# Create a table
connection = sqlite3.connect(":memory:")
connection.row_factory = sqlite3.Row
connection.execute("CREATE TABLE Products (Name TEXT, Description TEXT)")

# Add rows
connection.executemany("INSERT INTO Products VALUES (?, ?)", [
    ("Harbor Blend whole bean coffee", "Medium roast, roasted weekly"),
    ("Aged harbour cheddar", "Matured for two years"),
    ("Cold-pressed olive oil", "First cold pressing"),
])

# Each row becomes a dict: its column names are the member names the template reads
products = [dict(row) for row in connection.execute("SELECT Name, Description FROM Products")]
connection.close()

assembler = DocumentAssembler()
assembler.assemble_document("product-bullets.docx", "product-bullets-from-database.docx",
                            DataSourceInfo(products, "products"))

print("Bullet list generated from database rows successfully.")
```
{{< /tab >}}
{{< tab "product-bullets.docx" >}}
{{< tab-text >}}
The following sample file is used in this example: [product-bullets.docx](/assembly/python-net/_sample_files/developer-guide/basic-usage/generate-bullet-lists/product-bullets.docx)
{{< /tab-text >}}
{{< /tab >}}
{{< tab "product-bullets-from-database.docx" >}}  
```text
Binary file (DOCX, 8 KB)
```
[Download full output](/assembly/python-net/_output_files/developer-guide/basic-usage/generate-bullet-lists/generate_bullet_list_from_database_rows/product-bullets-from-database.docx)
{{< /tab >}}
{{< /tabs >}}

## Simple Bullet List (Name Only)

For simple lists showing only names:

{{< tabs "example3" >}}
{{< tab "Python" >}}
```python
from groupdocs.assembly import DataSourceInfo, DocumentAssembler

items = [
    "Next-day delivery",
    "Cold-chain storage",
    "Menu pairing advice",
]

assembler = DocumentAssembler()
assembler.assemble_document("simple-bullets.docx", "simple-bullets-report.docx",
                            DataSourceInfo(items, "items"))

print("Simple bullet list generated successfully.")
```
{{< /tab >}}
{{< tab "simple-bullets.docx" >}}
{{< tab-text >}}
The following sample file is used in this example: [simple-bullets.docx](/assembly/python-net/_sample_files/developer-guide/basic-usage/generate-bullet-lists/simple-bullets.docx)
{{< /tab-text >}}
{{< /tab >}}
{{< tab "simple-bullets-report.docx" >}}  
```text
Binary file (DOCX, 8 KB)
```
[Download full output](/assembly/python-net/_output_files/developer-guide/basic-usage/generate-bullet-lists/simple_bullet_list_name_only/simple-bullets-report.docx)
{{< /tab >}}
{{< /tabs >}}

Template for simple list:

```text
Items:
• <<foreach [item in items]>><<[item]>>
<</foreach>>
```

A string has no members to name, so the data band names its iteration variable (`item`) and outputs the item itself with `<<[item]>>`.

## Bullet List in Spreadsheet

Bullet lists work in spreadsheet templates too:

{{< tabs "example4" >}}
{{< tab "Python" >}}
```python
from groupdocs.assembly import DataSourceInfo, DocumentAssembler

products = [
    {"Name": "Harbor Blend whole bean coffee", "Description": "Medium roast, roasted weekly"},
    {"Name": "Aged harbour cheddar", "Description": "Matured for two years"},
]

assembler = DocumentAssembler()
assembler.assemble_document("product-bullets.xlsx", "product-bullets-report.xlsx",
                            DataSourceInfo(products, "products"))

print("Bullet list generated in spreadsheet successfully.")
```
{{< /tab >}}
{{< tab "product-bullets.xlsx" >}}
{{< tab-text >}}
The following sample file is used in this example: [product-bullets.xlsx](/assembly/python-net/_sample_files/developer-guide/basic-usage/generate-bullet-lists/product-bullets.xlsx)
{{< /tab-text >}}
{{< /tab >}}
{{< tab "product-bullets-report.xlsx" >}}  
```text
Binary file (XLSX, 7 KB)
```
[Download full output](/assembly/python-net/_output_files/developer-guide/basic-usage/generate-bullet-lists/bullet_list_in_spreadsheet/product-bullets-report.xlsx)
{{< /tab >}}
{{< /tabs >}}

In the spreadsheet, the data band is a row: its first cell opens the band and its last cell closes it, and the bullet character is part of the cell text:

| Product | Description |
|---------|-------------|
| `<<foreach [in products]>>• <<[Name]>>` | `<<[Description]>><</foreach>>` |

## Bullet List in Email

Generate bullet lists in email messages. This template is an EML file whose plain-text body holds the data band:

{{< tabs "example5" >}}
{{< tab "Python" >}}
```python
from groupdocs.assembly import DataSourceInfo, DocumentAssembler

products = [
    {"Name": "Harbor Blend whole bean coffee", "Description": "Medium roast, roasted weekly"},
    {"Name": "Aged harbour cheddar", "Description": "Matured for two years"},
]

assembler = DocumentAssembler()
assembler.assemble_document("product-bullets.eml", "product-bullets-report.eml",
                            DataSourceInfo(products, "products"))

print("Bullet list generated in email successfully.")
```
{{< /tab >}}
{{< tab "product-bullets.eml" >}}
{{< tab-text >}}
The following sample file is used in this example: [product-bullets.eml](/assembly/python-net/_sample_files/developer-guide/basic-usage/generate-bullet-lists/product-bullets.eml)
{{< /tab-text >}}
{{< /tab >}}
{{< tab "product-bullets-report.eml" >}}  
```text
Binary file (EML, 877 bytes)
```
[Download full output](/assembly/python-net/_output_files/developer-guide/basic-usage/generate-bullet-lists/bullet_list_in_email/product-bullets-report.eml)
{{< /tab >}}
{{< /tabs >}}

The message body:

```text
We provide the following products:

<<foreach [in products]>>• <<[Name]>> - <<[Description]>>
<</foreach>>
Harbor Lane Provisions
```

{{< alert style="warning" >}}
In Word documents, ensure the bullet list formatting is applied in the template. The foreach data band will repeat the list item format for each collection element.
{{< /alert >}}

### Advanced Usage Topics

To learn more about nested bullet lists, conditional list items, and advanced list formatting, please refer to the [advanced usage section]({{< ref "assembly/python-net/developer-guide/advanced-usage/_index.md" >}}).

## More resources

### GitHub Examples

You may easily run the code above and see the feature in action in our GitHub examples:

* [GroupDocs.Assembly for .NET examples, plugins, and showcase](https://github.com/groupdocs-assembly/GroupDocs.Assembly-for-.NET)
* [GroupDocs.Assembly for Java examples, plugins, and showcase](https://github.com/groupdocs-assembly/GroupDocs.Assembly-for-Java)
* [GroupDocs.Assembly for Python via .NET examples, plugins, and showcase](https://github.com/groupdocs-assembly/GroupDocs.Assembly-for-Python-via-.NET)

### Free Online Apps

Along with the full-featured library, we provide simple but powerful free online apps.

To assemble documents from templates and data sources, you can use the online apps from the **[GroupDocs.Assembly App Product Family](https://products.groupdocs.app/assembly/family)**.
