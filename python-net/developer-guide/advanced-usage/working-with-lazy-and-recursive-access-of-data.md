---
id: working-with-lazy-and-recursive-access-of-data
url: assembly/python-net/working-with-lazy-and-recursive-access-of-data
title: Working with Lazy And Recursive Access of Data
weight: 26
description: "Nested and recursive Python dicts as a GroupDocs.Assembly for Python via .NET data source: member access at any depth, structures that refer back to themselves, the dict indexer and its limit, and when the engine reads the data."
keywords: lazy access, recursive data, nested dict, circular reference, indexer, Python, GroupDocs.Assembly
productName: GroupDocs.Assembly for Python via .NET
hideChildren: False
---
{{< alert style="info" >}}The example reads the shop data described in [The Business Layer]({{< ref "assembly/python-net/developer-guide/basic-usage/working-with-a-business-case/the-business-layer.md" >}}).{{< /alert >}}

## Purpose

A report often needs data that is related to its root object at several levels: a customer, its account, its account manager, the other customers of that manager. The .NET version of this page builds such data with a custom C# type whose indexers fetch each property, related entity and list of child entities lazily, when the template first asks for it.

In Python, the same data is a structure of nested dicts and lists, and the template reaches every level by member access: `root.Entities.AccountManager.Name`. The structure may also refer back to itself. A dict that appears in several places, such as an account manager that each of its customers points to, is one object for the engine, so a template can follow the references round as far as it needs. See [Using Data Sources]({{< ref "assembly/python-net/developer-guide/basic-usage/working-with-groupdocs.assembly-engine/template-syntax-part-1-of-2.md#using-data-sources" >}}) for how the engine reads Python data.

## Creating Template

The template reads the properties of the root entity, its related entities, its child entities, and then goes from the root to its account manager and back to the manager's customers:

```text
Using properties of the root entity
<<[root["CustomerName"]]>>
<<[root.ShippingAddress]>>

Using related entities of the root entity
<<[root.Entities.Account.Login]>>
<<[root.Entities.AccountManager.Name]>>

Using child entities of the root entity
<<foreach [order in root.Children.Orders]>><<[order.OrderNumber]>>: <<[order.Product.ProductName]>>
<</foreach>>
Invoice | Amount due
<<foreach [invoice in root.Children.Invoices]>><<[invoice.Number]>> | <<[invoice.Amount]>><</foreach>>

Following the references back
<<foreach [customer in root.Entities.AccountManager.Customers]>><<[customer.CustomerName]>> (<<[customer.Entities.Account.Login]>>) is managed by <<[customer.Entities.AccountManager.Name]>>, who manages <<[customer.Entities.AccountManager.Customers.Count()]>> customers
<</foreach>>
```

The invoices are a table-row data band in the template.

## Download Template

Get the template from here.

*   [recursive-customer-data.docx](/assembly/python-net/_sample_files/developer-guide/advanced-usage/working-with-lazy-and-recursive-access-of-data/recursive-customer-data.docx)

## Generating The Report

The code loads Quayside Bistro and Saltmarsh Deli from `customers.json`, gives each its related and child entities as nested dicts, and puts both in the list of customers of their account manager, Mei Tanaka. Each customer's `AccountManager` is that same manager dict, so the data is circular: manager, customer, manager again.

{{< tabs "example1" >}}
{{< tab "Python" >}}
```python
import json

from groupdocs.assembly import DataSourceInfo, DocumentAssembler

with open("customers.json", encoding="utf-8") as f:
    customers = {c["CustomerName"]: c for c in json.load(f)}

manager = {"Name": "Mei Tanaka", "Customers": []}


def add_entities(customer, login):
    # Related entities and child entities of a customer, as nested dicts and lists
    customer["Entities"] = {"Account": {"Login": login}, "AccountManager": manager}
    customer["Children"] = {
        "Orders": customer["Order"],
        "Invoices": [{"Number": "INV-%d" % o["OrderNumber"], "Amount": o["Price"]} for o in customer["Order"]],
    }
    # The manager refers back to the customer: the structure is circular
    manager["Customers"].append(customer)
    return customer


root = add_entities(customers["Quayside Bistro"], "quayside-bistro")
add_entities(customers["Saltmarsh Deli"], "saltmarsh-deli")

assembler = DocumentAssembler()
assembler.assemble_document("recursive-customer-data.docx", "recursive-customer-data-report.docx", DataSourceInfo(root, "root"))
```
{{< /tab >}}
{{< tab "recursive-customer-data.docx" >}}
{{< tab-text >}}
The following sample file is used in this example: [recursive-customer-data.docx](/assembly/python-net/_sample_files/developer-guide/advanced-usage/working-with-lazy-and-recursive-access-of-data/recursive-customer-data.docx)
{{< /tab-text >}}
{{< /tab >}}
{{< tab "customers.json" >}}
{{< tab-text >}}
The following sample file is used in this example: [customers.json](/assembly/python-net/_sample_files/developer-guide/advanced-usage/working-with-lazy-and-recursive-access-of-data/customers.json)
{{< /tab-text >}}
{{< /tab >}}
{{< tab "recursive-customer-data-report.docx" >}}  
```text
Binary file (DOCX, 8 KB)
```
[Download full output](/assembly/python-net/_output_files/developer-guide/advanced-usage/working-with-lazy-and-recursive-access-of-data/generating_the_report/recursive-customer-data-report.docx)
{{< /tab >}}
{{< /tabs >}}

## Accessing a Dict by Key

A dict passed to the engine also has an indexer, so `<<[root["CustomerName"]]>>` reads a value by its key, as in the template above. Use it for a key that is not an identifier, such as `<<[row["First Name"]]>>`. The indexer returns the value as `object`, however, which the engine cannot index again or read members of. The indexer chain of the .NET template, `root.Entities["Account"]["Login"]`, fails in Python with:

```text
Can not resolve an indexer on type 'System.Object'.
```

Write such a chain with member access instead, `root.Entities.Account.Login`, as the template above does.

## When the Engine Reads the Data

Python data is read eagerly. `DataSourceInfo(root, "root")` copies the whole structure into .NET objects when it is created, so:

*   The data must be complete before `DataSourceInfo` is created. A change made to a dict afterwards does not reach the report.
*   A value cannot be computed on demand. The engine reads only dicts, lists, tuples and sets, and the values `str`, `int`, `float`, `decimal.Decimal`, `bool`, `None`, `datetime`, `date`, `time` and `bytes`. Another Python object, such as an instance of a class with properties, raises a `TypeError`, and the `__getitem__` of a dict subclass is not called.
*   A list cannot contain itself: that raises a `ValueError`. A dict can be referred to from any number of places, itself included.

To keep a large report fast, load only the data its template reads before you call `assemble_document`.
