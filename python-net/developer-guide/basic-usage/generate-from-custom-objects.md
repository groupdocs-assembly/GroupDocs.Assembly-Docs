---
id: assembly-basic-usage-custom-objects
url: assembly/python-net/basic-usage-custom-objects
linktitle: Generate from Custom Objects
title: Generate Document from Python Dicts and Lists
weight: 6
description: "Generate documents with GroupDocs.Assembly for Python via .NET by binding Python dicts, lists and nested dicts to template documents."
keywords: custom objects, Python dict, Python list, nested dict, data binding, Python, assemble document, generate from objects
productName: GroupDocs.Assembly for Python via .NET
hideChildren: False
---

## Overview

One of the most common scenarios in document assembly is generating reports from your application's own data. GroupDocs.Assembly for Python via .NET binds Python dicts and lists directly to templates: each dict reaches the template as an object whose members are the dict's keys, so the template text is the same as for .NET objects.

The main classes involved are:
- [DocumentAssembler](https://reference.groupdocs.com/assembly/python-net/groupdocs.assembly/documentassembler/) - assembles documents from templates
- [DataSourceInfo](https://reference.groupdocs.com/assembly/python-net/groupdocs.assembly/datasourceinfo/) - wraps data source objects

Here are the steps to generate documents from your own data:

* Describe each record as a dict whose keys are the member names the template reads
* Fill the dict (or a list of dicts) with data
* Create a template document with expression tags referencing those members
* Use DocumentAssembler to assemble the template with your data
* Save the assembled document

{{< alert style="info" >}}
A dict's values may be `str`, `int`, `float`, `decimal.Decimal`, `bool`, `datetime`/`date`, `None`, and nested dicts and lists. The value's type decides what the template can do with it: a date format such as `"yyyy-MM-dd"` needs a `datetime` or `date`, and a currency format needs a number. Anything else (a function, an instance of your own class) raises `TypeError` before the engine is called.
{{< /alert >}}

## Describe a Customer

Start by deciding which keys the template reads. A customer record looks like this:

```python
from datetime import datetime
from decimal import Decimal

customer = {
    "Name": "Quayside Bistro",
    "Email": "orders@quaysidebistro.example",
    "Address": "3 Harbour Steps, Port Ellery",
    "RegistrationDate": datetime(2015, 1, 14),
    "Balance": Decimal("1250.75"),
}
```

## Generate Document from Single Object

Generate a document from a single dict:

{{< tabs "example1" >}}
{{< tab "Python" >}}
```python
from datetime import datetime
from decimal import Decimal

from groupdocs.assembly import DataSourceInfo, DocumentAssembler

# Create and populate the record
customer = {
    "Name": "Quayside Bistro",
    "Email": "orders@quaysidebistro.example",
    "Address": "3 Harbour Steps, Port Ellery",
    "RegistrationDate": datetime(2015, 1, 14),
    "Balance": Decimal("1250.75"),
}

# Assemble document
assembler = DocumentAssembler()
assembler.assemble_document("customer-profile.docx", "customer-profile-report.docx",
                            DataSourceInfo(customer, "customer"))

print("Document generated from custom object successfully.")
```
{{< /tab >}}
{{< tab "customer-profile.docx" >}}
{{< tab-text >}}
The following sample file is used in this example: [customer-profile.docx](/assembly/python-net/_sample_files/developer-guide/basic-usage/generate-from-custom-objects/customer-profile.docx)
{{< /tab-text >}}
{{< /tab >}}
{{< tab "customer-profile-report.docx" >}}  
```text
Binary file (DOCX, 7 KB)
```
[Download full output](/assembly/python-net/_output_files/developer-guide/basic-usage/generate-from-custom-objects/generate_document_from_single_object/customer-profile-report.docx)
{{< /tab >}}
{{< /tabs >}}

## Template Example

Your template (customer-profile.docx) can reference the record's members:

```text
Customer Information

Name: <<[customer.Name]>>
Email: <<[customer.Email]>>
Address: <<[customer.Address]>>
Registration Date: <<[customer.RegistrationDate]:"yyyy-MM-dd">>
Balance: <<[customer.Balance]:"C">>
```

## Generate Document from Object Collection

You can also generate documents from a list of dicts:

{{< tabs "example2" >}}
{{< tab "Python" >}}
```python
from decimal import Decimal

from groupdocs.assembly import DataSourceInfo, DocumentAssembler

# Create a list of records
customers = [
    {"Name": "Quayside Bistro", "Email": "orders@quaysidebistro.example", "Balance": Decimal("1000")},
    {"Name": "Lantern Street Café", "Email": "orders@lanternstreetcafe.example", "Balance": Decimal("2500")},
    {"Name": "Saltmarsh Deli", "Email": "orders@saltmarshdeli.example", "Balance": Decimal("750")},
]

assembler = DocumentAssembler()
assembler.assemble_document("customer-balances.docx", "customer-balances-report.docx",
                            DataSourceInfo(customers, "customers"))

print("Document generated from collection successfully.")
```
{{< /tab >}}
{{< tab "customer-balances.docx" >}}
{{< tab-text >}}
The following sample file is used in this example: [customer-balances.docx](/assembly/python-net/_sample_files/developer-guide/basic-usage/generate-from-custom-objects/customer-balances.docx)
{{< /tab-text >}}
{{< /tab >}}
{{< tab "customer-balances-report.docx" >}}  
```text
Binary file (DOCX, 7 KB)
```
[Download full output](/assembly/python-net/_output_files/developer-guide/basic-usage/generate-from-custom-objects/generate_document_from_object_collection/customer-balances-report.docx)
{{< /tab >}}
{{< /tabs >}}

Template for collection (using data band):

```text
Customers List:

<<foreach [in customers]>>
<<[Name]>> - <<[Email]>> - Balance: <<[Balance]:"C">>
<</foreach>>
```

## Using Nested Objects

A dict can hold other dicts:

{{< tabs "example3" >}}
{{< tab "Python" >}}
```python
from datetime import datetime
from decimal import Decimal

from groupdocs.assembly import DataSourceInfo, DocumentAssembler

order = {
    "OrderId": 10001,
    "OrderDate": datetime(2015, 1, 14),
    "Customer": {
        "Name": "Quayside Bistro",
        "Email": "orders@quaysidebistro.example",
    },
    "TotalAmount": Decimal("552.00"),
}

assembler = DocumentAssembler()
assembler.assemble_document("order-confirmation.docx", "order-confirmation-report.docx",
                            DataSourceInfo(order, "order"))

print("Document generated from nested objects successfully.")
```
{{< /tab >}}
{{< tab "order-confirmation.docx" >}}
{{< tab-text >}}
The following sample file is used in this example: [order-confirmation.docx](/assembly/python-net/_sample_files/developer-guide/basic-usage/generate-from-custom-objects/order-confirmation.docx)
{{< /tab-text >}}
{{< /tab >}}
{{< tab "order-confirmation-report.docx" >}}  
```text
Binary file (DOCX, 7 KB)
```
[Download full output](/assembly/python-net/_output_files/developer-guide/basic-usage/generate-from-custom-objects/using_nested_objects/order-confirmation-report.docx)
{{< /tab >}}
{{< /tabs >}}

Template with nested object access:

```text
Order #<<[order.OrderId]>>
Date: <<[order.OrderDate]:"yyyy-MM-dd">>

Customer:
Name: <<[order.Customer.Name]>>
Email: <<[order.Customer.Email]>>

Total: <<[order.TotalAmount]:"C">>
```

## Calculating Values

A .NET object can expose a method such as `GetTotal()` for the template to call. A dict has no methods, and a function stored in a dict is rejected with `TypeError` ("function cannot be part of a data source given as a dict"). Calculate the value in the template expression instead, or store the result under its own key in Python:

{{< tabs "example4" >}}
{{< tab "Python" >}}
```python
from decimal import Decimal

from groupdocs.assembly import DataSourceInfo, DocumentAssembler

product = {
    "Name": "Lighthouse Espresso beans",
    "Price": Decimal("21.75"),
    "Quantity": 2,
}

assembler = DocumentAssembler()
assembler.assemble_document("product-line.docx", "product-line-report.docx",
                            DataSourceInfo(product, "product"))

print("Document generated with a calculated total successfully.")
```
{{< /tab >}}
{{< tab "product-line.docx" >}}
{{< tab-text >}}
The following sample file is used in this example: [product-line.docx](/assembly/python-net/_sample_files/developer-guide/basic-usage/generate-from-custom-objects/product-line.docx)
{{< /tab-text >}}
{{< /tab >}}
{{< tab "product-line-report.docx" >}}  
```text
Binary file (DOCX, 7 KB)
```
[Download full output](/assembly/python-net/_output_files/developer-guide/basic-usage/generate-from-custom-objects/calculating_values/product-line-report.docx)
{{< /tab >}}
{{< /tabs >}}

Template calculating the total:

```text
Product: <<[product.Name]>>
Price: <<[product.Price]:"C">>
Quantity: <<[product.Quantity]>>
Total: <<[product.Price * product.Quantity]:"C">>
```

{{< alert style="warning" >}}
Keep calculations in templates simple. When a value needs your application's logic, compute it in Python and pass it as one more key (`"Total": price * quantity`).
{{< /alert >}}

## Using Instances of Your Own Classes

An instance of a Python class cannot be passed as it is: the call raises `TypeError` ("Object of type Customer is not JSON serializable"). Pass its attributes as a dict with `vars()`. This converts one level only, so a nested instance needs its own `vars()`:

{{< tabs "example5" >}}
{{< tab "Python" >}}
```python
from decimal import Decimal

from groupdocs.assembly import DataSourceInfo, DocumentAssembler


class Customer(object):
    def __init__(self, name, email, balance):
        self.Name = name
        self.Email = email
        self.Balance = balance


customers = [
    Customer("Quayside Bistro", "orders@quaysidebistro.example", Decimal("1000")),
    Customer("Pier Nine Kitchen", "orders@piernine.example", Decimal("320.50")),
]

# vars() turns each instance into the dict of its attributes
assembler = DocumentAssembler()
assembler.assemble_document("customer-balances.docx", "customer-balances-from-classes.docx",
                            DataSourceInfo([vars(customer) for customer in customers], "customers"))

print("Document generated from class instances successfully.")
```
{{< /tab >}}
{{< tab "customer-balances.docx" >}}
{{< tab-text >}}
The following sample file is used in this example: [customer-balances.docx](/assembly/python-net/_sample_files/developer-guide/basic-usage/generate-from-custom-objects/customer-balances.docx)
{{< /tab-text >}}
{{< /tab >}}
{{< tab "customer-balances-from-classes.docx" >}}  
```text
Binary file (DOCX, 7 KB)
```
[Download full output](/assembly/python-net/_output_files/developer-guide/basic-usage/generate-from-custom-objects/using_instances_of_your_own_classes/customer-balances-from-classes.docx)
{{< /tab >}}
{{< /tabs >}}

### Advanced Usage Topics

To learn more about working with complex data hierarchies, collections, LINQ queries over your data, and performance optimization, please refer to the [advanced usage section]({{< ref "assembly/python-net/developer-guide/advanced-usage/_index.md" >}}).

## More resources

### GitHub Examples

You may easily run the code above and see the feature in action in our GitHub examples:

* [GroupDocs.Assembly for .NET examples, plugins, and showcase](https://github.com/groupdocs-assembly/GroupDocs.Assembly-for-.NET)
* [GroupDocs.Assembly for Java examples, plugins, and showcase](https://github.com/groupdocs-assembly/GroupDocs.Assembly-for-Java)
* [GroupDocs.Assembly for Python via .NET examples, plugins, and showcase](https://github.com/groupdocs-assembly/GroupDocs.Assembly-for-Python-via-.NET)

### Free Online Apps

Along with the full-featured library, we provide simple but powerful free online apps.

To assemble documents from templates and data sources, you can use the online apps from the **[GroupDocs.Assembly App Product Family](https://products.groupdocs.app/assembly/family)**.
