---
id: assembly-basic-usage-database-datasource
url: assembly/python-net/basic-usage-database-datasource
linktitle: Generate from Database
title: Generate Document from Database
weight: 9
description: "Create reports in Python from database query results: turn the rows into dicts and pass them to GroupDocs.Assembly for Python via .NET."
keywords: database, SQL, sqlite3, database rows, dict rows, generate from database, Python, assemble from database
productName: GroupDocs.Assembly for Python via .NET
hideChildren: False
---

## Overview

GroupDocs.Assembly for Python via .NET generates documents from the results of your database queries. Python's database drivers return rows; turn each row into a dict keyed by column name, and the template reads the columns by name, as it would read the columns of a .NET `DataTable`. The examples use Python's built-in `sqlite3` module with an in-memory database they create; any DB-API driver (PostgreSQL, MySQL, SQL Server, Oracle) returns rows the same way.

The main classes involved are:
- [DocumentAssembler](https://reference.groupdocs.com/assembly/python-net/groupdocs.assembly/documentassembler/) - assembles documents
- [DataSourceInfo](https://reference.groupdocs.com/assembly/python-net/groupdocs.assembly/datasourceinfo/) - wraps data sources
- Python's `sqlite3` module (or your database's DB-API driver): connections, cursors and rows

Here are the steps to generate documents from databases:

* Connect to your database with its Python driver
* Execute SQL queries and turn the rows into a list of dicts
* Create a template document with expression tags referencing table and column names
* Use DocumentAssembler to assemble the template with the rows
* Save the assembled document

{{< alert style="info" >}}
The ADO.NET classes a .NET application passes to the engine (`DataSet`, `DataTable`, `DataView`, `IDataReader`) have no Python form. In Python, a table is a list of dicts, several tables are a dict of such lists, and related rows are nested lists. A column's Python type decides what the template sees: `sqlite3` returns `int`, `float`, `str`, `bytes` and `None`.
{{< /alert >}}

## Generate Document from Query Rows

The simplest approach is a list of dicts, one per row:

{{< tabs "example1" >}}
{{< tab "Python" >}}
```python
import sqlite3

from groupdocs.assembly import DataSourceInfo, DocumentAssembler


def create_database():
    # An in-memory database standing in for your own
    connection = sqlite3.connect(":memory:")
    connection.executescript("""
        CREATE TABLE Customers (CustomerId INTEGER PRIMARY KEY, CustomerName TEXT, Email TEXT, Balance REAL);
        INSERT INTO Customers VALUES (1, 'Quayside Bistro', 'orders@quaysidebistro.example', 1250.75);
        INSERT INTO Customers VALUES (2, 'Lantern Street Café', 'orders@lanternstreetcafe.example', 2480.00);
        INSERT INTO Customers VALUES (3, 'Saltmarsh Deli', 'orders@saltmarshdeli.example', 640.50);
        INSERT INTO Customers VALUES (4, 'Pier Nine Kitchen', 'orders@piernine.example', 1890.20);
    """)
    return connection


def query(connection, sql):
    # Each row becomes a dict keyed by column name, as the template reads it
    connection.row_factory = sqlite3.Row
    return [dict(row) for row in connection.execute(sql)]


connection = create_database()
try:
    customers = query(connection, "SELECT CustomerName, Email, Balance FROM Customers")
finally:
    connection.close()

# Assemble document
assembler = DocumentAssembler()
assembler.assemble_document("customer-accounts.docx", "customer-accounts-report.docx",
                            DataSourceInfo(customers, "customers"))

print("Document generated from query rows successfully.")
```
{{< /tab >}}
{{< tab "customer-accounts.docx" >}}
{{< tab-text >}}
The following sample file is used in this example: [customer-accounts.docx](/assembly/python-net/_sample_files/developer-guide/basic-usage/generate-from-database/customer-accounts.docx)
{{< /tab-text >}}
{{< /tab >}}
{{< tab "customer-accounts-report.docx" >}}  
```text
Binary file (DOCX, 8 KB)
```
[Download full output](/assembly/python-net/_output_files/developer-guide/basic-usage/generate-from-database/generate_document_from_query_rows/customer-accounts-report.docx)
{{< /tab >}}
{{< /tabs >}}

## Template Example for Query Rows

In your template, reference columns by name:

```text
Customers List:

<<foreach [in customers]>>
<<[CustomerName]>> - <<[Email]>> - Balance: <<[Balance]:"C">>
<</foreach>>
```

## Generate Document from Several Tables

When working with multiple tables, put each table's rows under its name in one dict:

{{< tabs "example2" >}}
{{< tab "Python" >}}
```python
import sqlite3

from groupdocs.assembly import DataSourceInfo, DocumentAssembler


def create_database():
    # An in-memory database standing in for your own
    connection = sqlite3.connect(":memory:")
    connection.executescript("""
        CREATE TABLE Customers (CustomerId INTEGER PRIMARY KEY, CustomerName TEXT, Email TEXT, Balance REAL);
        INSERT INTO Customers VALUES (1, 'Quayside Bistro', 'orders@quaysidebistro.example', 1250.75);
        INSERT INTO Customers VALUES (2, 'Lantern Street Café', 'orders@lanternstreetcafe.example', 2480.00);
        INSERT INTO Customers VALUES (3, 'Saltmarsh Deli', 'orders@saltmarshdeli.example', 640.50);
        INSERT INTO Customers VALUES (4, 'Pier Nine Kitchen', 'orders@piernine.example', 1890.20);
        CREATE TABLE Orders (OrderId INTEGER PRIMARY KEY, CustomerId INTEGER, Amount REAL);
        INSERT INTO Orders VALUES (10001, 1, 552.00);
        INSERT INTO Orders VALUES (10002, 2, 522.00);
        INSERT INTO Orders VALUES (10003, 3, 281.00);
        INSERT INTO Orders VALUES (10004, 1, 132.00);
        INSERT INTO Orders VALUES (10005, 2, 192.00);
        INSERT INTO Orders VALUES (10006, 1, 516.00);
        INSERT INTO Orders VALUES (10007, 4, 198.00);
        INSERT INTO Orders VALUES (10008, 3, 456.00);
    """)
    return connection


def query(connection, sql):
    # Each row becomes a dict keyed by column name, as the template reads it
    connection.row_factory = sqlite3.Row
    return [dict(row) for row in connection.execute(sql)]


connection = create_database()
try:
    # Load customers table and orders table
    data_set = {
        "Customers": query(connection, "SELECT * FROM Customers"),
        "Orders": query(connection, "SELECT * FROM Orders"),
    }
finally:
    connection.close()

assembler = DocumentAssembler()
assembler.assemble_document("customers-and-orders.docx", "customers-and-orders-report.docx",
                            DataSourceInfo(data_set, "ds"))

print("Document generated from several tables successfully.")
```
{{< /tab >}}
{{< tab "customers-and-orders.docx" >}}
{{< tab-text >}}
The following sample file is used in this example: [customers-and-orders.docx](/assembly/python-net/_sample_files/developer-guide/basic-usage/generate-from-database/customers-and-orders.docx)
{{< /tab-text >}}
{{< /tab >}}
{{< tab "customers-and-orders-report.docx" >}}  
```text
Binary file (DOCX, 8 KB)
```
[Download full output](/assembly/python-net/_output_files/developer-guide/basic-usage/generate-from-database/generate_document_from_several_tables/customers-and-orders-report.docx)
{{< /tab >}}
{{< /tabs >}}

## Template Example for Several Tables

Reference tables by name in your template:

```text
Customers:
<<foreach [in ds.Customers]>>
<<[CustomerName]>> - <<[Email]>>
<</foreach>>

Orders:
<<foreach [in ds.Orders]>>
Order #<<[OrderId]>> - Amount: <<[Amount]:"C">>
<</foreach>>
```

## Reading Rows as a Stream

A .NET application can hand the engine an open `IDataReader` and let it read the rows one by one. The engine cannot read from a Python cursor: read the rows into a list first, as above, and keep large results small by selecting only the columns and rows the report shows.

## Filtering and Sorting Rows

Where .NET filters and sorts a `DataView`, Python lets the database do it in the query:

{{< tabs "example3" >}}
{{< tab "Python" >}}
```python
import sqlite3

from groupdocs.assembly import DataSourceInfo, DocumentAssembler


def create_database():
    # An in-memory database standing in for your own
    connection = sqlite3.connect(":memory:")
    connection.executescript("""
        CREATE TABLE Customers (CustomerId INTEGER PRIMARY KEY, CustomerName TEXT, Email TEXT, Balance REAL);
        INSERT INTO Customers VALUES (1, 'Quayside Bistro', 'orders@quaysidebistro.example', 1250.75);
        INSERT INTO Customers VALUES (2, 'Lantern Street Café', 'orders@lanternstreetcafe.example', 2480.00);
        INSERT INTO Customers VALUES (3, 'Saltmarsh Deli', 'orders@saltmarshdeli.example', 640.50);
        INSERT INTO Customers VALUES (4, 'Pier Nine Kitchen', 'orders@piernine.example', 1890.20);
    """)
    return connection


def query(connection, sql, parameters=()):
    # Each row becomes a dict keyed by column name, as the template reads it
    connection.row_factory = sqlite3.Row
    return [dict(row) for row in connection.execute(sql, parameters)]


connection = create_database()
try:
    # Filtered and sorted by the database
    customers = query(connection,
                      "SELECT * FROM Customers WHERE Balance > ? ORDER BY CustomerName ASC", (1000,))
finally:
    connection.close()

assembler = DocumentAssembler()
assembler.assemble_document("customer-accounts.docx", "customer-accounts-filtered.docx",
                            DataSourceInfo(customers, "customers"))

print("Document generated from filtered rows successfully.")
```
{{< /tab >}}
{{< tab "customer-accounts.docx" >}}
{{< tab-text >}}
The following sample file is used in this example: [customer-accounts.docx](/assembly/python-net/_sample_files/developer-guide/basic-usage/generate-from-database/customer-accounts.docx)
{{< /tab-text >}}
{{< /tab >}}
{{< tab "customer-accounts-filtered.docx" >}}  
```text
Binary file (DOCX, 7 KB)
```
[Download full output](/assembly/python-net/_output_files/developer-guide/basic-usage/generate-from-database/filtering_and_sorting_rows/customer-accounts-filtered.docx)
{{< /tab >}}
{{< /tabs >}}

## Working with Related Tables

A .NET `DataSet` relation lets a template call `GetChildRows("CustomerOrders")` on a customer row. Python rows have no such method: nest each customer's orders under the customer instead, and the template iterates them as a member:

{{< tabs "example4" >}}
{{< tab "Python" >}}
```python
import sqlite3

from groupdocs.assembly import DataSourceInfo, DocumentAssembler


def create_database():
    # An in-memory database standing in for your own
    connection = sqlite3.connect(":memory:")
    connection.executescript("""
        CREATE TABLE Customers (CustomerId INTEGER PRIMARY KEY, CustomerName TEXT, Email TEXT, Balance REAL);
        INSERT INTO Customers VALUES (1, 'Quayside Bistro', 'orders@quaysidebistro.example', 1250.75);
        INSERT INTO Customers VALUES (2, 'Lantern Street Café', 'orders@lanternstreetcafe.example', 2480.00);
        INSERT INTO Customers VALUES (3, 'Saltmarsh Deli', 'orders@saltmarshdeli.example', 640.50);
        INSERT INTO Customers VALUES (4, 'Pier Nine Kitchen', 'orders@piernine.example', 1890.20);
        CREATE TABLE Orders (OrderId INTEGER PRIMARY KEY, CustomerId INTEGER, Amount REAL);
        INSERT INTO Orders VALUES (10001, 1, 552.00);
        INSERT INTO Orders VALUES (10002, 2, 522.00);
        INSERT INTO Orders VALUES (10003, 3, 281.00);
        INSERT INTO Orders VALUES (10004, 1, 132.00);
        INSERT INTO Orders VALUES (10005, 2, 192.00);
        INSERT INTO Orders VALUES (10006, 1, 516.00);
        INSERT INTO Orders VALUES (10007, 4, 198.00);
        INSERT INTO Orders VALUES (10008, 3, 456.00);
    """)
    return connection


def query(connection, sql, parameters=()):
    # Each row becomes a dict keyed by column name, as the template reads it
    connection.row_factory = sqlite3.Row
    return [dict(row) for row in connection.execute(sql, parameters)]


connection = create_database()
try:
    customers = query(connection, "SELECT * FROM Customers ORDER BY CustomerId")
    # Relate the tables: each customer gets the list of its own orders
    for customer in customers:
        customer["Orders"] = query(connection,
                                   "SELECT OrderId, Amount FROM Orders WHERE CustomerId = ? ORDER BY OrderId",
                                   (customer["CustomerId"],))
finally:
    connection.close()

assembler = DocumentAssembler()
assembler.assemble_document("customer-orders.docx", "customer-orders-report.docx",
                            DataSourceInfo(customers, "customers"))

print("Document generated with related rows successfully.")
```
{{< /tab >}}
{{< tab "customer-orders.docx" >}}
{{< tab-text >}}
The following sample file is used in this example: [customer-orders.docx](/assembly/python-net/_sample_files/developer-guide/basic-usage/generate-from-database/customer-orders.docx)
{{< /tab-text >}}
{{< /tab >}}
{{< tab "customer-orders-report.docx" >}}  
```text
Binary file (DOCX, 8 KB)
```
[Download full output](/assembly/python-net/_output_files/developer-guide/basic-usage/generate-from-database/working_with_related_tables/customer-orders-report.docx)
{{< /tab >}}
{{< /tabs >}}

Template with related rows:

```text
<<foreach [in customers]>>
Customer: <<[CustomerName]>>
Orders:
<<foreach [in Orders]>>
  - Order #<<[OrderId]>>: <<[Amount]:"C">>
<</foreach>>
<</foreach>>
```

{{< alert style="warning" >}}
When using database connections, always release them. Close the connection in a `finally` block, as above, or with `contextlib.closing`. A customer with no orders gets an empty list, which works as long as another customer has orders: an empty list on its own carries no column names, and the template then fails with "Can not get the value of member ... on type 'System.Object'".
{{< /alert >}}

### Advanced Usage Topics

To learn more about working with complex data, several data sources, and performance optimization for large datasets, please refer to the [advanced usage section]({{< ref "assembly/python-net/developer-guide/advanced-usage/_index.md" >}}).

## More resources

### GitHub Examples

You may easily run the code above and see the feature in action in our GitHub examples:

* [GroupDocs.Assembly for .NET examples, plugins, and showcase](https://github.com/groupdocs-assembly/GroupDocs.Assembly-for-.NET)
* [GroupDocs.Assembly for Java examples, plugins, and showcase](https://github.com/groupdocs-assembly/GroupDocs.Assembly-for-Java)
* [GroupDocs.Assembly for Python via .NET examples, plugins, and showcase](https://github.com/groupdocs-assembly/GroupDocs.Assembly-for-Python-via-.NET)

### Free Online Apps

Along with the full-featured library, we provide simple but powerful free online apps.

To assemble documents from templates and data sources, you can use the online apps from the **[GroupDocs.Assembly App Product Family](https://products.groupdocs.app/assembly/family)**.
