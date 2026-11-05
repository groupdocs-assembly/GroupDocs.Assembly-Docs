---
id: the-business-layer
url: assembly/python-net/the-business-layer
title: The Business Layer
weight: 2
description: "The data the GroupDocs.Assembly for Python via .NET examples read: the Harbor Lane Provisions customers, orders, products, account managers and staff as JSON, XML, CSV and document tables, and how a Python example loads each file."
keywords: business layer, data source, JSON, XML, CSV, dict, DocumentTable, Python, GroupDocs.Assembly
productName: GroupDocs.Assembly for Python via .NET
hideChildren: False
---
The .NET version of this page lists the C# classes of a business layer: a `DataLayer` class that builds customer, order and product objects, reads them from a database, a `DataSet`, XML and JSON files, and a `CommonUtilities` class that resolves template and report paths and applies the licence. In Python, the business layer is the set of data files the examples read, and a few lines that load each of them. This page describes those files, as they are in the sample set, and how a page loads each one.

The data is that of Harbor Lane Provisions, the specialty-food wholesaler of the [business case]({{< ref "assembly/python-net/developer-guide/basic-usage/working-with-a-business-case/business-case-of-a-shopping-store.md" >}}).

## Common Utilities

### Template and Report Locations

The examples need no path helpers. Each example runs in a folder that holds only its input files, reads them by their bare file names (`"customers.json"`, `"shop-customer-orders.docx"`) and writes its report next to them (`"shop-customer-orders-report.docx"`). The tabs beside each example link the files it reads.

### Applying Product License

The examples do not set a licence themselves. Set the `GROUPDOCS_LIC_PATH` environment variable to the path or URL of your licence file, and GroupDocs.Assembly for Python via .NET applies it at the first call into the engine. To apply a licence in code instead, call `License().set_license(...)` with a path or an open file before the first report:

```python
from groupdocs.assembly import License

License().set_license("GroupDocs.Assembly.lic")
```

### Metered Licensing

A metered licence is applied with the public and private keys of your subscription:

```python
from groupdocs.assembly import License, Metered

Metered().set_metered_key("PublicKey", "PrivateKey")
print("Licensed:", License().is_licensed)
```

See [Install GroupDocs.Assembly for Python via .NET and Apply License]({{< ref "assembly/python-net/developer-guide/basic-usage/install-and-apply-license.md" >}}) for the details.

## Data Layer

### The Shop Data in Python

Where the .NET examples build `Customer`, `Order`, `Product` and `Service` objects, the Python examples pass dicts and lists. A dict's keys are the member names the template reads, so `<<[c.CustomerName]>>` and `<<[o.Product.ProductName]>>` read a dict exactly as they read a C# object. Python's types decide what the template sees: a `str` is a string, an `int` a 64-bit integer, a `float` a double, a `datetime` a date-time value. JSON has no date type, so a page whose template reads a date turns the date strings into `datetime` objects while loading the file, with an `object_hook`.

#### Getting Customers' Details

`customers.json` holds the four customers of the shop, each with its orders:

| Member | Python type | Example |
|---|---|---|
| `CustomerName` | `str` | Quayside Bistro |
| `ShippingAddress` | `str` | 3 Harbour Steps, Port Ellery |
| `CustomerContactNumber` | `str` | +1 555 0142 811 |
| `Barcode` | `str` | 20150114001 |
| `Photo` | `str`, a picture file name | quayside-bistro.png |
| `Document` | `str`, a document file name | outer-document.docx |
| `Color` | `str`, an HTML color | #2E8B7A |
| `Order` | `list` of orders | |
| `Order[].OrderNumber` | `int` | 10001 |
| `Order[].Product` | `dict`: `ProductName` (`str`), `UnitInStock` (`int`), `Discount` (`int`, percent), `ProductPrice` (`str`) | Harbor Blend whole bean coffee, 240, 0, $18.40 |
| `Order[].ProductQuantity` | `int` | 30 |
| `Order[].Price` | `int` | 552 |
| `Order[].OrderDate`, `Order[].ShippingDate` | `str` in the file (`"2015-01-14T00:00:00"`), `datetime` once loaded | 2015-01-14 |
| `Order[].Barcode` | `str` | HLP-10001 |
| `Order[].Services` | `list` of dicts with a `ServiceName` (`str`) | Next-day delivery |

Quayside Bistro, Lantern Street Café, Saltmarsh Deli and Pier Nine Kitchen placed ten orders between them, all dated 2015. A page whose template reads the dates loads the file as follows; the other pages call `json.load(f)` alone.

{{< tabs "example1" >}}
{{< tab "Python" >}}
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


with open("customers.json", encoding="utf-8") as f:
    customers = json.load(f, object_hook=parse_dates)

assembler = DocumentAssembler()
assembler.assemble_document("shop-customer-orders.docx", "shop-customer-orders-report.docx", DataSourceInfo(customers, "customers"))
```
{{< /tab >}}
{{< tab "shop-customer-orders.docx" >}}
{{< tab-text >}}
The following sample file is used in this example: [shop-customer-orders.docx](/assembly/python-net/_sample_files/developer-guide/basic-usage/working-with-a-business-case/the-business-layer/shop-customer-orders.docx)
{{< /tab-text >}}
{{< /tab >}}
{{< tab "customers.json" >}}
{{< tab-text >}}
The following sample file is used in this example: [customers.json](/assembly/python-net/_sample_files/developer-guide/basic-usage/working-with-a-business-case/the-business-layer/customers.json)
{{< /tab-text >}}
{{< /tab >}}
{{< tab "shop-customer-orders-report.docx" >}}  
```text
Binary file (DOCX, 9 KB)
```
[Download full output](/assembly/python-net/_output_files/developer-guide/basic-usage/working-with-a-business-case/the-business-layer/getting_customers_details/shop-customer-orders-report.docx)
{{< /tab >}}
{{< /tabs >}}

#### Getting Order Details

`orders.json` holds the same ten orders as one flat list, where the .NET `GetOrdersData` method walks the customers' orders. Each order carries the members above and a `Customer` dict (the customer's members without its orders), so a template can read `<<[o.Customer.CustomerName]>>` or group the orders with `GroupBy(o => o.Customer)`: two orders of one customer hold equal customer dicts, and the engine compares them by value.

{{< tabs "example2" >}}
{{< tab "Python" >}}
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


with open("orders.json", encoding="utf-8") as f:
    orders = json.load(f, object_hook=parse_dates)

assembler = DocumentAssembler()
assembler.assemble_document("shop-order-list.docx", "shop-order-list-report.docx", DataSourceInfo(orders, "orders"))
```
{{< /tab >}}
{{< tab "shop-order-list.docx" >}}
{{< tab-text >}}
The following sample file is used in this example: [shop-order-list.docx](/assembly/python-net/_sample_files/developer-guide/basic-usage/working-with-a-business-case/the-business-layer/shop-order-list.docx)
{{< /tab-text >}}
{{< /tab >}}
{{< tab "orders.json" >}}
{{< tab-text >}}
The following sample file is used in this example: [orders.json](/assembly/python-net/_sample_files/developer-guide/basic-usage/working-with-a-business-case/the-business-layer/orders.json)
{{< /tab-text >}}
{{< /tab >}}
{{< tab "shop-order-list-report.docx" >}}  
```text
Binary file (DOCX, 8 KB)
```
[Download full output](/assembly/python-net/_output_files/developer-guide/basic-usage/working-with-a-business-case/the-business-layer/getting_order_details/shop-order-list-report.docx)
{{< /tab >}}
{{< /tabs >}}

#### Getting Product Details

`products.json` is the list of the ten products the orders name, each with `ProductName`, `UnitInStock`, `Discount` and `ProductPrice`. It holds no dates, so `json.load` is all it takes.

{{< tabs "example3" >}}
{{< tab "Python" >}}
```python
import json

from groupdocs.assembly import DataSourceInfo, DocumentAssembler

with open("products.json", encoding="utf-8") as f:
    products = json.load(f)

assembler = DocumentAssembler()
assembler.assemble_document("shop-product-list.docx", "shop-product-list-report.docx", DataSourceInfo(products, "products"))
```
{{< /tab >}}
{{< tab "shop-product-list.docx" >}}
{{< tab-text >}}
The following sample file is used in this example: [shop-product-list.docx](/assembly/python-net/_sample_files/developer-guide/basic-usage/working-with-a-business-case/the-business-layer/shop-product-list.docx)
{{< /tab-text >}}
{{< /tab >}}
{{< tab "products.json" >}}
{{< tab-text >}}
The following sample file is used in this example: [products.json](/assembly/python-net/_sample_files/developer-guide/basic-usage/working-with-a-business-case/the-business-layer/products.json)
{{< /tab-text >}}
{{< /tab >}}
{{< tab "shop-product-list-report.docx" >}}  
```text
Binary file (DOCX, 8 KB)
```
[Download full output](/assembly/python-net/_output_files/developer-guide/basic-usage/working-with-a-business-case/the-business-layer/getting_product_details/shop-product-list-report.docx)
{{< /tab >}}
{{< /tabs >}}

#### Getting Single Customer Details

`customer.json` is one customer, Quayside Bistro, with its three orders: the first item of `customers.json`, where the .NET `GetCustomerData` method takes the first customer of the list. The pages pass it under the name `customer`.

{{< tabs "example4" >}}
{{< tab "Python" >}}
```python
import json

from groupdocs.assembly import DataSourceInfo, DocumentAssembler

with open("customer.json", encoding="utf-8") as f:
    customer = json.load(f)

assembler = DocumentAssembler()
assembler.assemble_document("shop-customer-card.docx", "shop-customer-card-report.docx", DataSourceInfo(customer, "customer"))
```
{{< /tab >}}
{{< tab "shop-customer-card.docx" >}}
{{< tab-text >}}
The following sample file is used in this example: [shop-customer-card.docx](/assembly/python-net/_sample_files/developer-guide/basic-usage/working-with-a-business-case/the-business-layer/shop-customer-card.docx)
{{< /tab-text >}}
{{< /tab >}}
{{< tab "customer.json" >}}
{{< tab-text >}}
The following sample file is used in this example: [customer.json](/assembly/python-net/_sample_files/developer-guide/basic-usage/working-with-a-business-case/the-business-layer/customer.json)
{{< /tab-text >}}
{{< /tab >}}
{{< tab "shop-customer-card-report.docx" >}}  
```text
Binary file (DOCX, 7 KB)
```
[Download full output](/assembly/python-net/_output_files/developer-guide/basic-usage/working-with-a-business-case/the-business-layer/getting_single_customer_details/shop-customer-card-report.docx)
{{< /tab >}}
{{< /tabs >}}

### Database Entities

The .NET examples read the same customers, orders and products from an SQL Server database through LINQ to SQL entities. In Python, read the rows with your database driver and turn each row into a dict: the column names become the members the template reads. The following example loads the products into an in-memory SQLite database and reads them back with `sqlite3`, whose `sqlite3.Row` objects convert to dicts. See [Generate Document from Database]({{< ref "assembly/python-net/developer-guide/basic-usage/generate-from-database.md" >}}) for more.

{{< tabs "example5" >}}
{{< tab "Python" >}}
```python
import json
import sqlite3

from groupdocs.assembly import DataSourceInfo, DocumentAssembler

# A database with the products, as a shop would keep them
connection = sqlite3.connect(":memory:")
connection.execute("CREATE TABLE Products (ProductName TEXT, UnitInStock INTEGER, Discount INTEGER, ProductPrice TEXT)")
with open("products.json", encoding="utf-8") as f:
    for p in json.load(f):
        connection.execute("INSERT INTO Products VALUES (?, ?, ?, ?)",
                           (p["ProductName"], p["UnitInStock"], p["Discount"], p["ProductPrice"]))

# Each row becomes a dict whose keys are the column names
connection.row_factory = sqlite3.Row
products = [dict(row) for row in connection.execute("SELECT * FROM Products ORDER BY ProductName")]
connection.close()

assembler = DocumentAssembler()
assembler.assemble_document("shop-product-list.docx", "shop-product-list-from-database.docx", DataSourceInfo(products, "products"))
```
{{< /tab >}}
{{< tab "shop-product-list.docx" >}}
{{< tab-text >}}
The following sample file is used in this example: [shop-product-list.docx](/assembly/python-net/_sample_files/developer-guide/basic-usage/working-with-a-business-case/the-business-layer/shop-product-list.docx)
{{< /tab-text >}}
{{< /tab >}}
{{< tab "products.json" >}}
{{< tab-text >}}
The following sample file is used in this example: [products.json](/assembly/python-net/_sample_files/developer-guide/basic-usage/working-with-a-business-case/the-business-layer/products.json)
{{< /tab-text >}}
{{< /tab >}}
{{< tab "shop-product-list-from-database.docx" >}}  
```text
Binary file (DOCX, 8 KB)
```
[Download full output](/assembly/python-net/_output_files/developer-guide/basic-usage/working-with-a-business-case/the-business-layer/database_entities/shop-product-list-from-database.docx)
{{< /tab >}}
{{< /tabs >}}

### DataSet Source

ADO.NET `DataSet`, `DataTable` and `DataRow` objects have no Python form. Related tables are nested dicts and lists in Python, as in `customers.json`, or a `DocumentTableSet` when the tables come from a document (see [Use Tables of Documents as Data Sources](#use-tables-of-documents-as-data-sources) below).

### XML and JSON Data Sources

`managers.json` and `managers.xml` hold the same data: Harbor Lane's three account managers, Mei Tanaka, Daniel Reyes and Sofia Marino, each with a `Name` and the supply contracts they signed, each `Contract` with a `Client` (its `Name`) and a `Price`. Nine contracts in all, worth 430000.

```xml
<Managers>
  <Manager>
    <Name>Mei Tanaka</Name>
    <Contract>
      <Client>
        <Name>Harbourview Hotel</Name>
      </Client>
      <Price>120000</Price>
    </Contract>
    ...
  </Manager>
  ...
</Managers>
```

#### Getting Data From a JSON File

A page reads a JSON file with `json.load` and passes the result, as above. The following example reads `managers.json`.

{{< tabs "example6" >}}
{{< tab "Python" >}}
```python
import json

from groupdocs.assembly import DataSourceInfo, DocumentAssembler

with open("managers.json", encoding="utf-8") as f:
    managers = json.load(f)

assembler = DocumentAssembler()
assembler.assemble_document("shop-manager-contracts.docx", "shop-manager-contracts-report.docx", DataSourceInfo(managers, "managers"))
```
{{< /tab >}}
{{< tab "shop-manager-contracts.docx" >}}
{{< tab-text >}}
The following sample file is used in this example: [shop-manager-contracts.docx](/assembly/python-net/_sample_files/developer-guide/basic-usage/working-with-a-business-case/the-business-layer/shop-manager-contracts.docx)
{{< /tab-text >}}
{{< /tab >}}
{{< tab "managers.json" >}}
{{< tab-text >}}
The following sample file is used in this example: [managers.json](/assembly/python-net/_sample_files/developer-guide/basic-usage/working-with-a-business-case/the-business-layer/managers.json)
{{< /tab-text >}}
{{< /tab >}}
{{< tab "shop-manager-contracts-report.docx" >}}  
```text
Binary file (DOCX, 8 KB)
```
[Download full output](/assembly/python-net/_output_files/developer-guide/basic-usage/working-with-a-business-case/the-business-layer/getting_data_from_a_json_file/shop-manager-contracts-report.docx)
{{< /tab >}}
{{< /tabs >}}

A page can also hand the file to the engine with `JsonDataSource("managers.json")`, which types the values itself (see [Accessing JSON Data]({{< ref "assembly/python-net/developer-guide/basic-usage/working-with-groupdocs.assembly-engine/groupdocs.assembly-engine-apis.md#accessing-json-data" >}})).

#### Getting Data From an XML File

An XML file goes to the engine as an `XmlDataSource`. The same template reads `managers.xml`:

{{< tabs "example7" >}}
{{< tab "Python" >}}
```python
from groupdocs.assembly import DataSourceInfo, DocumentAssembler
from groupdocs.assembly.data import XmlDataSource

managers = XmlDataSource("managers.xml")

assembler = DocumentAssembler()
assembler.assemble_document("shop-manager-contracts.docx", "shop-manager-contracts-from-xml.docx", DataSourceInfo(managers, "managers"))
```
{{< /tab >}}
{{< tab "shop-manager-contracts.docx" >}}
{{< tab-text >}}
The following sample file is used in this example: [shop-manager-contracts.docx](/assembly/python-net/_sample_files/developer-guide/basic-usage/working-with-a-business-case/the-business-layer/shop-manager-contracts.docx)
{{< /tab-text >}}
{{< /tab >}}
{{< tab "managers.xml" >}}
{{< tab-text >}}
The following sample file is used in this example: [managers.xml](/assembly/python-net/_sample_files/developer-guide/basic-usage/working-with-a-business-case/the-business-layer/managers.xml)
{{< /tab-text >}}
{{< /tab >}}
{{< tab "shop-manager-contracts-from-xml.docx" >}}  
```text
Binary file (DOCX, 8 KB)
```
[Download full output](/assembly/python-net/_output_files/developer-guide/basic-usage/working-with-a-business-case/the-business-layer/getting_data_from_an_xml_file/shop-manager-contracts-from-xml.docx)
{{< /tab >}}
{{< /tabs >}}

### CSV Data Source

`persons.csv` lists Harbor Lane's staff with a header line: `Name`, `Age` and `Birth`, an ISO 8601 date and time.

```text
Name,Age,Birth
Amara Osei,41,1984-03-12T09:30:00
Jonas Weber,37,1988-07-04T14:00:00
Lena Park,29,1996-11-21T07:45:00
```

A page reads it with a `CsvDataSource` told that the first line holds the column names. The engine recognizes the numbers and the dates itself.

{{< tabs "example8" >}}
{{< tab "Python" >}}
```python
from groupdocs.assembly import DataSourceInfo, DocumentAssembler
from groupdocs.assembly.data import CsvDataLoadOptions, CsvDataSource

persons = CsvDataSource("persons.csv", CsvDataLoadOptions(True))

assembler = DocumentAssembler()
assembler.assemble_document("shop-staff-list.docx", "shop-staff-list-report.docx", DataSourceInfo(persons, "persons"))
```
{{< /tab >}}
{{< tab "shop-staff-list.docx" >}}
{{< tab-text >}}
The following sample file is used in this example: [shop-staff-list.docx](/assembly/python-net/_sample_files/developer-guide/basic-usage/working-with-a-business-case/the-business-layer/shop-staff-list.docx)
{{< /tab-text >}}
{{< /tab >}}
{{< tab "persons.csv" >}}
{{< tab-text >}}
The following sample file is used in this example: [persons.csv](/assembly/python-net/_sample_files/developer-guide/basic-usage/working-with-a-business-case/the-business-layer/persons.csv)
{{< /tab-text >}}
{{< /tab >}}
{{< tab "shop-staff-list-report.docx" >}}  
```text
Binary file (DOCX, 8 KB)
```
[Download full output](/assembly/python-net/_output_files/developer-guide/basic-usage/working-with-a-business-case/the-business-layer/csv_data_source/shop-staff-list-report.docx)
{{< /tab >}}
{{< /tabs >}}

### Use Tables of Documents as Data Sources

Five files hold the account managers' figures as tables of Word, PowerPoint and Excel documents. A page loads one table as a `DocumentTable`, or all the tables of a document as a `DocumentTableSet`.

| File | What it holds |
|---|---|
| `contracts.xlsx` | One worksheet, `Contracts`: `Client`, `Manager` and `Price` of the nine contracts. |
| `managers.docx` | Two tables: an unused one, then the top 5 managers with their total contract price (`Manager`, `Total Contract Price`). |
| `managers.pptx` | The same two tables on one slide. |
| `related-tables.xlsx` | Three worksheets linked by ID: `MANAGER` (`ID`, `NAME`), `CLIENT` (`ID`, `NAME`) and `CONTRACT` (`ID`, `CLIENT_ID`, `MANAGER_ID`, `PRICE`). |
| `multiple-tables.docx` | Three tables: `Planet`/`Number`, the staff (`First Name`, `Last Name`) and Harbor Lane's suppliers (`Name`, `Address`). |

#### Use Spreadsheets as Data Sources

The first worksheet of `contracts.xlsx`, with column names from its first row. A space in a column name becomes an underscore, and a column whose cells all hold numbers is a `float` column.

{{< tabs "example9" >}}
{{< tab "Python" >}}
```python
from groupdocs.assembly.data import DocumentTable, DocumentTableOptions

options = DocumentTableOptions()
options.first_row_contains_column_names = True

# Use data of the first worksheet
table = DocumentTable("contracts.xlsx", 0, options)

# Check column count, names, and types
print("Columns:", table.columns.count)
for column in table.columns:
    print(column.name, column.type.__name__)
```
{{< /tab >}}
{{< tab "contracts.xlsx" >}}
{{< tab-text >}}
The following sample file is used in this example: [contracts.xlsx](/assembly/python-net/_sample_files/developer-guide/basic-usage/working-with-a-business-case/the-business-layer/contracts.xlsx)
{{< /tab-text >}}
{{< /tab >}}
{{< tab "use-spreadsheets-as-data-sources.txt" >}}  
```text
Columns: 3
Client str
Manager str
Price float
```
[Download full output](/assembly/python-net/_output_files/developer-guide/basic-usage/working-with-a-business-case/the-business-layer/use_spreadsheets_as_data_sources/use-spreadsheets-as-data-sources.txt)
{{< /tab >}}
{{< /tabs >}}

#### Use Tables of Word Processing Documents as Data Sources

The second table of `managers.docx`, with its first row read as data and only the first four rows loaded. The columns then take default names.

{{< tabs "example10" >}}
{{< tab "Python" >}}
```python
from groupdocs.assembly.data import DocumentTable, DocumentTableOptions

# Do not extract column names from the first row, so that the first row is treated as a data row.
# Limit the largest row index, so that only the first four data rows are loaded.
options = DocumentTableOptions()
options.max_row_index = 3

# Use data of the second table in the document
table = DocumentTable("managers.docx", 1, options)

# Default column names are used, because the names are not extracted from the first row
print("Columns:", table.columns.count)
print([column.name for column in table.columns])
```
{{< /tab >}}
{{< tab "managers.docx" >}}
{{< tab-text >}}
The following sample file is used in this example: [managers.docx](/assembly/python-net/_sample_files/developer-guide/basic-usage/working-with-a-business-case/the-business-layer/managers.docx)
{{< /tab-text >}}
{{< /tab >}}
{{< tab "use-tables-of-word-processing-documents-as-data-sources.txt" >}}  
```text
Columns: 2
['Column1', 'Column2']
```
[Download full output](/assembly/python-net/_output_files/developer-guide/basic-usage/working-with-a-business-case/the-business-layer/use_tables_of_word_processing_documents_as_data_sources/use-tables-of-word-processing-documents-as-data-sources.txt)
{{< /tab >}}
{{< /tabs >}}

#### Use Tables of Presentation Documents as Data Sources

The same for the table on the slide of `managers.pptx`:

{{< tabs "example11" >}}
{{< tab "Python" >}}
```python
from groupdocs.assembly.data import DocumentTable, DocumentTableOptions

# Do not extract column names from the first row, so that the first row is treated as a data row.
# Limit the largest row index, so that only the first four data rows are loaded.
options = DocumentTableOptions()
options.max_row_index = 3

# Use data of the second table in the presentation
table = DocumentTable("managers.pptx", 1, options)

# Default column names are used, because the names are not extracted from the first row
print("Columns:", table.columns.count)
print([column.name for column in table.columns])
```
{{< /tab >}}
{{< tab "managers.pptx" >}}
{{< tab-text >}}
The following sample file is used in this example: [managers.pptx](/assembly/python-net/_sample_files/developer-guide/basic-usage/working-with-a-business-case/the-business-layer/managers.pptx)
{{< /tab-text >}}
{{< /tab >}}
{{< tab "use-tables-of-presentation-documents-as-data-sources.txt" >}}  
```text
Columns: 2
['Column1', 'Column2']
```
[Download full output](/assembly/python-net/_output_files/developer-guide/basic-usage/working-with-a-business-case/the-business-layer/use_tables_of_presentation_documents_as_data_sources/use-tables-of-presentation-documents-as-data-sources.txt)
{{< /tab >}}
{{< /tabs >}}

#### Use All Tables of a Document as Data Sources

A `DocumentTableSet` loads every table of a document at once. A handler sets the load options of each table, and relations link the tables of `related-tables.xlsx` by their ID columns, so a template can walk from a manager to its contracts and from a contract to its client.

{{< tabs "example12" >}}
{{< tab "Python" >}}
```python
from groupdocs.assembly.data import DocumentTableOptions, DocumentTableSet


def load_table(args):
    # The first row of every worksheet holds its column names
    options = DocumentTableOptions()
    options.first_row_contains_column_names = True
    args.options = options


tables = DocumentTableSet("related-tables.xlsx", load_table)
tables.relations.add(tables.tables["CLIENT"].columns["ID"], tables.tables["CONTRACT"].columns["CLIENT_ID"])
tables.relations.add(tables.tables["MANAGER"].columns["ID"], tables.tables["CONTRACT"].columns["MANAGER_ID"])

for table in tables.tables:
    print(table.name, [column.name for column in table.columns])
```
{{< /tab >}}
{{< tab "related-tables.xlsx" >}}
{{< tab-text >}}
The following sample file is used in this example: [related-tables.xlsx](/assembly/python-net/_sample_files/developer-guide/basic-usage/working-with-a-business-case/the-business-layer/related-tables.xlsx)
{{< /tab-text >}}
{{< /tab >}}
{{< tab "use-all-tables-of-a-document-as-data-sources.txt" >}}  
```text
MANAGER ['ID', 'NAME']
CLIENT ['ID', 'NAME']
CONTRACT ['ID', 'CLIENT_ID', 'MANAGER_ID', 'PRICE']
```
[Download full output](/assembly/python-net/_output_files/developer-guide/basic-usage/working-with-a-business-case/the-business-layer/use_all_tables_of_a_document_as_data_sources/use-all-tables-of-a-document-as-data-sources.txt)
{{< /tab >}}
{{< /tabs >}}

The tables of a Word document have no names of their own, so a `DocumentTableSet` names them `Table1`, `Table2` and so on:

{{< tabs "example13" >}}
{{< tab "Python" >}}
```python
from groupdocs.assembly.data import DocumentTableOptions, DocumentTableSet


def load_table(args):
    # The first row of every table holds its column names
    options = DocumentTableOptions()
    options.first_row_contains_column_names = True
    args.options = options


tables = DocumentTableSet("multiple-tables.docx", load_table)

for table in tables.tables:
    print(table.name, [column.name for column in table.columns])
```
{{< /tab >}}
{{< tab "multiple-tables.docx" >}}
{{< tab-text >}}
The following sample file is used in this example: [multiple-tables.docx](/assembly/python-net/_sample_files/developer-guide/basic-usage/working-with-a-business-case/the-business-layer/multiple-tables.docx)
{{< /tab-text >}}
{{< /tab >}}
{{< tab "use-all-tables-of-a-document-as-data-sources-2.txt" >}}  
```text
Table1 ['Planet', 'Number']
Table2 ['First_Name', 'Last_Name']
Table3 ['Name', 'Address']
```
[Download full output](/assembly/python-net/_output_files/developer-guide/basic-usage/working-with-a-business-case/the-business-layer/use_all_tables_of_a_document_as_data_sources_2/use-all-tables-of-a-document-as-data-sources-2.txt)
{{< /tab >}}
{{< /tabs >}}

### Pictures

Each customer's `Photo` names a picture of the sample set: `quayside-bistro.png`, `lantern-street-cafe.png`, `saltmarsh-deli.png` and `pier-nine-kitchen.png`, 240 by 240 pixels. An image tag such as `<<image [Photo]>>` loads the file by that name from the folder the example runs in, so the image pages list the pictures among their input files. `logo.png` is the Harbor Lane Provisions logo.

## The .NET Classes

The complete `DataLayer` and `CommonUtilities` classes of the .NET examples have no Python counterpart: every page loads its data with the few lines shown above. The `DynamicEntity` class, which serves data lazily through indexers, is discussed in [Working with Lazy And Recursive Access of Data]({{< ref "assembly/python-net/developer-guide/advanced-usage/working-with-lazy-and-recursive-access-of-data.md" >}}).
