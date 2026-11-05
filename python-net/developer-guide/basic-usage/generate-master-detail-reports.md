---
id: assembly-basic-usage-master-detail
url: assembly/python-net/basic-usage-master-detail
linktitle: Generate Master-Detail Reports
title: Generate Master-Detail Reports
weight: 18
description: "Create parent-child reports from nested Python dicts and lists with nested data bands, in paragraphs and in tables, using GroupDocs.Assembly for Python via .NET."
keywords: master detail, parent child, nested foreach, hierarchical data, orders and items, generate master detail, nested dicts, Python
productName: GroupDocs.Assembly for Python via .NET
hideChildren: False
---

## Overview

Master-detail reports display hierarchical data where each master record (parent) has associated detail records (children). GroupDocs.Assembly for Python via .NET supports master-detail reports through nested foreach data bands, allowing you to display parent records with their related child records.

The main classes involved are:
- [DocumentAssembler](https://reference.groupdocs.com/assembly/python-net/groupdocs.assembly/documentassembler/) - assembles documents
- [DataSourceInfo](https://reference.groupdocs.com/assembly/python-net/groupdocs.assembly/datasourceinfo/) - wraps data sources

Here are the steps to generate master-detail reports:

* Define data structures with parent-child relationships
* Create a template with nested foreach data bands
* Outer foreach iterates over master records
* Inner foreach iterates over detail records for each master
* Assemble the document with your hierarchical data

{{< alert style="info" >}}
Nested foreach data bands allow you to create complex hierarchical reports. The outer band processes master records, while inner bands process related detail records.
{{< /alert >}}

## Define Master-Detail Data Structure

In Python, no classes are needed: a master record is a dict, and one of its keys holds the list of its detail records, each a dict too. Every order below has an `Items` list:

```python
order = {
    "OrderId": 1001,
    "OrderDate": datetime(2015, 1, 14),
    "CustomerName": "Quayside Bistro",
    "Items": [
        {"ProductName": "Harbor Blend whole bean coffee", "Quantity": 2, "Price": Decimal("18.40")},
    ],
}
```

The order date is a `datetime`, so the template can format it; the prices are `Decimal`, so sums keep their cents.

## Generate Master-Detail Report

Create a master-detail report from hierarchical data:

{{< tabs "example1" >}}
{{< tab "Python" >}}
```python
from datetime import datetime
from decimal import Decimal

from groupdocs.assembly import DataSourceInfo, DocumentAssembler

# Create sample data with master-detail relationship
orders = [
    {
        "OrderId": 1001,
        "OrderDate": datetime(2015, 1, 14),
        "CustomerName": "Quayside Bistro",
        "Items": [
            {"ProductName": "Harbor Blend whole bean coffee", "Quantity": 2, "Price": Decimal("18.40")},
            {"ProductName": "Oat and honey biscuits", "Quantity": 10, "Price": Decimal("3.20")},
        ],
    },
    {
        "OrderId": 1002,
        "OrderDate": datetime(2015, 1, 16),
        "CustomerName": "Lantern Street Café",
        "Items": [
            {"ProductName": "Lighthouse Espresso beans", "Quantity": 1, "Price": Decimal("21.75")},
        ],
    },
]

# Assemble document
assembler = DocumentAssembler()
assembler.assemble_document("order-details.docx", "order-details-report.docx",
                            DataSourceInfo(orders, "orders"))

print("Master-detail report generated successfully.")
```
{{< /tab >}}
{{< tab "order-details.docx" >}}
{{< tab-text >}}
The following sample file is used in this example: [order-details.docx](/assembly/python-net/_sample_files/developer-guide/basic-usage/generate-master-detail-reports/order-details.docx)
{{< /tab-text >}}
{{< /tab >}}
{{< tab "order-details-report.docx" >}}  
```text
Binary file (DOCX, 7 KB)
```
[Download full output](/assembly/python-net/_output_files/developer-guide/basic-usage/generate-master-detail-reports/generate_master_detail_report/order-details-report.docx)
{{< /tab >}}
{{< /tabs >}}

## Template Structure for Master-Detail

In your template (order-details.docx), use nested foreach data bands:

```text
<<foreach [in orders]>>Order #<<[OrderId]>>
Date: <<[OrderDate]:"yyyy-MM-dd">>
Customer: <<[CustomerName]>>

Items:
<<foreach [in Items]>>  - <<[ProductName]>> (Qty: <<[Quantity]>>, Price: <<[Price]:"C">>)
<</foreach>>
Total: <<[Items.Sum(i => i.Price * i.Quantity)]:"C">>

<</foreach>>
```

Each band opens in the first paragraph it repeats and closes at the start of the paragraph after its last one. After assembly, you'll get:

```text
Order #1001
Date: 2015-01-14
Customer: Quayside Bistro

Items:
  - Harbor Blend whole bean coffee (Qty: 2, Price: $18.40)
  - Oat and honey biscuits (Qty: 10, Price: $3.20)

Total: $68.80

Order #1002
Date: 2015-01-16
Customer: Lantern Street Café

Items:
  - Lighthouse Espresso beans (Qty: 1, Price: $21.75)

Total: $21.75
```

## Master-Detail in Tables

You can also create master-detail reports in table format:

{{< tabs "example2" >}}
{{< tab "Python" >}}
```python
from decimal import Decimal

from groupdocs.assembly import DataSourceInfo, DocumentAssembler

orders = [
    {
        "OrderId": 1001,
        "CustomerName": "Quayside Bistro",
        "Items": [
            {"ProductName": "Harbor Blend whole bean coffee", "Quantity": 2, "Price": Decimal("18.40")},
            {"ProductName": "Oat and honey biscuits", "Quantity": 10, "Price": Decimal("3.20")},
        ],
    },
]

assembler = DocumentAssembler()
assembler.assemble_document("order-items-table.docx", "order-items-table-report.docx",
                            DataSourceInfo(orders, "orders"))

print("Master-detail table generated successfully.")
```
{{< /tab >}}
{{< tab "order-items-table.docx" >}}
{{< tab-text >}}
The following sample file is used in this example: [order-items-table.docx](/assembly/python-net/_sample_files/developer-guide/basic-usage/generate-master-detail-reports/order-items-table.docx)
{{< /tab-text >}}
{{< /tab >}}
{{< tab "order-items-table-report.docx" >}}  
```text
Binary file (DOCX, 8 KB)
```
[Download full output](/assembly/python-net/_output_files/developer-guide/basic-usage/generate-master-detail-reports/master_detail_in_tables/order-items-table-report.docx)
{{< /tab >}}
{{< /tabs >}}

Template table structure:

| Order ID | Customer | Product | Quantity | Price |
|----------|----------|---------|----------|-------|
| `<<foreach [in orders]>><<[OrderId]>>` | `<<[CustomerName]>>` | | | |
| `<<foreach [in Items]>>` | | `<<[ProductName]>>` | `<<[Quantity]>>` | `<<[Price]:"C">><</foreach>><</foreach>>` |

The outer band spans both rows: it opens in the first cell of the order row and closes in the last cell of the item row. The inner band is the item row alone, so the table gets one order row followed by one row per item.

## Using Aggregates in Master-Detail

Calculate totals and aggregates for each master record:

{{< tabs "example3" >}}
{{< tab "Python" >}}
```python
from decimal import Decimal

from groupdocs.assembly import DataSourceInfo, DocumentAssembler

orders = [
    {
        "OrderId": 1001,
        "CustomerName": "Quayside Bistro",
        "Items": [
            {"ProductName": "Harbor Blend whole bean coffee", "Quantity": 2, "Price": Decimal("18.40")},
            {"ProductName": "Oat and honey biscuits", "Quantity": 10, "Price": Decimal("3.20")},
        ],
    },
]

assembler = DocumentAssembler()
assembler.assemble_document("order-items-subtotals.docx", "order-items-subtotals-report.docx",
                            DataSourceInfo(orders, "orders"))

print("Master-detail report with aggregates generated successfully.")
```
{{< /tab >}}
{{< tab "order-items-subtotals.docx" >}}
{{< tab-text >}}
The following sample file is used in this example: [order-items-subtotals.docx](/assembly/python-net/_sample_files/developer-guide/basic-usage/generate-master-detail-reports/order-items-subtotals.docx)
{{< /tab-text >}}
{{< /tab >}}
{{< tab "order-items-subtotals-report.docx" >}}  
```text
Binary file (DOCX, 7 KB)
```
[Download full output](/assembly/python-net/_output_files/developer-guide/basic-usage/generate-master-detail-reports/using_aggregates_in_master_detail/order-items-subtotals-report.docx)
{{< /tab >}}
{{< /tabs >}}

Template with aggregates:

```text
<<foreach [in orders]>>Order #<<[OrderId]>> - <<[CustomerName]>>

Items:
<<foreach [in Items]>>  <<[ProductName]>> - <<[Quantity]>> x <<[Price]:"C">> = <<[Quantity * Price]:"C">>
<</foreach>>
Subtotal: <<[Items.Sum(i => i.Price * i.Quantity)]:"C">>
Item Count: <<[Items.Count()]>>

<</foreach>>
```

{{< alert style="warning" >}}
When using nested foreach data bands, ensure proper closing tags. Each opening `<<foreach>>` must have a corresponding closing `<</foreach>>`, and an inner band must close before the band around it.
{{< /alert >}}

### Advanced Usage Topics

To learn more about complex hierarchical structures, multiple levels of nesting, and advanced master-detail patterns, please refer to the [advanced usage section]({{< ref "assembly/python-net/developer-guide/advanced-usage/_index.md" >}}).

## More resources

### GitHub Examples

You may easily run the code above and see the feature in action in our GitHub examples:

* [GroupDocs.Assembly for .NET examples, plugins, and showcase](https://github.com/groupdocs-assembly/GroupDocs.Assembly-for-.NET)
* [GroupDocs.Assembly for Java examples, plugins, and showcase](https://github.com/groupdocs-assembly/GroupDocs.Assembly-for-Java)
* [GroupDocs.Assembly for Python via .NET examples, plugins, and showcase](https://github.com/groupdocs-assembly/GroupDocs.Assembly-for-Python-via-.NET)

### Free Online Apps

Along with the full-featured library, we provide simple but powerful free online apps.

To assemble documents from templates and data sources, you can use the online apps from the **[GroupDocs.Assembly App Product Family](https://products.groupdocs.app/assembly/family)**.
