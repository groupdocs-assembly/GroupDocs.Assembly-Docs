---
id: template-syntax-part-2-of-2
url: assembly/python-net/template-syntax-part-2-of-2
title: Template Syntax - Part 2 of 2
weight: 2
description: "GroupDocs.Assembly template syntax, part 2: expression tags and format strings, data bands over Python lists, cell merging, numbered lists, table-row data bands, charts and the enumeration extension methods."
keywords: template syntax, expression tag, foreach, data band, table-row data band, cellMerge, restartNum, enumeration extension methods, Python, GroupDocs.Assembly
productName: GroupDocs.Assembly for Python via .NET
hideChildren: False
---
{{< alert style="info" >}}This article is the second part of the Template Syntax series of articles. For first part, please visit [Template Syntax - Part 1 of 2]({{< ref "assembly/python-net/developer-guide/basic-usage/working-with-groupdocs.assembly-engine/template-syntax-part-1-of-2.md" >}}).{{< /alert >}}

## Outputting Expression Results

You can output expression results to your reports using expression tags. An expression tag denotes a placeholder for an expression result within a template. While building a report, the corresponding expression is evaluated, and this placeholder is replaced with the formatted result of the expression.

An expression tag has no name and consists of the following elements:

*   An expression enclosed by brackets
*   An optional format string enclosed by double quotes and preceded by the ":" character
*   An optional `html` switch

```text
<<[expression]:"format" -html>>
```

If `html` switch is not present, the result of the corresponding expression is written to a document as a plain text at runtime. Font attributes are derived from the first character of the corresponding tag in this case.

If `html` switch is present, the expression result is considered to be a HTML block and is written as such. This feature is useful, when you need to format text parts of an expression result in different ways. For example, the following tag is replaced with a content like "**Bold** and *italic* text" at runtime.

```text
<<["<b>Bold</b> and <i>italic</i> text"] -html>>
```

To format a numeric or date-time expression result, you can specify a format string as an element of the corresponding expression tag. Such format strings are the .NET ones, the same as the ones that you pass to [`IFormattable.ToString`](http://msdn.microsoft.com/en-us/library/system.iformattable.tostring(v=vs.110).aspx) method implementors, not Python's `strftime` or `format()` codes. That is, for example, given that `d` is a Python `datetime`, you can use the following template to format the value using the "yyyy.MM.dd" pattern (Python's `"%Y.%m.%d"`).

```text
<<[d]:"yyyy.MM.dd">>
```

Likewise, a number takes .NET numeric format strings, such as `"0.00"` or `"N2"`.

## Outputting Sequential Data

You can output a sequence of elements of the same type to your report using a data band. A `data band` has a body that represents a template for a single element of such a sequence. While building a report, sequence elements are enumerated, and the following procedure takes place for each of the elements:

1.  The data band body is duplicated and appended to the report.
2.  The appended data band body is populated with the element's data.

**Note --** A data band body can contain nested data bands.

A data band body is defined between the corresponding opening and closing `foreach` tags within a template as follows.

```text
<<foreach [sequence_expression]>>
data_band_body
<</foreach>>
```

You can reference an element of the corresponding sequence in template expressions within a data band body using an iteration variable. At runtime, an iteration variable represents a sequence element for which an iteration is currently being performed. You can declare an iteration variable within the corresponding opening `foreach` tag.

An opening `foreach` tag defines a `foreach` statement enclosed by brackets. The following table describes elements of this statement.

| Element | Optional? | Remarks |
| --- | --- | --- |
| **Iteration Variable Type** | Yes | You can specify the type of an iteration variable explicitly. This type must be known by the engine (see [Setting up Known External Types]({{< ref "assembly/python-net/developer-guide/basic-usage/working-with-groupdocs.assembly-engine/groupdocs.assembly-engine-apis.md#setting-up-known-external-types" >}}) for more information). If you do not specify the type explicitly, it is determined implicitly by the engine depending on the type of the corresponding sequence. The type of an item made from a Python dict has no name you can write, so leave the type out for such items. |
| **Iteration Variable Name** | Yes | You can specify the name of an iteration variable to use it while accessing the variable's members. The name must be unique within the scope of the corresponding `foreach` tag. If you do not specify the name, you can access the variable's members using the contextual object member access syntax (see [Using Contextual Object Member Access]({{< ref "assembly/python-net/developer-guide/basic-usage/working-with-groupdocs.assembly-engine/template-syntax-part-1-of-2.md#using-contextual-object-member-access" >}}) for more information). |
| **"in" Keyword** | No | |
| **Sequence Expression** | No | A sequence expression must return an [IEnumerable](http://msdn.microsoft.com/en-us/library/system.collections.ienumerable(v=vs.110).aspx) implementor. In Python data, that is a list, a tuple or a set; a `DocumentTable` and the arrays of a `JsonDataSource` are sequences as well. |

The complete syntax of a `foreach` tag (including optional elements) is as follows.

```text
<<foreach [variable_type variable_name in sequence_expression]>>
data_band_body
<</foreach>>
```

### Common Data Bands

A common data band is a data band which body starts and ends within paragraphs that belong to a single story or table cell.

In particular, a common data band can be entirely located within a single paragraph. In this case, while building a report, the band is replaced with contents that are entirely located within the same paragraph as well. The following example illustrates such a scenario. Given that items is a Python list of the strings "item1", "item2", and "item3", you can use the following template to enumerate them with commas in a single paragraph.

```text
The items are: <<foreach [item in items]>><<[item]>>, <</foreach>>and others.
```

In this case, the engine produces a report as follows.

```text
The items are: item1, item2, item3, and others.
```

When the body of a common data band starts and ends within different paragraphs, the engine duplicates on iteration only those paragraph breaks which are located within the body. The following table illustrates the relevant cases.

**Note --** Examples in the table are given with paragraph marks shown as per Microsoft Word® editor.

| Template | Report |
| --- | --- |
| `prefix <<foreach [item in items]>><<[item]>>¶`<br/>`<</foreach>>suffix` | `prefix item1¶`<br/>`item2¶`<br/>`item3¶`<br/>`suffix` |
| `prefix<<foreach [item in items]>>¶`<br/>`<<[item]>><</foreach>> suffix` | `prefix¶`<br/>`item1¶`<br/>`item2¶`<br/>`item3 suffix` |
| `prefix¶`<br/>`<<foreach [item in items]>><<[item]>>¶`<br/>`<</foreach>>suffix` | `prefix¶`<br/>`item1¶`<br/>`item2¶`<br/>`item3¶`<br/>`suffix` |
| `prefix<<foreach [item in items]>>¶`<br/>`<<[item]>><</foreach>>¶`<br/>`suffix` | `prefix¶`<br/>`item1¶`<br/>`item2¶`<br/>`item3¶`<br/>`suffix` |
| `prefix¶`<br/>`<<foreach [item in items]>>¶`<br/>`<<[item]>>¶`<br/>`<</foreach>>¶`<br/>`suffix` | `prefix¶`<br/>`¶`<br/>`item1¶`<br/>`¶`<br/>`item2¶`<br/>`¶`<br/>`item3¶`<br/>`¶`<br/>`suffix` |

While building a report, duplicated paragraph breaks derive common attributes from their template prototypes. In particular, this fact enables you to build numbered or bulleted lists in reports dynamically (see [Numbered Lists](#numbered-lists)).

### Merging Table Cells Dynamically

You can merge table cells with equal textual contents within your reports dynamically using `cellMerge` tags. Syntax of a `cellMerge` tag is defined as follows.

```text
<<cellMerge>>
```

By default, a `cellMerge` tag causes a cell merging operation only in a vertical direction during runtime. However, you can alter this behavior in the following ways:

- To merge cells only in a horizontal direction, use the `horz` switch as follows.
  `<<cellMerge -horz>>`

- To merge cells in both – vertical and horizontal – directions, use the `both` switch as follows.
  `<<cellMerge -both>>`

For two or more successive table cells to be merged dynamically in either direction by the engine, the following requirements must be met:

- Each of the cells must contain a `cellMerge` tag denoting a cell merging operation in the same direction (or directions).
- Each of the cells must not be already merged in another direction. This requirement does not apply when a `both` switch is used.
- The cells must have equal textual contents ignoring leading and trailing whitespaces.

Consider the following template.

| **...** | **...** | **...** |
| ------- | ----------------------------- | ------- |
| **...** | **<<cellMerge>><<[value1]>>** | **...** |
| **...** | **<<cellMerge>><<[value2]>>** | **...** |
| **...** | **...** | **...** |

If `value1` and `value2` have the same value, say "Hello", table cells containing `cellMerge` tags are successfully merged during runtime and a result report looks as follows then.

<table style="font-weight: bold">
	<tbody>
		<tr>
			<td>...</td>
			<td>...</td>
			<td>...</td>
		</tr>
		<tr>
			<td>...</td>
			<td rowspan="2">Hello</td>
			<td>...</td>
		</tr>
		<tr>
			<td>...</td>
			<td>...</td>
		</tr>
		<tr>
			<td>...</td>
			<td>...</td>
			<td>...</td>
		</tr>
	</tbody>
</table>

If `value1` and `value2` have different values, say "Hello" and "World", table cells containing `cellMerge` tags are not merged during runtime and a result report looks as follows then.

| **...** | **...**   | **...** |
| ------- | --------- | ------- |
| **...** | **Hello** | **...** |
| **...** | **World** | **...** |
| **...** | **...**   | **...** |

**Note –** A cellMerge tag can be normally used within a table data band.

You can define an additional restriction on dynamic merging of table cells by providing an expression for a `cellMerge` tag using the following syntax.

```text
<<cellMerge [expression]>>
```

During runtime, expressions defined for `cellMerge` tags are evaluated and dynamic cell merging is discarded for those tags, which expressions return unequal values, even if all other conditions for merging such as equal cell textual contents are met. In particular, this feature is useful when cells corresponding to different data band sequence elements should not be merged as shown in the following example.

Assume that `invoices` is a list of invoices, each a dict with a `Number` and the `Items` it lists, each item a dict with a `Ware`, a `Pack` and a `Quantity`:

```python
invoices = [
    {"Number": 11342, "Items": [
        {"Ware": "Cold-pressed olive oil", "Pack": "Bottle 1.0 L", "Quantity": 30},
        {"Ware": "Cold-pressed olive oil", "Pack": "Bottle 0.5 L", "Quantity": 50},
    ]},
    {"Number": 15385, "Items": [
        {"Ware": "Cold-pressed olive oil", "Pack": "Bottle 1.0 L", "Quantity": 110},
    ]},
]
```

You could use the following template to output information on several invoices in one table.

| **#** | **Ware** | **Pack** | **Quantity** |
| --- | --- | --- | --- |
| **<<foreach [invoice in invoices]>><<foreach [item in invoice.Items]>><<[invoice.Number]>><<cellMerge>>** | **<<[item.Ware]>><<cellMerge>>** | **<<[item.Pack]>>** | **<<[item.Quantity]>><</foreach>><</foreach>>** |

A result document would look as follows then.

<table style="font-weight: bold">
	<tbody>
		<tr>
			<td>#</td>
			<td>Ware</td>
			<td>Pack</td>
			<td>Quantity</td>
		</tr>
		<tr>
			<td rowspan="2">11342</td>
			<td rowspan="3">Cold-pressed olive oil</td>
			<td>Bottle 1.0 L</td>
			<td>30</td>
		</tr>
		<tr>
			<td>Bottle 0.5 L</td>
			<td>50</td>
		</tr>
		<tr>
			<td>15385</td>
			<td>Bottle 1.0 L</td>
			<td>110</td>
		</tr>
	</tbody>
</table>

That is, cells corresponding to the same wares at different invoices would be merged, which is unwanted. To prevent this from happening, you can use the following template instead.

| **#** | **Ware** | **Pack** | **Quantity** |
| --- | --- | --- | --- |
| **<<foreach [invoice in invoices]>><<foreach [item in invoice.Items]>><<[invoice.Number]>><<cellMerge>>** | **<<[item.Ware]>><<cellMerge [invoice.IndexOf()]>>** | **<<[item.Pack]>>** | **<<[item.Quantity]>><</foreach>><</foreach>>** |

Then, a result document looks as follows.

<table style="font-weight: bold">
	<tbody>
		<tr>
			<td>#</td>
			<td>Ware</td>
			<td>Pack</td>
			<td>Quantity</td>
		</tr>
		<tr>
			<td rowspan="2">11342</td>
			<td rowspan="2">Cold-pressed olive oil</td>
			<td>Bottle 1.0 L</td>
			<td>30</td>
		</tr>
		<tr>
			<td>Bottle 0.5 L</td>
			<td>50</td>
		</tr>
		<tr>
			<td>15385</td>
			<td>Cold-pressed olive oil</td>
			<td>Bottle 1.0 L</td>
			<td>110</td>
		</tr>
	</tbody>
</table>

### Numbered Lists

Given the above declaration of items, you can get a report with their numbered list using the following template. "1. " in the template stands for a numbered list label.

```text
1. <<foreach [item in items]>><<[item]>>
<</foreach>>
```

In this case, the engine produces a report as follows.

```text
1. item1
2. item2
3. item3
```

#### Dynamic list numbering restart

This feature is useful when working with a nested numbered list within a data band as shown in the following example.

Assume that `orders` is a list of orders, each a dict with a `ClientName`, a `ClientAddress` and the `Services` ordered, each service a dict with a `Name`:

```python
orders = [
    {"ClientName": "Quayside Bistro", "ClientAddress": "3 Harbour Steps, Port Ellery",
     "Services": [{"Name": "Next-day delivery"}, {"Name": "Menu pairing advice"}]},
    {"ClientName": "Saltmarsh Deli", "ClientAddress": "7 Marsh Lane, Port Ellery",
     "Services": [{"Name": "Next-day delivery"}, {"Name": "Cold-chain storage"}, {"Name": "Shelf restocking"}]},
]
```

You could try to use the following template to output information on several orders in one document.

```text
<<foreach [order in orders]>><<[order.ClientName]>> (<<[order.ClientAddress]>>)
1. <<foreach [service in order.Services]>><<[service.Name]>>
<</foreach>><</foreach>>
```

But then, a result document would look as follows.

```text
Quayside Bistro (3 Harbour Steps, Port Ellery)

   1. Next-day delivery
   2. Menu pairing advice

Saltmarsh Deli (7 Marsh Lane, Port Ellery)

   3. Next-day delivery
   4. Cold-chain storage
   5. Shelf restocking
```

That is, there would be a single numbered list across all orders, which is not applicable for this scenario. However, you can make list numbering to restart for every order by putting a restartNum tag into your template before a corresponding foreach tag as follows.

```text
<<foreach [order in orders]>><<[order.ClientName]>> (<<[order.ClientAddress]>>)
1. <<restartNum>><<foreach [service in order.Services]>><<[service.Name]>>
<</foreach>><</foreach>>
```

{{< alert style="warning" >}}When using with a data band, it is required to put a restartNum tag before a corresponding foreach tag in the same numbered paragraph.{{< /alert >}}

Then, a result document looks as follows.

```text
Quayside Bistro (3 Harbour Steps, Port Ellery)

   1. Next-day delivery
   2. Menu pairing advice

Saltmarsh Deli (7 Marsh Lane, Port Ellery)

   1. Next-day delivery
   2. Cold-chain storage
   3. Shelf restocking
```

{{< alert style="warning" >}}You can use a restartNum tag without a data band to dynamically restart list numbering for a containing paragraph, for example, the tag can be used to restart list numbering for a document inserted dynamically.{{< /alert >}}

### Table-Row Data Bands

A table-row data band is a data band which body occupies single or multiple rows of a single document table. The body of such a band starts at the beginning of the first occupied row and ends at the end of the last occupied row as follows.

| | | |
| --- | --- | --- |
| `<<foreach ...>>` ... | ... | ... |
| ... | ... | ... |
| ... | ... | ... `<</foreach>>` |

The following examples in this section are given using `ds`, a `DocumentTableSet` loaded from `related-tables.xlsx`: the worksheets `MANAGER`, `CLIENT` and `CONTRACT` of Harbor Lane's account managers, their clients and their contracts, related through their ID columns. Each contract row has a parent manager row and a parent client row, so a template reads `c.Manager.Name` for a contract `c`, and `m.Contract` for the contracts of a manager `m`. Table and field names are case-insensitive. Each example loads the tables with the same code:

```python
from groupdocs.assembly.data import DocumentTableOptions, DocumentTableSet


def load_table(args):
    # The first row of every worksheet holds its column names
    options = DocumentTableOptions()
    options.first_row_contains_column_names = True
    args.options = options


ds = DocumentTableSet("related-tables.xlsx", load_table)
ds.relations.add(ds.tables["CLIENT"].columns["ID"], ds.tables["CONTRACT"].columns["CLIENT_ID"])
ds.relations.add(ds.tables["MANAGER"].columns["ID"], ds.tables["CONTRACT"].columns["MANAGER_ID"])
```

The most common use case of a table-row data band is the building of a document table that represents a list of items. You can use a template like the following one to achieve this.

| Client | Manager | Contract Price |
| --- | --- | --- |
| `<<foreach [c in ds.Contract]>><<[c.Client.Name]>>` | `<<[c.Manager.Name]>>` | `<<[c.Price]>><</foreach>>` |
| Total: |  | `<<[ds.Contract.Sum(c => c.Price)]>>` |

{{< tabs "example1" >}}
{{< tab "Python" >}}
```python
from groupdocs.assembly import DataSourceInfo, DocumentAssembler
from groupdocs.assembly.data import DocumentTableOptions, DocumentTableSet


def load_table(args):
    # The first row of every worksheet holds its column names
    options = DocumentTableOptions()
    options.first_row_contains_column_names = True
    args.options = options


ds = DocumentTableSet("related-tables.xlsx", load_table)
ds.relations.add(ds.tables["CLIENT"].columns["ID"], ds.tables["CONTRACT"].columns["CLIENT_ID"])
ds.relations.add(ds.tables["MANAGER"].columns["ID"], ds.tables["CONTRACT"].columns["MANAGER_ID"])

assembler = DocumentAssembler()
assembler.assemble_document("contract-list.docx", "contract-list-report.docx", DataSourceInfo(ds, "ds"))
```
{{< /tab >}}
{{< tab "contract-list.docx" >}}
{{< tab-text >}}
The following sample file is used in this example: [contract-list.docx](/assembly/python-net/_sample_files/developer-guide/basic-usage/working-with-groupdocs.assembly-engine/template-syntax-part-2-of-2/contract-list.docx)
{{< /tab-text >}}
{{< /tab >}}
{{< tab "related-tables.xlsx" >}}
{{< tab-text >}}
The following sample file is used in this example: [related-tables.xlsx](/assembly/python-net/_sample_files/developer-guide/basic-usage/working-with-groupdocs.assembly-engine/template-syntax-part-2-of-2/related-tables.xlsx)
{{< /tab-text >}}
{{< /tab >}}
{{< tab "contract-list-report.docx" >}}  
```text
Binary file (DOCX, 8 KB)
```
[Download full output](/assembly/python-net/_output_files/developer-guide/basic-usage/working-with-groupdocs.assembly-engine/template-syntax-part-2-of-2/table_row_data_bands/contract-list-report.docx)
{{< /tab >}}
{{< /tabs >}}

In this case, the engine produces a report as follows.

| Client | Manager | Contract Price |
| --- | --- | --- |
| Harbourview Hotel | Mei Tanaka | 120000 |
| Quayside Bistro | Mei Tanaka | 75000 |
| Saltmarsh Deli | Mei Tanaka | 35000 |
| Lantern Street Café | Daniel Reyes | 65000 |
| Millbrook Market | Daniel Reyes | 55000 |
| Pier Nine Kitchen | Sofia Marino | 35000 |
| The Copper Kettle | Sofia Marino | 25000 |
| Driftwood Grill | Sofia Marino | 10000 |
| Tidewater Tavern | Sofia Marino | 10000 |
| Total: |  | 430000 |

To populate a document table with a master-detail data, you can use nested table-row data bands like in the following template.

| Manager/Client | Contract Price |
| --- | --- |
| `<<foreach [m in ds.Manager]>><<[m.Name]>>` | `<<[m.Contract.Sum(c => c.Price)]>>` |
| `<<foreach [c in m.Contract]>>- <<[c.Client.Name]>>` | `<<[c.Price]>><</foreach>><</foreach>>` |
| Total: | `<<[ds.Contract.Sum(c => c.Price)]>>` |

{{< tabs "example2" >}}
{{< tab "Python" >}}
```python
from groupdocs.assembly import DataSourceInfo, DocumentAssembler
from groupdocs.assembly.data import DocumentTableOptions, DocumentTableSet


def load_table(args):
    # The first row of every worksheet holds its column names
    options = DocumentTableOptions()
    options.first_row_contains_column_names = True
    args.options = options


ds = DocumentTableSet("related-tables.xlsx", load_table)
ds.relations.add(ds.tables["CLIENT"].columns["ID"], ds.tables["CONTRACT"].columns["CLIENT_ID"])
ds.relations.add(ds.tables["MANAGER"].columns["ID"], ds.tables["CONTRACT"].columns["MANAGER_ID"])

assembler = DocumentAssembler()
assembler.assemble_document("manager-contract-totals.docx", "manager-contract-totals-report.docx", DataSourceInfo(ds, "ds"))
```
{{< /tab >}}
{{< tab "manager-contract-totals.docx" >}}
{{< tab-text >}}
The following sample file is used in this example: [manager-contract-totals.docx](/assembly/python-net/_sample_files/developer-guide/basic-usage/working-with-groupdocs.assembly-engine/template-syntax-part-2-of-2/manager-contract-totals.docx)
{{< /tab-text >}}
{{< /tab >}}
{{< tab "related-tables.xlsx" >}}
{{< tab-text >}}
The following sample file is used in this example: [related-tables.xlsx](/assembly/python-net/_sample_files/developer-guide/basic-usage/working-with-groupdocs.assembly-engine/template-syntax-part-2-of-2/related-tables.xlsx)
{{< /tab-text >}}
{{< /tab >}}
{{< tab "manager-contract-totals-report.docx" >}}  
```text
Binary file (DOCX, 8 KB)
```
[Download full output](/assembly/python-net/_output_files/developer-guide/basic-usage/working-with-groupdocs.assembly-engine/template-syntax-part-2-of-2/table_row_data_bands_2/manager-contract-totals-report.docx)
{{< /tab >}}
{{< /tabs >}}

In this case, the engine produces a report as follows.

| Manager/Client | Contract Price |
| --- | --- |
| Mei Tanaka | 230000 |
| - Harbourview Hotel | 120000 |
| - Quayside Bistro | 75000 |
| - Saltmarsh Deli | 35000 |
| Daniel Reyes | 120000 |
| - Lantern Street Café | 65000 |
| - Millbrook Market | 55000 |
| Sofia Marino | 80000 |
| - Pier Nine Kitchen | 35000 |
| - The Copper Kettle | 25000 |
| - Driftwood Grill | 10000 |
| - Tidewater Tavern | 10000 |
| Total: | 430000 |

You can normally use common data bands nested to table-row data bands as well like in the following template.

| Manager | Clients |
| --- | --- |
| `<<foreach [m in ds.Manager]>><<[m.Name]>>` | `<<foreach [c in m.Contract]>><<[c.IndexOf() != 0 ? ", " : ""]>><<[c.Client.Name]>><</foreach>><</foreach>>` |

{{< tabs "example3" >}}
{{< tab "Python" >}}
```python
from groupdocs.assembly import DataSourceInfo, DocumentAssembler
from groupdocs.assembly.data import DocumentTableOptions, DocumentTableSet


def load_table(args):
    # The first row of every worksheet holds its column names
    options = DocumentTableOptions()
    options.first_row_contains_column_names = True
    args.options = options


ds = DocumentTableSet("related-tables.xlsx", load_table)
ds.relations.add(ds.tables["CLIENT"].columns["ID"], ds.tables["CONTRACT"].columns["CLIENT_ID"])
ds.relations.add(ds.tables["MANAGER"].columns["ID"], ds.tables["CONTRACT"].columns["MANAGER_ID"])

assembler = DocumentAssembler()
assembler.assemble_document("manager-clients.docx", "manager-clients-report.docx", DataSourceInfo(ds, "ds"))
```
{{< /tab >}}
{{< tab "manager-clients.docx" >}}
{{< tab-text >}}
The following sample file is used in this example: [manager-clients.docx](/assembly/python-net/_sample_files/developer-guide/basic-usage/working-with-groupdocs.assembly-engine/template-syntax-part-2-of-2/manager-clients.docx)
{{< /tab-text >}}
{{< /tab >}}
{{< tab "related-tables.xlsx" >}}
{{< tab-text >}}
The following sample file is used in this example: [related-tables.xlsx](/assembly/python-net/_sample_files/developer-guide/basic-usage/working-with-groupdocs.assembly-engine/template-syntax-part-2-of-2/related-tables.xlsx)
{{< /tab-text >}}
{{< /tab >}}
{{< tab "manager-clients-report.docx" >}}  
```text
Binary file (DOCX, 8 KB)
```
[Download full output](/assembly/python-net/_output_files/developer-guide/basic-usage/working-with-groupdocs.assembly-engine/template-syntax-part-2-of-2/table_row_data_bands_3/manager-clients-report.docx)
{{< /tab >}}
{{< /tabs >}}

In this case, the engine produces a report as follows.

| Manager | Clients |
| --- | --- |
| Mei Tanaka | Harbourview Hotel, Quayside Bistro, Saltmarsh Deli |
| Daniel Reyes | Lantern Street Café, Millbrook Market |
| Sofia Marino | Pier Nine Kitchen, The Copper Kettle, Driftwood Grill, Tidewater Tavern |

The same templates work with Python data: given that `ds` is a dict whose `Contract` key holds a list of contract dicts, each with a `Client` dict, a `Manager` dict and a `Price`, and whose `Manager` key holds the managers, each with its `Contract` list, `ds.Contract` and `m.Contract` are lists, and `c.Manager.Name` a member of a nested dict.

### Extension Methods of Iteration Variables

GroupDocs.Assembly Engine provides special extension methods for iteration variables of any type. You can normally use these extension methods in template expressions. The following list describes the extension methods.

*   `IndexOf()`

Returns the zero-based index of a sequence item that is represented by the corresponding iteration variable. You can use this extension method to distinguish sequence items with different indexes and then handle them in different ways. For example, given that `items` is a Python list of the strings "item1", "item2", and "item3", you can use the following template to enumerate them prefixing all of them but the first one with commas.

```text
The items are: <<foreach [
    item in items]>><<[item.IndexOf() != 0
        ? ", "
        : ""]>><<[item]>><</foreach>>.
```

In this case, the engine produces a report as follows.

```text
The items are: item1, item2, item3.
```

*   `NumberOf()`

Returns the one-based index of a sequence item that is represented by the corresponding iteration variable. You can use this extension method to number sequence `items` without involving Microsoft Word® lists. For example, given the previous declaration of items, you can enumerate and number them in a document table using the following template.

| No. | Item |
| --- | --- |
| `<<foreach [item in items]>><<[item.NumberOf()]>>` | `<<[item]>><</foreach>>` |

In this case, the engine produces a report as follows.

| No. | Item |
| --- | --- |
| 1 | item1 |
| 2 | item2 |
| 3 | item3 |

### Charts Representing Sequential Data

GroupDocs.Assembly Engine enables you to use charts to represent your sequential data. To declare a chart that is going to be populated with data dynamically within your template, do the following steps:

1.  Add a chart to your template at the place where you want it to appear in a result document.
2.  Configure the appearance of the chart.
3.  Add required chart series and configure their appearance as well.
4.  Add a title to the chart, if missing.
5.  Add an opening foreach tag to the chart title.
6.  Depending on the type of the chart, add x tags to the chart title or chart series' names as follows.

    ```text
    <<x [x_value_expression]>>
    ```

    * For a scatter or bubble chart, you can go one of the following ways:
        - To use the same x-value expression for all chart series, add a single x tag to the chart title after the corresponding foreach tag.
        - To use different x-value expressions for every chart series, add multiple x tags to chart series' names – one for each chart series. An x-value expression for a scatter or bubble chart must return a numeric value.
    * For a chart of another type, add a single x tag to the chart title after the corresponding foreach tag. In this case, an x-value expression must return a numeric, date, or string value.
7.  For a chart of any type, add y tags to chart series' names as follows.

    ```text
    <<y [y_value_expression]>>
    ```

    An y-value expression must return a numeric value.

8.  For a bubble chart, add size tags to chart series' names as follows.

    ```text
    <<size [bubble_size_expression]>>
    ```

    A bubble-size expression must return a numeric value.

9.  For a chart with dynamic data, you can select which series to include into it dynamically based upon conditions. In particular, this feature is useful when you need to restrict access to sensitive data in chart series for some users of your application. To use the feature, do the following steps:

    * Declare a chart with dynamic data in the usual way
    * For series to be removed from the chart based upon conditions dynamically, define the conditions in names of these series using removeif tags having the following syntax

    ```text
    <<removeif [conditional_expression]>>
    ```

    A conditional expression must return a Boolean value.

**Note:** A closing foreach tag is not used for a chart.

While composing expressions for x, y, and size tags, you can normally reference an iteration variable declared at the corresponding foreach tag in a chart title in the same way as if you intended to output results of expressions within a data band.

**Note:** You can normally use charts with dynamic data within data bands.

During runtime, a chart with a foreach tag in its title is processed by the engine as follows:

1.  A sequence expression declared at the foreach tag is evaluated and iterated.
2.  For every sequence item, expressions declared at x, y, and size tags are evaluated.
3.  Results of these expressions are used to populate corresponding chart series.
4.  All foreach, x, y, and size tags are removed from the chart title and chart series' names.

Consider the following example. Assume that `managers` is a list of managers, each a dict with a `Name` and its `Contract` list, each contract a dict with a `Price`, as `managers.json` holds them. You can represent the total contract prices achieved by managers in a column chart whose title holds `<<foreach [m in managers]>><<x [m.Name]>>` and whose series name holds `<<y [m.Contract.Sum(c => c.Price)]>>`. The chart pages show such templates and their reports: see [Working with Chart Series Coloring]({{< ref "assembly/python-net/developer-guide/advanced-usage/working-with-chart-series-coloring/_index.md" >}}) and [Working with Chart Reports - Filtered Ordered Grouped]({{< ref "assembly/python-net/developer-guide/advanced-usage/working-with-chart-reports-filtered-ordered-grouped/_index.md" >}}).

## Enumeration Extension Methods

### The Enumeration

GroupDocs.Assembly Engine enables you to perform common manipulations on a sequential data through the engine's built-in extension methods for `IEnumerable`, which apply to Python lists as they do to .NET collections. These extension methods mimic some extension methods of [IEnumerable<T>](http://msdn.microsoft.com/en-us/library/9eekhta0(v=vs.110).aspx) providing the same signatures and behavior features. Thus, you can group, sort, and perform other sequential data manipulations in template expressions in a familiar way.

### The Enumeration Extension

Below table describes the built-in extension methods. The following notation conventions are used within the table:

*   `Selector` stands for a lambda function returning a value and taking an enumeration item as its single argument. See [Using Lambda Functions]({{< ref "assembly/python-net/developer-guide/basic-usage/working-with-groupdocs.assembly-engine/template-syntax-part-1-of-2.md#using-lambda-functions" >}}) for more information.
*   `ComparableSelector` stands for `Selector` returning [IComparable](http://msdn.microsoft.com/en-US/library/system.icomparable(v=vs.110).aspx): a string, a number or a date-time value, for instance.
*   `Predicate` stands for `Selector` returning a Boolean value.

Examples in this table are given using `persons` and `otherPersons`, lists of dicts each with a `Name` (`str`), an `Age` (`int`) and `Children` (a list of such dicts). Dicts compare by value: `Distinct`, `GroupBy` and `Contains` treat two dicts of one list with equal values as equal items.

**Note –** Two lists of Python data have item types of their own, even when their dicts have the same keys, unless they hold at least one dict object in common. So `persons.Concat(otherPersons)` and `persons.Union(otherPersons)` fail with "Can not resolve method 'Concat'" when the two lists were loaded separately (by `json.load`, for instance), and `persons.Contains(...)` never finds an item of `otherPersons`. They work when the lists share a dict, as `persons = [amara, jonas]` and `otherPersons = [lena, amara]` do, or keep the persons in one list and select from it with `Where`.

| Extension Method | Examples and Notes |
| --- | --- |
| `All(Predicate)` | `persons.All(p => p.Age < 50)` |
| `Any()` | `persons.Any()` |
| `Any(Predicate)` | `persons.Any(p => p.Name == "Amara Osei")` |
| `Average(Selector)` | `persons.Average(p => p.Age)`<br/>The input selector must return a value of any type that has predefined or user-defined addition and division operators. |
| `Concat(IEnumerable)` | `persons.Concat(otherPersons)`<br/>An implicit reference conversion must exist between types of items of concatenated enumerations. |
| `Contains(Object)` | `persons.Contains(otherPersons.First())` |
| `Count()` | `persons.Count()` |
| `Count(Predicate)` | `persons.Count(p => p.Age > 30)` |
| `Distinct()` | `persons.Distinct()` |
| `First()` | `persons.First()` |
| `First(Predicate)` | `persons.First(p => p.Age > 30)` |
| `FirstOrDefault()` | `persons.FirstOrDefault()` |
| `FirstOrDefault(Predicate)` | `persons.FirstOrDefault(p => p.Age > 30)` |
| `GroupBy(Selector)` | `persons.GroupBy(p => p.Age)`<br/>Or<br/>`persons.GroupBy(p => new { Age = p.Age, Count = p.Children.Count() })`<br/>This method returns an enumeration of group objects. Each group has a unique key defined by the input selector and contains items of the source enumeration associated with this key. You can access the key of a group instance using the `Key` property. You can treat a group itself as an enumeration of items that the group contains. |
| `Last()` | `persons.Last()` |
| `Last(Predicate)` | `persons.Last(p => p.Age > 100)` |
| `LastOrDefault()` | `persons.LastOrDefault()` |
| `LastOrDefault(Predicate)` | `persons.LastOrDefault(p => p.Age > 100)` |
| `Max(ComparableSelector)` | `persons.Max(p => p.Age)` |
| `Min(ComparableSelector)` | `persons.Min(p => p.Age)` |
| `OrderBy(ComparableSelector)` | `persons.OrderBy(p => p.Age)`<br/>Or<br/>`persons.OrderBy(p => p.Age).ThenByDescending(p => p.Name)`<br/>Or<br/>`persons.OrderBy(p => p.Age).ThenByDescending(p => p.Name).ThenBy(p => p.Children.Count())`<br/>This method returns an enumeration ordered by a single key. To specify additional ordering keys, you can use the following extension methods of an ordered enumeration: <ul><li>`ThenBy(ComparableSelector)`</li><li>`ThenByDescending(ComparableSelector)`</li></ul> |
| `OrderByDescending(ComparableSelector)` | `persons.OrderByDescending(p => p.Age)`<br/>Or<br/>`persons.OrderByDescending(p => p.Age).ThenByDescending(p => p.Name)`<br/>Or<br/>`persons.OrderByDescending(p => p.Age).ThenByDescending(p => p.Name).ThenBy(p => p.Children.Count())`<br/>See the previous note. |
| `Single()` | `persons.Single()` |
| `Single(Predicate)` | `persons.Single(p => p.Name == "Amara Osei")` |
| `SingleOrDefault()` | `persons.SingleOrDefault()` |
| `SingleOrDefault(Predicate)` | `persons.SingleOrDefault(p => p.Name == "Amara Osei")` |
| `Skip(int)` | `persons.Skip(10)` |
| `SkipWhile(Predicate)` | `persons.SkipWhile(p => p.Age < 21)` |
| `Sum(Selector)` | `persons.Sum(p => p.Children.Count())`<br/>The input selector must return a value of any type that has a predefined or user-defined addition operator. |
| `Take(int)` | `persons.Take(5)` |
| `TakeWhile(Predicate)` | `persons.TakeWhile(p => p.Age < 50)` |
| `Union(IEnumerable)` | `persons.Union(otherPersons)`<br/>An implicit reference conversion must exist between types of items of united enumerations. |
| `Where(Predicate)` | `persons.Where(p => p.Age > 18)` |
