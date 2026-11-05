---
id: quick-start-guide
url: assembly/python-net/quick-start-guide
title: Quick Start Guide
linkTitle: Quick Start Guide
second_title: A simple example of how to use GroupDocs.Assembly for Python via .NET
weight: 4
keywords: quick start, hello world, get started, first report, template, docx, pdf, xlsx, json, pip install, venv, virtual environment, GroupDocs.Assembly, python
description: "Set up a virtual environment, install groupdocs-assembly-net, and run three minimal examples - fill a Word table from a list of dicts, turn a JSON file into a PDF report, and fill an Excel sheet - in under five minutes."
productName: GroupDocs.Assembly for Python via .NET
hideChildren: False
toc: True
---

This guide provides a quick overview of how to set up and start using GroupDocs.Assembly for Python via .NET. The library fills templates, ordinary Word, Excel, PowerPoint, email, HTML or text documents with tags in them, with your data, and saves the result as a report.

## Prerequisites

To proceed, make sure you have:

1. **Configured** environment as described in the [System Requirements]({{< ref "assembly/python-net/getting-started/system-requirements.md" >}}) topic.
2. **Optionally** you may [Get a Temporary License](https://purchase.groupdocs.com/temporary-license/) to test all the product features.

## Set Up Your Development Environment

For best practices, use a virtual environment to manage dependencies in Python applications. Learn more about virtual environments at the [Create and Use Virtual Environments](https://packaging.python.org/en/latest/guides/installing-using-pip-and-virtual-environments/#create-and-use-virtual-environments) documentation topic.

### Create and Activate a Virtual Environment

Create a virtual environment:

{{< tabs "example1">}}
{{< tab "Windows" >}}
```ps
py -m venv .venv
```
{{< /tab >}}
{{< tab "Linux" >}}
```bash
python3 -m venv .venv
```
{{< /tab >}}
{{< tab "macOS" >}}
```bash
python3 -m venv .venv
```
{{< /tab >}}
{{< /tabs >}}

Activate a virtual environment:

{{< tabs "example2">}}
{{< tab "Windows" >}}
```ps
.venv\Scripts\activate
```
{{< /tab >}}
{{< tab "Linux" >}}
```bash
source .venv/bin/activate
```
{{< /tab >}}
{{< tab "macOS" >}}
```bash
source .venv/bin/activate
```
{{< /tab >}}
{{< /tabs >}}

### Install `groupdocs-assembly-net` Package

After activating the virtual environment, run the following command in your terminal to install the latest version of the package:

{{< tabs "example3">}}
{{< tab "Windows" >}}
```ps
py -m pip install groupdocs-assembly-net
```
{{< /tab >}}
{{< tab "Linux" >}}
```bash
python3 -m pip install groupdocs-assembly-net
```
{{< /tab >}}
{{< tab "macOS" >}}
```bash
python3 -m pip install groupdocs-assembly-net
```
{{< /tab >}}
{{< /tabs >}}

Ensure the package is installed successfully. You should see the message

```bash
Successfully installed groupdocs-assembly-net-*
```

## Example 1: Fill a Word table from a list of dicts

To quickly test the library, let's fill the table of a Word template with the orders of one customer. The template, `order-table.docx`, has a heading, a table whose second row repeats for each order, and a total:

```text
Orders of <<[customer]>>
| Order                              | Product          | Quantity          | Price                               |
| <<foreach [o in orders]>><<[o.Number]>> | <<[o.Product]>> | <<[o.Quantity]>> | <<[o.Price]:"0.00">><</foreach>> |
Total: <<[orders.Sum(o => o.Price)]:"0.00">> USD
```

{{< tabs "demo_app_table_report">}}
{{< tab "table_report.py" >}}
```python
import os

from groupdocs.assembly import DataSourceInfo, DocumentAssembler, License

def table_report():
    # Optionally set a license
    license_path = os.path.abspath("./GroupDocs.Assembly.lic")
    if os.path.exists(license_path):
        License().set_license(license_path)

    # The data: one dict per table row, with the keys the template reads
    orders = [
        {"Number": 10001, "Product": "Harbor Blend whole bean coffee", "Quantity": 30, "Price": 552.0},
        {"Number": 10004, "Product": "Aged harbour cheddar", "Quantity": 8, "Price": 132.0},
        {"Number": 10006, "Product": "Cold-pressed olive oil", "Quantity": 40, "Price": 516.0},
    ]

    # Each data source has the name the template uses for it
    assembler = DocumentAssembler()
    assembler.assemble_document("order-table.docx", "order-table-report.docx", [
        DataSourceInfo("Quayside Bistro", "customer"),
        DataSourceInfo(orders, "orders"),
    ])
    print("The report is saved to order-table-report.docx")

if __name__ == "__main__":
    table_report()
```
{{< /tab >}}
{{< tab "order-table.docx" >}}
{{< tab-text >}}
The following sample file is used in this example: [order-table.docx](/assembly/python-net/_sample_files/getting-started/quick-start-guide/order-table.docx)
{{< /tab-text >}}
{{< /tab >}}
{{< tab "order-table-report.docx" >}}  
```text
Binary file (DOCX, 8 KB)
```
[Download full output](/assembly/python-net/_output_files/getting-started/quick-start-guide/table_report/order-table-report.docx)
{{< /tab >}}
{{< /tabs >}}

### Run the App

{{< tabs "run_the_app_table_report">}}
{{< tab "Windows" >}}
```ps
py table_report.py
```
{{< /tab >}}
{{< tab "Linux" >}}
```bash
python3 table_report.py
```
{{< /tab >}}
{{< tab "macOS" >}}
```bash
python3 table_report.py
```
{{< /tab >}}
{{< /tabs >}}

### Explanation
- `DocumentAssembler()`: The class that builds reports. One instance can build any number of them.
- `DataSourceInfo(orders, "orders")`: A data source and the name the template's tags use for it. A list of dicts is a collection: the `<<foreach [o in orders]>>` band repeats the table row once for each dict, and `o.Number` reads the dict's `"Number"` key.
- `assemble_document(template, report, sources)`: Fills the template and writes the report. The data sources go as a list, or as one `DataSourceInfo` when there is only one.
- `<<[orders.Sum(o => o.Price)]:"0.00">>`: Template expressions can compute: `Sum`, `Count`, `Where`, `OrderBy`, `GroupBy` and more work on the Python list, and `:"0.00"` formats the number.

## Example 2: Turn a JSON file into a PDF report

The data often comes from a file. This example reads the customers of Harbor Lane Provisions and their orders from `customers.json`, and the template `orders-by-customer.docx` lists the orders of each customer:

```text
Harbor Lane Provisions: orders by customer
<<foreach [c in customers]>>
<<[c.CustomerName]>>
  • <<foreach [o in c.Order]>><<[o.Product.ProductName]>>: <<[o.ProductQuantity]>> units, <<[o.Price]>> USD, shipped <<[o.ShippingDate]:"d MMMM yyyy">>
<</foreach>>Total: <<[c.Order.Sum(o => o.Price)]>> USD
<</foreach>>
```

{{< tabs "demo_app_json_to_pdf">}}
{{< tab "json_to_pdf.py" >}}
```python
import json
from datetime import datetime

from groupdocs.assembly import DataSourceInfo, DocumentAssembler

def parse_dates(item):
    # JSON has no dates: turn the order dates into datetime objects for the template
    for key in ("OrderDate", "ShippingDate"):
        if key in item:
            item[key] = datetime.strptime(item[key], "%Y-%m-%dT%H:%M:%S")
    return item

def json_to_pdf():
    with open("customers.json", encoding="utf-8") as f:
        customers = json.load(f, object_hook=parse_dates)

    # A Word template, a PDF report: the report's extension picks the format
    assembler = DocumentAssembler()
    assembler.assemble_document("orders-by-customer.docx", "orders-by-customer.pdf", DataSourceInfo(customers, "customers"))
    print("Customers:", len(customers))

if __name__ == "__main__":
    json_to_pdf()
```
{{< /tab >}}
{{< tab "orders-by-customer.docx" >}}
{{< tab-text >}}
The following sample file is used in this example: [orders-by-customer.docx](/assembly/python-net/_sample_files/getting-started/quick-start-guide/orders-by-customer.docx)
{{< /tab-text >}}
{{< /tab >}}
{{< tab "customers.json" >}}
{{< tab-text >}}
The following sample file is used in this example: [customers.json](/assembly/python-net/_sample_files/getting-started/quick-start-guide/customers.json)
{{< /tab-text >}}
{{< /tab >}}
{{< tab "orders-by-customer.pdf" >}}  
```text
Binary file (PDF, 47 KB)
```
[Download full output](/assembly/python-net/_output_files/getting-started/quick-start-guide/json_to_pdf/orders-by-customer.pdf)
{{< /tab >}}
{{< /tabs >}}

### Run the App

{{< tabs "run_the_app_json_to_pdf">}}
{{< tab "Windows" >}}
```ps
py json_to_pdf.py
```
{{< /tab >}}
{{< tab "Linux" >}}
```bash
python3 json_to_pdf.py
```
{{< /tab >}}
{{< tab "macOS" >}}
```bash
python3 json_to_pdf.py
```
{{< /tab >}}
{{< /tabs >}}

### Explanation
- `json.load(f, object_hook=parse_dates)`: Reads the file into dicts and lists, which `DataSourceInfo` takes as they are. JSON has no date type, so the hook turns the date strings into `datetime` objects: the template formats `ShippingDate` as a date (`"d MMMM yyyy"`).
- `c.Order` and `o.Product.ProductName`: Nested dicts and lists are read with dots, as in the JSON.
- `"orders-by-customer.pdf"`: The report is saved in the format of its extension. The same template gives DOCX, PDF, HTML, XPS and the other [supported formats]({{< ref "assembly/python-net/getting-started/supported-document-formats.md" >}}).

## Example 3: Fill an Excel sheet

Templates can be spreadsheets too. The template `stock-sheet.xlsx` has a header row and a row that repeats for each product of `products.json`:

```text
Harbor Lane Provisions: stock
| Product                                   | In stock          | Discount, %     | Price                                 |
| <<foreach [p in products]>><<[p.ProductName]>> | <<[p.UnitInStock]>> | <<[p.Discount]>> | <<[p.ProductPrice]>><</foreach>> |
```

{{< tabs "demo_app_fill_spreadsheet">}}
{{< tab "fill_spreadsheet.py" >}}
```python
import json

from groupdocs.assembly import DataSourceInfo, DocumentAssembler, DocumentAssemblyOptions

def fill_spreadsheet():
    with open("products.json", encoding="utf-8") as f:
        products = json.load(f)

    # Write numbers as numbers: by default every value goes into a text cell
    assembler = DocumentAssembler()
    assembler.options = DocumentAssemblyOptions.USE_SPREADSHEET_DATA_TYPES
    assembler.assemble_document("stock-sheet.xlsx", "stock-sheet-report.xlsx", DataSourceInfo(products, "products"))
    print("Products:", len(products))

if __name__ == "__main__":
    fill_spreadsheet()
```
{{< /tab >}}
{{< tab "stock-sheet.xlsx" >}}
{{< tab-text >}}
The following sample file is used in this example: [stock-sheet.xlsx](/assembly/python-net/_sample_files/getting-started/quick-start-guide/stock-sheet.xlsx)
{{< /tab-text >}}
{{< /tab >}}
{{< tab "products.json" >}}
{{< tab-text >}}
The following sample file is used in this example: [products.json](/assembly/python-net/_sample_files/getting-started/quick-start-guide/products.json)
{{< /tab-text >}}
{{< /tab >}}
{{< tab "stock-sheet-report.xlsx" >}}  
```text
Binary file (XLSX, 8 KB)
```
[Download full output](/assembly/python-net/_output_files/getting-started/quick-start-guide/fill_spreadsheet/stock-sheet-report.xlsx)
{{< /tab >}}
{{< /tabs >}}

### Run the App

{{< tabs "run_the_app_fill_spreadsheet">}}
{{< tab "Windows" >}}
```ps
py fill_spreadsheet.py
```
{{< /tab >}}
{{< tab "Linux" >}}
```bash
python3 fill_spreadsheet.py
```
{{< /tab >}}
{{< tab "macOS" >}}
```bash
python3 fill_spreadsheet.py
```
{{< /tab >}}
{{< /tabs >}}

### Explanation
- `stock-sheet.xlsx`: In a spreadsheet the data band is a row of cells, from the cell that opens `<<foreach>>` to the cell that closes it; the report gets one row per product.
- `DocumentAssemblyOptions.USE_SPREADSHEET_DATA_TYPES`: Writes each value as its type, so `UnitInStock` and `Discount` are number cells that formulas can use, and `ProductPrice` (a string in the JSON) is a text cell. Without the option, every value is written as text.

## Next Steps
- [Supported Document Formats]({{< ref "assembly/python-net/getting-started/supported-document-formats.md" >}}): Review the template and report formats.
- [Licensing and Evaluation]({{< ref "assembly/python-net/getting-started/licensing-and-subscription.md" >}}): Check details on licensing and the evaluation limits.
- [Developer Guide]({{< ref "assembly/python-net/developer-guide/_index.md" >}}): Dive into the template syntax, the data sources and every kind of report: tables, lists, charts, images, barcodes and email.
- [Technical Support]({{< ref "assembly/python-net/technical-support.md" >}}): Contact support for assistance if you encounter issues.
