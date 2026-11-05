---
id: assembly-basic-usage-generate-tables
url: assembly/python-net/basic-usage-generate-tables
linktitle: Generate Tables
title: Generate Tables from Collection Data
weight: 15
description: "Create dynamic tables in Word and Excel documents from Python lists of dicts and JSON files with table-row data bands, using GroupDocs.Assembly for Python via .NET."
keywords: generate tables, table reports, foreach data band, table rows, collection data, tabular data, dynamic tables, Python list, JSON, Python
productName: GroupDocs.Assembly for Python via .NET
hideChildren: False
---

## Overview

Tables are one of the most common ways to display structured data in documents. GroupDocs.Assembly for Python via .NET makes it easy to generate dynamic tables by iterating over collections and populating table rows with data.

The main classes involved are:
- [DocumentAssembler](https://reference.groupdocs.com/assembly/python-net/groupdocs.assembly/documentassembler/) - assembles documents
- [DataSourceInfo](https://reference.groupdocs.com/assembly/python-net/groupdocs.assembly/datasourceinfo/) - wraps data sources

Here are the steps to generate tables from collections:

* Create a table in your template document with a header row
* Add a data band row using `<<foreach>>` syntax to iterate over your collection
* Reference collection item properties in table cells
* Close the data band with `<</foreach>>`
* Assemble the document with your collection data

{{< alert style="info" >}}
Table-row data bands automatically repeat the table row for each item in the collection, creating a complete table with all data rows.
{{< /alert >}}

## Generate Table from a Python List

Create a table from a list of dicts:

{{< tabs "example1" >}}
{{< tab "Python" >}}
```python
from decimal import Decimal

from groupdocs.assembly import DataSourceInfo, DocumentAssembler

# Create sample data
products = [
    {"Name": "Harbor Blend whole bean coffee", "Price": Decimal("18.40"), "Quantity": 5},
    {"Name": "Aged harbour cheddar", "Price": Decimal("16.50"), "Quantity": 20},
    {"Name": "Cold-pressed olive oil", "Price": Decimal("12.90"), "Quantity": 15},
]

# Assemble document
assembler = DocumentAssembler()
assembler.assemble_document("stock-table.docx", "stock-table-report.docx",
                            DataSourceInfo(products, "products"))

print("Table generated successfully.")
```
{{< /tab >}}
{{< tab "stock-table.docx" >}}
{{< tab-text >}}
The following sample file is used in this example: [stock-table.docx](/assembly/python-net/_sample_files/developer-guide/basic-usage/generate-tables-from-collection/stock-table.docx)
{{< /tab-text >}}
{{< /tab >}}
{{< tab "stock-table-report.docx" >}}  
```text
Binary file (DOCX, 7 KB)
```
[Download full output](/assembly/python-net/_output_files/developer-guide/basic-usage/generate-tables-from-collection/generate_table_from_a_python_list/stock-table-report.docx)
{{< /tab >}}
{{< /tabs >}}

## Template Structure for Tables

In your template document (stock-table.docx), create a table with this structure:

| Product Name | Price | Quantity |
|--------------|-------|----------|
| `<<foreach [in products]>><<[Name]>>` | `<<[Price]>>` | `<<[Quantity]>><</foreach>>` |

The data band spans the entire data row: it opens in the row's first cell and closes in its last cell. After assembly, you'll get:

| Product Name | Price | Quantity |
|--------------|-------|----------|
| Harbor Blend whole bean coffee | 18.40 | 5 |
| Aged harbour cheddar | 16.50 | 20 |
| Cold-pressed olive oil | 12.90 | 15 |

## Generate Table with Formatting

You can format table cell values using format strings:

{{< tabs "example2" >}}
{{< tab "Python" >}}
```python
from decimal import Decimal

from groupdocs.assembly import DataSourceInfo, DocumentAssembler

products = [
    {"Name": "Harbor Blend whole bean coffee", "Price": Decimal("18.40"), "Quantity": 5},
    {"Name": "Aged harbour cheddar", "Price": Decimal("16.50"), "Quantity": 20},
]

assembler = DocumentAssembler()
assembler.assemble_document("stock-price-table.docx", "stock-price-table-report.docx",
                            DataSourceInfo(products, "products"))
```
{{< /tab >}}
{{< tab "stock-price-table.docx" >}}
{{< tab-text >}}
The following sample file is used in this example: [stock-price-table.docx](/assembly/python-net/_sample_files/developer-guide/basic-usage/generate-tables-from-collection/stock-price-table.docx)
{{< /tab-text >}}
{{< /tab >}}
{{< tab "stock-price-table-report.docx" >}}  
```text
Binary file (DOCX, 7 KB)
```
[Download full output](/assembly/python-net/_output_files/developer-guide/basic-usage/generate-tables-from-collection/generate_table_with_formatting/stock-price-table-report.docx)
{{< /tab >}}
{{< /tabs >}}

Template with formatting:

| Product Name | Price | Quantity |
|--------------|-------|----------|
| `<<foreach [in products]>><<[Name]>>` | `<<[Price]:"C">>` | `<<[Quantity]>><</foreach>>` |

The `:"C"` format string formats the price as currency.

## Generate Table from a JSON File

ADO.NET's `DataTable` has no Python counterpart. Rows kept in a JSON file can be passed as they are with [JsonDataSource](https://reference.groupdocs.com/assembly/python-net/groupdocs.assembly.data/jsondatasource/): the file holds an array of objects, and their property names are the member names the template reads.

{{< tabs "example3" >}}
{{< tab "Python" >}}
```python
from groupdocs.assembly import DataSourceInfo, DocumentAssembler
from groupdocs.assembly.data import JsonDataSource

products = JsonDataSource("stock-list.json")

assembler = DocumentAssembler()
assembler.assemble_document("stock-price-table.docx", "stock-price-table-from-json.docx",
                            DataSourceInfo(products, "products"))

print("Table generated from JSON file successfully.")
```
{{< /tab >}}
{{< tab "stock-price-table.docx" >}}
{{< tab-text >}}
The following sample file is used in this example: [stock-price-table.docx](/assembly/python-net/_sample_files/developer-guide/basic-usage/generate-tables-from-collection/stock-price-table.docx)
{{< /tab-text >}}
{{< /tab >}}
{{< tab "stock-list.json" >}}
{{< tab-text >}}
The following sample file is used in this example: [stock-list.json](/assembly/python-net/_sample_files/developer-guide/basic-usage/generate-tables-from-collection/stock-list.json)
{{< /tab-text >}}
{{< /tab >}}
{{< tab "stock-price-table-from-json.docx" >}}  
```text
Binary file (DOCX, 7 KB)
```
[Download full output](/assembly/python-net/_output_files/developer-guide/basic-usage/generate-tables-from-collection/generate_table_from_a_json_file/stock-price-table-from-json.docx)
{{< /tab >}}
{{< /tabs >}}

## Generate Table with Totals

Add a total row after the data rows:

{{< tabs "example4" >}}
{{< tab "Python" >}}
```python
from decimal import Decimal

from groupdocs.assembly import DataSourceInfo, DocumentAssembler

products = [
    {"Name": "Harbor Blend whole bean coffee", "Price": Decimal("18.40"), "Quantity": 5},
    {"Name": "Aged harbour cheddar", "Price": Decimal("16.50"), "Quantity": 20},
    {"Name": "Cold-pressed olive oil", "Price": Decimal("12.90"), "Quantity": 15},
]

assembler = DocumentAssembler()
assembler.assemble_document("stock-totals-table.docx", "stock-totals-table-report.docx",
                            DataSourceInfo(products, "products"))

print("Table with totals generated successfully.")
```
{{< /tab >}}
{{< tab "stock-totals-table.docx" >}}
{{< tab-text >}}
The following sample file is used in this example: [stock-totals-table.docx](/assembly/python-net/_sample_files/developer-guide/basic-usage/generate-tables-from-collection/stock-totals-table.docx)
{{< /tab-text >}}
{{< /tab >}}
{{< tab "stock-totals-table-report.docx" >}}  
```text
Binary file (DOCX, 8 KB)
```
[Download full output](/assembly/python-net/_output_files/developer-guide/basic-usage/generate-tables-from-collection/generate_table_with_totals/stock-totals-table-report.docx)
{{< /tab >}}
{{< /tabs >}}

Template structure:

| Product Name | Price | Quantity |
|--------------|-------|----------|
| `<<foreach [in products]>><<[Name]>>` | `<<[Price]:"C">>` | `<<[Quantity]>><</foreach>>` |
| **Total** | `<<[products.Sum(p => p.Price)]:"C">>` | `<<[products.Sum(p => p.Quantity)]>>` |

## Generate Table in Spreadsheet

Tables work similarly in spreadsheet templates:

{{< tabs "example5" >}}
{{< tab "Python" >}}
```python
from decimal import Decimal

from groupdocs.assembly import DataSourceInfo, DocumentAssembler

products = [
    {"Name": "Harbor Blend whole bean coffee", "Price": Decimal("18.40"), "Quantity": 5},
    {"Name": "Aged harbour cheddar", "Price": Decimal("16.50"), "Quantity": 20},
]

assembler = DocumentAssembler()
assembler.assemble_document("stock-table.xlsx", "stock-table-report.xlsx",
                            DataSourceInfo(products, "products"))

print("Table generated in spreadsheet successfully.")
```
{{< /tab >}}
{{< tab "stock-table.xlsx" >}}
{{< tab-text >}}
The following sample file is used in this example: [stock-table.xlsx](/assembly/python-net/_sample_files/developer-guide/basic-usage/generate-tables-from-collection/stock-table.xlsx)
{{< /tab-text >}}
{{< /tab >}}
{{< tab "stock-table-report.xlsx" >}}  
```text
Binary file (XLSX, 7 KB)
```
[Download full output](/assembly/python-net/_output_files/developer-guide/basic-usage/generate-tables-from-collection/generate_table_in_spreadsheet/stock-table-report.xlsx)
{{< /tab >}}
{{< /tabs >}}

The worksheet holds the same header row and data band row as the Word table, in plain cells.

{{< alert style="warning" >}}
In spreadsheet templates, the data band is a range of cells: the band opens in the first cell of the row and closes in its last cell, and the row is repeated for each item. The cells need no Excel table around them.
{{< /alert >}}

### Advanced Usage Topics

To learn more about filtering, sorting, grouping table data, conditional table rows, and advanced table formatting, please refer to the [advanced usage section]({{< ref "assembly/python-net/developer-guide/advanced-usage/_index.md" >}}).

## More resources

### GitHub Examples

You may easily run the code above and see the feature in action in our GitHub examples:

* [GroupDocs.Assembly for .NET examples, plugins, and showcase](https://github.com/groupdocs-assembly/GroupDocs.Assembly-for-.NET)
* [GroupDocs.Assembly for Java examples, plugins, and showcase](https://github.com/groupdocs-assembly/GroupDocs.Assembly-for-Java)
* [GroupDocs.Assembly for Python via .NET examples, plugins, and showcase](https://github.com/groupdocs-assembly/GroupDocs.Assembly-for-Python-via-.NET)

### Free Online Apps

Along with the full-featured library, we provide simple but powerful free online apps.

To assemble documents from templates and data sources, you can use the online apps from the **[GroupDocs.Assembly App Product Family](https://products.groupdocs.app/assembly/family)**.
