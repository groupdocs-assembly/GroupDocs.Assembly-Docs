---
id: template-syntax-part-2-of-2
url: assembly/nodejs-java/template-syntax-part-2-of-2
title: Template Syntax - Part 2 of 2
weight: 2
description: "Expression output and formatting, data bands, cell merging, numbered lists, charts and enumeration extension methods in GroupDocs.Assembly for Node.js via Java templates."
keywords: template syntax, expression tags, foreach, data bands, cellMerge, restartNum, charts, extension methods, node.js
productName: GroupDocs.Assembly for Node.js via Java
hideChildren: False
toc: True
---
{{< alert style="info" >}}This article is the second part of the Template Syntax series of articles. For the first part, see [Template Syntax - Part 1 of 2](/assembly/nodejs-java/template-syntax-part-1-of-2/).{{< /alert >}}

The examples in this article use JSON data. The data source name used in templates is the name you pass to `DataSourceInfo`:

```javascript
const groupdocs = require('@groupdocs/groupdocs.assembly');

const assembler = new groupdocs.DocumentAssembler();
assembler.assembleDocument('template.docx', 'report.docx',
    new groupdocs.DataSourceInfo(new groupdocs.JsonDataSource('persons.json'), 'persons'));
```

## Outputting Expression Results

You can output expression results to your reports using expression tags. An expression tag denotes a placeholder for an expression result within a template. While building a report, the corresponding expression is evaluated, and this placeholder is replaced with the formatted result of the expression.

An expression tag has no name and consists of the following elements:

*   An expression enclosed by brackets
*   An optional format string enclosed by double quotes and preceded by the ":" character
*   An optional `html` switch

```
<<[expression]:"format" -html>>
```

If the `html` switch is not present, the result of the corresponding expression is written to a document as plain text at runtime. Font attributes are derived from the first character of the corresponding tag in this case.

If the `html` switch is present, the expression result is considered to be an HTML block and is written as such. This feature is useful when you need to format text parts of an expression result in different ways. For example, the following tag is replaced with content like "**Bold** and *italic* text" at runtime.

```
<<["<b>Bold</b> and <i>italic</i> text"] -html>>
```

To format a numeric or date-time expression result, you can specify a format string as an element of the corresponding expression tag. Such format strings are the same as the ones that you pass to the Java `DecimalFormat` or `SimpleDateFormat` constructors. That is, for example, given that `d` is a date value, you can use the following template to format the value using the "yyyy.MM.dd" pattern.

```
<<[d]:"yyyy.MM.dd">>
```

With JSON data, date values are usually stored as ISO 8601 strings, for example `"1981-03-15T00:00:00"`. `JsonDataSource` recognizes such strings as dates, so you can format them directly. Numbers are formatted in the same way:

```
<<[person.Birthday]:"yyyy.MM.dd">> <<[person.Salary]:"#,##0.00">>
```

**Note:** Grouping and decimal separators, as well as month and day names, follow the default locale of the JVM that runs the engine.

## Outputting Sequential Data

You can output a sequence of elements of the same type to your report using a data band. A *data band* has a body that represents a template for a single element of such a sequence. While building a report, sequence elements are enumerated, and the following procedure takes place for each of the elements:

1.  The data band body is duplicated and appended to the report.
2.  The appended data band body is populated with the element's data.

**Note:** A data band body can contain nested data bands.

A data band body is defined between the corresponding opening and closing `foreach` tags within a template as follows.

```
<<foreach ...>>
data_band_body
<</foreach>>
```

You can reference an element of the corresponding sequence in template expressions within a data band body using an iteration variable. At runtime, an iteration variable represents a sequence element for which an iteration is currently being performed. You can declare an iteration variable within the corresponding opening `foreach` tag.

An opening `foreach` tag defines a `foreach` statement enclosed by brackets. The following table describes elements of this statement.

| Element | Optional? | Remarks |
| --- | --- | --- |
| **Iteration Variable Type** | Yes | You can specify the Java type of an iteration variable explicitly. This type must be known by the engine (see [Setting up Known External Types](/assembly/nodejs-java/groupdocs-assembly-engine-apis/#setting-up-known-external-types) for more information). If you do not specify the type explicitly, it is determined implicitly by the engine depending on the type of the corresponding sequence. |
| **Iteration Variable Name** | Yes | You can specify the name of an iteration variable to use it while accessing the variable's members. The name must be unique within the scope of the corresponding `foreach` tag. If you do not specify the name, you can access the variable's members using the contextual object member access syntax (see [Using Contextual Object Member Access](/assembly/nodejs-java/template-syntax-part-1-of-2/#using-contextual-object-member-access) for more information). |
| **"in" Keyword** | No | |
| **Sequence Expression** | No | A sequence expression must return a Java `Iterable` implementor, such as a JSON array, a repeated XML element, a CSV data source, or a `DataTable`. |

The complete syntax of a `foreach` tag (including optional elements) is as follows.

```
<<foreach [variable_type variable_name in sequence_expression]>>
data_band_body
<</foreach>>
```

### Common Data Bands

A common data band is a data band whose body starts and ends within paragraphs that belong to a single story or table cell.

Several examples below refer to `items`, an enumeration of the strings "item1", "item2", and "item3". In JSON, keep such values in objects, for example:

```json
[ { "Value": "item1" }, { "Value": "item2" }, { "Value": "item3" } ]
```

Then either output `item.Value` inside the band, or project the objects to strings with `select`: `<<foreach [item in items.select(i => i.Value)]>>`. A JSON array of bare strings (`["item1", "item2"]`) is not exposed to templates as plain string values.

In particular, a common data band can be entirely located within a single paragraph. In this case, while building a report, the band is replaced with contents that are entirely located within the same paragraph as well. The following example illustrates such a scenario. Given the previous declaration of `items`, you can use the following template to enumerate them with commas in a single paragraph.

```
The items are: <<foreach [item in items]>><<[item.Value]>>, <</foreach>>and others.
```

In this case, the engine produces a report as follows.

```
The items are: item1, item2, item3, and others.
```

When the body of a common data band starts and ends within different paragraphs, the engine duplicates on iteration only those paragraph breaks which are located within the body. The following table illustrates the relevant cases (here `items` is an enumeration of strings).

**Note:** Examples in the table are given with paragraph marks shown as per Microsoft Word® editor.

| Template | Report |
| --- | --- |
| `prefix <<foreach [item in items]>><<[item]>>¶`<br/>`<</foreach>>suffix`|`prefix item1¶`<br/>`item2¶`<br/>`item3¶`<br/>`suffix`|
| `prefix<<foreach [item in items]>>¶`<br/>`<<[item]>><</foreach>> suffix`|`prefix¶`<br/>`item1¶`<br/>`item2¶`<br/>`item3 suffix`|
| `prefix¶`<br/>`<<foreach [item in items]>><<[item]>>¶`<br/>`<</foreach>>suffix`| `prefix¶`<br/>`item1¶`<br/>`item2¶`<br/>`item3¶`<br/>`suffix`|
| `prefix<<foreach [item in items]>>¶`<br/>`<<[item]>><</foreach>>¶`<br/>`suffix`|`prefix¶`<br/>`item1¶`<br/>`item2¶`<br/>`item3¶`<br/>`suffix`|
| `prefix¶`<br/>`<<foreach [item in items]>>¶`<br/>`<<[item]>>¶`<br/>`<</foreach>>¶`<br/>`suffix`|`prefix¶`<br/>`¶`<br/>`item1¶`<br/>`¶`<br/>`item2¶`<br/>`¶`<br/>`item3¶`<br/>`¶`<br/>`suffix`|

While building a report, duplicated paragraph breaks derive common attributes from their template prototypes. In particular, this fact enables you to build numbered or bulleted lists in reports dynamically (see [Numbered Lists](#numbered-lists)).

### Merging Table Cells Dynamically

You can merge table cells with equal textual contents within your reports dynamically using `cellMerge` tags. The syntax of a `cellMerge` tag is defined as follows.

```
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

| **...** | **...**                       | **...** |
| ------- | ----------------------------- | ------- |
| **...** | **<<cellMerge>><<[value1]>>** | **...** |
| **...** | **<<cellMerge>><<[value2]>>** | **...** |
| **...** | **...**                       | **...** |

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

**Note:** A `cellMerge` tag can be normally used within a table data band.

You can define an additional restriction on dynamic merging of table cells by providing an expression for a `cellMerge` tag using the following syntax.

```
<<cellMerge [expression]>>
```

During runtime, expressions defined for `cellMerge` tags are evaluated and dynamic cell merging is discarded for those tags whose expressions return unequal values, even if all other conditions for merging such as equal cell textual contents are met. In particular, this feature is useful when cells corresponding to different data band sequence elements should not be merged as shown in the following example.

Assume that you have the following invoice data in `invoices.json`, passed to the engine as `invoices`.

```json
[
  {
    "Number": 11342,
    "Items": [
      { "Ware": "Natural Mineral Water", "Pack": "Bottle 1.0 L", "Quantity": 30 },
      { "Ware": "Natural Mineral Water", "Pack": "Bottle 0.5 L", "Quantity": 50 }
    ]
  },
  {
    "Number": 15385,
    "Items": [
      { "Ware": "Natural Mineral Water", "Pack": "Bottle 1.0 L", "Quantity": 110 }
    ]
  }
]
```

You could use the following template to output information on several invoices in one table.

| **#**                                                        | **Ware**                              | **Pack**                 | **Quantity**                                         |
| ------------------------------------------------------------ | ------------------------------------- | ------------------------ | ---------------------------------------------------- |
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
			<td rowspan="3">Natural Mineral Water</td>
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

| **#**                                                        | **Ware**                                                  | **Pack**                 | **Quantity**                                         |
| ------------------------------------------------------------ | --------------------------------------------------------- | ------------------------ | ---------------------------------------------------- |
| **<<foreach [invoice in invoices]>><<foreach [item in invoice.Items]>><<[invoice.Number]>><<cellMerge>>** | **<<[item.Ware]>><<cellMerge [invoice.indexOf()]>>** | **<<[item.Pack]>>** | **<<[item.Quantity]>><</foreach>><</foreach>>** |

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
			<td rowspan="2">Natural Mineral Water</td>
			<td>Bottle 1.0 L</td>
			<td>30</td>
		</tr>
		<tr>
			<td>Bottle 0.5 L</td>
			<td>50</td>
		</tr>
		<tr>
			<td>15385</td>
			<td>Natural Mineral Water</td>
			<td>Bottle 1.0 L</td>
			<td>110</td>
		</tr>
	</tbody>
</table>

### Numbered Lists

"1. " in the template stands for a numbered list label (a paragraph formatted as a Microsoft Word numbered list item).

```
1. <<foreach [item in items]>><<[item]>>
<</foreach>>
```

In this case, the engine produces a report as follows.

```
1. item1
2. item2
3. item3
```

#### Dynamic List Numbering Restart

This feature is useful when working with a nested numbered list within a data band as shown in the following example.

Assume that you have the following order data in `orders.json`, passed to the engine as `orders`.

```json
[
  {
    "ClientName": "Jane Doe",
    "ClientAddress": "445 Mount Eden Road Mount Eden Auckland 1024",
    "Services": [ { "Name": "Regular Cleaning" }, { "Name": "Oven Cleaning" } ]
  },
  {
    "ClientName": "John Smith",
    "ClientAddress": "43 Vogel Street Roslyn Palmerston North 4414",
    "Services": [ { "Name": "Regular Cleaning" }, { "Name": "Oven Cleaning" }, { "Name": "Carpet Cleaning" } ]
  }
]
```

You could try to use the following template to output information on several orders in one document.

```
<<foreach [order in orders]>><<[order.ClientName]>> (<<[order.ClientAddress]>>)
1. <<foreach [service in order.Services]>><<[service.Name]>>
<</foreach>><</foreach>>
```

But then, the resulting document would look as follows:

```
Jane Doe (445 Mount Eden Road Mount Eden Auckland 1024)
     1. Regular Cleaning
     2. Oven Cleaning
John Smith (43 Vogel Street Roslyn Palmerston North 4414)
     3. Regular Cleaning
     4. Oven Cleaning
     5. Carpet Cleaning
```

That is, there would be a single numbered list across all orders, which is not applicable for this scenario. However, you can make list numbering restart for every order by putting a `restartNum` tag into your template before the corresponding `foreach` tag as follows:

```
<<foreach [order in orders]>><<[order.ClientName]>> (<<[order.ClientAddress]>>)
1. <<restartNum>><<foreach [service in order.Services]>><<[service.Name]>>
<</foreach>><</foreach>>
```

{{< alert style="warning" >}}When used with a data band, a `restartNum` tag must be put before the corresponding `foreach` tag in the same numbered paragraph.{{< /alert >}}

Then, the resulting document looks as follows:

```
Jane Doe (445 Mount Eden Road Mount Eden Auckland 1024)
   1.  Regular Cleaning
   2.  Oven Cleaning

John Smith (43 Vogel Street Roslyn Palmerston North 4414)
   1.  Regular Cleaning
   2.  Oven Cleaning
   3.  Carpet Cleaning
```

{{< alert style="info" >}}You can use a `restartNum` tag without a data band to dynamically restart list numbering for a containing paragraph, if needed; for example, the tag can be used to restart list numbering for a document inserted dynamically.{{< /alert >}}

### Table-Row Data Bands

A table-row data band is a data band whose body occupies single or multiple rows of a single document table. The body of such a band starts at the beginning of the first occupied row and ends at the end of the last occupied row as follows.

<table>
<tbody>
<tr><td>&nbsp;</td><td>&nbsp;</td><td>&nbsp;</td></tr>
<tr><td><code>&lt;&lt;foreach ...&gt;&gt; ...</code></td><td>...</td><td>...</td></tr>
<tr><td>...</td><td>...</td><td>...</td></tr>
<tr><td>...</td><td>...</td><td><code>... &lt;&lt;/foreach&gt;&gt;</code></td></tr>
<tr><td>&nbsp;</td><td>&nbsp;</td><td>&nbsp;</td></tr>
</tbody>
</table>

The examples in this section use the following contract data in `contracts.json`, passed to the engine as `contracts`.

```json
[
  { "Client": "A Company", "Manager": "John Smith", "Price": 1200000 },
  { "Client": "B Ltd.", "Manager": "John Smith", "Price": 750000 },
  { "Client": "C & D", "Manager": "John Smith", "Price": 350000 },
  { "Client": "E Corp.", "Manager": "Tony Anderson", "Price": 650000 },
  { "Client": "F & Partners", "Manager": "Tony Anderson", "Price": 550000 },
  { "Client": "G & Co.", "Manager": "July James", "Price": 350000 },
  { "Client": "H Group", "Manager": "July James", "Price": 250000 },
  { "Client": "I & Sons", "Manager": "July James", "Price": 100000 },
  { "Client": "J Ent.", "Manager": "July James", "Price": 100000 }
]
```

The most common use case of a table-row data band is building a document table that represents a list of items. You can use a template like the following one to achieve this.

| Client | Manager | Contract Price |
| --- | --- | --- |
| `<<foreach [c in contracts]>><<[c.Client]>>`|`<<[c.Manager]>>`|`<<[c.Price]>><</foreach>>`|
| Total: | |`<<[contracts.sum(c => c.Price)]>>`|

In this case, the engine produces a report as follows.

| Client | Manager | Contract Price |
| --- | --- | --- |
| A Company | John Smith | 1200000 |
| B Ltd. | John Smith | 750000 |
| C & D | John Smith | 350000 |
| E Corp. | Tony Anderson | 650000 |
| F & Partners | Tony Anderson | 550000 |
| G & Co. | July James | 350000 |
| H Group | July James | 250000 |
| I & Sons | July James | 100000 |
| J Ent. | July James | 100000 |
| Total: ||4300000|

To populate a document table with master-detail data, you can use nested table-row data bands like in the following template. Here the contracts are grouped by manager with `groupBy`; each group exposes its key through `key` and is itself an enumeration of its contracts. With hierarchical JSON (managers that contain their contracts), you would iterate the nested arrays directly instead.

| Manager/Client | Contract Price |
| --- | --- |
| `<<foreach [g in contracts.groupBy(c => c.Manager)]>><<[g.key]>>`|`<<[g.sum(c => c.Price)]>>`|
| `<<foreach [c in g]>>   <<[c.Client]>>`|`<<[c.Price]>><</foreach>><</foreach>>`|
| Total: |`<<[contracts.sum(c => c.Price)]>>`|

In this case, the engine produces a report as follows.

| Manager/Client | Contract Price |
| --- | --- |
| John Smith | 2300000 |
|    A Company | 1200000 |
|    B Ltd. | 750000 |
|    C & D | 350000 |
| Tony Anderson | 1200000 |
|    E Corp. | 650000 |
|    F & Partners | 550000 |
| July James | 800000 |
|    G & Co. | 350000 |
|    H Group | 250000 |
|    I & Sons | 100000 |
|    J Ent. | 100000 |
| Total: | 4300000 |

You can normally use common data bands nested in table-row data bands as well, like in the following template.

| Manager | Clients |
| --- | --- |
| `<<foreach [g in contracts.groupBy(c => c.Manager)]>><<[g.key]>>`|`<<foreach [c in g]>><<[c.Client]>> <</foreach>><</foreach>>`|

In this case, the engine produces a report as follows.

| Manager | Clients |
| --- | --- |
| John Smith | A Company B Ltd. C & D |
| Tony Anderson | E Corp. F & Partners |
| July James | G & Co. H Group I & Sons J Ent. |

### Extension Methods of Iteration Variables

The GroupDocs.Assembly engine provides special extension methods for iteration variables of any type. You can normally use these extension methods in template expressions. The following list describes the extension methods.

*   `indexOf()`

Returns the zero-based index of a sequence item that is represented by the corresponding iteration variable. You can use this extension method to distinguish sequence items with different indexes and then handle them in different ways. For example, given that `items` is an enumeration of the strings "item1", "item2", and "item3", you can use the following template to enumerate them prefixing all of them but the first one with commas.

```
The items are: <<foreach [
    item in items]>><<[item.indexOf() != 0
        ? ", "
        : ""]>><<[item]>><</foreach>>.
```

In this case, the engine produces a report as follows.

```
The items are: item1, item2, item3.
```

*   `numberOf()`

Returns the one-based index of a sequence item that is represented by the corresponding iteration variable. You can use this extension method to number sequence items without involving Microsoft Word® lists. For example, given the previous declaration of `items`, you can enumerate and number them in a document table using the following template.

| No. | Item |
| --- | --- |
| `<<foreach [item in items]>><<[item.numberOf()]>>`|`<<[item]>><</foreach>>`|

In this case, the engine produces a report as follows.

| No. | Item |
| --- | --- |
| 1 | item1 |
| 2 | item2 |
| 3 | item3 |

### Charts Representing Sequential Data

The GroupDocs.Assembly engine enables you to use charts to represent your sequential data. To declare a chart that is going to be populated with data dynamically within your template, do the following steps:

1.  Add a chart to your template at the place where you want it to appear in a result document.
2.  Configure the appearance of the chart.
3.  Add required chart series and configure their appearance as well.
4.  Add a title to the chart, if missing.
5.  Add an opening `foreach` tag to the chart title.
6.  Depending on the type of the chart, add `x` tags to the chart title or chart series' names as follows.

    ```
    <<x [x_value_expression]>>
    ```

    1.  For a scatter or bubble chart, you can go one of the following ways:
        1.  To use the same x-value expression for all chart series, add a single `x` tag to the chart title after the corresponding `foreach` tag.
        2.  To use different x-value expressions for every chart series, add multiple `x` tags to chart series' names – one for each chart series.
            An x-value expression for a scatter or bubble chart must return a numeric value.
    2.  For a chart of another type, add a single `x` tag to the chart title after the corresponding `foreach` tag. In this case, an x-value expression must return a numeric, date, or string value.
7.  For a chart of any type, add `y` tags to chart series' names as follows.

    ```
    <<y [y_value_expression]>>
    ```

    A y-value expression must return a numeric value.

8.  For a bubble chart, add `size` tags to chart series' names as follows.

    ```
    <<size [bubble_size_expression]>>
    ```

    A bubble-size expression must return a numeric value.

9.  For a chart with dynamic data, you can select which series to include into it dynamically based upon conditions. In particular, this feature is useful when you need to restrict access to sensitive data in chart series for some users of your application. To use the feature, do the following steps:

    1.  Declare a chart with dynamic data in the usual way.
    2.  For series to be removed from the chart based upon conditions dynamically, define the conditions in names of these series using `removeif` tags having the following syntax.

    ```
    <<removeif [conditional_expression]>>
    ```

    A conditional expression must return a Boolean value.

**Note:** A closing `foreach` tag is not used for a chart.

While composing expressions for `x`, `y`, and `size` tags, you can normally reference an iteration variable declared at the corresponding `foreach` tag in a chart title in the same way as if you intended to output results of expressions within a data band.

**Note:** You can normally use charts with dynamic data within data bands.

During runtime, a chart with a `foreach` tag in its title is processed by the engine as follows:

1.  A sequence expression declared at the `foreach` tag is evaluated and iterated.
2.  For every sequence item, expressions declared at `x`, `y`, and `size` tags are evaluated.
3.  Results of these expressions are used to populate corresponding chart series.
4.  All `foreach`, `x`, `y`, and `size` tags are removed from the chart title and chart series' names.

For example, given the `contracts` data from [Table-Row Data Bands](#table-row-data-bands), you can represent total contract prices achieved by managers in a column chart by putting the following tag into the chart title

```
<<foreach [g in contracts.groupBy(c => c.Manager)]>><<x [g.key]>>
```

and the following tag into the name of the chart series.

```
<<y [g.sum(c => c.Price)]>>
```

## Enumeration Extension Methods

### The Enumeration

The GroupDocs.Assembly engine enables you to perform common manipulations on sequential data through the engine's built-in extension methods for Java `Iterable`. These extension methods mimic some extension methods of .NET `IEnumerable<T>`, providing the same signatures and behavior features. Thus, you can group, sort, and perform other sequential data manipulations in template expressions in a familiar way.

### The Enumeration Extension

The table below describes the built-in extension methods. The following notation conventions are used within the table:

*   `Selector` stands for a lambda function returning a value and taking an enumeration item as its single argument. See [Using Lambda Functions](/assembly/nodejs-java/template-syntax-part-1-of-2/#using-lambda-functions) for more information.
*   `ComparableSelector` stands for `Selector` returning a comparable value (a Java `Comparable`, such as a number, string, or date).
*   `Predicate` stands for `Selector` returning a Boolean value.

Examples in this table are given using `persons` and `otherPersons`, enumerations of person objects loaded from JSON like the following one.

```json
[
  { "Name": "John Smith", "Age": 45, "Children": [ { "Name": "Ann", "Age": 12 }, { "Name": "Bob", "Age": 9 } ] },
  { "Name": "Jane Doe", "Age": 28, "Children": [] },
  { "Name": "Mark Green", "Age": 45, "Children": [ { "Name": "Tim", "Age": 3 } ] }
]
```

| Extension Method | Examples and Notes |
| --- | --- |
| `all(Predicate)` | `persons.all(p => p.Age < 50)` |
| `any()` | `persons.any()` |
| `any(Predicate)` | `persons.any(p => p.Name == "John Smith")` |
| `average(Selector)` | `persons.average(p => p.Age)`<br/>The input selector must return a value of any type that has predefined addition and division operators. |
| `concat(Iterable)` | `persons.concat(otherPersons)`<br/>An implicit reference conversion must exist between types of items of concatenated enumerations. |
| `contains(Object)` | `persons.contains(otherPersons.first())` |
| `count()` | `persons.count()` |
| `count(Predicate)` | `persons.count(p => p.Age > 30)` |
| `distinct()` | `persons.distinct()` |
| `first()` | `persons.first()` |
| `first(Predicate)` | `persons.first(p => p.Age > 30)` |
| `firstOrDefault()` | `persons.firstOrDefault()` |
| `firstOrDefault(Predicate)` | `persons.firstOrDefault(p => p.Age > 30)` |
| `groupBy(Selector)` | `persons.groupBy(p => p.Age)`<br/>Or<br/>`persons.groupBy(p => new { age = p.Age, count = p.Children.count() })`<br/>This method returns an enumeration of group objects. Each group has a unique key defined by the input selector and contains items of the source enumeration associated with this key. You can access the key of a group instance using the `key` member, for example, `g.key` or `g.key.age` for an anonymous-type key. You can treat a group itself as an enumeration of items that the group contains. |
| `last()` | `persons.last()` |
| `last(Predicate)` | `persons.last(p => p.Age > 100)` |
| `lastOrDefault()` | `persons.lastOrDefault()` |
| `lastOrDefault(Predicate)` | `persons.lastOrDefault(p => p.Age > 100)` |
| `max(ComparableSelector)` | `persons.max(p => p.Age)` |
| `min(ComparableSelector)` | `persons.min(p => p.Age)` |
| `orderBy(ComparableSelector)` | `persons.orderBy(p => p.Age)`<br/>Or<br/>`persons.orderBy(p => p.Age).thenByDescending(p => p.Name)`<br/>Or<br/>`persons.orderBy(p => p.Age).thenByDescending(p => p.Name).thenBy(p => p.Children.count())`<br/>This method returns an enumeration ordered by a single key. To specify additional ordering keys, you can use the following extension methods of an ordered enumeration:<ul><li>`thenBy(ComparableSelector)`</li><li>`thenByDescending(ComparableSelector)`</li></ul> |
| `orderByDescending(ComparableSelector)` | `persons.orderByDescending(p => p.Age)`<br/>Or<br/>`persons.orderByDescending(p => p.Age).thenByDescending(p => p.Name)`<br/>Or<br/>`persons.orderByDescending(p => p.Age).thenByDescending(p => p.Name).thenBy(p => p.Children.count())`<br/>See the previous note. |
| `select(Selector)` | `persons.select(p => p.Name)`<br/>Returns an enumeration of values produced by the selector. |
| `single()` | `persons.single()` |
| `single(Predicate)` | `persons.single(p => p.Name == "John Smith")` |
| `singleOrDefault()` | `persons.singleOrDefault()` |
| `singleOrDefault(Predicate)` | `persons.singleOrDefault(p => p.Name == "John Smith")` |
| `skip(int)` | `persons.skip(10)` |
| `skipWhile(Predicate)` | `persons.skipWhile(p => p.Age < 21)` |
| `sum(Selector)` | `persons.sum(p => p.Children.count())`<br/>The input selector must return a value of any type that has a predefined addition operator. |
| `take(int)` | `persons.take(5)` |
| `takeWhile(Predicate)` | `persons.takeWhile(p => p.Age < 50)` |
| `union(Iterable)` | `persons.union(otherPersons)`<br/>An implicit reference conversion must exist between types of items of united enumerations. |
| `where(Predicate)` | `persons.where(p => p.Age > 18)` |
