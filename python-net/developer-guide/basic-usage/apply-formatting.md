---
id: assembly-basic-usage-formatting
url: assembly/python-net/basic-usage-formatting
linktitle: Apply Formatting for various types
title: Apply Formatting to Numbers, Dates, and Text in Python
weight: 22
description: "Format numbers, dates and text from Python dicts in templates with format strings and text functions, using GroupDocs.Assembly for Python via .NET."
keywords: formatting, number format, date format, text format, format strings, numeric formatting, date formatting, Decimal, datetime, Python
productName: GroupDocs.Assembly for Python via .NET
hideChildren: False
---

## Overview

GroupDocs.Assembly for Python via .NET provides comprehensive formatting capabilities for numbers, dates, and text in templates. You can use format strings (.NET format strings, whichever language calls the assembler) and built-in text transformation functions to control how data is displayed in your documents.

The main syntax elements are:
- Format strings: `<<[expression]:"format">>` - apply .NET format strings
- Text functions: `upper`, `lower`, `caps`, `firstCap` - transform text case

Here are the steps to apply formatting:

* Use format strings in expression tags for numbers and dates
* Apply text transformation functions for string formatting
* Combine formatting with expressions and calculations
* Test formatting to ensure desired output

{{< alert style="info" >}}
Format strings follow .NET formatting conventions, not Python's. Use standard numeric format specifiers (C, N, F, etc.) and date/time format strings (yyyy-MM-dd, etc.). The value's Python type decides what a format string can do: an `int`, `float` or `Decimal` takes a numeric format, a `datetime` or `date` takes a date format, and a `str` is written as it is.
{{< /alert >}}

## Format Numbers

Format numeric values using format strings:

{{< tabs "example1" >}}
{{< tab "Python" >}}
```python
from decimal import Decimal

from groupdocs.assembly import DataSourceInfo, DocumentAssembler

invoice = {
    "Amount": Decimal("1500.75"),
    "Percentage": 0.15,
    "Quantity": 25,
}

assembler = DocumentAssembler()
assembler.assemble_document("invoice-numbers.docx", "invoice-numbers-report.docx",
                            DataSourceInfo(invoice, "invoice"))

print("Numbers formatted successfully.")
```
{{< /tab >}}
{{< tab "invoice-numbers.docx" >}}
{{< tab-text >}}
The following sample file is used in this example: [invoice-numbers.docx](/assembly/python-net/_sample_files/developer-guide/basic-usage/apply-formatting/invoice-numbers.docx)
{{< /tab-text >}}
{{< /tab >}}
{{< tab "invoice-numbers-report.docx" >}}  
```text
Binary file (DOCX, 7 KB)
```
[Download full output](/assembly/python-net/_output_files/developer-guide/basic-usage/apply-formatting/format_numbers/invoice-numbers-report.docx)
{{< /tab >}}
{{< /tabs >}}

## Template Examples for Number Formatting

In your template, use format strings:

```text
Amount: <<[invoice.Amount]:"C">>
Percentage: <<[invoice.Percentage]:"P">>
Quantity: <<[invoice.Quantity]:"N0">>
```

Common numeric format strings:
- `"C"` - Currency (e.g., $1,500.75)
- `"N"` or `"N2"` - Number with decimals (e.g., 1,500.75)
- `"F"` or `"F2"` - Fixed-point (e.g., 1500.75)
- `"P"` - Percentage (e.g., 15.00%)
- `"D"` - Decimal (for integers)

The currency symbol and the separators come from the culture of the process: the examples above are what en-US writes.

## Format Dates and Times

Format date-time values. A date format needs a `datetime` or a `date` in the data; a date kept as a string is written unchanged.

{{< tabs "example2" >}}
{{< tab "Python" >}}
```python
from datetime import datetime

from groupdocs.assembly import DataSourceInfo, DocumentAssembler

report = {
    "CreatedDate": datetime(2015, 1, 15, 14, 30, 0),
    "DueDate": datetime(2015, 2, 15),
}

assembler = DocumentAssembler()
assembler.assemble_document("report-dates.docx", "report-dates-report.docx",
                            DataSourceInfo(report, "report"))

print("Dates formatted successfully.")
```
{{< /tab >}}
{{< tab "report-dates.docx" >}}
{{< tab-text >}}
The following sample file is used in this example: [report-dates.docx](/assembly/python-net/_sample_files/developer-guide/basic-usage/apply-formatting/report-dates.docx)
{{< /tab-text >}}
{{< /tab >}}
{{< tab "report-dates-report.docx" >}}  
```text
Binary file (DOCX, 7 KB)
```
[Download full output](/assembly/python-net/_output_files/developer-guide/basic-usage/apply-formatting/format_dates_and_times/report-dates-report.docx)
{{< /tab >}}
{{< /tabs >}}

## Template Examples for Date Formatting

```text
Created: <<[report.CreatedDate]:"yyyy-MM-dd HH:mm">>
Due Date: <<[report.DueDate]:"MMMM dd, yyyy">>
```

Common date format strings:
- `"yyyy-MM-dd"` - 2015-01-15
- `"MM/dd/yyyy"` - 01/15/2015
- `"MMMM dd, yyyy"` - January 15, 2015
- `"dd.MM.yyyy"` - 15.01.2015
- `"HH:mm"` - 14:30

## Format Text (Case Transformation)

Transform text case using built-in functions:

{{< tabs "example3" >}}
{{< tab "Python" >}}
```python
from groupdocs.assembly import DataSourceInfo, DocumentAssembler

product = {
    "Name": "harbor blend whole bean coffee",
    "Description": "SMALL-BATCH HOUSE ROAST",
}

assembler = DocumentAssembler()
assembler.assemble_document("product-text-case.docx", "product-text-case-report.docx",
                            DataSourceInfo(product, "product"))

print("Text formatted successfully.")
```
{{< /tab >}}
{{< tab "product-text-case.docx" >}}
{{< tab-text >}}
The following sample file is used in this example: [product-text-case.docx](/assembly/python-net/_sample_files/developer-guide/basic-usage/apply-formatting/product-text-case.docx)
{{< /tab-text >}}
{{< /tab >}}
{{< tab "product-text-case-report.docx" >}}  
```text
Binary file (DOCX, 7 KB)
```
[Download full output](/assembly/python-net/_output_files/developer-guide/basic-usage/apply-formatting/format_text_case_transformation/product-text-case-report.docx)
{{< /tab >}}
{{< /tabs >}}

## Template Examples for Text Formatting

```text
Name: <<[product.Name]:upper>>
Description: <<[product.Description]:lower>>
Title: <<[product.Name]:caps>>
Sentence: <<[product.Name]:firstCap>>
```

Text transformation functions:
- `:upper` - Convert to UPPERCASE
- `:lower` - Convert to lowercase
- `:caps` - Capitalize Each Word
- `:firstCap` - Capitalize first letter only

The function names are case-sensitive: `:Caps` or `:firstcap` fails with "Expression tag is not well-formed".

## Combine Formatting with Calculations

Format calculated values:

{{< tabs "example4" >}}
{{< tab "Python" >}}
```python
from decimal import Decimal

from groupdocs.assembly import DataSourceInfo, DocumentAssembler

order = {"Quantity": 5, "UnitPrice": Decimal("18.40")}

assembler = DocumentAssembler()
assembler.assemble_document("order-line-total.docx", "order-line-total-report.docx",
                            DataSourceInfo(order, "order"))

print("Calculations formatted successfully.")
```
{{< /tab >}}
{{< tab "order-line-total.docx" >}}
{{< tab-text >}}
The following sample file is used in this example: [order-line-total.docx](/assembly/python-net/_sample_files/developer-guide/basic-usage/apply-formatting/order-line-total.docx)
{{< /tab-text >}}
{{< /tab >}}
{{< tab "order-line-total-report.docx" >}}  
```text
Binary file (DOCX, 7 KB)
```
[Download full output](/assembly/python-net/_output_files/developer-guide/basic-usage/apply-formatting/combine_formatting_with_calculations/order-line-total-report.docx)
{{< /tab >}}
{{< /tabs >}}

Template:

```text
Quantity: <<[order.Quantity]>>
Unit Price: <<[order.UnitPrice]:"C">>
Total: <<[order.Quantity * order.UnitPrice]:"C">>
```

## Custom Numeric Formats

Use custom format strings for specific requirements:

{{< tabs "example5" >}}
{{< tab "Python" >}}
```python
from groupdocs.assembly import DataSourceInfo, DocumentAssembler

data = {
    "Phone": 5550142811,
    "Code": 42,
    "Rate": 0.1234,
}

assembler = DocumentAssembler()
assembler.assemble_document("custom-number-formats.docx", "custom-number-formats-report.docx",
                            DataSourceInfo(data, "data"))

print("Custom formats applied successfully.")
```
{{< /tab >}}
{{< tab "custom-number-formats.docx" >}}
{{< tab-text >}}
The following sample file is used in this example: [custom-number-formats.docx](/assembly/python-net/_sample_files/developer-guide/basic-usage/apply-formatting/custom-number-formats.docx)
{{< /tab-text >}}
{{< /tab >}}
{{< tab "custom-number-formats-report.docx" >}}  
```text
Binary file (DOCX, 7 KB)
```
[Download full output](/assembly/python-net/_output_files/developer-guide/basic-usage/apply-formatting/custom_numeric_formats/custom-number-formats-report.docx)
{{< /tab >}}
{{< /tabs >}}

Template with custom formats:

```text
Phone: <<[data.Phone]:"(###) ###-####">>
Code: <<[data.Code]:"000">>
Rate: <<[data.Rate]:"0.00%">>
```

A digit placeholder format such as `"(###) ###-####"` needs a number: keep the phone number an `int` in the data, not a string.

## Formatting in Different Document Types

Formatting works consistently across document types:

{{< tabs "example6" >}}
{{< tab "Python" >}}
```python
from datetime import datetime
from decimal import Decimal

from groupdocs.assembly import DataSourceInfo, DocumentAssembler

invoice = {
    "Amount": Decimal("1500.75"),
    "CreatedDate": datetime(2015, 1, 15, 14, 30, 0),
}

assembler = DocumentAssembler()
assembler.assemble_document("invoice-formatting.xlsx", "invoice-formatting-report.xlsx",
                            DataSourceInfo(invoice, "invoice"))

print("Formatting applied in spreadsheet successfully.")
```
{{< /tab >}}
{{< tab "invoice-formatting.xlsx" >}}
{{< tab-text >}}
The following sample file is used in this example: [invoice-formatting.xlsx](/assembly/python-net/_sample_files/developer-guide/basic-usage/apply-formatting/invoice-formatting.xlsx)
{{< /tab-text >}}
{{< /tab >}}
{{< tab "invoice-formatting-report.xlsx" >}}  
```text
Binary file (XLSX, 7 KB)
```
[Download full output](/assembly/python-net/_output_files/developer-guide/basic-usage/apply-formatting/formatting_in_different_document_types/invoice-formatting-report.xlsx)
{{< /tab >}}
{{< /tabs >}}

The spreadsheet template holds the same tags in its cells:

| Amount | Created |
|--------|---------|
| `<<[invoice.Amount]:"C">>` | `<<[invoice.CreatedDate]:"yyyy-MM-dd">>` |

{{< alert style="warning" >}}
Format strings and text functions are case-sensitive. Use uppercase letters for standard format specifiers (C, N, F, P) and follow .NET formatting conventions exactly.
{{< /alert >}}

### Advanced Usage Topics

To learn more about custom format providers, culture-specific formatting, and advanced formatting scenarios, please refer to the [advanced usage section]({{< ref "assembly/python-net/developer-guide/advanced-usage/_index.md" >}}).

## More resources

### GitHub Examples

You may easily run the code above and see the feature in action in our GitHub examples:

* [GroupDocs.Assembly for .NET examples, plugins, and showcase](https://github.com/groupdocs-assembly/GroupDocs.Assembly-for-.NET)
* [GroupDocs.Assembly for Java examples, plugins, and showcase](https://github.com/groupdocs-assembly/GroupDocs.Assembly-for-Java)
* [GroupDocs.Assembly for Python via .NET examples, plugins, and showcase](https://github.com/groupdocs-assembly/GroupDocs.Assembly-for-Python-via-.NET)

### Free Online Apps

Along with the full-featured library, we provide simple but powerful free online apps.

To assemble documents from templates and data sources, you can use the online apps from the **[GroupDocs.Assembly App Product Family](https://products.groupdocs.app/assembly/family)**.
