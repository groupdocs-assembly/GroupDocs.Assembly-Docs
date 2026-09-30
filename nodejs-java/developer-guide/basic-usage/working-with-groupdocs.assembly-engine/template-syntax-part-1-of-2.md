---
id: template-syntax-part-1-of-2
url: assembly/nodejs-java/template-syntax-part-1-of-2
title: Template Syntax - Part 1 of 2
weight: 1
description: "Template tags, expressions, types, operators, lambda functions, data sources, images, links, variables and conditional blocks in GroupDocs.Assembly for Node.js via Java templates."
keywords: template syntax, template tags, expressions, conditional blocks, contextual member access, lambda functions, node.js
productName: GroupDocs.Assembly for Node.js via Java
hideChildren: False
toc: True
---
{{< alert style="info" >}}This article is the first part of the Template Syntax series of articles. For the second part, see [Template Syntax - Part 2 of 2](/assembly/nodejs-java/template-syntax-part-2-of-2/).{{< /alert >}}

GroupDocs.Assembly for Node.js via Java uses the Java assembly engine. The template syntax is the same as in GroupDocs.Assembly for Java, and template expressions are evaluated with Java types and semantics: values coming from your data are Java objects (`java.lang.String`, `java.lang.Integer`, `java.util.Date`, and so on), and you call their Java members in expressions.

## Composing Template

A typical template for the GroupDocs.Assembly engine is composed of common document contents and tags that describe the template's structure and data bindings. You can form these tags using just running text that can occupy multiple paragraphs to be more descriptive.

A tag body must meet the following requirements:

*   A tag body must be surrounded by "<<" and ">>" character sequences.
*   A tag body must contain only text nodes.
*   A tag body must not be located inside markup document nodes.

A tag body typically consists of the following elements:

*   A tag name
*   An expression surrounded by brackets
*   A set of switches available for the tag, each of which is preceded by the "-" character

```
<<tag_name [expression] -switch1 -switch2 ...>>
```

An optional comment can be written to provide a human-readable explanation.

```
<<tag_name [expression] -switch1 -switch2 ... // optional_comment >>
```

Particular tags can have additional elements. Some tags require closing counterparts. A closing tag has the "/" character that precedes its name. This tag's name must match the name of the corresponding opening tag.

```
<</tag_name>>
```

**Note:** Tag body elements are case-sensitive.

## Composing Expressions

### Using Lexical Tokens

The following table describes lexical tokens that you can use in template expressions and restrictions on these tokens' usage compared with the C# Language Specification 5.0, which the engine's expression grammar is based on.

| Token | Restrictions |
| --- | --- |
| **Keyword** | Only the following tokens are reserved as keywords: `true`, `false`, `null`, `new`, and `in` |
| **Identifier** |<ul><li>The feature of keyword escaping through the "@" character is not supported.</li><li>Unicode character escapes are not permitted in identifiers.</li></ul>|
| **Literal** | <ul><li>32-bit Unicode character escapes are not supported.</li><li>Unsigned integer and decimal literals are not permitted.</li></ul>|
| **Operator** | See [Using Operators](#using-operators) |

You can use the following identifiers that are not preceded by a member access operator in template expressions:

*   The name of a passed data source object (the name you give in `DataSourceInfo`)
*   The name of an iteration variable within its scope (see [Outputting Sequential Data](/assembly/nodejs-java/template-syntax-part-2-of-2/#outputting-sequential-data) for more information)
*   The name of a lambda function parameter within the scope of the lambda function
*   The name of a variable declared by a `var` tag (see [Using Variables](#using-variables))
*   A fully or partially qualified name of a Java type that is known by the engine (see [Setting up Known External Types](/assembly/nodejs-java/groupdocs-assembly-engine-apis/#setting-up-known-external-types) for more information)
*   The name of a member of an object that is determined as follows:
    *   Inside a data band body, the object is resolved to the innermost iteration variable.
    *   Outside a data band body, the object is resolved to a passed data source.

The feature of omitting an object identifier while accessing the object's members is also known as the contextual object member access. See [Using Contextual Object Member Access](#using-contextual-object-member-access) for more information.

### Using Types

Template expressions operate on Java types. In Node.js, the objects that reach the engine are created by the data source classes (`JsonDataSource`, `XmlDataSource`, `CsvDataSource`, `DataSet`, `DocumentTable`); plain JavaScript objects cannot be passed as data. Values read from these sources are Java values such as `String`, `Integer`, `Long`, `Double`, `Boolean`, and `Date`.

Besides the data, you can reference Java types by name in template expressions, for example, to call static methods. You can use the identifier of a public Java type in template expressions only if the following requirements are met:

*   The type is known by the engine. Aliases of simple types (`int`, `long`, `double`, `boolean`, and others) and `String` are known by default. Other types, such as `java.lang.Math` or `java.lang.Integer`, must be added to `DocumentAssembler.getKnownTypes()` (see [Setting up Known External Types](/assembly/nodejs-java/groupdocs-assembly-engine-apis/#setting-up-known-external-types)).
*   The type is not void.
*   The type does not represent an array.
*   The type is not an open or closed generic type.

The following example makes `java.lang.Math` and `java.lang.Integer` available to templates:

```javascript
const java = require('java');
java.options.push('--add-opens=java.base/java.lang=ALL-UNNAMED'); // see the note below
const groupdocs = require('@groupdocs/groupdocs.assembly');

const assembler = new groupdocs.DocumentAssembler();
assembler.getKnownTypes().add(java.findClassSync('java.lang.Math'));
assembler.getKnownTypes().add(java.findClassSync('java.lang.Integer'));
// Template: <<[Math.max(3, 7)]>> <<[Integer.parseInt("42") + 1]>>
```

{{< alert style="warning" >}}On Java 16 and later, calling methods of JDK classes in template expressions (for example, `"abc".toUpperCase()`, `name.substring(0, 4)`, or `Math.max(3, 7)`) fails with an error such as *Can not resolve method 'toUpperCase' on type 'class java.lang.String'* unless the `java.lang` package is opened to the engine. Add the JVM option `--add-opens=java.base/java.lang=ALL-UNNAMED` through `java.options` **before** requiring `@groupdocs/groupdocs.assembly`, because the JVM is started when the package is loaded. Data member access, operators and built-in extension methods such as `count()` or `sum()` work without this option. On Java 8 and 11 the option is not required.{{< /alert >}}

The engine also enables you to use anonymous types in template expressions. Such types are useful while composing expressions with grouping by multiple keys. See [Enumeration Extension Methods](/assembly/nodejs-java/template-syntax-part-2-of-2/#enumeration-extension-methods) for the examples.

#### Type Members

The GroupDocs.Assembly engine enables you to access the following public (static and instance) members of accessible Java types in template expressions:

*   Fields
*   Methods
*   Constructors

However, you can use a functional type member in template expressions only if the following additional requirements are met:

*   The functional member returns a value.
*   The functional member does not take generic type arguments.

The engine supports the following features when dealing with functional members:

*   Overload resolution according to the C# Language Specification 5.0
*   Using of parameters taking a variable number of arguments

Members of JSON objects, XML elements, CSV columns and `DataTable` fields are accessed by their names, for example, `person.Name`. See [Using Data Sources](#using-data-sources).

### Using Extension Methods

The GroupDocs.Assembly engine enables you to use the following built-in extension methods in template expressions:

*   Extension methods mimicking the ones for `IEnumerable<T>` (see [Enumeration Extension Methods](/assembly/nodejs-java/template-syntax-part-2-of-2/#enumeration-extension-methods) for more information)
*   Extension methods for iteration variables (see [Extension Methods of Iteration Variables](/assembly/nodejs-java/template-syntax-part-2-of-2/#extension-methods-of-iteration-variables) for more information)

### Using Operators

The following list contains predefined operators that the GroupDocs.Assembly engine enables you to use in template expressions.

*   **Primary:**

    ```
    x.y f(x) a[x] new
    ```

*   **Unary:**

    ```
    - ! ~ (T)x
    ```

*   **Binary:**

    ```
    * / % + - << >> < > <= >= == != & ^ | && || ??
    ```

*   **Ternary:**

    ```
    ?:
    ```

The engine follows operator precedence, associations and overload resolution rules declared in the C# Language Specification 5.0 while evaluating template expressions. This behavior normally conforms to Java. But be aware of the following limitations and differences in the behavior compared with the specification and Java behavior:

*   String equality and inequality check operators test string contents, rather than string references.
*   Whereas the object initializer syntax is supported (including objects of anonymous types), the collection initializer syntax is not.

Also, the engine enables you to use lifted operators in template expressions. In Java, operands of lifted operators are represented by primitive type class wrappers like `Integer`, `Double`, and others, in contrast to nullable types in C#. That is, for example, given that variables `a` and `b` are of the `Integer` type and the value of `a` is null, expression `a + b` is evaluated to null by the engine, whereas it throws an exception in Java during runtime.

### Using Lambda Functions

The GroupDocs.Assembly engine enables you to use lambda functions only as arguments of built-in enumeration extension methods in template expressions. See [Enumeration Extension Methods](/assembly/nodejs-java/template-syntax-part-2-of-2/#enumeration-extension-methods) for more information.

You can use both explicit and implicit lambda function signatures in template expressions. If you do not specify the type of a parameter of a lambda function explicitly, the type is determined implicitly by the engine depending on the type of the corresponding enumeration. An explicitly specified parameter type must be known by the engine; with JSON, XML, and CSV data, implicit signatures are the practical choice.

```
<<foreach [p in persons.where(p => p.Age > 30).orderBy(p => p.Name)]>><<[p.Name]>>; <</foreach>>
```

### Using Variables

You can declare a variable in a template using a `var` tag and then reference it in subsequent expressions.

```
<<var [variable_type variable_name = expression]>>
```

The variable type is optional. If it is omitted, the type is determined by the type of the expression. You can assign a new value to a declared variable using the same tag without the type. The new value must be convertible to the variable's type.

```
<<var [total = persons.sum(p => p.Salary)]>>Total: <<[total]>>
<<var [int x = 5]>><<[x * 2]>> <<var [x = x + 1]>><<[x]>>
```

For the second line, the engine produces `10 6`.

### Using Data Sources

In Node.js, you pass data to the engine using the following classes:

*   `JsonDataSource` – JSON data (see [Working with JSON Data Sources](/assembly/nodejs-java/working-with-json-data-sources/))
*   `XmlDataSource` – XML data (see [Working with XML Data Sources](/assembly/nodejs-java/working-with-xml-data-sources/))
*   `CsvDataSource` – CSV data (see [Working with CSV Data Sources](/assembly/nodejs-java/working-with-csv-data-sources/))
*   `DataSet` and `DataTable` – tabular data built in code
*   `DocumentTable` – tables extracted from documents (see [Using Documents as Data Source](/assembly/nodejs-java/using-documents-as-data-source/))

A JSON array or a repeated XML element is exposed to templates as an enumeration of objects (rows), and nested arrays become related child enumerations. Therefore the rules below for `DataSet`, `DataTable`, and row objects also apply to hierarchical JSON and XML data.

#### DataSet Objects

The GroupDocs.Assembly engine enables you to access `DataTable` objects contained within a particular `DataSet` instance by table names using the "." operator in template expressions. That is, for example, given that `ds` is a `DataSet` instance that contains a `DataTable` named "Persons", you can access the table using the following syntax.

```
ds.Persons
```

The same syntax applies to a JSON data source whose root object has several array properties. For example, given that the following JSON is passed as `ds`, you can access the cities using `ds.Cities`.

```json
{
  "Cities": [
    { "Name": "Auckland", "Persons": [ { "Name": "John Smith", "Age": 45 }, { "Name": "Jane Doe", "Age": 28 } ] },
    { "Name": "Wellington", "Persons": [ { "Name": "Mark Green", "Age": 31 } ] }
  ],
  "Date": "2026-09-30T10:00:00"
}
```

**Note:** Table names are case-insensitive.

**Note:** If the JSON root is an array, or an object whose only property is an array, the data source name refers to that array directly. For example, for `{ "Persons": [ ... ] }` passed as `ds`, use `ds.count()` or `<<foreach [p in ds]>>`, not `ds.Persons`.

#### DataTable Objects

The GroupDocs.Assembly engine enables you to treat `DataTable` objects in template expressions as enumerations of their rows. That is, you can use template expressions evaluated to such objects in `foreach` tags (see [Outputting Sequential Data](/assembly/nodejs-java/template-syntax-part-2-of-2/#outputting-sequential-data) for more information).

Also, you can normally apply enumeration extension methods (see [Enumeration Extension Methods](/assembly/nodejs-java/template-syntax-part-2-of-2/#enumeration-extension-methods) for more information) to `DataTable` objects in template expressions. For example, given that `persons` is a `DataTable` instance, you can count its rows using the following syntax.

```
persons.count()
```

#### DataTable Row Objects

The GroupDocs.Assembly engine enables you to access data associated with a particular `DataTable` row instance in template expressions using the "." operator. The following table describes which identifiers you can use to access different kinds of the data.

| Data Kind       | Identifier | Examples of Template Expressions                             |
| --------------- | ---------- | ------------------------------------------------------------ |
| **Field Value** | Field name | Given that `r` is a row that has a field named "Name", you can access the field's value using the following syntax.<br />`r.Name` |
| **Parent Row** | Parent table name | Given that `r` is a row of a `DataTable` that has a parent `DataTable` named "City", you can access the parent row of `r` using the following syntax.<br />`r.City`<br />Given that the "City" `DataTable` has a field named "Name", you can access the field's value for the parent row using the following syntax.<br />`r.City.Name` |
| **Child Rows** | Child table name | Given that `r` is a row of a `DataTable` that has a child `DataTable` named "Persons", you can access the enumeration of the child rows of `r` using the following syntax.<br />`r.Persons`<br />Given that the "Persons" `DataTable` has a field named "Age", you can count the child rows that correspond to persons over thirty years old using the following syntax.<br />`r.Persons.count(p => p.Age > 30)` |

**Note:** Field and table names are case-insensitive.

To determine parent-child relationships for a particular `DataTable` instance, the engine uses `DataRelation` objects contained within the corresponding `DataSet` instance. Thus, you can manage these relationships in a common way.

For JSON data, relations follow the nesting. With the JSON shown above, the following template outputs every person together with the name of the parent city (accessed through the parent table name `Cities`) and the number of persons over thirty in each city.

```
<<foreach [c in ds.Cities]>><<[c.Name]>>: <<[c.Persons.count(p => p.Age > 30)]>>; <</foreach>>
<<foreach [c in ds.Cities]>><<foreach [p in c.Persons]>><<[p.Name]>> (<<[p.Cities.Name]>>); <</foreach>><</foreach>>
```

The engine produces the following output.

```
Auckland: 1; Wellington: 1;
John Smith (Auckland); Jane Doe (Auckland); Mark Green (Wellington);
```

### Using Images

You can insert images to your reports dynamically using image tags. To declare a dynamically inserted image within your template, follow these steps:

1.  Add a textbox to your template at the place where you want an image to be inserted.
2.  Set common image attributes such as frame, size, and others for the textbox, making the textbox look like a blank inserted image.
3.  Specify an image tag within the textbox using the following syntax.

    ```
    <<image [image_expression]>>
    ```

The expression declared within an image tag is used by the engine to build an image to be inserted. The expression must return a value of one of the following Java types:

*   A byte array containing image data
*   An `InputStream` instance able to read image data
*   A `BufferedImage` object
*   A string containing an image URI (for example, a file path or a URL stored in your JSON or XML data)

While building a report, the following procedure is applied to an image tag:

*   The expression declared within the tag is evaluated and its result is used to form an image.
*   The corresponding textbox is filled with this image.
*   The tag is removed from the textbox.

**Note:** If the expression declared within an image tag returns a stream object, then it is closed by the engine as soon as the corresponding image is built.

By default, the engine stretches an image filling a textbox to the size of the textbox. However, you can change this behavior in the following ways:

*   To keep the size of the textbox and stretch the image within bounds of the textbox preserving the ratio of the image, use the `keepRatio` switch as follows:

    ```
    <<image [image_expression] -keepRatio>>
    ```

*   To keep the width of the textbox and change its height preserving the ratio of the image, use the `fitHeight` switch as follows:

    ```
    <<image [image_expression] -fitHeight>>
    ```

*   To keep the height of the textbox and change its width preserving the ratio of the image, use the `fitWidth` switch as follows:

    ```
    <<image [image_expression] -fitWidth>>
    ```

*   To change the size of the textbox according to the size of the image, use the `fitSize` switch as follows:

    ```
    <<image [image_expression] -fitSize>>
    ```

### Adding Combobox and Dropdown List Items Dynamically

You can dynamically add items to comboboxes and dropdown lists defined in your template by taking the following steps:

1. Add a combobox or dropdown list content control to your template at a place where you want it to appear in a result document.
2. By editing content control properties, add an `item` tag to the title of this content control using the following syntax.

```
<<item [value_expression] [display_name_expression]>>
```

Here, `value_expression` defines a value of a combobox or dropdown list item to be added dynamically. This expression is mandatory and must return a non-empty value.

In turn, `display_name_expression` defines a display name of the combobox or dropdown list item to be added. This expression is optional. If it is omitted, then during runtime, a value of `value_expression` is used as a display name as well.

**Note:** Values of both `value_expression` and `display_name_expression` can be of any types. During runtime, Java `Object.toString()` is invoked to get textual representations of these expressions' values.

While building a report, `value_expression` and `display_name_expression` are evaluated and a corresponding combobox or dropdown list item is added. A declaring `item` tag is removed then.

A single `item` tag causes addition of a single combobox or dropdown list item during runtime. You can add multiple combobox or dropdown list items using multiple `item` tags as shown in the following snippet.

```
<<item ...>><<item ...>>
```

Also, you can normally use `item` tags within data bands to add a combobox or dropdown list item per item of a data collection. For example, given that `clients` is an enumeration of objects having a field named "Name" (such as a JSON array), you can use the following template to cover such a scenario.

```
<<foreach [client in clients]>><<item [client.Name]>><</foreach>>
```

An `item` tag can also be combined with an `if` tag to add a combobox or dropdown list item depending on a condition as shown in the following snippet.

```
<<if ...>><<item ...>><</if>>
```

Existing combobox and dropdown list items are not affected by `item` tags. Thus, you can combine both ways of adding combobox and dropdown list items using a template: static and dynamic.

**Note:** While inserting a combobox or dropdown list, Microsoft Word adds a default item that has to be removed manually, if the item is unwanted.

### Using Hyperlinks

Using GroupDocs.Assembly, you can insert hyperlinks to URIs or bookmarks to your reports dynamically using link tags. The syntax of a link tag is defined below for various types of documents:

#### Word Processing and Emails

```
<<link [uri_or_bookmark_expression] [display_text_expression]>>
```

#### Spreadsheets

If the insertion of the link to cell A1 is required:

```
<<link ["A1"] ["Home"]>>
```

#### Presentations

```
<<link ["Slide1"] ["Home"]>>
```

### Using Contextual Object Member Access

You can make your templates less cumbersome using the contextual object member access feature. This feature enables you to access members of some objects without specifying the objects' identifiers in template expressions. An object to which the feature can be applied is determined depending on a context as follows:

*   Inside a data band body, the object is resolved to the innermost iteration variable.
*   Outside a data band body, the object is resolved to a passed data source.

Obviously, inside a data band body, you cannot use the feature to access members of an outer iteration variable or a passed data source object. With the exception of this restriction, you can use both contextual and common object member access syntax interchangeably depending on your needs and preferences.

Consider the following example. Given that `ds` is a data source (a `DataSet` instance, or a JSON object with several properties passed as `ds`) containing a table named "Persons" that has fields named "Name" and "Age", you can use the following template to list the contents of the table.

| No. | Name | Age |
| --- | --- | --- |
|`<<foreach [p in ds.Persons]>><<[p.numberOf()]>>`|`<<[p.Name]>>`|`<<[p.Age]>><</foreach>>`|
|`Count: <<[ds.Persons.count()]>>`| | |

Alternatively, you can use the following template involving the contextual object member access syntax to get the same results.

| No. | Name | Age |
| --- | --- | --- |
|`<<foreach [in Persons]>><<[numberOf()]>>`|`<<[Name]>>`|`<<[Age]>><</foreach>>`|
|`Count: <<[Persons.count()]>>`| | |

### Using Conditional Blocks

You can use different document blocks to represent the same data depending on a condition with the help of conditional blocks. A conditional block represents a set of template options, each of which is bound with a conditional expression. At runtime, these conditional expressions are sequentially evaluated, until an expression that returns true is reached. Then, the conditional block is replaced with the corresponding template option populated with data.

A conditional block can have a default template option that is not bound with a conditional expression. At runtime, this template option is used when none of the conditional expressions return true. If a default template option is missing and none of the conditional expressions return true, then the whole conditional block is removed during runtime.

You can use the following syntax to declare a conditional block:

```
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

A common conditional block is a conditional block whose body starts and ends within paragraphs that belong to a single story or table cell.

If a conditional block belongs to a single paragraph, it can be used as a replacement for an expression tag that involves the ternary "?:" operator. For example, given that `items` is an enumeration, you can use the following template to represent the count of elements in the enumeration:

```
You have chosen <<if [!items.any()]>>no items<<else>><<[items.count()]>> item(s)<</if>>.
```

**Note:** A template option of a common conditional block can be composed of multiple paragraphs, if needed.

You can normally use common conditional blocks within data bands. For example, given that `items` is an enumeration of the strings "item1", "item2", and "item3" (see [Common Data Bands](/assembly/nodejs-java/template-syntax-part-2-of-2/#common-data-bands) for how to get such an enumeration from JSON), you can use the following template to enumerate them and apply different formatting for even and odd elements (the formatting is applied to the text in the template document):

```
<<foreach [item in items]>><<if [item.indexOf() % 2 == 0]>><<[item]>>
<<else>><<[item]>>
<</if>><</foreach>>
```

In this case, the engine produces a report as follows:

```
item1
item2
item3
```

You can use data bands within common conditional blocks as well. For example, given the previous declaration of `items`, you can check whether the enumeration contains any elements before outputting their list:

```
<<if [!items.any()]>>No data.
<<else>><<foreach [item in items]>><<[item]>>
<</foreach>><</if>>
```

#### Table-Row Conditional Blocks

A table-row conditional block is a conditional block whose body occupies single or multiple rows of a single document table. The body of such a block (as well as the body of its every template option) starts at the beginning of the first occupied row and ends at the end of the last occupied row as follows.

**Note:** Table rows occupied by different template options in the following template are highlighted with different colors.

<table>
<tbody>
<tr><td>&nbsp;</td><td>&nbsp;</td><td>&nbsp;</td></tr>
<tr style="background-color: #e2efd9;"><td><code>&lt;&lt;if ...&gt;&gt; ...</code></td><td>...</td><td>...</td></tr>
<tr style="background-color: #e2efd9;"><td>...</td><td>...</td><td>...</td></tr>
<tr style="background-color: #fff2cc;"><td><code>&lt;&lt;elseif ...&gt;&gt; ...</code></td><td>...</td><td>...</td></tr>
<tr style="background-color: #fff2cc;"><td>...</td><td>...</td><td>...</td></tr>
<tr style="background-color: #deeaf6;"><td><code>&lt;&lt;else&gt;&gt; ...</code></td><td>...</td><td>...</td></tr>
<tr style="background-color: #deeaf6;"><td>...</td><td>...</td><td>...</td></tr>
<tr style="background-color: #deeaf6;"><td>...</td><td>...</td><td><code>... &lt;&lt;/if&gt;&gt;</code></td></tr>
<tr><td>&nbsp;</td><td>&nbsp;</td><td>&nbsp;</td></tr>
</tbody>
</table>

The following examples in this section use `client`, a single client object, and `clients`, an enumeration of client objects. In Node.js, such data typically comes from JSON like the following one (passed as `clients`):

```json
[
  { "Name": "A Company", "Country": "Australia", "LocalAddress": "219-241 Cleveland St, STRAWBERRY HILLS NSW 1427" },
  { "Name": "E Corp.", "Country": "New Zealand", "LocalAddress": "445 Mount Eden Road, Mount Eden, Auckland 1024" },
  { "Name": "G & Co.", "Country": "Greece", "LocalAddress": "Karkisias 6, GR-111 42 ATHINA" }
]
```

Using table-row conditional blocks, you can pick a single row to output among several rows of a single document table depending on a condition, like in the following example:

<table>
<tbody>
<tr><td>...</td><td>...</td><td>...</td></tr>
<tr style="background-color: #e2efd9;"><td><code>&lt;&lt;if [client.Country == "New Zealand"]&gt;&gt;&lt;&lt;[client.Name]&gt;&gt;</code></td><td colspan="2"><code>&lt;&lt;[client.LocalAddress]&gt;&gt;</code></td></tr>
<tr style="background-color: #f2f2f2;"><td><code>&lt;&lt;else&gt;&gt;&lt;&lt;[client.Name]&gt;&gt;</code></td><td><code>&lt;&lt;[client.Country]&gt;&gt;</code></td><td><code>&lt;&lt;[client.LocalAddress]&gt;&gt;&lt;&lt;/if&gt;&gt;</code></td></tr>
<tr><td>...</td><td>...</td><td>...</td></tr>
</tbody>
</table>

You can normally use table-row conditional blocks within data bands to make elements of an enumeration look different depending on a condition. Consider the following template:

<table>
<tbody>
<tr style="background-color: #e2efd9;"><td><code>&lt;&lt;foreach [in clients]&gt;&gt;&lt;&lt;if [Country == "New Zealand"]&gt;&gt;&lt;&lt;[Name]&gt;&gt;</code></td><td colspan="2"><code>&lt;&lt;[LocalAddress]&gt;&gt;</code></td></tr>
<tr style="background-color: #f2f2f2;"><td><code>&lt;&lt;else&gt;&gt;&lt;&lt;[Name]&gt;&gt;</code></td><td><code>&lt;&lt;[Country]&gt;&gt;</code></td><td><code>&lt;&lt;[LocalAddress]&gt;&gt;&lt;&lt;/if&gt;&gt;&lt;&lt;/foreach&gt;&gt;</code></td></tr>
</tbody>
</table>

In this case, the engine produces the report as below (the New Zealand client occupies a row with a merged address cell):

<table>
<tbody>
<tr><td>A Company</td><td>Australia</td><td>219-241 Cleveland St, STRAWBERRY HILLS NSW 1427</td></tr>
<tr><td>E Corp.</td><td colspan="2">445 Mount Eden Road, Mount Eden, Auckland 1024</td></tr>
<tr><td>G &amp; Co.</td><td>Greece</td><td>Karkisias 6, GR-111 42 ATHINA</td></tr>
</tbody>
</table>

{{< alert style="info" >}}You can use common conditional blocks within table-row data bands as well.{{< /alert >}}

Also, you can use data bands inside table-row conditional blocks. For example, you can provide an alternate content for an empty table-row data band using the following template:

<table>
<tbody>
<tr><td><b>Client</b></td><td><b>Country</b></td><td><b>Local Address</b></td></tr>
<tr><td colspan="3"><code>&lt;&lt;if [!clients.any()]&gt;&gt;No data</code></td></tr>
<tr><td><code>&lt;&lt;else&gt;&gt;&lt;&lt;foreach [in clients]&gt;&gt;&lt;&lt;[Name]&gt;&gt;</code></td><td><code>&lt;&lt;[Country]&gt;&gt;</code></td><td><code>&lt;&lt;[LocalAddress]&gt;&gt;&lt;&lt;/foreach&gt;&gt;&lt;&lt;/if&gt;&gt;</code></td></tr>
</tbody>
</table>

In case the corresponding enumeration is empty, the engine produces a report as below:

<table>
<tbody>
<tr><td><b>Client</b></td><td><b>Country</b></td><td><b>Local Address</b></td></tr>
<tr><td colspan="3">No data</td></tr>
</tbody>
</table>

{{< alert style="info" >}}If tags denoting boundaries of a template option are contained within a single table cell, the option is considered to be a common template option, rather than a table-row one. That is, the option is considered to occupy contents within the cell, rather than the whole row. That is why a single-cell alternate content in the previous example is located between the opening `if` and `else` tags, rather than between the `else` and closing `if` tags.{{< /alert >}}
