---
id: assembly-basic-usage-aggregates
url: assembly/python-net/basic-usage-aggregates
linktitle: Use Simple Aggregates
title: Use Simple Aggregates (Sum, Count, Average)
weight: 24
description: "Calculate sums, counts, averages, minimums and maximums of Python lists in templates with LINQ aggregate methods, using GroupDocs.Assembly for Python via .NET."
keywords: aggregates, sum, count, average, min, max, totals, calculations, aggregate functions, LINQ aggregates, Python list, Python
productName: GroupDocs.Assembly for Python via .NET
hideChildren: False
---

## Overview

GroupDocs.Assembly for Python via .NET supports LINQ-based aggregate functions that allow you to calculate sums, counts, averages, and other aggregate values directly in templates. These functions work with collections and enable you to display totals, summaries, and statistical information in your documents.

The main aggregate functions are:
- `Sum()` - calculate sum of numeric values
- `Count()` - count number of items
- `Average()` - calculate average of numeric values
- `Min()` - find minimum value
- `Max()` - find maximum value

Here are the steps to use aggregates:

* Create a template with aggregate expressions
* Use LINQ aggregate methods on collections
* Reference aggregate results in your template
* Assemble the document with your data

{{< alert style="info" >}}
Aggregate functions use LINQ syntax and work with any collection the template sees: a Python list, or the items of a JSON, XML or CSV data source. Keep money in `Decimal` values: their sums and averages keep exact cents.
{{< /alert >}}

## Calculate Sum

Calculate the sum of values in a collection:

{{< tabs "example1" >}}
{{< tab "Python" >}}
```python
from decimal import Decimal

from groupdocs.assembly import DataSourceInfo, DocumentAssembler

items = [
    {"ProductName": "Harbor Blend whole bean coffee", "Price": Decimal("18.40"), "Quantity": 1},
    {"ProductName": "Oat and honey biscuits", "Price": Decimal("3.20"), "Quantity": 2},
    {"ProductName": "Chestnut honey", "Price": Decimal("7.80"), "Quantity": 1},
]

assembler = DocumentAssembler()
assembler.assemble_document("aggregate-sum.docx", "aggregate-sum-report.docx",
                            DataSourceInfo(items, "items"))

print("Sum calculated successfully.")
```
{{< /tab >}}
{{< tab "aggregate-sum.docx" >}}
{{< tab-text >}}
The following sample file is used in this example: [aggregate-sum.docx](/assembly/python-net/_sample_files/developer-guide/basic-usage/use-aggregates/aggregate-sum.docx)
{{< /tab-text >}}
{{< /tab >}}
{{< tab "aggregate-sum-report.docx" >}}  
```text
Binary file (DOCX, 7 KB)
```
[Download full output](/assembly/python-net/_output_files/developer-guide/basic-usage/use-aggregates/calculate_sum/aggregate-sum-report.docx)
{{< /tab >}}
{{< /tabs >}}

## Template Example for Sum

In your template (aggregate-sum.docx):

```text
Items:
<<foreach [in items]>><<[ProductName]>> - <<[Price]:"C">> x <<[Quantity]>>
<</foreach>>
Total: <<[items.Sum(i => i.Price * i.Quantity)]:"C">>
```

## Calculate Count

Count the number of items in a collection:

{{< tabs "example2" >}}
{{< tab "Python" >}}
```python
from groupdocs.assembly import DataSourceInfo, DocumentAssembler

products = [
    "Harbor Blend whole bean coffee",
    "Aged harbour cheddar",
    "Cold-pressed olive oil",
    "Smoked sea salt",
]

assembler = DocumentAssembler()
assembler.assemble_document("aggregate-count.docx", "aggregate-count-report.docx",
                            DataSourceInfo(products, "products"))

print("Count calculated successfully.")
```
{{< /tab >}}
{{< tab "aggregate-count.docx" >}}
{{< tab-text >}}
The following sample file is used in this example: [aggregate-count.docx](/assembly/python-net/_sample_files/developer-guide/basic-usage/use-aggregates/aggregate-count.docx)
{{< /tab-text >}}
{{< /tab >}}
{{< tab "aggregate-count-report.docx" >}}  
```text
Binary file (DOCX, 7 KB)
```
[Download full output](/assembly/python-net/_output_files/developer-guide/basic-usage/use-aggregates/calculate_count/aggregate-count-report.docx)
{{< /tab >}}
{{< /tabs >}}

Template:

```text
Products:
<<foreach [p in products]>>- <<[p]>>
<</foreach>>
Total Products: <<[products.Count()]>>
```

The products are strings, so the data band names its iteration variable (`p`) and outputs it with `<<[p]>>`.

## Calculate Average

Calculate the average of numeric values:

{{< tabs "example3" >}}
{{< tab "Python" >}}
```python
from decimal import Decimal

from groupdocs.assembly import DataSourceInfo, DocumentAssembler

sales = [
    {"Amount": Decimal("1000.00")},
    {"Amount": Decimal("1500.00")},
    {"Amount": Decimal("800.00")},
    {"Amount": Decimal("1200.00")},
]

assembler = DocumentAssembler()
assembler.assemble_document("aggregate-average.docx", "aggregate-average-report.docx",
                            DataSourceInfo(sales, "sales"))

print("Average calculated successfully.")
```
{{< /tab >}}
{{< tab "aggregate-average.docx" >}}
{{< tab-text >}}
The following sample file is used in this example: [aggregate-average.docx](/assembly/python-net/_sample_files/developer-guide/basic-usage/use-aggregates/aggregate-average.docx)
{{< /tab-text >}}
{{< /tab >}}
{{< tab "aggregate-average-report.docx" >}}  
```text
Binary file (DOCX, 7 KB)
```
[Download full output](/assembly/python-net/_output_files/developer-guide/basic-usage/use-aggregates/calculate_average/aggregate-average-report.docx)
{{< /tab >}}
{{< /tabs >}}

Template:

```text
Sales:
<<foreach [in sales]>><<[Amount]:"C">>
<</foreach>>
Average Sale: <<[sales.Average(s => s.Amount)]:"C">>
```

## Calculate Min and Max

Find minimum and maximum values:

{{< tabs "example4" >}}
{{< tab "Python" >}}
```python
from decimal import Decimal

from groupdocs.assembly import DataSourceInfo, DocumentAssembler

sales = [
    {"Amount": Decimal("1000.00")},
    {"Amount": Decimal("1500.00")},
    {"Amount": Decimal("800.00")},
]

assembler = DocumentAssembler()
assembler.assemble_document("aggregate-min-max.docx", "aggregate-min-max-report.docx",
                            DataSourceInfo(sales, "sales"))

print("Min and max calculated successfully.")
```
{{< /tab >}}
{{< tab "aggregate-min-max.docx" >}}
{{< tab-text >}}
The following sample file is used in this example: [aggregate-min-max.docx](/assembly/python-net/_sample_files/developer-guide/basic-usage/use-aggregates/aggregate-min-max.docx)
{{< /tab-text >}}
{{< /tab >}}
{{< tab "aggregate-min-max-report.docx" >}}  
```text
Binary file (DOCX, 7 KB)
```
[Download full output](/assembly/python-net/_output_files/developer-guide/basic-usage/use-aggregates/calculate_min_and_max/aggregate-min-max-report.docx)
{{< /tab >}}
{{< /tabs >}}

Template:

```text
Minimum Sale: <<[sales.Min(s => s.Amount)]:"C">>
Maximum Sale: <<[sales.Max(s => s.Amount)]:"C">>
```

## Multiple Aggregates

Use multiple aggregates in the same template:

{{< tabs "example5" >}}
{{< tab "Python" >}}
```python
from decimal import Decimal

from groupdocs.assembly import DataSourceInfo, DocumentAssembler

items = [
    {"ProductName": "Harbor Blend whole bean coffee", "Price": Decimal("18.40"), "Quantity": 1},
    {"ProductName": "Oat and honey biscuits", "Price": Decimal("3.20"), "Quantity": 2},
    {"ProductName": "Chestnut honey", "Price": Decimal("7.80"), "Quantity": 1},
]

assembler = DocumentAssembler()
assembler.assemble_document("aggregate-summary.docx", "aggregate-summary-report.docx",
                            DataSourceInfo(items, "items"))

print("Multiple aggregates calculated successfully.")
```
{{< /tab >}}
{{< tab "aggregate-summary.docx" >}}
{{< tab-text >}}
The following sample file is used in this example: [aggregate-summary.docx](/assembly/python-net/_sample_files/developer-guide/basic-usage/use-aggregates/aggregate-summary.docx)
{{< /tab-text >}}
{{< /tab >}}
{{< tab "aggregate-summary-report.docx" >}}  
```text
Binary file (DOCX, 7 KB)
```
[Download full output](/assembly/python-net/_output_files/developer-guide/basic-usage/use-aggregates/multiple_aggregates/aggregate-summary-report.docx)
{{< /tab >}}
{{< /tabs >}}

Template:

```text
Items:
<<foreach [in items]>><<[ProductName]>> - <<[Price]:"C">> x <<[Quantity]>>
<</foreach>>
Summary:
Total Items: <<[items.Count()]>>
Total Quantity: <<[items.Sum(i => i.Quantity)]>>
Total Amount: <<[items.Sum(i => i.Price * i.Quantity)]:"C">>
Average Price: <<[items.Average(i => i.Price)]:"C">>
```

## Aggregates with Conditions

Use aggregates with filtered data:

{{< tabs "example6" >}}
{{< tab "Python" >}}
```python
from decimal import Decimal

from groupdocs.assembly import DataSourceInfo, DocumentAssembler

items = [
    {"ProductName": "Harbor Blend whole bean coffee", "Price": Decimal("18.40"), "Quantity": 1},
    {"ProductName": "Oat and honey biscuits", "Price": Decimal("3.20"), "Quantity": 2},
    {"ProductName": "Lighthouse Espresso beans", "Price": Decimal("21.75"), "Quantity": 1},
]

assembler = DocumentAssembler()
assembler.assemble_document("aggregate-filtered.docx", "aggregate-filtered-report.docx",
                            DataSourceInfo(items, "items"))

print("Conditional aggregates calculated successfully.")
```
{{< /tab >}}
{{< tab "aggregate-filtered.docx" >}}
{{< tab-text >}}
The following sample file is used in this example: [aggregate-filtered.docx](/assembly/python-net/_sample_files/developer-guide/basic-usage/use-aggregates/aggregate-filtered.docx)
{{< /tab-text >}}
{{< /tab >}}
{{< tab "aggregate-filtered-report.docx" >}}  
```text
Binary file (DOCX, 7 KB)
```
[Download full output](/assembly/python-net/_output_files/developer-guide/basic-usage/use-aggregates/aggregates_with_conditions/aggregate-filtered-report.docx)
{{< /tab >}}
{{< /tabs >}}

Template:

```text
High-value items (Price > 15):
<<foreach [in items.Where(i => i.Price > 15)]>><<[ProductName]>> - <<[Price]:"C">>
<</foreach>>
Total High-value: <<[items.Where(i => i.Price > 15).Sum(i => i.Price)]:"C">>
```

## Aggregates in Master-Detail Reports

Calculate aggregates for detail records within master records:

{{< tabs "example7" >}}
{{< tab "Python" >}}
```python
from decimal import Decimal

from groupdocs.assembly import DataSourceInfo, DocumentAssembler

orders = [
    {
        "OrderId": 1001,
        "Items": [
            {"ProductName": "Harbor Blend whole bean coffee", "Price": Decimal("18.40"), "Quantity": 1},
            {"ProductName": "Oat and honey biscuits", "Price": Decimal("3.20"), "Quantity": 2},
        ],
    },
]

assembler = DocumentAssembler()
assembler.assemble_document("aggregate-master-detail.docx", "aggregate-master-detail-report.docx",
                            DataSourceInfo(orders, "orders"))

print("Master-detail aggregates calculated successfully.")
```
{{< /tab >}}
{{< tab "aggregate-master-detail.docx" >}}
{{< tab-text >}}
The following sample file is used in this example: [aggregate-master-detail.docx](/assembly/python-net/_sample_files/developer-guide/basic-usage/use-aggregates/aggregate-master-detail.docx)
{{< /tab-text >}}
{{< /tab >}}
{{< tab "aggregate-master-detail-report.docx" >}}  
```text
Binary file (DOCX, 7 KB)
```
[Download full output](/assembly/python-net/_output_files/developer-guide/basic-usage/use-aggregates/aggregates_in_master_detail_reports/aggregate-master-detail-report.docx)
{{< /tab >}}
{{< /tabs >}}

Template:

```text
<<foreach [in orders]>>Order #<<[OrderId]>>
Items:
<<foreach [in Items]>>  <<[ProductName]>> - <<[Price]:"C">> x <<[Quantity]>>
<</foreach>>
Order Total: <<[Items.Sum(i => i.Price * i.Quantity)]:"C">>

<</foreach>>
```

{{< alert style="warning" >}}
Aggregate functions require collections. Ensure your data source is a collection (a Python list, or the items of a JSON, XML or CSV data source) when using aggregates.
{{< /alert >}}

### Advanced Usage Topics

To learn more about grouping, filtering with aggregates, custom aggregate functions, and performance optimization, please refer to the [advanced usage section]({{< ref "assembly/python-net/developer-guide/advanced-usage/_index.md" >}}).

## More resources

### GitHub Examples

You may easily run the code above and see the feature in action in our GitHub examples:

* [GroupDocs.Assembly for .NET examples, plugins, and showcase](https://github.com/groupdocs-assembly/GroupDocs.Assembly-for-.NET)
* [GroupDocs.Assembly for Java examples, plugins, and showcase](https://github.com/groupdocs-assembly/GroupDocs.Assembly-for-Java)
* [GroupDocs.Assembly for Python via .NET examples, plugins, and showcase](https://github.com/groupdocs-assembly/GroupDocs.Assembly-for-Python-via-.NET)

### Free Online Apps

Along with the full-featured library, we provide simple but powerful free online apps.

To assemble documents from templates and data sources, you can use the online apps from the **[GroupDocs.Assembly App Product Family](https://products.groupdocs.app/assembly/family)**.
