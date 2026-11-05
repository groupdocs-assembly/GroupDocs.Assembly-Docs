---
id: assembly-basic-usage-conditional-content
url: assembly/python-net/basic-usage-conditional-content
linktitle: Add Conditional Content
title: Add Conditional Content with If/Else
weight: 23
description: "Display content conditionally in templates with if/elseif/else blocks that test the values of Python dicts, using GroupDocs.Assembly for Python via .NET."
keywords: conditional content, if else, conditional blocks, conditional display, conditional formatting, if elseif, Python dict, Python
productName: GroupDocs.Assembly for Python via .NET
hideChildren: False
---

## Overview

Conditional blocks allow you to display different content in your documents based on data values. GroupDocs.Assembly for Python via .NET supports if/elseif/else syntax, enabling you to create dynamic documents that adapt their content based on conditions.

The main syntax elements are:
- `<<if [condition]>>` - display content if condition is true
- `<<elseif [condition]>>` - display content if previous conditions are false and this condition is true
- `<<else>>` - display content if all conditions are false
- `<</if>>` - closing tag

Here are the steps to use conditional content:

* Create a template with conditional blocks
* Define conditions using expressions that return boolean values
* Provide content for each condition branch
* Assemble the document with your data

{{< alert style="info" >}}
Conditional expressions must return boolean values. The template writes them with C# operators, also when Python calls the assembler: comparison operators (==, !=, <, >, <=, >=), logical operators (&&, ||, !), and method calls that return bool. A Python `bool` in the data is a boolean in the template.
{{< /alert >}}

## Simple If/Else Block

Display content based on a simple condition:

{{< tabs "example1" >}}
{{< tab "Python" >}}
```python
from decimal import Decimal

from groupdocs.assembly import DataSourceInfo, DocumentAssembler

customer = {
    "Name": "Quayside Bistro",
    "Balance": Decimal("1500.00"),
}

assembler = DocumentAssembler()
assembler.assemble_document("customer-status.docx", "customer-status-report.docx",
                            DataSourceInfo(customer, "customer"))

print("Conditional content generated successfully.")
```
{{< /tab >}}
{{< tab "customer-status.docx" >}}
{{< tab-text >}}
The following sample file is used in this example: [customer-status.docx](/assembly/python-net/_sample_files/developer-guide/basic-usage/conditional-content/customer-status.docx)
{{< /tab-text >}}
{{< /tab >}}
{{< tab "customer-status-report.docx" >}}  
```text
Binary file (DOCX, 7 KB)
```
[Download full output](/assembly/python-net/_output_files/developer-guide/basic-usage/conditional-content/simple_if_else_block/customer-status-report.docx)
{{< /tab >}}
{{< /tabs >}}

## Template Example for Simple If/Else

In your template (customer-status.docx):

```text
Customer: <<[customer.Name]>>

<<if [customer.Balance > 1000]>>
Status: Premium Customer
You have a high balance and qualify for special benefits.
<<else>>
Status: Standard Customer
Thank you for your business.
<</if>>
```

## If/Elseif/Else Block

Use multiple conditions with elseif:

{{< tabs "example2" >}}
{{< tab "Python" >}}
```python
from decimal import Decimal

from groupdocs.assembly import DataSourceInfo, DocumentAssembler

order = {"Amount": Decimal("750.00")}

assembler = DocumentAssembler()
assembler.assemble_document("order-discount.docx", "order-discount-report.docx",
                            DataSourceInfo(order, "order"))

print("Multiple conditions processed successfully.")
```
{{< /tab >}}
{{< tab "order-discount.docx" >}}
{{< tab-text >}}
The following sample file is used in this example: [order-discount.docx](/assembly/python-net/_sample_files/developer-guide/basic-usage/conditional-content/order-discount.docx)
{{< /tab-text >}}
{{< /tab >}}
{{< tab "order-discount-report.docx" >}}  
```text
Binary file (DOCX, 7 KB)
```
[Download full output](/assembly/python-net/_output_files/developer-guide/basic-usage/conditional-content/if_elseif_else_block/order-discount-report.docx)
{{< /tab >}}
{{< /tabs >}}

Template with elseif:

```text
Order Amount: <<[order.Amount]:"C">>

<<if [order.Amount > 1000]>>
Discount: 10% (Large order discount)
<<elseif [order.Amount > 500]>>
Discount: 5% (Medium order discount)
<<else>>
Discount: No discount available
<</if>>
```

## Conditional Content with Collections

Check if collections have items. A Python list reaches the template as a .NET collection, so it has the LINQ methods `Any()`, `Count()` and the others:

{{< tabs "example3" >}}
{{< tab "Python" >}}
```python
from groupdocs.assembly import DataSourceInfo, DocumentAssembler

report = {
    "Items": ["Harbor Blend whole bean coffee", "Aged harbour cheddar", "Cold-pressed olive oil"],
}

assembler = DocumentAssembler()
assembler.assemble_document("report-items.docx", "report-items-report.docx",
                            DataSourceInfo(report, "report"))

print("Conditional content with collections generated successfully.")
```
{{< /tab >}}
{{< tab "report-items.docx" >}}
{{< tab-text >}}
The following sample file is used in this example: [report-items.docx](/assembly/python-net/_sample_files/developer-guide/basic-usage/conditional-content/report-items.docx)
{{< /tab-text >}}
{{< /tab >}}
{{< tab "report-items-report.docx" >}}  
```text
Binary file (DOCX, 7 KB)
```
[Download full output](/assembly/python-net/_output_files/developer-guide/basic-usage/conditional-content/conditional_content_with_collections/report-items-report.docx)
{{< /tab >}}
{{< /tabs >}}

Template:

```text
<<if [report.Items.Any()]>>
Items:
<<foreach [item in report.Items]>>- <<[item]>>
<</foreach>><<else>>
No items available.
<</if>>
```

The items are strings, so the data band names its iteration variable (`item`) and outputs it with `<<[item]>>`. The band opens in the item's paragraph and closes at the start of the next one, so it repeats one paragraph per item; a `<<foreach>>` tag on a line of its own would repeat an empty paragraph too.

## Conditional Content in Data Bands

Use conditional blocks within foreach loops:

{{< tabs "example4" >}}
{{< tab "Python" >}}
```python
from decimal import Decimal

from groupdocs.assembly import DataSourceInfo, DocumentAssembler

products = [
    {"Name": "Harbor Blend whole bean coffee", "Price": Decimal("18.40"), "InStock": True},
    {"Name": "Lighthouse Espresso beans", "Price": Decimal("21.75"), "InStock": False},
    {"Name": "Chestnut honey", "Price": Decimal("7.80"), "InStock": True},
]

assembler = DocumentAssembler()
assembler.assemble_document("product-stock-status.docx", "product-stock-status-report.docx",
                            DataSourceInfo(products, "products"))

print("Conditional content in data band generated successfully.")
```
{{< /tab >}}
{{< tab "product-stock-status.docx" >}}
{{< tab-text >}}
The following sample file is used in this example: [product-stock-status.docx](/assembly/python-net/_sample_files/developer-guide/basic-usage/conditional-content/product-stock-status.docx)
{{< /tab-text >}}
{{< /tab >}}
{{< tab "product-stock-status-report.docx" >}}  
```text
Binary file (DOCX, 7 KB)
```
[Download full output](/assembly/python-net/_output_files/developer-guide/basic-usage/conditional-content/conditional_content_in_data_bands/product-stock-status-report.docx)
{{< /tab >}}
{{< /tabs >}}

Template:

```text
<<foreach [in products]>><<[Name]>> - <<[Price]:"C">>
<<if [InStock]>>✓ In Stock<<else>>✗ Out of Stock<</if>>

<</foreach>>
```

Each product gives three paragraphs: its name and price, its stock status, and an empty line.

## Complex Conditions

Use logical operators for complex conditions:

{{< tabs "example5" >}}
{{< tab "Python" >}}
```python
from groupdocs.assembly import DataSourceInfo, DocumentAssembler

employee = {
    "Name": "Amara Osei",
    "YearsOfService": 5,
    "Salary": 75000,
    "Department": "Engineering",
}

assembler = DocumentAssembler()
assembler.assemble_document("employee-review.docx", "employee-review-report.docx",
                            DataSourceInfo(employee, "employee"))

print("Complex conditions processed successfully.")
```
{{< /tab >}}
{{< tab "employee-review.docx" >}}
{{< tab-text >}}
The following sample file is used in this example: [employee-review.docx](/assembly/python-net/_sample_files/developer-guide/basic-usage/conditional-content/employee-review.docx)
{{< /tab-text >}}
{{< /tab >}}
{{< tab "employee-review-report.docx" >}}  
```text
Binary file (DOCX, 7 KB)
```
[Download full output](/assembly/python-net/_output_files/developer-guide/basic-usage/conditional-content/complex_conditions/employee-review-report.docx)
{{< /tab >}}
{{< /tabs >}}

Template with complex conditions:

```text
<<if [employee.YearsOfService >= 5 && employee.Salary > 70000]>>
Eligible for promotion
<<elseif [employee.Department == "Engineering"]>>
Consider for technical leadership
<<else>>
Standard review process
<</if>>
```

## Conditional Formatting

Apply different formatting based on conditions:

{{< tabs "example6" >}}
{{< tab "Python" >}}
```python
from decimal import Decimal

from groupdocs.assembly import DataSourceInfo, DocumentAssembler

invoice = {
    "Amount": Decimal("1500.00"),
    "IsPaid": False,
}

assembler = DocumentAssembler()
assembler.assemble_document("invoice-payment-status.docx", "invoice-payment-status-report.docx",
                            DataSourceInfo(invoice, "invoice"))

print("Conditional formatting applied successfully.")
```
{{< /tab >}}
{{< tab "invoice-payment-status.docx" >}}
{{< tab-text >}}
The following sample file is used in this example: [invoice-payment-status.docx](/assembly/python-net/_sample_files/developer-guide/basic-usage/conditional-content/invoice-payment-status.docx)
{{< /tab-text >}}
{{< /tab >}}
{{< tab "invoice-payment-status-report.docx" >}}  
```text
Binary file (DOCX, 7 KB)
```
[Download full output](/assembly/python-net/_output_files/developer-guide/basic-usage/conditional-content/conditional_formatting/invoice-payment-status-report.docx)
{{< /tab >}}
{{< /tabs >}}

Template:

```text
Amount: <<[invoice.Amount]:"C">>

<<if [invoice.IsPaid]>>
Status: PAID
<<else>>
Status: UNPAID - Payment Required
<</if>>
```

## Using Methods in Conditions

A condition can call any method of a value that returns bool, such as `Items.Any()` or `Name.StartsWith("Q")`. A Python dict carries data, not methods, so a test that a .NET class would write as its own method (`order.HasItems()`) is computed in Python and passed as a key:

{{< tabs "example7" >}}
{{< tab "Python" >}}
```python
from groupdocs.assembly import DataSourceInfo, DocumentAssembler

items = [{"Name": "Smoked sea salt"}]
order = {
    "Items": items,
    "HasItems": len(items) > 0,
}

assembler = DocumentAssembler()
assembler.assemble_document("order-contents.docx", "order-contents-report.docx",
                            DataSourceInfo(order, "order"))

print("Conditional with methods processed successfully.")
```
{{< /tab >}}
{{< tab "order-contents.docx" >}}
{{< tab-text >}}
The following sample file is used in this example: [order-contents.docx](/assembly/python-net/_sample_files/developer-guide/basic-usage/conditional-content/order-contents.docx)
{{< /tab-text >}}
{{< /tab >}}
{{< tab "order-contents-report.docx" >}}  
```text
Binary file (DOCX, 7 KB)
```
[Download full output](/assembly/python-net/_output_files/developer-guide/basic-usage/conditional-content/using_methods_in_conditions/order-contents-report.docx)
{{< /tab >}}
{{< /tabs >}}

Template:

```text
<<if [order.HasItems]>>
Order contains items.
<<else>>
Order is empty.
<</if>>
```

{{< alert style="warning" >}}
Conditional blocks must be properly closed with `<</if>>`. Nested conditional blocks are supported, but ensure proper nesting and closing of all blocks. A block closed with `<<if>>` instead fails with "Tag 'if' is not well-formed. Tag end is unexpected."
{{< /alert >}}

### Advanced Usage Topics

To learn more about table-row conditional blocks, conditional formatting in different document types, and advanced conditional scenarios, please refer to the [advanced usage section]({{< ref "assembly/python-net/developer-guide/advanced-usage/_index.md" >}}).

## More resources

### GitHub Examples

You may easily run the code above and see the feature in action in our GitHub examples:

* [GroupDocs.Assembly for .NET examples, plugins, and showcase](https://github.com/groupdocs-assembly/GroupDocs.Assembly-for-.NET)
* [GroupDocs.Assembly for Java examples, plugins, and showcase](https://github.com/groupdocs-assembly/GroupDocs.Assembly-for-Java)
* [GroupDocs.Assembly for Python via .NET examples, plugins, and showcase](https://github.com/groupdocs-assembly/GroupDocs.Assembly-for-Python-via-.NET)

### Free Online Apps

Along with the full-featured library, we provide simple but powerful free online apps.

To assemble documents from templates and data sources, you can use the online apps from the **[GroupDocs.Assembly App Product Family](https://products.groupdocs.app/assembly/family)**.
