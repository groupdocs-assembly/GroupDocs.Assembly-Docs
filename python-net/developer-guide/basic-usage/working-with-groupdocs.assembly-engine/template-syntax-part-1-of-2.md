---
id: template-syntax-part-1-of-2
url: assembly/python-net/template-syntax-part-1-of-2
title: Template Syntax - Part 1 of 2
weight: 1
description: "GroupDocs.Assembly template syntax, part 1: tags, expressions, types, operators, lambda functions, Python dicts and lists and other data sources, images, documents, checkboxes, comboboxes, hyperlinks, contextual member access and conditional blocks."
keywords: template syntax, tags, expressions, data sources, dict, contextual object member access, conditional blocks, Python, GroupDocs.Assembly
productName: GroupDocs.Assembly for Python via .NET
hideChildren: False
---
{{< alert style="info" >}}This article is the first part of the Template Syntax series of articles. For second part, please visit [Template Syntax - Part 2 of 2]({{< ref "assembly/python-net/developer-guide/basic-usage/working-with-groupdocs.assembly-engine/template-syntax-part-2-of-2.md" >}}).{{< /alert >}}

The template syntax is the same in GroupDocs.Assembly for Python via .NET as in GroupDocs.Assembly for .NET: a template written for one works with the other. Template expressions follow the syntax of C#, whatever language the application that builds the report is written in. What differs is the data: a Python application passes dicts, lists and Python values, which the engine reads as .NET objects (see [Using Data Sources](#using-data-sources)).

## Composing Template

A typical template for GroupDocs.Assembly Engine is composed of common document contents and tags that describe the template's structure and data bindings. You can form these tags using just running text that can occupy multiple paragraphs to be more descriptive.

A tag body must meet the following requirements:

*   A tag body must be surrounded by "`<<`" and "`>>`" character sequences.
*   A tag body must contain only text nodes.
*   A tag body must not be located inside markup document nodes.

A tag body typically consists of the following elements:

*   A tag name
*   An expression surrounded by brackets
*   A set of switches available for the tag, each of which is preceded by the "`-`" character

```text
<<tag_name [expression] -switch1 -switch2 ...>>
```

An optional comment can be written to provide a human-readable explanation.

```text
<<tag_name [expression] -switch1 -switch2 ... // optional_comment >>
```

Particular tags can have additional elements. Some tags require closing counterparts. A closing tag has the "`/`" character that precedes its name. This tag's name must match to the name of the corresponding opening tag.

```text
<</tag_name>>
```

**Note:** Tag body elements are case-sensitive.

## Composing Expressions

### Using Lexical Tokens

The following table describes lexical tokens that you can use in template expressions and restrictions on these tokens' usage comparing with [C# Language Specification 5.0](http://www.microsoft.com/en-us/download/details.aspx?id=7029).

| Token | Restrictions |
| --- | --- |
| **Keyword** | Only the following tokens are reserved as keywords: `true`, `false`, `null`, `new`, and `in` |
| **Identifier** | <ul><li>The feature of keyword escaping through the "@" character is not supported.</li><li>Unicode character escapes are not permitted in identifiers.</li></ul> |
| **Literal** | None |
| **Operator** | See [Using Operators](#using-operators) |

The literals and keywords are those of C#, not of Python: write `true`, `false` and `null` in a template, not `True`, `False` and `None`, and enclose strings in double quotes.

You can use the following identifiers that are not preceded by a member access operator in template expressions:

*   The name of a passed data source object
*   The name of an iteration variable within its scope (see [Outputting Sequential Data]({{< ref "assembly/python-net/developer-guide/basic-usage/working-with-groupdocs.assembly-engine/template-syntax-part-2-of-2.md#outputting-sequential-data" >}}) for more information)
*   The name of a lambda function parameter within the scope of the lambda function
*   A fully or partially qualified name of a type that is known by the engine (see [Setting up Known External Types]({{< ref "assembly/python-net/developer-guide/basic-usage/working-with-groupdocs.assembly-engine/groupdocs.assembly-engine-apis.md#setting-up-known-external-types" >}}) for more information)
*   The name of a member of an object that is determined as follows:
    *   Inside a data band body, the object is resolved to the innermost iteration variable.
    *   Outside a data band body, the object is resolved to a passed data source.

The feature of the omitting of an object identifier while accessing the object's members is also known as the contextual object member access. See [Using Contextual Object Member Access](#using-contextual-object-member-access) for more information.

### Using Types

GroupDocs.Assembly Engine enables you to use .NET types in template expressions. A Python application deals with two kinds of them:

*   The types of the data it passes. The engine reads a `str` as a .NET `String`, an `int` as an `Int64`, a `datetime` as a `DateTime`, and a dict as an object of a type it makes from the dict's keys (see [Using Data Sources](#using-data-sources)). A template uses the members of these types, `<<[c.CustomerName.ToUpper()]>>` or `<<[o.OrderDate.Month]>>`, but cannot name a type made from a dict: its name is generated.
*   The types of the .NET runtime that a template calls by name, such as `Math` in `<<[Math.Round(price, 2)]>>`. Such a type must be known by the engine (see [Setting up Known External Types]({{< ref "assembly/python-net/developer-guide/basic-usage/working-with-groupdocs.assembly-engine/groupdocs.assembly-engine-apis.md#setting-up-known-external-types" >}})).

You can use the identifier of a type in template expressions only if the following additional requirements are met:

*   The type is not void.
*   The type does not represent an array.
*   The type is not an open or closed generic type.

**Note:** Whereas using of generic types' identifiers is forbidden in template expressions, you can use identifiers of nullable types in the shorthand `"T?"` form.

Also, the engine enables you to use anonymous types in template expressions. Such types are useful while composing expressions with grouping by multiple keys. See [Enumeration Extension Methods]({{< ref "assembly/python-net/developer-guide/basic-usage/working-with-groupdocs.assembly-engine/template-syntax-part-2-of-2.md#enumeration-extension-methods" >}}) for the examples.

#### Type Members

GroupDocs.Assembly Engine enables you to access the following public (static and instance) members of accessible types in template expressions:

*   Fields
*   Properties
*   Indexer getters
*   Methods
*   Constructors

The keys of a Python dict are properties of its object, and the dict also has an indexer that reads a value by its key (see [Using Data Sources](#using-data-sources)).

However, you can use a functional type member in template expressions only if the following additional requirements are met:

*   The functional member returns a value.
*   The functional member does not have `ref` or `out` parameters.
*   The functional member does not take generic type arguments.

The engine supports the following features when dealing with functional members:

*   Overload resolution according to [C# Language Specification 5.0](http://www.microsoft.com/en-us/download/details.aspx?id=7029)
*   Using of default parameter values without support of named parameters
*   Using of parameters taking a variable number of arguments

### Using Extension Methods

GroupDocs.Assembly Engine enables you to use the following built-in extension methods in template expressions:

*   Extension methods mimicking the ones for `IEnumerable<T>`, which apply to Python lists (see [Enumeration Extension Methods]({{< ref "assembly/python-net/developer-guide/basic-usage/working-with-groupdocs.assembly-engine/template-syntax-part-2-of-2.md#enumeration-extension-methods" >}}) for more information)
*   Extension methods for iteration variables (see [Extension Methods of Iteration Variables]({{< ref "assembly/python-net/developer-guide/basic-usage/working-with-groupdocs.assembly-engine/template-syntax-part-2-of-2.md#extension-methods-of-iteration-variables" >}}) for more information)

**Note:** Extension methods, other than the built-in ones, can be used only in the form of plain static methods in template expressions.

### Using Operators

The following list contains predefined and user-defined operators that Document Assembler enables you to use in template expressions.

*   **Primary:**

    ```text
    x.y f(x) a[x] new x?.y a?[x]
    ```

*   **Unary:**

    ```text
    - ! ~ (T)x
    ```

*   **Binary:**

    ```text
    * / % + - << >> < > <= >= == != & ^ | && || ??
    ```

*   **Ternary:**

    ```text
    ?:
    ```

The engine follows operator precedence, associativity and overload resolution rules declared at [C# Language Specification 5.0](http://www.microsoft.com/en-us/download/details.aspx?id=7029) while evaluating template expressions. But be aware of the following limitations in the behavior comparing with the specification:

*   Implicit user-defined conversions are supported only when specified explicitly.
*   The indexing of multi-dimensional arrays is not supported.
*   Whereas the object initializer syntax is supported (including objects of anonymous types), the collection initializer syntax is not.

Also, the engine enables you to use lifted operators in template expressions.

The operators are those of C#: `&&`, `||` and `!` rather than Python's `and`, `or` and `not`, and `/` between two integers is an integer division, as in C#. To divide integers exactly, cast one of them: `(double)o.Price / o.ProductQuantity`.

### Using Lambda Functions

GroupDocs.Assembly Engine enables you to use lambda functions only as arguments of built-in enumeration extension methods in template expressions. See [Enumeration Extension Methods]({{< ref "assembly/python-net/developer-guide/basic-usage/working-with-groupdocs.assembly-engine/template-syntax-part-2-of-2.md#enumeration-extension-methods" >}}) for more information.

**Note:** Lambda functions declared within template expressions are written in the C# form, `p => p.Age > 30`, and are not interchangeable with delegates. Thus, you can not pass a Python function or lambda to a template as an argument of built-in enumeration extension methods.

You can use both explicit and implicit lambda function signatures in template expressions. If you do not specify the type of a parameter of a lambda function explicitly, the type is determined implicitly by the engine depending on the type of the corresponding enumeration.

### Using Data Sources

{{< alert style="info" >}}[The Business Layer]({{< ref "assembly/python-net/developer-guide/basic-usage/working-with-a-business-case/the-business-layer.md" >}}) describes the data files the examples of this documentation read and how each is loaded.{{< /alert >}}

#### Python Dicts and Lists

A Python application passes its data as dicts, lists and Python values. When `DataSourceInfo` is created, the engine copies them into .NET objects as follows:

| Python | In a template |
| --- | --- |
| `dict` | An object whose properties are the dict's keys: `<<[c.CustomerName]>>`. All dicts that hold the same place, such as the items of one list or the values of one key across the items, are objects of one type, which has the keys of all of them. |
| `list`, `tuple`, `set` | A sequence (`List<T>`) that `foreach` tags and enumeration extension methods iterate. |
| `str` | `String`. A string of digits stays a string: `"007"` is not the number 7. |
| `int` | `Int64` (`bool` is `Boolean`). |
| `float` | `Double`. |
| `decimal.Decimal` | `Decimal`. |
| `datetime`, `date` | `DateTime` (a `date` at midnight). An aware `datetime` is a `DateTimeOffset`. |
| `time` | `TimeSpan`. |
| `bytes` | A byte array, which image and doc tags take. |
| `None` | `null`. |

A few consequences are worth knowing:

*   **Missing keys.** A key that some dicts of a list have and others lack, or hold `None` for, makes the property nullable: it is `null` where the key is absent. A value-type property, such as an `int` or a `datetime`, then becomes nullable (`Int64?`, `DateTime?`): operators and format strings work on it as they are, but its members are read through `Value`, `<<[o.Date.Value.Month]>>`.
*   **Mixed values.** Values of different kinds under one key, or in one list, make the property or the item an `Object`, which can be output but whose members cannot be read.
*   **Empty lists.** An empty list has no item to take a type from: `<<foreach [o in c.Orders]>><<[o.Product]>>` fails on a customer whose only `Orders` is `[]`, unless another customer's `Orders` has items. Give the data an item, or apply `DocumentAssemblyOptions.ALLOW_MISSING_MEMBERS`.
*   **Equality.** Two objects made from dicts of one type are equal when their values are, so `Distinct()` and `GroupBy(o => o.Customer)` work on the copies of a customer that `json.load` gives each of its orders. Dicts that hold different places, such as the items of two lists under different keys, are of different types and never equal (see the note in [Enumeration Extension Methods]({{< ref "assembly/python-net/developer-guide/basic-usage/working-with-groupdocs.assembly-engine/template-syntax-part-2-of-2.md#the-enumeration-extension" >}})).
*   **Shared and circular data.** A dict that appears in several places is one object, so a structure may refer back to itself (see [Working with Lazy And Recursive Access of Data]({{< ref "assembly/python-net/developer-guide/advanced-usage/working-with-lazy-and-recursive-access-of-data.md" >}})).
*   **The indexer.** A dict's object also reads a value by its key, `<<[r["First Name"]]>>`, which is how to reach a key that is not an identifier. The indexer returns an `Object`, which cannot be indexed again.
*   **Copied once.** The data is copied when `DataSourceInfo` is created: a change to a dict made afterwards does not reach the report. Other Python objects, such as instances of your classes, cannot be part of the data; turn them into dicts first.

#### Document Table Sets

ADO.NET `DataSet` objects have no Python form. A `DocumentTableSet`, which loads all the tables of a Word, Excel or PowerPoint document, plays their part: GroupDocs.Assembly Engine enables you to access the `DocumentTable` objects contained within a particular `DocumentTableSet` instance by table names using the "." operator in template expressions. That is, for example, given that `ds` is a `DocumentTableSet` instance that contains a table named "Persons", you can access the table using the following syntax.

```text
ds.Persons
```

**Note:** Table names are case-insensitive.

A Python dict holding lists plays the same part for your own data: given that `ds` is `{"Persons": [...]}`, `ds.Persons` is the list.

#### Document Tables

GroupDocs.Assembly Engine enables you to treat `DocumentTable` objects in template expressions as enumerations of their rows, as it treats ADO.NET `DataTable` and `DataView` objects. That is, you can use template expressions evaluated to such objects in `foreach` tags (see [Outputting Sequential Data]({{< ref "assembly/python-net/developer-guide/basic-usage/working-with-groupdocs.assembly-engine/template-syntax-part-2-of-2.md#outputting-sequential-data" >}}) for more information).

Also, you can normally apply enumeration extension methods (see [Enumeration Extension Methods]({{< ref "assembly/python-net/developer-guide/basic-usage/working-with-groupdocs.assembly-engine/template-syntax-part-2-of-2.md#enumeration-extension-methods" >}}) for more information) to `DocumentTable` objects in template expressions. For example, given that persons is a `DocumentTable` instance, you can count its rows using the following syntax.

```text
persons.Count()
```

#### Rows of Document Tables

GroupDocs.Assembly Engine enables you to access a data associated with a particular row of a `DocumentTable` in template expressions using the "." operator. The following table describes, which identifiers you can use to access different kinds of the data.

| Data Kind | Identifier | Examples of Template Expressions |
| --- | --- | --- |
| **Field Value** | Field name | Given that `r` is a row that has a field named "Name", you can access the field's value using the following syntax:<br />`r.Name`. |
| **Single Parent or Child Row** | Parent (child) table name | Given that `r` is a row of a table that has a parent (child) table named "City", you can access the single parent (child) row of `r` using the following syntax:<br />`r.City`.<br />Given that the "City" table has a field named "Name", you can access the field's value for the single parent (child) row using the following syntax:<br />`r.City.Name`. |
| **Enumeration of Child or Parent Rows** | Child (parent) table name | Given that `r` is a row of a table that has a child (parent) table named "Persons", you can access the enumeration of the child (parent) rows of `r` using the following syntax:<br />`r.Persons`.<br />Given that the "Persons" table has a field named "Age", you can count the child (parent) rows that correspond to persons over thirty years old using the following syntax:<br />`r.Persons.Count(p => p.Age > 30)`. |

{{< alert style="warning" >}} Field and table names are case-insensitive.{{< /alert >}}

A row of a document table has no indexer: read its fields by name with the "." operator. A column name with a space has an underscore in its place (`Total_Contract_Price`).

To determine parent-child relationships between the tables of a `DocumentTableSet`, the engine uses the relations you add to its `relations` collection, which link a column of the parent table to a column of the child table. See [Defining Relations Between DocumentTable Instances Loaded from a Single Document]({{< ref "assembly/python-net/developer-guide/advanced-usage/defining-relations-between-documenttable-instances-loaded-from-a-single-document.md" >}}) and the examples of [Table-Row Data Bands]({{< ref "assembly/python-net/developer-guide/basic-usage/working-with-groupdocs.assembly-engine/template-syntax-part-2-of-2.md#table-row-data-bands" >}}).

#### Database Rows

The .NET engine also reads ADO.NET `IDataReader` and `IDataRecord` implementors. A Python database cursor is not one: fetch the rows in Python and pass them as dicts, one per row, whose keys are the column names. With `sqlite3`, set `connection.row_factory = sqlite3.Row` and pass `[dict(row) for row in cursor]`. See [Generate Document from Database]({{< ref "assembly/python-net/developer-guide/basic-usage/generate-from-database.md" >}}).

### Using Images

You can insert images to your reports dynamically using image tags. To declare a dynamically inserted image within your template, please follow these steps:

1.  Add a textbox to your template at the place where you want an image to be inserted.
2.  Set common image attributes such as frame, size, and others for the textbox, making the textbox look like a blank inserted image.
3.  Specify an image tag within the textbox using the following syntax.

    ```text
    <<image [image_expression]>>
    ```

The expression declared within an image tag is used by the engine to build an image to be inserted. For Python data, the expression must return a value of one of the following types:

*   A byte array containing an image data: a `bytes` value in the data
*   A string containing an image URI, path, or Base64-encoded image data: a `str` value in the data

A path is resolved against the current folder of the Python process. The .NET engine also takes a `Stream` or an `Image` object, which Python data cannot hold.

While building a report, the following procedure is applied to an image tag:

*   The expression declared within the tag is evaluated and its result is used to form an image.
*   The corresponding textbox is filled with this image.
*   The tag is removed from the textbox.

By default, the assembler stretches an image filling a textbox to the size of the textbox. However, you can change this behavior in the following ways:

*   To keep the size of the textbox and stretch the image within bounds of the textbox preserving the ratio of the image, use the *keepRatio* switch as follows:

    ```text
    <<image [image_expression] -keepRatio>>
    ```

*   To keep the width of the textbox and change its height preserving the ratio of the image, use the fitHeight switch as follows.

    ```text
    <<image [image_expression] -fitHeight>>
    ```

*   To keep the height of the textbox and change its width preserving the ratio of the image, use the fitWidth switch as follows.

    ```text
    <<image [image_expression] -fitWidth>>
    ```

*   To change the size of the textbox according to the size of the image, use the fitSize switch as follows.

    ```text
    <<image [image_expression] -fitSize>>
    ```

*   To change the size of the textbox according to the size of the image without increasing the size of the textbox, use the fitSizeLim switch as follows.

    ```text
    <<image [image_expression] -fitSizeLim>>
    ```

    {{< alert style="warning" >}}If the size of the image is greater than the size of the textbox, then the fitSizeLim switch acts like fitHeight or fitWidth. Otherwise, the fitSizeLim switch acts like fitSize.{{< /alert >}}

### Inserting Documents

You can insert contents of outer documents to your reports dynamically using doc tags. A doc tag denotes a placeholder within a template for a document to be inserted during runtime.

Syntax of a doc tag is defined as follows.

```text
<<doc [document_expression]>>
```

{{< alert style="warning" >}}A doc tag can be used almost anywhere in a template document except textboxes and charts.{{< /alert >}}

An expression declared within a doc tag is used by the assembler to load a document to be inserted during runtime. For Python data, the expression must return a value of one of the following types:

*   A byte array containing document data: a `bytes` value in the data
*   A string containing a document URI, path, or Base64-encoded document data: a `str` value in the data

The .NET engine also takes a `Stream` or a `Document` object, which Python data cannot hold.

While building a report, an expression declared within a doc tag is evaluated and its result is used to load a document which content replaces the doc tag then.

By default, a document being inserted is not checked against template syntax and is not populated with data. However, you can enable this by using a build switch as follows.

```text
<<doc [document_expression] -build>>
```

When a build switch is used, the assembler treats a document being inserted as a template that can access the following data available at the scope of a corresponding doc tag:

*   Data sources
*   Variables
*   A contextual object
*   Known external types

### Setting Checkbox Values Dynamically

You can set checkbox values to either checked or unchecked in your reports dynamically by taking the following steps:

1.  Add a checkbox content control to your template at a place where you want it to appear in a result document.
2.  By editing content control properties, add a check tag to the title of the checkbox content control using the following syntax.

```text
<<check [conditional_expression]>>
```

Here, conditional\_expression defines a condition upon which the value of the checkbox content control is to be set to checked (or unchecked, if the condition is not met). The conditional expression must return a Boolean value: a Python `bool` in the data, or a comparison such as `[o.Discount > 0]`.

While building a report, a conditional expression declared within a check tag is evaluated and the value of its containing checkbox content control is set accordingly. The check tag itself is removed then.

{{< alert style="warning" >}}Dynamic checkbox value setting is available for Word Processing documents only.{{< /alert >}}

### Adding Combobox and Dropdown List Items Dynamically

You can dynamically add items to comboboxes and dropdown lists defined in your template by taking the following steps:

1. Add a combobox or dropdown list content control to your template at a place where you want it to appear in a result document.
2. By editing content control properties, add an `item` tag to the title of this content control using the following syntax.

```text
<<item [value_expression] [display_name_expression]>>
```

Here, `value_expression` defines a value of a combobox or dropdown list item to be added dynamically. This expression is mandatory and must return a non-empty value.

In turn, `display_name_expression` defines a display name of the combobox or dropdown list item to be added. This expression is optional. If it is omitted, then during runtime, a value of `value_expression` is used as a display name as well.

**Note –** Values of both `value_expression` and `display_name_expression` can be of any types. During runtime, `Object.ToString()` is invoked to get textual representations of these expressions' values.

While building a report, `value_expression` and `display_name_expression` are evaluated and a corresponding combobox or dropdown list item is added. A declaring `item` tag is removed then.

A single `item` tag causes addition of a single combobox or dropdown list item during runtime. You can add multiple combobox or dropdown list items using multiple `item` tags as shown in the following snippet.

```text
<<item ...>><<item ...>>
```

Also, you can normally use `item` tags within data bands to add a combobox or dropdown list item per item of a data collection. For example, given that `clients` is a list of dicts having a key named "Name", you can use the following template to cover such a scenario.

```text
<<foreach [client in clients]>><<item [client.Name]>><</foreach>>
```

An `item` tag can also be combined with an `if` tag to add a combobox or dropdown list item depending on a condition as shown in the following snippet.

```text
<<if ...>><<item ...>><</if>>
```

Existing combobox and dropdown list items are not affected by `item` tags. Thus, you can combine both ways of adding combobox and dropdown list items using a template: static and dynamic.

**Note –** While inserting a combobox or dropdown list, Microsoft Word adds a default item that has to be removed manually, if the item is unwanted.

### Using Hyperlinks

Using GroupDocs.Assembly, you can insert hyperlinks to URI or Bookmarks to your reports dynamically using link tags. The syntax of a link tag is defined below for various types of documents:

#### Word Processing and Emails

```text
<<link [uri_or_bookmark_expression] [display_text_expression]>>
```

#### Spreadsheets

If the insertion of the link to cell A1 is required:

```text
<<link ["A1"] ["Home"]>>
```

#### Presentations

```text
<<link ["Slide1"] ["Home"]>>
```

### Using Contextual Object Member Access

You can make your templates less cumbersome using the contextual object member access feature. This feature enables you to access members of some objects without specifying the objects' identifiers in template expressions. An object to which the feature can be applied is determined depending on a context as follows:

*   Inside a data band body, the object is resolved to the innermost iteration variable.
*   Outside a data band body, the object is resolved to a passed data source.

Obviously, inside a data band body, you can not use the feature to access members of an outer iteration variable or a passed data source object. With the exception of this restriction, you can use both contextual and common object member access syntaxes interchangeably depending on your needs and preferences.

Consider the following example. Given that `ds` is a dict whose "Persons" key holds a list of dicts with "Name" and "Age" keys, you can use the following template to list the persons in a table.

| No. | Name | Age |
| --- | --- | --- |
| `<<foreach [p in ds.Persons]>><<[p.NumberOf()]>>` | `<<[p.Name]>>` | `<<[p.Age]>><</foreach>>` |
| `Count: <<[ds.Persons.Count()]>>` |  |  |

Alternatively, you can use the following template involving the contextual object member access syntax to get the same results. The data source is then passed without a name.

| No. | Name | Age |
| --- | --- | --- |
| `<<foreach [in Persons]>><<[NumberOf()]>>` | `<<[Name]>>` | `<<[Age]>><</foreach>>` |
| `Count: <<[Persons.Count()]>>` |  |  |

The following example builds a report from each template with Harbor Lane's staff:

{{< tabs "example1" >}}
{{< tab "Python" >}}
```python
from groupdocs.assembly import DataSourceInfo, DocumentAssembler

ds = {
    "Persons": [
        {"Name": "Amara Osei", "Age": 41},
        {"Name": "Jonas Weber", "Age": 37},
        {"Name": "Lena Park", "Age": 29},
    ]
}

assembler = DocumentAssembler()
# The data source is named "ds" in the first template
assembler.assemble_document("staff-table-named.docx", "staff-table-named-report.docx", DataSourceInfo(ds, "ds"))
# The second template uses the contextual object member access: no name
assembler.assemble_document("staff-table-contextual.docx", "staff-table-contextual-report.docx", DataSourceInfo(ds))
```
{{< /tab >}}
{{< tab "staff-table-named.docx" >}}
{{< tab-text >}}
The following sample file is used in this example: [staff-table-named.docx](/assembly/python-net/_sample_files/developer-guide/basic-usage/working-with-groupdocs.assembly-engine/template-syntax-part-1-of-2/staff-table-named.docx)
{{< /tab-text >}}
{{< /tab >}}
{{< tab "staff-table-contextual.docx" >}}
{{< tab-text >}}
The following sample file is used in this example: [staff-table-contextual.docx](/assembly/python-net/_sample_files/developer-guide/basic-usage/working-with-groupdocs.assembly-engine/template-syntax-part-1-of-2/staff-table-contextual.docx)
{{< /tab-text >}}
{{< /tab >}}
{{< tab "using-contextual-object-member-access-outputs.zip" >}}  
```text
staff-table-contextual-report.docx (7 KB)
staff-table-named-report.docx (7 KB)
```
[Download full output](/assembly/python-net/_output_files/developer-guide/basic-usage/working-with-groupdocs.assembly-engine/template-syntax-part-1-of-2/using_contextual_object_member_access/using-contextual-object-member-access-outputs.zip)
{{< /tab >}}
{{< /tabs >}}

### Using Conditional Blocks

You can use different document blocks to represent the same data depending on a condition with the help of conditional blocks. A conditional block represents a set of template options, each of which is bound with a conditional expression. At runtime, these conditional expressions are sequentially evaluated, until an expression that returns true is reached. Then, the conditional block is replaced with the corresponding template option populated with data.

A conditional block can have a default template option that is not bound with a conditional expression. At runtime, this template option is used, when none of conditional expressions return true. If a default template option is missing and none of conditional expressions return true, then the whole conditional block is removed during runtime.

You can use the following syntax to declare a conditional block:

```text
<<if [conditional_expression1]>>
template_option1
<<elseif [conditional_expression2]>>
template_option2
...
<<else>>
default_template_option
<</if>>
```

**Note:** A conditional expression must return a Boolean value.

#### Common Conditional Blocks

A common conditional block is a conditional block which body starts and ends within paragraphs that belong to a single story or table cell.

If a conditional block belongs to a single paragraph, it can be used as a replacement for an expression tag that involves the ternary "?:" operator. For example, given that items is an enumeration, you can use the following template to represent the count of elements in the enumeration:

```text
You have chosen <<if [!items.Any()]>>no items<<else>><<[items.Count()]>> item(s)<</if>>.
```

**Note:** A template option of a common conditional block can be composed of multiple paragraphs, if needed.

You can normally use common conditional blocks within data bands. For example, given that items is a list of the strings "item1", "item2", and "item3", you can use the following template to enumerate them and apply different formatting for even and odd elements:

```text
<<foreach [item in items]>><<if [IndexOf() % 2 == 0]>><<[item]>>
<<else>><<[item]>>
<</if>><</foreach>>
```

In this case, the engine produces a report as follows:

```text
item1
item2
item3
```

You can use data bands within common conditional blocks as well. For example, given the previous declaration of items, you can check whether the enumeration contains any elements before outputting their list:

```text
<<if [!items.Any()]>>No data.
<<else>><<foreach [item in items]>><<[item]>>
<</foreach>><</if>>
```

#### Table-Row Conditional Block

A table-row conditional block is a conditional block which body occupies single or multiple rows of a single document table. The body of such a block (as well as the body of its every template option) starts at the beginning of the first occupied row and ends at the end of the last occupied row as follows:

| | | |
| --- | --- | --- |
| `<<if ...>>` ... | ... | ... |
| ... | ... | ... |
| `<<elseif ...>>` ... | ... | ... |
| ... | ... | ... |
| `<<else>>` ... | ... | ... |
| ... | ... | ... |
| ... | ... | ... `<</if>>` |

The following examples in this section are given using `client`, a dict of a client, and `clients`, a list of such dicts, each having the "Name", "Country" and "LocalAddress" keys.

Using table-row conditional blocks, you can pick to output a single row among several rows of a single document table depending on a condition like in the following example, where the row for a client of New Zealand merges its second and third cells:

| | | |
| --- | --- | --- |
| ... | ... | ... |
| `<<if [client.Country == "New Zealand"]>><<[client.Name]>>` | `<<[client.LocalAddress]>>` (two merged cells) | |
| `<<else>><<[client.Name]>>` | `<<[client.Country]>>` | `<<[client.LocalAddress]>><</if>>` |
| ... | ... | ... |

You can normally use table-row conditional blocks within data bands to make elements of an enumeration look differently depending on a condition. Consider the following template:

| | | |
| --- | --- | --- |
| `<<foreach [in clients]>><<if [Country == "New Zealand"]>><<[Name]>>` | `<<[LocalAddress]>>` (two merged cells) | |
| `<<else>><<[Name]>>` | `<<[Country]>>` | `<<[LocalAddress]>><</if>><</foreach>>` |

In this case, the engine produces the report as below, the clients of New Zealand having no country cell:

| Name | Country | Local Address |
| --- | --- | --- |
| A Company | Australia | 219-241 Cleveland St, STRAWBERRY HILLS NSW 1427 |
| B Ltd. | Brazil | Avenida João Jorge, 112, ap. 31, Vila Industrial, Campinas - SP, 13035-680 |
| C & D | Canada | 101-3485 RUE DE LA MONTAGNE, MONTRÉAL (QUÉBEC) H2G 2A6 |
| E Corp. | | 445 Mount Eden Road, Mount Eden, Auckland 1024 |
| F & Partners | | 20 Greens Road, Tuahiwi, Kaiapoi 7691 |
| G & Co. | Greece | Karkisias 6, GR-111 42 ATHINA, GRÉCE |
| H Group | Hungary | Budapest, Fiktív utca 82., IV. em./28., 2806 |
| I & Sons | | 43 Vogel Street, Roslyn, Palmerston North 4414 |
| J Ent. | Japan | Hakusan 4-Chōme 3-2, Bunkyō-ku, TŌKYŌ, 112-0001, Japan |

{{< alert style="info" >}}**Note:** You can use common conditional blocks within table-row data bands as well.{{< /alert >}}

Also, you can use data bands inside table-row conditional blocks. For example, you can provide an alternate content for an empty table-row data band using the following template:

| Client | Country | Local Address |
| --- | --- | --- |
| `<<if [!clients.Any()]>>No data` | | |
| `<<else>><<foreach [in clients]>><<[Name]>>` | `<<[Country]>>` | `<<[LocalAddress]>><</foreach>><</if>>` |

In case, the corresponding enumeration is empty, the engine produces a report as below:

| Client | Country | Local Address |
| --- | --- | --- |
| No data | | |

{{< alert style="info" >}}**Note:** If tags denoting boundaries of a template option are contained within a single table cell, the option is considered to be a common template option, rather than a table-row one. That is, the option is considered to occupy contents within the cell, rather than the whole row. That is why, a single-cell alternate content in the previous example is located between an opening if and else tags, rather than between an else and closing if tags.{{< /alert >}}

For Python data, an empty `clients` list has no items to take a type from, so `Name`, `Country` and `LocalAddress` are unknown members in the `foreach` of this template, although it is never entered. Apply `DocumentAssemblyOptions.ALLOW_MISSING_MEMBERS` when the list can be empty, or see [Implicit Enumeration Determination]({{< ref "assembly/python-net/developer-guide/basic-usage/working-with-groupdocs.assembly-engine/groupdocs.assembly-engine-apis.md#implicit-enumeration-determination" >}}).
