---
id: assembly-basic-usage-template-syntax-basics
url: assembly/python-net/basic-usage-template-syntax-basics
linktitle: Basic Template Syntax
title: Basic Template Syntax - Expression Tags and Fields
weight: 5
description: "Introduction to the basic template syntax of GroupDocs.Assembly for Python via .NET: expression tags that output values from Python dicts, calculations, string methods and format strings."
keywords: template syntax, expression tags, fields, basic syntax, template expressions, Python dict, assemble, generate, Python
productName: GroupDocs.Assembly for Python via .NET
hideChildren: False
---

## Overview

GroupDocs.Assembly for Python via .NET uses a simple, LINQ-based template syntax that allows you to embed expressions directly in your documents. Expression tags are the foundation of template syntax, enabling you to output data values and perform calculations.

The main syntax elements are:
- Expression tags `<<[expression]>>` - output expression results
- Data bands `<<foreach>>` - iterate over collections
- Conditional blocks `<<if>>` - display content conditionally

Here are the steps to use basic template syntax:

* Create a template document in Word, Excel, PowerPoint, or HTML format
* Insert expression tags using `<<[expression]>>` syntax
* Reference the keys of your Python dicts (and the methods of their values) in expressions
* Assemble the document with your data source

{{< alert style="info" >}}
Template syntax is case-sensitive, and the expressions inside tags follow C# language rules whichever language calls the assembler: a Python program's templates still write `&&`, `==` and `"text"`. A dict key is a member name: `person.Name` reads the `"Name"` key of the dict passed as `person`. Expression tags are evaluated at runtime and replaced with their computed values.
{{< /alert >}}

## Basic Expression Tags

Expression tags are the simplest way to output data in templates. They use the syntax `<<[expression]>>`:

{{< tabs "example1" >}}
{{< tab "Python" >}}
```python
from groupdocs.assembly import DataSourceInfo, DocumentAssembler

# Sample data: the keys are the member names the template reads
person = {"Name": "Amara Osei", "Age": 41, "Email": "amara.osei@harborlane.example"}

# Assemble document
assembler = DocumentAssembler()
assembler.assemble_document("person-details.docx", "person-details-report.docx",
                            DataSourceInfo(person, "person"))

print("Document assembled with expression tags.")
```
{{< /tab >}}
{{< tab "person-details.docx" >}}
{{< tab-text >}}
The following sample file is used in this example: [person-details.docx](/assembly/python-net/_sample_files/developer-guide/basic-usage/basic-template-syntax/person-details.docx)
{{< /tab-text >}}
{{< /tab >}}
{{< tab "person-details-report.docx" >}}  
```text
Binary file (DOCX, 7 KB)
```
[Download full output](/assembly/python-net/_output_files/developer-guide/basic-usage/basic-template-syntax/basic_expression_tags/person-details-report.docx)
{{< /tab >}}
{{< /tabs >}}

## Template Example with Expression Tags

In your template document (person-details.docx), use expression tags like this:

```text
Name: <<[person.Name]>>
Age: <<[person.Age]>>
Email: <<[person.Email]>>
```

After assembly, the output will be:

```text
Name: Amara Osei
Age: 41
Email: amara.osei@harborlane.example
```

## Using Contextual Object Member Access

When using a single data source, you can omit the data source name and use contextual access:

{{< tabs "example2" >}}
{{< tab "Python" >}}
```python
from decimal import Decimal

from groupdocs.assembly import DataSourceInfo, DocumentAssembler

product = {"Name": "Harbor Blend whole bean coffee", "Price": Decimal("18.40"), "Stock": 240}

assembler = DocumentAssembler()
assembler.assemble_document("product-summary.docx", "product-summary-report.docx",
                            DataSourceInfo(product))

print("Document assembled with contextual access.")
```
{{< /tab >}}
{{< tab "product-summary.docx" >}}
{{< tab-text >}}
The following sample file is used in this example: [product-summary.docx](/assembly/python-net/_sample_files/developer-guide/basic-usage/basic-template-syntax/product-summary.docx)
{{< /tab-text >}}
{{< /tab >}}
{{< tab "product-summary-report.docx" >}}  
```text
Binary file (DOCX, 7 KB)
```
[Download full output](/assembly/python-net/_output_files/developer-guide/basic-usage/basic-template-syntax/using_contextual_object_member_access/product-summary-report.docx)
{{< /tab >}}
{{< /tabs >}}

Template with contextual access:

```text
Product: <<[Name]>>
Price: <<[Price]>>
Stock: <<[Stock]>>
```

The price is a `Decimal`, so it reaches the template as a .NET `decimal` and keeps its two decimal places: `18.40`.

## Simple Calculations in Expressions

You can perform calculations directly in expression tags:

{{< tabs "example3" >}}
{{< tab "Python" >}}
```python
from decimal import Decimal

from groupdocs.assembly import DataSourceInfo, DocumentAssembler

order = {"Quantity": 5, "UnitPrice": Decimal("18.40")}

assembler = DocumentAssembler()
assembler.assemble_document("order-calculation.docx", "order-calculation-report.docx",
                            DataSourceInfo(order, "order"))

print("Document assembled with calculations.")
```
{{< /tab >}}
{{< tab "order-calculation.docx" >}}
{{< tab-text >}}
The following sample file is used in this example: [order-calculation.docx](/assembly/python-net/_sample_files/developer-guide/basic-usage/basic-template-syntax/order-calculation.docx)
{{< /tab-text >}}
{{< /tab >}}
{{< tab "order-calculation-report.docx" >}}  
```text
Binary file (DOCX, 7 KB)
```
[Download full output](/assembly/python-net/_output_files/developer-guide/basic-usage/basic-template-syntax/simple_calculations_in_expressions/order-calculation-report.docx)
{{< /tab >}}
{{< /tabs >}}

Template with calculations:

```text
Quantity: <<[order.Quantity]>>
Unit Price: <<[order.UnitPrice]>>
Total: <<[order.Quantity * order.UnitPrice]>>
```

The total is `92.00`: an `int` times a `Decimal` is a `decimal` in the template, as in Python.

## Using String Methods

You can use .NET string methods in expressions: a Python `str` reaches the template as a .NET `string`.

{{< tabs "example4" >}}
{{< tab "Python" >}}
```python
from groupdocs.assembly import DataSourceInfo, DocumentAssembler

company = {"Name": "Harbor Lane Provisions", "Website": "HTTPS://HarborLane.example/"}

assembler = DocumentAssembler()
assembler.assemble_document("company-header.docx", "company-header-report.docx",
                            DataSourceInfo(company, "company"))

print("Document assembled with string methods.")
```
{{< /tab >}}
{{< tab "company-header.docx" >}}
{{< tab-text >}}
The following sample file is used in this example: [company-header.docx](/assembly/python-net/_sample_files/developer-guide/basic-usage/basic-template-syntax/company-header.docx)
{{< /tab-text >}}
{{< /tab >}}
{{< tab "company-header-report.docx" >}}  
```text
Binary file (DOCX, 7 KB)
```
[Download full output](/assembly/python-net/_output_files/developer-guide/basic-usage/basic-template-syntax/using_string_methods/company-header-report.docx)
{{< /tab >}}
{{< /tabs >}}

Template with string methods:

```text
Company: <<[company.Name.ToUpper()]>>
Website: <<[company.Website.ToLower()]>>
```

## Expression Tag Formatting

You can format expression results using format strings:

{{< tabs "example5" >}}
{{< tab "Python" >}}
```python
from datetime import datetime
from decimal import Decimal

from groupdocs.assembly import DataSourceInfo, DocumentAssembler

invoice = {
    "Amount": Decimal("1500.50"),
    "Date": datetime(2015, 1, 15),
    "Percentage": 0.15,
}

assembler = DocumentAssembler()
assembler.assemble_document("invoice-format-strings.docx", "invoice-format-strings-report.docx",
                            DataSourceInfo(invoice, "invoice"))

print("Document assembled with formatting.")
```
{{< /tab >}}
{{< tab "invoice-format-strings.docx" >}}
{{< tab-text >}}
The following sample file is used in this example: [invoice-format-strings.docx](/assembly/python-net/_sample_files/developer-guide/basic-usage/basic-template-syntax/invoice-format-strings.docx)
{{< /tab-text >}}
{{< /tab >}}
{{< tab "invoice-format-strings-report.docx" >}}  
```text
Binary file (DOCX, 7 KB)
```
[Download full output](/assembly/python-net/_output_files/developer-guide/basic-usage/basic-template-syntax/expression_tag_formatting/invoice-format-strings-report.docx)
{{< /tab >}}
{{< /tabs >}}

Template with formatting:

```text
Amount: <<[invoice.Amount]:"C">>
Date: <<[invoice.Date]:"yyyy-MM-dd">>
Percentage: <<[invoice.Percentage]:"P">>
```

A date format needs a `datetime` (or a `date`) in the data. A string is written as it is: `<<[invoice.Date]:"MMMM dd, yyyy">>` gives `January 15, 2015` for `datetime(2015, 1, 15)` but `2015-01-15` for the text `"2015-01-15"`.

{{< alert style="warning" >}}
Format strings follow .NET formatting conventions, not Python's: use "C" for currency, "P" for percentage, and .NET date/time format strings such as "yyyy-MM-dd" for dates (not `%Y-%m-%d`). "C" and "P" follow the culture of the process: under en-US the amount above is written $1,500.50.
{{< /alert >}}

### Advanced Usage Topics

To learn more about data bands, conditional blocks, LINQ expressions, and advanced template syntax features, please refer to the [advanced usage section]({{< ref "assembly/python-net/developer-guide/advanced-usage/_index.md" >}}).

## More resources

### GitHub Examples

You may easily run the code above and see the feature in action in our GitHub examples:

* [GroupDocs.Assembly for .NET examples, plugins, and showcase](https://github.com/groupdocs-assembly/GroupDocs.Assembly-for-.NET)
* [GroupDocs.Assembly for Java examples, plugins, and showcase](https://github.com/groupdocs-assembly/GroupDocs.Assembly-for-Java)
* [GroupDocs.Assembly for Python via .NET examples, plugins, and showcase](https://github.com/groupdocs-assembly/GroupDocs.Assembly-for-Python-via-.NET)

### Free Online Apps

Along with the full-featured library, we provide simple but powerful free online apps.

To assemble documents from templates and data sources, you can use the online apps from the **[GroupDocs.Assembly App Product Family](https://products.groupdocs.app/assembly/family)**.
