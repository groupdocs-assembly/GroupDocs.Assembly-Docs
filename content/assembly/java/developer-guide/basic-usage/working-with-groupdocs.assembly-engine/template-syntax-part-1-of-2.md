---
id: template-syntax-part-1-of-2
url: assembly/java/template-syntax-part-1-of-2
title: Template Syntax - Part 1 of 2
weight: 1
description: ""
keywords: 
productName: GroupDocs.Assembly for Java
hideChildren: False
---
{{< alert style="info" >}}This article is the first part of the Template Syntax series of articles. For second part, please visit Template Syntax - Part 2 of 2.{{< /alert >}}

## Composing Template

A typical template for [GroupDocs.Assembly](https://apireference.groupdocs.com/java/assembly/com.groupdocs.assembly/package-frame) Engine is composed of common document contents and tags that describe the template's structure and data bindings. You can form these tags using just running text that can occupy multiple paragraphs to be more descriptive.

A tag body must meet the following requirements:

*   A tag body must be surrounded by "<<" and ">>" character sequences.
*   A tag body must contain only text nodes.
*   A tag body must not be located inside markup document nodes.

A tag body typically consists of the following elements:

*   A tag name
*   An expression surrounded by brackets
*   A set of switches available for the tag, each of which is preceded by the "-" character

```java
<<tag_name [expression] -switch1 -switch2 ...>>
```

An optional comment can be written to provide a human-readable explanation.

```java
<<tag_name [expression] –switch1 –switch2 ... // optional_comment >>
```

{{< alert style="warning" >}}The optional comment feature is supported by version 19.1 or greater{{< /alert >}}

Particular tags can have additional elements. Some tags require closing counterparts. A closing tag has the "/" character that precedes its name. This tag's name must match to the name of the corresponding opening tag.

```java
<</tag_name>>
```

**Note:** Tag body elements are case-sensitive.

## Composing Expressions

### Using Lexical Tokens

The following table describes lexical tokens that you can use in template expressions and restrictions on these tokens' usage comparing with [C# Language Specification 5.0](http://www.microsoft.com/en-us/download/details.aspx?id=7029).

| Token | Restrictions |
| --- | --- |
| **Keyword** | Only the following tokens are reserved as keywords: `true`, `false`, `null`, `new`, and `in` |
| **Identifier** |<ul><br/>	<li>The feature of keyword escaping through the "@" character is not supported.</li><br/>	<li>Unicode character escapes are not permitted in identifiers.</li><br/></ul>|
| **Literal** | <ul><br/>	<li>32-bit Unicode character escapes are not supported</li><br/>	<li>Unsigned integer and decimal literals are not permitted</li><br/></ul>|
| **Operator** | See [Using Operators](https://docs.groupdocs.com/assembly/java/template-syntax-part-1-of-2/#using-operators) |

You can use the following identifiers that are not preceded by a member access operator in template expressions:

*   The name of a passed data source object
*   The name of an iteration variable within its scope (see [Outputting Sequential Data](https://docs.groupdocs.com/assembly/java/template-syntax-part-2-of-2/#outputting-sequential-data) for more information)
*   The name of a lambda function parameter within the scope of the lambda function
*   A fully or partially qualified name of a type that is known by the engine (see [Setting up Known External Types](https://docs.groupdocs.com/assembly/java/groupdocs-assembly-engine-apis/#setting-up-known-external-types) for more information)
*   The name of a member of an object that is determined as follows:
    *   Inside a data band body, the object is resolved to the innermost iteration variable.
    *   Outside a data band body, the object is resolved to a passed data source.

The feature of the omitting of an object identifier while accessing the object's members is also known as the contextual object member access. See [Using Contextual Object Member Access](https://docs.groupdocs.com/assembly/java/template-syntax-part-1-of-2/#using-contextual-object-member-access) for more information.

### Using Types

[GroupDocs.Assembly](https://apireference.groupdocs.com/java/assembly/com.groupdocs.assembly/package-frame) Engine enables you to use external visible types in template expressions. A `visible type` is a public type with outer types (if any) are public as well. You can use a data source object of any visible type to pass it to the engine.

However, you can use the identifier of a visible type in template expressions only if the following additional requirements are met:

*   The type is not void.
*   The type does not represent an array.
*   The type is not an open or closed generic type.

Also, the engine enables you to use anonymous types in template expressions. Such types are useful while composing expressions with grouping by multiple keys. See [Enumeration Extension Methods](https://docs.groupdocs.com/assembly/java/template-syntax-part-2-of-2/#enumeration-extension-methods) for the examples.

#### Type Members

GroupDocs.Assembly Engine enables you to access the following public (static and instance) members of accessible types in template expressions:

*   Fields
*   Methods
*   Constructors

However, you can use a functional type member in template expressions only if the following additional requirements are met:

*   The functional member returns a value.
*   The functional member does not take generic type arguments.

The engine supports the following features when dealing with functional members:

*   Overload resolution according to [C# Language Specification 5.0](http://www.microsoft.com/en-us/download/details.aspx?id=7029)
*   Using of parameters taking a variable number of arguments

### Using Extension Methods

GroupDocs.Assembly Engine enables you to use the following built-in extension methods in template expressions:

*   Extension methods mimicking the ones for `IEnumerable<T>` (see [Enumeration Extension Methods](https://docs.groupdocs.com/assembly/java/template-syntax-part-2-of-2/#enumeration-extension-methods) for more information)
*   Extension methods for iteration variables (see [Extension Methods of Iteration Variables](https://docs.groupdocs.com/assembly/java/template-syntax-part-2-of-2/#extension-methods-of-iteration-variables) for more information)

### Using Operators

The following list contains predefined operators that GroupDocs.Assembly Engine enables you to use in template expressions.

*   **Primary:**
  
    ```java
    x.y f(x) a[x] new
    ```
    
*   **Unary:**
  
    ```java
    - ! ~ (T)x
    ```
    
*   **Binary:**
  
    ```java
    * / % + - << >> < > <= >= == != & ^ | && || ??
    ```
    
*   **Ternary:**
  
    ```java
    ?:
    ```
    

The engine follows operator precedence, associations and overload resolution rules declared at [C# Language Specification 5.0](http://www.microsoft.com/en-us/download/details.aspx?id=7029) while evaluating template expressions. This behavior normally conforms to Java. But be aware of the following limitations and differences in the behavior comparing with the specification and Java behavior:

*   String equality and inequality check operators test string contents, rather than string references.
*   Whereas the object initializer syntax is supported (including objects of anonymous types), the collection initializer syntax is not.

Also, the engine enables you to use lifted operators in template expressions. In Java, operands of lifted operators are represented by primitive type class wrappers like Integer, Double, and others, in contrast to nullable types in C#. That is, for example, given that variables a and b are of the Integer type and the value of a is null, expression "a + b" is evaluated to null by the engine, whereas it throws an exception in Java during runtime.

### Using Lambda Functions

GroupDocs.Assembly Engine enables you to use lambda functions only as arguments of built-in enumeration extension methods in template expressions. See [Enumeration Extension Methods](https://docs.groupdocs.com/assembly/java/template-syntax-part-2-of-2/#enumeration-extension-methods) for more information.

You can use both explicit and implicit lambda function signatures in template expressions. If you do not specify the type of a parameter of a lambda function explicitly, the type is determined implicitly by the engine depending on the type of the corresponding enumeration.

### Using Data Sources

#### DataSet Objects

{{< alert style="info" >}}This link will explain you how we utilized the DataSet Objects in Business Layer.{{< /alert >}}

GroupDocs.Assembly Engine enables you to access `DataTable` objects contained within a particular `DataSet` instance by table names using the "." operator in template expressions. That is, for example, given that `ds` is a `DataSet` instance that contains a `DataTable` named "Persons", you can access the table using the following syntax.

```java
ds.Persons
```

**Note** Table names are case-insensitive.

#### DataTable Objects

GroupDocs.Assembly Engine enables you to treat [`DataTable`](https://apireference.groupdocs.com/java/assembly/com.groupdocs.assembly.system.data/DataTable) objects in template expressions as enumerations of their rows. That is, you can use template expressions evaluated to such objects in `foreach` tags (see [Outputting Sequential Data](https://docs.groupdocs.com/assembly/java/template-syntax-part-2-of-2/#outputting-sequential-data) for more information).

Also, you can normally apply enumeration extension methods (see [Enumeration Extension Methods](https://docs.groupdocs.com/assembly/java/template-syntax-part-2-of-2/#enumeration-extension-methods) for more information) to `DataTable` objects in template expressions. For example, given that persons is a `DataTable` instance, you can count its rows using the following syntax.

```java
persons.count()
```

#### DataTable Row Objects

GroupDocs.Assembly Engine enables you to access a data associated with a particular [`DataTable`](https://apireference.groupdocs.com/java/assembly/com.groupdocs.assembly.system.data/DataTable) row instance in template expressions using the "." operator. The following table describes, which identifiers you can use to access different kinds of the data.

| Data Kind       | Identifier | Examples of Template Expressions                             |
| --------------- | ---------- | ------------------------------------------------------------ |
| **Field Value** | Field name | Given that r is a row that has a field named "Name", you can access the field's value using the following syntax.<br />`r.Name` |
| **Parent Row** | Parent table name | Given that r is a row of a DataTable that has a parent DataTable named "City", you can access the parent row of r using the following syntax.<br />`r.City`<br />Given that the "City" DataTable has a field named "Name", you can access the field's value for the parent row using the following syntax.<br />`r.City.Name` |
| **Child Rows** | Child table name | Given that r is a row of a DataTable that has a child DataTable named "Persons", you can access the enumeration of the child rows of r using the following syntax.<br />`r.Persons`<br />Given that the "Persons" DataTable has a field named "Age", you can count the child rows that correspond to persons over thirty years old using the following syntax.<br />`r.Persons.count(p => p.Age > 30)` |


**Note:** Field and table names are case-insensitive.

To determine parent-child relationships for a particular `DataTable` instance, the engine uses [DataRelation](https://apireference.groupdocs.com/java/assembly/com.groupdocs.assembly.system.data/DataRelation) objects contained within the corresponding [`DataSet`](https://apireference.groupdocs.com/java/assembly/com.groupdocs.assembly.system.data/DataSet) instance. Thus, you can manage these relationships in a common way.

### Using Images

{{< alert style="info" >}}See Common List with Image template using images in it.{{< /alert >}}

You can insert images to your reports dynamically using image tags. To declare a dynamically inserted image within your template, please follow these steps:

1.  Add a textbox to your template at the place where you want an image to be inserted.
2.  Set common image attributes such as frame, size, and others for the textbox, making the textbox look like a blank inserted image.
3.  Specify an image tag within the textbox using the following syntax.
  
    ```java
    <<image [image_expression]>>
    ```
    

The expression declared within an image tag is used by the engine to build an image to be inserted. The expression must return a value of one of the following types:

*   A byte array containing an image data
*   An InputStream instance able to read an image data
*   A BufferedImage object
*   A string containing an image URI

While building a report, the following procedure is applied to an image tag:

*   The expression declared within the tag is evaluated and its result is used to form an image.
*   The corresponding textbox is filled with this image.
*   The tag is removed from the textbox.

**Note:** If the expression declared within an image tag returns a stream object, then it is closed by the engine as soon as the corresponding image is built.

By default, the engine stretches an image filling a textbox to the size of the textbox. However, you can change this behavior in the following ways:

*   To keep the size of the textbox and stretch the image within bounds of the textbox preserving the ratio of the image, use the *keepRatio* switch as follows:
  ```java
    <<image [image_expression] -keepRatio>>
  ```
  
*   To keep the width of the textbox and change its height preserving the ratio of the image, use the fitHeight switch as follows:
  ```java
    <<image [image_expression] -fitHeight>>
  ```
  
*   To keep the height of the textbox and change its width preserving the ratio of the image, use the fitWidth switch as follows:
  
    ```java
    <<image [image_expression] -fitWidth>>
    ```
    
* To change the size of the textbox according to the size of the image, use the fitSize switch as follows:

    ```java
    <<image [image_expression] -fitSize>>
    ```

### Adding Combobox and Dropdown List Items Dynamically

You can dynamically add items to comboboxes and dropdown lists defined in your template by taking the following steps:

1. Add a combobox or dropdown list content control to your template at a place where you want it to appear in a result document.
2. By editing content control properties, add an `item` tag to the title of this content control using the following syntax.

```java
<<item [value_expression] [display_name_expression]>>
```

Here, `value_expression` defines a value of a combobox or dropdown list item to be added dynamically. This expression is mandatory and must return a non-empty value.

In turn, `display_name_expression` defines a display name of the combobox or dropdown list item to be added. This expression is optional. If it is omitted, then during runtime, a value of `value_expression` is used as a display name as well.

**Note –** Values of both `value_expression` and `display_name_expression` can be of any types. During runtime, `Object.toString()` is invoked to get textual representations of these expressions’ values.

While building a report, `value_expression` and `display_name_expression` are evaluated and a corresponding combobox or dropdown list item is added. A declaring `item` tag is removed then.

A single `item` tag causes addition of a single combobox or dropdown list item during runtime. You can add multiple combobox or dropdown list items using multiple `item` tags as shown in the following snippet.

```java
<<item ...>><<item ...>>
```

Also, you can normally use `item` tags within data bands to add a combobox or dropdown list item per item of a data collection. For example, given that `clients` is a `DataTable` instance having a field named “Name”, you can use the following template to cover such a scenario.

```java
<<foreach [client in clients]>><<item [client.Name]>><</foreach>>
```

An `item` tag can also be combined with an `if` tag to add a combobox or dropdown list item depending on a condition as shown in the following snippet.

```java
<<if ...>><<item ...>><</if>>
```

Existing combobox and dropdown list items are not affected by `item` tags. Thus, you can combine both ways of adding combobox and dropdown list items using a template: static and dynamic.

**Note –** While inserting a combobox or dropdown list, Microsoft Word adds a default item that has to be removed manually, if the item is unwanted.

### Using Hyperlinks 

Using GroupDocs.Assembly, you can insert hyperlinks to URI or Bookmarks to your reports dynamically using link tags. The syntax of a link tag is defined below for various types of documents:

#### Word Processing and Emails

```java
<<link [uri_or_bookmark_expression][display_text_expression]>>
```

#### Spreadsheets

If the insertion of the link to cell A1 is required: 

```java
<<link ["A1"] ["Home"]>>
```

#### Presentations

```java
<<link ["Slide1"] ["Home"]>>
```

### Using Contextual Object Member Access

{{< alert style="info" >}}See [In-Table List with Filtering, Grouping, and Ordering](https://docs.groupdocs.com/assembly/java/in-table-list-with-filtering-grouping-and-ordering-in-word-processing-document/#adding-syntax-to-be-evaluated-by-groupdocsassembly-engine) template Contextual Object Member Access in it.{{< /alert >}}

You can make your templates less cumbersome using the contextual object member access feature. This feature enables you to access members of some objects without specifying the objects' identifiers in template expressions. An object to which the feature can be applied is determined depending on a context as follows:

*   Inside a data band body, the object is resolved to the innermost iteration variable.
*   Outside a data band body, the object is resolved to a passed data source.

Obviously, inside a data band body, you can not use the feature to access members of an outer iteration variable or a passed data source object. With the exception of this restriction, you can use both contextual and common object member access syntax interchangeably depending on your needs and preferences.

Consider the following example. Given that `ds` is a `DataSet` instance containing a `DataTable` object named "Persons" that has fields named "Name" and "Age", you can use the following template to list the contents of the table.

| No. | Name | Age |
| --- | --- | --- |
|`<<foreach [p in ds.Persons]>><<[p.numberOf()]>>`|`<<[p.Name]>>`|`<<[p.Age]>><</foreach>>`|
|`Count: <<[ds.Persons.count()]>>`| | |

Alternatively, you can use the following template involving the contextual object member access syntax to get the same results.

| No. | Name | Age |
| --- | --- | --- |
|`<<foreach [in Persons]>><<[numberOf()]>>`|`<<[Name]>>`|`<<[Age]>><</foreach>> `|
|`Count: <<[Persons.count()]>> `| | |

### Using Conditional Blocks

You can use different document blocks to represent the same data depending on a condition with the help of conditional blocks. A conditional block represents a set of template options, each of which is bound with a conditional expression. At runtime, these conditional expressions are sequentially evaluated, until an expression that returns true is reached. Then, the conditional block is replaced with the corresponding template option populated with data.

A conditional block can have a default template option that is not bound with a conditional expression. At runtime, this template option is used, when none of conditional expressions return true. If a default template option is missing and none of conditional expressions return true, then the whole conditional block is removed during runtime.

You can use the following syntax to declare a conditional block:

```java
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

{{< alert style="info" >}}See [Multicolored Numbered List](https://docs.groupdocs.com/assembly/java/multicolored-numbered-list-in-word-processing-document/#adding-syntax-to-be-evaluated-by-groupdocsassembly-engine) template using Common Conditional Blocks in it.{{< /alert >}}

A common conditional block is a conditional block which body starts and ends within paragraphs that belong to a single story or table cell.
If a conditional block belongs to a single paragraph, it can be used as a replacement for an expression tag that involves the ternary "?:" operator. For example, given that items is an enumeration, you can use the following template to represent the count of elements in the enumeration:

```java
You have chosen <<if [!items.any()]>>no items<<else>><<[items.count()]>> item(s)<</if>>.
```

**Note:** A template option of a common conditional block can be composed of multiple paragraphs, if needed.

You can normally use common conditional blocks within data bands. For example, given that items is an enumeration of the strings "item1", "item2", and "item3", you can use the following template to enumerate them and apply different formatting for even and odd elements:

```java
<<foreach [item in items]>><<if [indexOf() % 2 == 0]>><<[item]>>
<<else>><<[item]>>
<</if>><</foreach>>
```

In this case, the engine produces a report as follows:
```
item1  
item2  
item3
```

You can use data bands within common conditional blocks as well. For example, given the previous declaration of items, you can check whether the enumeration contains any elements before outputting their list:

```java
<<if [!items.any()]>>No data.
<<else>><<foreach [item in items]>><<[item]>>
<</foreach>><</if>>
```

#### Table-Row Conditional Block

{{< alert style="info" >}}See [In-Table List with Highlighted Rows](https://docs.groupdocs.com/assembly/java/in-table-list-with-highlighted-rows-in-word-processing-document/#adding-syntax-to-be-evaluated-by-groupdocsassembly-engine) template using Table-Row Conditional Block.{{< /alert >}}

A table-row conditional block is a conditional block which body occupies single or multiple rows of a single document table. The body of such a block (as well as the body of its every template option) starts at the beginning of the first occupied row and ends at the end of the last occupied row as follows:  
**Note:** Table rows occupied by different template options in the following template are highlighted with different colors.

td { border-bottom-color: rgb(0, 0, 0); border-bottom-style: solid; border-bottom-width: 0.75pt; border-left-color: rgb(0, 0, 0); border-left-style: solid; border-left-width: 0.75pt; border-right-color: rgb(0, 0, 0); border-right-style: solid; border-right-width: 0.75pt; border-top-color: rgb(0, 0, 0); border-top-style: solid; border-top-width: 0.75pt; padding-left: 5.03pt; padding-right: 5.03pt; vertical-align: top; }

<table cellspacing="0" cellpadding="0" style="border-collapse: collapse; margin-left: 0pt;"><tbody><tr><td style="background-color: rgb(242, 242, 242);"><p style="margin-top: 0pt; margin-right: 0pt; margin-bottom: 0pt; margin-left: 0pt;"><span style="color: rgb(127, 127, 127); font-family: &quot;Courier New&quot;; font-size: 11pt; font-weight: bold;">&nbsp;</span></p></td><td style="background-color: rgb(242, 242, 242);"><p style="margin-top: 0pt; margin-right: 0pt; margin-bottom: 0pt; margin-left: 0pt;"><span style="color: rgb(127, 127, 127); font-family: &quot;Courier New&quot;; font-size: 11pt; font-weight: bold;">&nbsp;</span></p></td><td style="background-color: rgb(242, 242, 242);"><p style="margin-top: 0pt; margin-right: 0pt; margin-bottom: 0pt; margin-left: 0pt;"><span style="color: rgb(127, 127, 127); font-family: &quot;Courier New&quot;; font-size: 11pt; font-weight: bold;">&nbsp;</span></p></td></tr><tr><td style="background-color: rgb(226, 239, 217);"><p style="margin-top: 0pt; margin-right: 0pt; margin-bottom: 0pt; margin-left: 0pt;"><span style="color: rgb(127, 127, 127); font-family: &quot;Courier New&quot;; font-size: 11pt; font-weight: bold;">&lt;&lt;if ...&gt;&gt; ...</span></p></td><td style="background-color: rgb(226, 239, 217);"><p style="margin-top: 0pt; margin-right: 0pt; margin-bottom: 0pt; margin-left: 0pt;"><span style="color: rgb(127, 127, 127); font-family: &quot;Courier New&quot;; font-size: 11pt; font-weight: bold;">...</span></p></td><td style="background-color: rgb(226, 239, 217);"><p style="margin-top: 0pt; margin-right: 0pt; margin-bottom: 0pt; margin-left: 0pt;"><span style="color: rgb(127, 127, 127); font-family: &quot;Courier New&quot;; font-size: 11pt; font-weight: bold;">...</span></p></td></tr><tr><td style="background-color: rgb(226, 239, 217);"><p style="margin-top: 0pt; margin-right: 0pt; margin-bottom: 0pt; margin-left: 0pt;"><span style="color: rgb(127, 127, 127); font-family: &quot;Courier New&quot;; font-size: 11pt; font-weight: bold;">...</span></p></td><td style="background-color: rgb(226, 239, 217);"><p style="margin-top: 0pt; margin-right: 0pt; margin-bottom: 0pt; margin-left: 0pt;"><span style="color: rgb(127, 127, 127); font-family: &quot;Courier New&quot;; font-size: 11pt; font-weight: bold;">...</span></p></td><td style="background-color: rgb(226, 239, 217);"><p style="margin-top: 0pt; margin-right: 0pt; margin-bottom: 0pt; margin-left: 0pt;"><span style="color: rgb(127, 127, 127); font-family: &quot;Courier New&quot;; font-size: 11pt; font-weight: bold;">...</span></p></td></tr><tr><td style="background-color: rgb(255, 242, 204);"><p style="margin-top: 0pt; margin-right: 0pt; margin-bottom: 0pt; margin-left: 0pt;"><span style="color: rgb(127, 127, 127); font-family: &quot;Courier New&quot;; font-size: 11pt; font-weight: bold;">&lt;&lt;elseif ...&gt;&gt; ...</span></p></td><td style="background-color: rgb(255, 242, 204);"><p style="margin-top: 0pt; margin-right: 0pt; margin-bottom: 0pt; margin-left: 0pt;"><span style="color: rgb(127, 127, 127); font-family: &quot;Courier New&quot;; font-size: 11pt; font-weight: bold;">...</span></p></td><td style="background-color: rgb(255, 242, 204);"><p style="margin-top: 0pt; margin-right: 0pt; margin-bottom: 0pt; margin-left: 0pt;"><span style="color: rgb(127, 127, 127); font-family: &quot;Courier New&quot;; font-size: 11pt; font-weight: bold;">...</span></p></td></tr><tr><td style="background-color: rgb(255, 242, 204);"><p style="margin-top: 0pt; margin-right: 0pt; margin-bottom: 0pt; margin-left: 0pt;"><span style="color: rgb(127, 127, 127); font-family: &quot;Courier New&quot;; font-size: 11pt; font-weight: bold;">...</span></p></td><td style="background-color: rgb(255, 242, 204);"><p style="margin-top: 0pt; margin-right: 0pt; margin-bottom: 0pt; margin-left: 0pt;"><span style="color: rgb(127, 127, 127); font-family: &quot;Courier New&quot;; font-size: 11pt; font-weight: bold;">...</span></p></td><td style="background-color: rgb(255, 242, 204);"><p style="margin-top: 0pt; margin-right: 0pt; margin-bottom: 0pt; margin-left: 0pt;"><span style="color: rgb(127, 127, 127); font-family: &quot;Courier New&quot;; font-size: 11pt; font-weight: bold;">...</span></p></td></tr><tr><td style="background-color: rgb(222, 234, 246);"><p style="margin-top: 0pt; margin-right: 0pt; margin-bottom: 0pt; margin-left: 0pt;"><span style="color: rgb(127, 127, 127); font-family: &quot;Courier New&quot;; font-size: 11pt; font-weight: bold;">&lt;&lt;else&gt;&gt; ...</span></p></td><td style="background-color: rgb(222, 234, 246);"><p style="margin-top: 0pt; margin-right: 0pt; margin-bottom: 0pt; margin-left: 0pt;"><span style="color: rgb(127, 127, 127); font-family: &quot;Courier New&quot;; font-size: 11pt; font-weight: bold;">...</span></p></td><td style="background-color: rgb(222, 234, 246);"><p style="margin-top: 0pt; margin-right: 0pt; margin-bottom: 0pt; margin-left: 0pt;"><span style="color: rgb(127, 127, 127); font-family: &quot;Courier New&quot;; font-size: 11pt; font-weight: bold;">...</span></p></td></tr><tr><td style="background-color: rgb(222, 234, 246);"><p style="margin-top: 0pt; margin-right: 0pt; margin-bottom: 0pt; margin-left: 0pt;"><span style="color: rgb(127, 127, 127); font-family: &quot;Courier New&quot;; font-size: 11pt; font-weight: bold;">...</span></p></td><td style="background-color: rgb(222, 234, 246);"><p style="margin-top: 0pt; margin-right: 0pt; margin-bottom: 0pt; margin-left: 0pt;"><span style="color: rgb(127, 127, 127); font-family: &quot;Courier New&quot;; font-size: 11pt; font-weight: bold;">...</span></p></td><td style="background-color: rgb(222, 234, 246);"><p style="margin-top: 0pt; margin-right: 0pt; margin-bottom: 0pt; margin-left: 0pt;"><span style="color: rgb(127, 127, 127); font-family: &quot;Courier New&quot;; font-size: 11pt; font-weight: bold;">...</span></p></td></tr><tr><td style="background-color: rgb(222, 234, 246);"><p style="margin-top: 0pt; margin-right: 0pt; margin-bottom: 0pt; margin-left: 0pt;"><span style="color: rgb(127, 127, 127); font-family: &quot;Courier New&quot;; font-size: 11pt; font-weight: bold;">...</span></p></td><td style="background-color: rgb(222, 234, 246);"><p style="margin-top: 0pt; margin-right: 0pt; margin-bottom: 0pt; margin-left: 0pt;"><span style="color: rgb(127, 127, 127); font-family: &quot;Courier New&quot;; font-size: 11pt; font-weight: bold;">...</span></p></td><td style="background-color: rgb(222, 234, 246);"><p style="margin-top: 0pt; margin-right: 0pt; margin-bottom: 0pt; margin-left: 0pt;"><span style="color: rgb(127, 127, 127); font-family: &quot;Courier New&quot;; font-size: 11pt; font-weight: bold;">... &lt;&lt;/if&gt;&gt;</span></p></td></tr><tr><td style="background-color: rgb(242, 242, 242);"><p style="margin-top: 0pt; margin-right: 0pt; margin-bottom: 0pt; margin-left: 0pt;"><span style="color: rgb(127, 127, 127); font-family: &quot;Courier New&quot;; font-size: 11pt; font-weight: bold;">&nbsp;</span></p></td><td style="background-color: rgb(242, 242, 242);"><p style="margin-top: 0pt; margin-right: 0pt; margin-bottom: 0pt; margin-left: 0pt;"><span style="color: rgb(127, 127, 127); font-family: &quot;Courier New&quot;; font-size: 11pt; font-weight: bold;">&nbsp;</span></p></td><td style="background-color: rgb(242, 242, 242);"><p style="margin-top: 0pt; margin-right: 0pt; margin-bottom: 0pt; margin-left: 0pt;"><span style="color: rgb(127, 127, 127); font-family: &quot;Courier New&quot;; font-size: 11pt; font-weight: bold;">&nbsp;</span></p></td></tr></tbody></table>
The following examples in this section are given using client, an instance of the Client class, and clients, an enumeration of instances of the Client class that is defined as follows:

```java
public class Client
{
    public String getName { ... }
    public String getCountry { ... }
    public String getLocalAddress { ... }
    ...
}
```

Using table-row conditional blocks, you can pick to output a single row among several rows of a single document table depending on a condition like in the following example:

<table cellspacing="0" cellpadding="0" style="border-collapse: collapse; margin-left: 0pt;"><tbody><tr><td style="background-color: rgb(242, 242, 242);"><p style="margin-top: 0pt; margin-right: 0pt; margin-bottom: 0pt; margin-left: 0pt;"><span style="color: rgb(127, 127, 127); font-family: &quot;Courier New&quot;; font-size: 11pt; font-weight: bold;">...</span></p></td><td style="background-color: rgb(242, 242, 242);"><p style="margin-top: 0pt; margin-right: 0pt; margin-bottom: 0pt; margin-left: 0pt;"><span style="color: rgb(127, 127, 127); font-family: &quot;Courier New&quot;; font-size: 11pt; font-weight: bold;">...</span></p></td><td style="background-color: rgb(242, 242, 242);"><p style="margin-top: 0pt; margin-right: 0pt; margin-bottom: 0pt; margin-left: 0pt;"><span style="color: rgb(127, 127, 127); font-family: &quot;Courier New&quot;; font-size: 11pt; font-weight: bold;">...</span></p></td></tr><tr><td style="background-color: rgb(226, 239, 217);"><p style="margin-top: 0pt; margin-right: 0pt; margin-bottom: 0pt; margin-left: 0pt;"><span style="color: rgb(127, 127, 127); font-family: &quot;Courier New&quot;; font-size: 11pt; font-weight: bold;">&lt;&lt;if [client.</span><span style="color: rgb(127, 127, 127); font-family: &quot;Courier New&quot;; font-size: 11pt; font-weight: bold;">getCountry</span><span style="color: rgb(127, 127, 127); font-family: &quot;Courier New&quot;; font-size: 11pt; font-weight: bold;"> == "New Zealand"]&gt;&gt;&lt;&lt;[client.</span><span style="color: rgb(127, 127, 127); font-family: &quot;Courier New&quot;; font-size: 11pt; font-weight: bold;">getName</span><span style="color: rgb(127, 127, 127); font-family: &quot;Courier New&quot;; font-size: 11pt; font-weight: bold;">]&gt;&gt;</span></p></td><td colspan="2" style="background-color: rgb(226, 239, 217);"><p style="margin-top: 0pt; margin-right: 0pt; margin-bottom: 0pt; margin-left: 0pt;"><span style="color: rgb(127, 127, 127); font-family: &quot;Courier New&quot;; font-size: 11pt; font-weight: bold;">&lt;&lt;[client.</span><span style="color: rgb(127, 127, 127); font-family: &quot;Courier New&quot;; font-size: 11pt; font-weight: bold;">getLocalAddress</span><span style="color: rgb(127, 127, 127); font-family: &quot;Courier New&quot;; font-size: 11pt; font-weight: bold;">]&gt;&gt;</span></p></td></tr><tr><td style="background-color: rgb(242, 242, 242);"><p style="margin-top: 0pt; margin-right: 0pt; margin-bottom: 0pt; margin-left: 0pt;"><span style="color: rgb(127, 127, 127); font-family: &quot;Courier New&quot;; font-size: 11pt; font-weight: bold;">&lt;&lt;else&gt;&gt;</span><span style="color: rgb(127, 127, 127); font-family: &quot;Courier New&quot;; font-size: 11pt; font-weight: bold;">&lt;&lt;[client.</span><span style="color: rgb(127, 127, 127); font-family: &quot;Courier New&quot;; font-size: 11pt; font-weight: bold;">getName</span><span style="color: rgb(127, 127, 127); font-family: &quot;Courier New&quot;; font-size: 11pt; font-weight: bold;">]&gt;&gt;</span></p></td><td style="background-color: rgb(242, 242, 242);"><p style="margin-top: 0pt; margin-right: 0pt; margin-bottom: 0pt; margin-left: 0pt;"><span style="color: rgb(127, 127, 127); font-family: &quot;Courier New&quot;; font-size: 11pt; font-weight: bold;">&lt;&lt;[client.</span><span style="color: rgb(127, 127, 127); font-family: &quot;Courier New&quot;; font-size: 11pt; font-weight: bold;">getCountry</span><span style="color: rgb(127, 127, 127); font-family: &quot;Courier New&quot;; font-size: 11pt; font-weight: bold;">]&gt;&gt;</span></p></td><td style="background-color: rgb(242, 242, 242);"><p style="margin-top: 0pt; margin-right: 0pt; margin-bottom: 0pt; margin-left: 0pt;"><span style="color: rgb(127, 127, 127); font-family: &quot;Courier New&quot;; font-size: 11pt; font-weight: bold;">&lt;&lt;[client.</span><span style="color: rgb(127, 127, 127); font-family: &quot;Courier New&quot;; font-size: 11pt; font-weight: bold;">getLocalAddress</span><span style="color: rgb(127, 127, 127); font-family: &quot;Courier New&quot;; font-size: 11pt; font-weight: bold;">]&gt;&gt;</span><span style="color: rgb(127, 127, 127); font-family: &quot;Courier New&quot;; font-size: 11pt; font-weight: bold;">&lt;&lt;/if&gt;&gt;</span></p></td></tr><tr><td style="background-color: rgb(242, 242, 242);"><p style="margin-top: 0pt; margin-right: 0pt; margin-bottom: 0pt; margin-left: 0pt;"><span style="color: rgb(127, 127, 127); font-family: &quot;Courier New&quot;; font-size: 11pt; font-weight: bold;">...</span></p></td><td style="background-color: rgb(242, 242, 242);"><p style="margin-top: 0pt; margin-right: 0pt; margin-bottom: 0pt; margin-left: 0pt;"><span style="color: rgb(127, 127, 127); font-family: &quot;Courier New&quot;; font-size: 11pt; font-weight: bold;">...</span></p></td><td style="background-color: rgb(242, 242, 242);"><p style="margin-top: 0pt; margin-right: 0pt; margin-bottom: 0pt; margin-left: 0pt;"><span style="color: rgb(127, 127, 127); font-family: &quot;Courier New&quot;; font-size: 11pt; font-weight: bold;">...</span></p></td></tr><tr style="height: 0pt;"><td style="width: 176.95pt; border-top-color: initial; border-top-style: none; border-top-width: initial; border-right-color: initial; border-right-style: none; border-right-width: initial; border-bottom-color: initial; border-bottom-style: none; border-bottom-width: initial; border-left-color: initial; border-left-style: none; border-left-width: initial;"></td><td style="width: 127.6pt; border-top-color: initial; border-top-style: none; border-top-width: initial; border-right-color: initial; border-right-style: none; border-right-width: initial; border-bottom-color: initial; border-bottom-style: none; border-bottom-width: initial; border-left-color: initial; border-left-style: none; border-left-width: initial;"></td><td style="width: 162.7pt; border-top-color: initial; border-top-style: none; border-top-width: initial; border-right-color: initial; border-right-style: none; border-right-width: initial; border-bottom-color: initial; border-bottom-style: none; border-bottom-width: initial; border-left-color: initial; border-left-style: none; border-left-width: initial;"></td></tr></tbody></table>
You can normally use table-row conditional blocks within data bands to make elements of an enumeration look differently depending on a condition. Consider the following template:

<table cellspacing="0" cellpadding="0" style="border-collapse: collapse; margin-left: 0pt;"><tbody><tr><td style="background-color: rgb(226, 239, 217);"><p style="margin-top: 0pt; margin-right: 0pt; margin-bottom: 0pt; margin-left: 0pt;"><span style="color: rgb(127, 127, 127); font-family: &quot;Courier New&quot;; font-size: 11pt; font-weight: bold;">&lt;&lt;foreach [in clients]&gt;&gt;&lt;&lt;if [</span><span style="color: rgb(127, 127, 127); font-family: &quot;Courier New&quot;; font-size: 11pt; font-weight: bold;">getCountry</span><span style="color: rgb(127, 127, 127); font-family: &quot;Courier New&quot;; font-size: 11pt; font-weight: bold;"> == "New Zealand"]&gt;&gt;&lt;&lt;[</span><span style="color: rgb(127, 127, 127); font-family: &quot;Courier New&quot;; font-size: 11pt; font-weight: bold;">getName</span><span style="color: rgb(127, 127, 127); font-family: &quot;Courier New&quot;; font-size: 11pt; font-weight: bold;">]&gt;&gt;</span></p></td><td colspan="2" style="background-color: rgb(226, 239, 217);"><p style="margin-top: 0pt; margin-right: 0pt; margin-bottom: 0pt; margin-left: 0pt;"><span style="color: rgb(127, 127, 127); font-family: &quot;Courier New&quot;; font-size: 11pt; font-weight: bold;">&lt;&lt;[</span><span style="color: rgb(127, 127, 127); font-family: &quot;Courier New&quot;; font-size: 11pt; font-weight: bold;">getLocalAddress</span><span style="color: rgb(127, 127, 127); font-family: &quot;Courier New&quot;; font-size: 11pt; font-weight: bold;">]&gt;&gt;</span></p></td></tr><tr><td style="background-color: rgb(242, 242, 242);"><p style="margin-top: 0pt; margin-right: 0pt; margin-bottom: 0pt; margin-left: 0pt;"><span style="color: rgb(127, 127, 127); font-family: &quot;Courier New&quot;; font-size: 11pt; font-weight: bold;">&lt;&lt;else&gt;&gt;&lt;&lt;[</span><span style="color: rgb(127, 127, 127); font-family: &quot;Courier New&quot;; font-size: 11pt; font-weight: bold;">getName</span><span style="color: rgb(127, 127, 127); font-family: &quot;Courier New&quot;; font-size: 11pt; font-weight: bold;">]&gt;&gt;</span></p></td><td style="background-color: rgb(242, 242, 242);"><p style="margin-top: 0pt; margin-right: 0pt; margin-bottom: 0pt; margin-left: 0pt;"><span style="color: rgb(127, 127, 127); font-family: &quot;Courier New&quot;; font-size: 11pt; font-weight: bold;">&lt;&lt;[</span><span style="color: rgb(127, 127, 127); font-family: &quot;Courier New&quot;; font-size: 11pt; font-weight: bold;">getCountry</span><span style="color: rgb(127, 127, 127); font-family: &quot;Courier New&quot;; font-size: 11pt; font-weight: bold;">]&gt;&gt;</span></p></td><td style="background-color: rgb(242, 242, 242);"><p style="margin-top: 0pt; margin-right: 0pt; margin-bottom: 0pt; margin-left: 0pt;"><span style="color: rgb(127, 127, 127); font-family: &quot;Courier New&quot;; font-size: 11pt; font-weight: bold;">&lt;&lt;[</span><span style="color: rgb(127, 127, 127); font-family: &quot;Courier New&quot;; font-size: 11pt; font-weight: bold;">getLocalAddress</span><span style="color: rgb(127, 127, 127); font-family: &quot;Courier New&quot;; font-size: 11pt; font-weight: bold;">]&gt;&gt;&lt;&lt;/if&gt;&gt;&lt;&lt;/foreach&gt;&gt;</span></p></td></tr><tr style="height: 0pt;"><td style="width: 176.95pt; border-top-color: initial; border-top-style: none; border-top-width: initial; border-right-color: initial; border-right-style: none; border-right-width: initial; border-bottom-color: initial; border-bottom-style: none; border-bottom-width: initial; border-left-color: initial; border-left-style: none; border-left-width: initial;"></td><td style="width: 127.6pt; border-top-color: initial; border-top-style: none; border-top-width: initial; border-right-color: initial; border-right-style: none; border-right-width: initial; border-bottom-color: initial; border-bottom-style: none; border-bottom-width: initial; border-left-color: initial; border-left-style: none; border-left-width: initial;"></td><td style="width: 162.7pt; border-top-color: initial; border-top-style: none; border-top-width: initial; border-right-color: initial; border-right-style: none; border-right-width: initial; border-bottom-color: initial; border-bottom-style: none; border-bottom-width: initial; border-left-color: initial; border-left-style: none; border-left-width: initial;"></td></tr></tbody></table>
In this case, the engine produces the report as below:

<table cellspacing="0" cellpadding="0" style="border-collapse: collapse; margin-left: 0pt;"><tbody><tr><td style="background-color: rgb(242, 242, 242); border-bottom-color: rgb(0, 0, 0); border-bottom-style: solid; border-bottom-width: 0.75pt; border-left-color: rgb(0, 0, 0); border-left-style: solid; border-left-width: 0.75pt; border-right-color: rgb(0, 0, 0); border-right-style: solid; border-right-width: 0.75pt; border-top-color: rgb(0, 0, 0); border-top-style: solid; border-top-width: 0.75pt; padding-left: 5.03pt; padding-right: 5.03pt; vertical-align: top; width: 166.15pt;"><p style="margin-top: 0pt; margin-right: 0pt; margin-bottom: 0pt; margin-left: 0pt;"><span style="color: rgb(127, 127, 127); font-family: &quot;Courier New&quot;; font-size: 11pt; font-weight: bold;">A Company</span></p></td><td style="background-color: rgb(242, 242, 242); border-bottom-color: rgb(0, 0, 0); border-bottom-style: solid; border-bottom-width: 0.75pt; border-left-color: rgb(0, 0, 0); border-left-style: solid; border-left-width: 0.75pt; border-right-color: rgb(0, 0, 0); border-right-style: solid; border-right-width: 0.75pt; border-top-color: rgb(0, 0, 0); border-top-style: solid; border-top-width: 0.75pt; padding-left: 5.03pt; padding-right: 5.03pt; vertical-align: top; width: 116.8pt;"><p style="margin-top: 0pt; margin-right: 0pt; margin-bottom: 0pt; margin-left: 0pt;"><span style="color: rgb(127, 127, 127); font-family: &quot;Courier New&quot;; font-size: 11pt; font-weight: bold;">Australia</span></p></td><td style="background-color: rgb(242, 242, 242); border-bottom-color: rgb(0, 0, 0); border-bottom-style: solid; border-bottom-width: 0.75pt; border-left-color: rgb(0, 0, 0); border-left-style: solid; border-left-width: 0.75pt; border-right-color: rgb(0, 0, 0); border-right-style: solid; border-right-width: 0.75pt; border-top-color: rgb(0, 0, 0); border-top-style: solid; border-top-width: 0.75pt; padding-left: 5.03pt; padding-right: 5.03pt; vertical-align: top; width: 151.9pt;"><p style="margin-top: 0pt; margin-right: 0pt; margin-bottom: 0pt; margin-left: 0pt;"><span style="color: rgb(127, 127, 127); font-family: &quot;Courier New&quot;; font-size: 11pt; font-weight: bold;">219-241 Cleveland St</span></p><p style="margin-top: 0pt; margin-right: 0pt; margin-bottom: 0pt; margin-left: 0pt;"><span style="color: rgb(127, 127, 127); font-family: &quot;Courier New&quot;; font-size: 11pt; font-weight: bold;">STRAWBERRY HILLS&nbsp; NSW&nbsp; 1427</span></p></td></tr><tr><td style="background-color: rgb(242, 242, 242); border-bottom-color: rgb(0, 0, 0); border-bottom-style: solid; border-bottom-width: 0.75pt; border-left-color: rgb(0, 0, 0); border-left-style: solid; border-left-width: 0.75pt; border-right-color: rgb(0, 0, 0); border-right-style: solid; border-right-width: 0.75pt; border-top-color: rgb(0, 0, 0); border-top-style: solid; border-top-width: 0.75pt; padding-left: 5.03pt; padding-right: 5.03pt; vertical-align: top; width: 166.15pt;"><p style="margin-top: 0pt; margin-right: 0pt; margin-bottom: 0pt; margin-left: 0pt;"><span style="color: rgb(127, 127, 127); font-family: &quot;Courier New&quot;; font-size: 11pt; font-weight: bold;">B Ltd.</span></p></td><td style="background-color: rgb(242, 242, 242); border-bottom-color: rgb(0, 0, 0); border-bottom-style: solid; border-bottom-width: 0.75pt; border-left-color: rgb(0, 0, 0); border-left-style: solid; border-left-width: 0.75pt; border-right-color: rgb(0, 0, 0); border-right-style: solid; border-right-width: 0.75pt; border-top-color: rgb(0, 0, 0); border-top-style: solid; border-top-width: 0.75pt; padding-left: 5.03pt; padding-right: 5.03pt; vertical-align: top; width: 116.8pt;"><p style="margin-top: 0pt; margin-right: 0pt; margin-bottom: 0pt; margin-left: 0pt;"><span style="color: rgb(127, 127, 127); font-family: &quot;Courier New&quot;; font-size: 11pt; font-weight: bold;">Brazil</span></p></td><td style="background-color: rgb(242, 242, 242); border-bottom-color: rgb(0, 0, 0); border-bottom-style: solid; border-bottom-width: 0.75pt; border-left-color: rgb(0, 0, 0); border-left-style: solid; border-left-width: 0.75pt; border-right-color: rgb(0, 0, 0); border-right-style: solid; border-right-width: 0.75pt; border-top-color: rgb(0, 0, 0); border-top-style: solid; border-top-width: 0.75pt; padding-left: 5.03pt; padding-right: 5.03pt; vertical-align: top; width: 151.9pt;"><p style="margin-top: 0pt; margin-right: 0pt; margin-bottom: 0pt; margin-left: 0pt;"><span style="color: rgb(127, 127, 127); font-family: &quot;Courier New&quot;; font-size: 11pt; font-weight: bold;">Avenida João Jorge, 112, ap. 31</span></p><p style="margin-top: 0pt; margin-right: 0pt; margin-bottom: 0pt; margin-left: 0pt;"><span style="color: rgb(127, 127, 127); font-family: &quot;Courier New&quot;; font-size: 11pt; font-weight: bold;">Vila Industrial</span></p><p style="margin-top: 0pt; margin-right: 0pt; margin-bottom: 0pt; margin-left: 0pt;"><span style="color: rgb(127, 127, 127); font-family: &quot;Courier New&quot;; font-size: 11pt; font-weight: bold;">Campinas - SP</span></p><p style="margin-top: 0pt; margin-right: 0pt; margin-bottom: 0pt; margin-left: 0pt;"><span style="color: rgb(127, 127, 127); font-family: &quot;Courier New&quot;; font-size: 11pt; font-weight: bold;">13035-680</span></p></td></tr><tr><td style="background-color: rgb(242, 242, 242); border-bottom-color: rgb(0, 0, 0); border-bottom-style: solid; border-bottom-width: 0.75pt; border-left-color: rgb(0, 0, 0); border-left-style: solid; border-left-width: 0.75pt; border-right-color: rgb(0, 0, 0); border-right-style: solid; border-right-width: 0.75pt; border-top-color: rgb(0, 0, 0); border-top-style: solid; border-top-width: 0.75pt; padding-left: 5.03pt; padding-right: 5.03pt; vertical-align: top; width: 166.15pt;"><p style="margin-top: 0pt; margin-right: 0pt; margin-bottom: 0pt; margin-left: 0pt;"><span style="color: rgb(127, 127, 127); font-family: &quot;Courier New&quot;; font-size: 11pt; font-weight: bold;">C &amp; D</span></p></td><td style="background-color: rgb(242, 242, 242); border-bottom-color: rgb(0, 0, 0); border-bottom-style: solid; border-bottom-width: 0.75pt; border-left-color: rgb(0, 0, 0); border-left-style: solid; border-left-width: 0.75pt; border-right-color: rgb(0, 0, 0); border-right-style: solid; border-right-width: 0.75pt; border-top-color: rgb(0, 0, 0); border-top-style: solid; border-top-width: 0.75pt; padding-left: 5.03pt; padding-right: 5.03pt; vertical-align: top; width: 116.8pt;"><p style="margin-top: 0pt; margin-right: 0pt; margin-bottom: 0pt; margin-left: 0pt;"><span style="color: rgb(127, 127, 127); font-family: &quot;Courier New&quot;; font-size: 11pt; font-weight: bold;">Canada</span></p></td><td style="background-color: rgb(242, 242, 242); border-bottom-color: rgb(0, 0, 0); border-bottom-style: solid; border-bottom-width: 0.75pt; border-left-color: rgb(0, 0, 0); border-left-style: solid; border-left-width: 0.75pt; border-right-color: rgb(0, 0, 0); border-right-style: solid; border-right-width: 0.75pt; border-top-color: rgb(0, 0, 0); border-top-style: solid; border-top-width: 0.75pt; padding-left: 5.03pt; padding-right: 5.03pt; vertical-align: top; width: 151.9pt;"><p style="margin-top: 0pt; margin-right: 0pt; margin-bottom: 0pt; margin-left: 0pt;"><span style="color: rgb(127, 127, 127); font-family: &quot;Courier New&quot;; font-size: 11pt; font-weight: bold;">101-3485 RUE DE LA MONTAGNE</span></p><p style="margin-top: 0pt; margin-right: 0pt; margin-bottom: 0pt; margin-left: 0pt;"><span style="color: rgb(127, 127, 127); font-family: &quot;Courier New&quot;; font-size: 11pt; font-weight: bold;">MONTRÉAL (QUÉBEC) H3G 2A6</span></p></td></tr><tr><td style="background-color: rgb(226, 239, 217); border-bottom-color: rgb(0, 0, 0); border-bottom-style: solid; border-bottom-width: 0.75pt; border-left-color: rgb(0, 0, 0); border-left-style: solid; border-left-width: 0.75pt; border-right-color: rgb(0, 0, 0); border-right-style: solid; border-right-width: 0.75pt; border-top-color: rgb(0, 0, 0); border-top-style: solid; border-top-width: 0.75pt; padding-left: 5.03pt; padding-right: 5.03pt; vertical-align: top; width: 166.15pt;"><p style="margin-top: 0pt; margin-right: 0pt; margin-bottom: 0pt; margin-left: 0pt;"><span style="color: rgb(127, 127, 127); font-family: &quot;Courier New&quot;; font-size: 11pt; font-weight: bold;">E Corp.</span></p></td><td colspan="2" style="background-color: rgb(226, 239, 217); border-bottom-color: rgb(0, 0, 0); border-bottom-style: solid; border-bottom-width: 0.75pt; border-left-color: rgb(0, 0, 0); border-left-style: solid; border-left-width: 0.75pt; border-right-color: rgb(0, 0, 0); border-right-style: solid; border-right-width: 0.75pt; border-top-color: rgb(0, 0, 0); border-top-style: solid; border-top-width: 0.75pt; padding-left: 5.03pt; padding-right: 5.03pt; vertical-align: top; width: 279.5pt;"><p style="margin-top: 0pt; margin-right: 0pt; margin-bottom: 0pt; margin-left: 0pt;"><span style="color: rgb(127, 127, 127); font-family: &quot;Courier New&quot;; font-size: 11pt; font-weight: bold;">445 Mount Eden Road</span></p><p style="margin-top: 0pt; margin-right: 0pt; margin-bottom: 0pt; margin-left: 0pt;"><span style="color: rgb(127, 127, 127); font-family: &quot;Courier New&quot;; font-size: 11pt; font-weight: bold;">Mount Eden</span></p><p style="margin-top: 0pt; margin-right: 0pt; margin-bottom: 0pt; margin-left: 0pt;"><span style="color: rgb(127, 127, 127); font-family: &quot;Courier New&quot;; font-size: 11pt; font-weight: bold;">Auckland 1024</span></p></td></tr><tr><td style="background-color: rgb(226, 239, 217); border-bottom-color: rgb(0, 0, 0); border-bottom-style: solid; border-bottom-width: 0.75pt; border-left-color: rgb(0, 0, 0); border-left-style: solid; border-left-width: 0.75pt; border-right-color: rgb(0, 0, 0); border-right-style: solid; border-right-width: 0.75pt; border-top-color: rgb(0, 0, 0); border-top-style: solid; border-top-width: 0.75pt; padding-left: 5.03pt; padding-right: 5.03pt; vertical-align: top; width: 166.15pt;"><p style="margin-top: 0pt; margin-right: 0pt; margin-bottom: 0pt; margin-left: 0pt;"><span style="color: rgb(127, 127, 127); font-family: &quot;Courier New&quot;; font-size: 11pt; font-weight: bold;">F &amp; Partners</span></p></td><td colspan="2" style="background-color: rgb(226, 239, 217); border-bottom-color: rgb(0, 0, 0); border-bottom-style: solid; border-bottom-width: 0.75pt; border-left-color: rgb(0, 0, 0); border-left-style: solid; border-left-width: 0.75pt; border-right-color: rgb(0, 0, 0); border-right-style: solid; border-right-width: 0.75pt; border-top-color: rgb(0, 0, 0); border-top-style: solid; border-top-width: 0.75pt; padding-left: 5.03pt; padding-right: 5.03pt; vertical-align: top; width: 279.5pt;"><p style="margin-top: 0pt; margin-right: 0pt; margin-bottom: 0pt; margin-left: 0pt;"><span style="color: rgb(127, 127, 127); font-family: &quot;Courier New&quot;; font-size: 11pt; font-weight: bold;">20 Greens Road</span></p><p style="margin-top: 0pt; margin-right: 0pt; margin-bottom: 0pt; margin-left: 0pt;"><span style="color: rgb(127, 127, 127); font-family: &quot;Courier New&quot;; font-size: 11pt; font-weight: bold;">Tuahiwi</span></p><p style="margin-top: 0pt; margin-right: 0pt; margin-bottom: 0pt; margin-left: 0pt;"><span style="color: rgb(127, 127, 127); font-family: &quot;Courier New&quot;; font-size: 11pt; font-weight: bold;">Kaiapoi 7691</span></p></td></tr><tr><td style="background-color: rgb(242, 242, 242); border-bottom-color: rgb(0, 0, 0); border-bottom-style: solid; border-bottom-width: 0.75pt; border-left-color: rgb(0, 0, 0); border-left-style: solid; border-left-width: 0.75pt; border-right-color: rgb(0, 0, 0); border-right-style: solid; border-right-width: 0.75pt; border-top-color: rgb(0, 0, 0); border-top-style: solid; border-top-width: 0.75pt; padding-left: 5.03pt; padding-right: 5.03pt; vertical-align: top; width: 166.15pt;"><p style="margin-top: 0pt; margin-right: 0pt; margin-bottom: 0pt; margin-left: 0pt;"><span style="color: rgb(127, 127, 127); font-family: &quot;Courier New&quot;; font-size: 11pt; font-weight: bold;">G &amp; Co.</span></p></td><td style="background-color: rgb(242, 242, 242); border-bottom-color: rgb(0, 0, 0); border-bottom-style: solid; border-bottom-width: 0.75pt; border-left-color: rgb(0, 0, 0); border-left-style: solid; border-left-width: 0.75pt; border-right-color: rgb(0, 0, 0); border-right-style: solid; border-right-width: 0.75pt; border-top-color: rgb(0, 0, 0); border-top-style: solid; border-top-width: 0.75pt; padding-left: 5.03pt; padding-right: 5.03pt; vertical-align: top; width: 116.8pt;"><p style="margin-top: 0pt; margin-right: 0pt; margin-bottom: 0pt; margin-left: 0pt;"><span style="color: rgb(127, 127, 127); font-family: &quot;Courier New&quot;; font-size: 11pt; font-weight: bold;">Greece</span></p></td><td style="background-color: rgb(242, 242, 242); border-bottom-color: rgb(0, 0, 0); border-bottom-style: solid; border-bottom-width: 0.75pt; border-left-color: rgb(0, 0, 0); border-left-style: solid; border-left-width: 0.75pt; border-right-color: rgb(0, 0, 0); border-right-style: solid; border-right-width: 0.75pt; border-top-color: rgb(0, 0, 0); border-top-style: solid; border-top-width: 0.75pt; padding-left: 5.03pt; padding-right: 5.03pt; vertical-align: top; width: 151.9pt;"><p style="margin-top: 0pt; margin-right: 0pt; margin-bottom: 0pt; margin-left: 0pt;"><span style="color: rgb(127, 127, 127); font-family: &quot;Courier New&quot;; font-size: 11pt; font-weight: bold;">Karkisias 6</span></p><p style="margin-top: 0pt; margin-right: 0pt; margin-bottom: 0pt; margin-left: 0pt;"><span style="color: rgb(127, 127, 127); font-family: &quot;Courier New&quot;; font-size: 11pt; font-weight: bold;">GR-111 42&nbsp; ATHINA</span></p><p style="margin-top: 0pt; margin-right: 0pt; margin-bottom: 0pt; margin-left: 0pt;"><span style="color: rgb(127, 127, 127); font-family: &quot;Courier New&quot;; font-size: 11pt; font-weight: bold;">GRÉCE</span></p></td></tr><tr><td style="background-color: rgb(242, 242, 242); border-bottom-color: rgb(0, 0, 0); border-bottom-style: solid; border-bottom-width: 0.75pt; border-left-color: rgb(0, 0, 0); border-left-style: solid; border-left-width: 0.75pt; border-right-color: rgb(0, 0, 0); border-right-style: solid; border-right-width: 0.75pt; border-top-color: rgb(0, 0, 0); border-top-style: solid; border-top-width: 0.75pt; padding-left: 5.03pt; padding-right: 5.03pt; vertical-align: top; width: 166.15pt;"><p style="margin-top: 0pt; margin-right: 0pt; margin-bottom: 0pt; margin-left: 0pt;"><span style="color: rgb(127, 127, 127); font-family: &quot;Courier New&quot;; font-size: 11pt; font-weight: bold;">H Group</span></p></td><td style="background-color: rgb(242, 242, 242); border-bottom-color: rgb(0, 0, 0); border-bottom-style: solid; border-bottom-width: 0.75pt; border-left-color: rgb(0, 0, 0); border-left-style: solid; border-left-width: 0.75pt; border-right-color: rgb(0, 0, 0); border-right-style: solid; border-right-width: 0.75pt; border-top-color: rgb(0, 0, 0); border-top-style: solid; border-top-width: 0.75pt; padding-left: 5.03pt; padding-right: 5.03pt; vertical-align: top; width: 116.8pt;"><p style="margin-top: 0pt; margin-right: 0pt; margin-bottom: 0pt; margin-left: 0pt;"><span style="color: rgb(127, 127, 127); font-family: &quot;Courier New&quot;; font-size: 11pt; font-weight: bold;">Hungary</span></p></td><td style="background-color: rgb(242, 242, 242); border-bottom-color: rgb(0, 0, 0); border-bottom-style: solid; border-bottom-width: 0.75pt; border-left-color: rgb(0, 0, 0); border-left-style: solid; border-left-width: 0.75pt; border-right-color: rgb(0, 0, 0); border-right-style: solid; border-right-width: 0.75pt; border-top-color: rgb(0, 0, 0); border-top-style: solid; border-top-width: 0.75pt; padding-left: 5.03pt; padding-right: 5.03pt; vertical-align: top; width: 151.9pt;"><p style="margin-top: 0pt; margin-right: 0pt; margin-bottom: 0pt; margin-left: 0pt;"><span style="color: rgb(127, 127, 127); font-family: &quot;Courier New&quot;; font-size: 11pt; font-weight: bold;">Budapest</span></p><p style="margin-top: 0pt; margin-right: 0pt; margin-bottom: 0pt; margin-left: 0pt;"><span style="color: rgb(127, 127, 127); font-family: &quot;Courier New&quot;; font-size: 11pt; font-weight: bold;">Fiktív utca 82., IV. em./28.</span></p><p style="margin-top: 0pt; margin-right: 0pt; margin-bottom: 0pt; margin-left: 0pt;"><span style="color: rgb(127, 127, 127); font-family: &quot;Courier New&quot;; font-size: 11pt; font-weight: bold;">2806</span></p></td></tr><tr><td style="background-color: rgb(226, 239, 217); border-bottom-color: rgb(0, 0, 0); border-bottom-style: solid; border-bottom-width: 0.75pt; border-left-color: rgb(0, 0, 0); border-left-style: solid; border-left-width: 0.75pt; border-right-color: rgb(0, 0, 0); border-right-style: solid; border-right-width: 0.75pt; border-top-color: rgb(0, 0, 0); border-top-style: solid; border-top-width: 0.75pt; padding-left: 5.03pt; padding-right: 5.03pt; vertical-align: top; width: 166.15pt;"><p style="margin-top: 0pt; margin-right: 0pt; margin-bottom: 0pt; margin-left: 0pt;"><span style="color: rgb(127, 127, 127); font-family: &quot;Courier New&quot;; font-size: 11pt; font-weight: bold;">I &amp; Sons</span></p></td><td colspan="2" style="background-color: rgb(226, 239, 217); border-bottom-color: rgb(0, 0, 0); border-bottom-style: solid; border-bottom-width: 0.75pt; border-left-color: rgb(0, 0, 0); border-left-style: solid; border-left-width: 0.75pt; border-right-color: rgb(0, 0, 0); border-right-style: solid; border-right-width: 0.75pt; border-top-color: rgb(0, 0, 0); border-top-style: solid; border-top-width: 0.75pt; padding-left: 5.03pt; padding-right: 5.03pt; vertical-align: top; width: 279.5pt;"><p style="margin-top: 0pt; margin-right: 0pt; margin-bottom: 0pt; margin-left: 0pt;"><span style="color: rgb(127, 127, 127); font-family: &quot;Courier New&quot;; font-size: 11pt; font-weight: bold;">43 Vogel Street</span></p><p style="margin-top: 0pt; margin-right: 0pt; margin-bottom: 0pt; margin-left: 0pt;"><span style="color: rgb(127, 127, 127); font-family: &quot;Courier New&quot;; font-size: 11pt; font-weight: bold;">Roslyn</span></p><p style="margin-top: 0pt; margin-right: 0pt; margin-bottom: 0pt; margin-left: 0pt;"><span style="color: rgb(127, 127, 127); font-family: &quot;Courier New&quot;; font-size: 11pt; font-weight: bold;">Palmerston North 4414</span></p></td></tr><tr><td style="background-color: rgb(242, 242, 242); border-bottom-color: rgb(0, 0, 0); border-bottom-style: solid; border-bottom-width: 0.75pt; border-left-color: rgb(0, 0, 0); border-left-style: solid; border-left-width: 0.75pt; border-right-color: rgb(0, 0, 0); border-right-style: solid; border-right-width: 0.75pt; border-top-color: rgb(0, 0, 0); border-top-style: solid; border-top-width: 0.75pt; padding-left: 5.03pt; padding-right: 5.03pt; vertical-align: top; width: 166.15pt;"><p style="margin-top: 0pt; margin-right: 0pt; margin-bottom: 0pt; margin-left: 0pt;"><span style="color: rgb(127, 127, 127); font-family: &quot;Courier New&quot;; font-size: 11pt; font-weight: bold;">J Ent.</span></p></td><td style="background-color: rgb(242, 242, 242); border-bottom-color: rgb(0, 0, 0); border-bottom-style: solid; border-bottom-width: 0.75pt; border-left-color: rgb(0, 0, 0); border-left-style: solid; border-left-width: 0.75pt; border-right-color: rgb(0, 0, 0); border-right-style: solid; border-right-width: 0.75pt; border-top-color: rgb(0, 0, 0); border-top-style: solid; border-top-width: 0.75pt; padding-left: 5.03pt; padding-right: 5.03pt; vertical-align: top; width: 116.8pt;"><p style="margin-top: 0pt; margin-right: 0pt; margin-bottom: 0pt; margin-left: 0pt;"><span style="color: rgb(127, 127, 127); font-family: &quot;Courier New&quot;; font-size: 11pt; font-weight: bold;">Japan</span></p></td><td style="background-color: rgb(242, 242, 242); border-bottom-color: rgb(0, 0, 0); border-bottom-style: solid; border-bottom-width: 0.75pt; border-left-color: rgb(0, 0, 0); border-left-style: solid; border-left-width: 0.75pt; border-right-color: rgb(0, 0, 0); border-right-style: solid; border-right-width: 0.75pt; border-top-color: rgb(0, 0, 0); border-top-style: solid; border-top-width: 0.75pt; padding-left: 5.03pt; padding-right: 5.03pt; vertical-align: top; width: 151.9pt;"><p style="margin-top: 0pt; margin-right: 0pt; margin-bottom: 0pt; margin-left: 0pt;"><span style="color: rgb(127, 127, 127); font-family: &quot;Courier New&quot;; font-size: 11pt; font-weight: bold;">Hakusan 4-Ch?me 3-2</span></p><p style="margin-top: 0pt; margin-right: 0pt; margin-bottom: 0pt; margin-left: 0pt;"><span style="color: rgb(127, 127, 127); font-family: &quot;Courier New&quot;; font-size: 11pt; font-weight: bold;">Bunky?-ku, T?KY?</span></p><p style="margin-top: 0pt; margin-right: 0pt; margin-bottom: 0pt; margin-left: 0pt;"><span style="color: rgb(127, 127, 127); font-family: &quot;Courier New&quot;; font-size: 11pt; font-weight: bold;">112-0001</span></p><p style="margin-top: 0pt; margin-right: 0pt; margin-bottom: 0pt; margin-left: 0pt;"><span style="color: rgb(127, 127, 127); font-family: &quot;Courier New&quot;; font-size: 11pt; font-weight: bold;">Japan</span></p></td></tr><tr style="height: 0pt;"><td style="width: 176.95pt; border-top-color: initial; border-top-style: none; border-top-width: initial; border-right-color: initial; border-right-style: none; border-right-width: initial; border-bottom-color: initial; border-bottom-style: none; border-bottom-width: initial; border-left-color: initial; border-left-style: none; border-left-width: initial;"></td><td style="width: 127.6pt; border-top-color: initial; border-top-style: none; border-top-width: initial; border-right-color: initial; border-right-style: none; border-right-width: initial; border-bottom-color: initial; border-bottom-style: none; border-bottom-width: initial; border-left-color: initial; border-left-style: none; border-left-width: initial;"></td><td style="width: 162.7pt; border-top-color: initial; border-top-style: none; border-top-width: initial; border-right-color: initial; border-right-style: none; border-right-width: initial; border-bottom-color: initial; border-bottom-style: none; border-bottom-width: initial; border-left-color: initial; border-left-style: none; border-left-width: initial;"></td></tr></tbody></table>
{{< alert style="info" >}}**Note:** You can use common conditional blocks within table-row data bands as well.{{< /alert >}}

Also, you can use data bands inside table-row conditional blocks. For example, you can provide an alternate content for an empty table-row data band using the following template:

<table cellspacing="0" cellpadding="0" style="border-collapse: collapse; margin-left: 0pt;"><tbody><tr><td style="background-color: rgb(242, 242, 242); border-bottom-color: rgb(0, 0, 0); border-bottom-style: solid; border-bottom-width: 0.75pt; border-left-color: rgb(0, 0, 0); border-left-style: solid; border-left-width: 0.75pt; border-right-color: rgb(0, 0, 0); border-right-style: solid; border-right-width: 0.75pt; border-top-color: rgb(0, 0, 0); border-top-style: solid; border-top-width: 0.75pt; padding-left: 5.03pt; padding-right: 5.03pt; vertical-align: top; width: 144.9pt;"><p style="margin-top: 0pt; margin-right: 0pt; margin-bottom: 0pt; margin-left: 0pt;"><span style="color: rgb(127, 127, 127); font-family: &quot;Courier New&quot;; font-size: 11pt; font-weight: bold;">Client</span></p></td><td style="background-color: rgb(242, 242, 242); border-bottom-color: rgb(0, 0, 0); border-bottom-style: solid; border-bottom-width: 0.75pt; border-left-color: rgb(0, 0, 0); border-left-style: solid; border-left-width: 0.75pt; border-right-color: rgb(0, 0, 0); border-right-style: solid; border-right-width: 0.75pt; border-top-color: rgb(0, 0, 0); border-top-style: solid; border-top-width: 0.75pt; padding-left: 5.03pt; padding-right: 5.03pt; vertical-align: top; width: 102.6pt;"><p style="margin-top: 0pt; margin-right: 0pt; margin-bottom: 0pt; margin-left: 0pt;"><span style="color: rgb(127, 127, 127); font-family: &quot;Courier New&quot;; font-size: 11pt; font-weight: bold;">getcountry</span></p></td><td style="background-color: rgb(242, 242, 242); border-bottom-color: rgb(0, 0, 0); border-bottom-style: solid; border-bottom-width: 0.75pt; border-left-color: rgb(0, 0, 0); border-left-style: solid; border-left-width: 0.75pt; border-right-color: rgb(0, 0, 0); border-right-style: solid; border-right-width: 0.75pt; border-top-color: rgb(0, 0, 0); border-top-style: solid; border-top-width: 0.75pt; padding-left: 5.03pt; padding-right: 5.03pt; vertical-align: top; width: 187.35pt;"><p style="margin-top: 0pt; margin-right: 0pt; margin-bottom: 0pt; margin-left: 0pt;"><span style="color: rgb(127, 127, 127); font-family: &quot;Courier New&quot;; font-size: 11pt; font-weight: bold;">Local Address</span></p></td></tr><tr><td colspan="3" style="background-color: rgb(242, 242, 242); border-bottom-color: rgb(0, 0, 0); border-bottom-style: solid; border-bottom-width: 0.75pt; border-left-color: rgb(0, 0, 0); border-left-style: solid; border-left-width: 0.75pt; border-right-color: rgb(0, 0, 0); border-right-style: solid; border-right-width: 0.75pt; border-top-color: rgb(0, 0, 0); border-top-style: solid; border-top-width: 0.75pt; padding-left: 5.03pt; padding-right: 5.03pt; vertical-align: top; width: 456.45pt;"><p style="margin-top: 0pt; margin-right: 0pt; margin-bottom: 0pt; margin-left: 0pt; text-align: center;"><span style="color: rgb(127, 127, 127); font-family: &quot;Courier New&quot;; font-size: 11pt; font-weight: bold;">&lt;&lt;if [!clients.</span><span style="color: rgb(127, 127, 127); font-family: &quot;Courier New&quot;; font-size: 11pt; font-weight: bold;">any</span><span style="color: rgb(127, 127, 127); font-family: &quot;Courier New&quot;; font-size: 11pt; font-weight: bold;">()]&gt;&gt;No data</span></p></td></tr><tr><td style="background-color: rgb(242, 242, 242); border-bottom-color: rgb(0, 0, 0); border-bottom-style: solid; border-bottom-width: 0.75pt; border-left-color: rgb(0, 0, 0); border-left-style: solid; border-left-width: 0.75pt; border-right-color: rgb(0, 0, 0); border-right-style: solid; border-right-width: 0.75pt; border-top-color: rgb(0, 0, 0); border-top-style: solid; border-top-width: 0.75pt; padding-left: 5.03pt; padding-right: 5.03pt; vertical-align: top; width: 144.9pt;"><p style="margin-top: 0pt; margin-right: 0pt; margin-bottom: 0pt; margin-left: 0pt;"><span style="color: rgb(127, 127, 127); font-family: &quot;Courier New&quot;; font-size: 11pt; font-weight: bold;">&lt;&lt;else&gt;&gt;&lt;&lt;foreach [in clients]&gt;&gt;&lt;&lt;[</span><span style="color: rgb(127, 127, 127); font-family: &quot;Courier New&quot;; font-size: 11pt; font-weight: bold;">getName</span><span style="color: rgb(127, 127, 127); font-family: &quot;Courier New&quot;; font-size: 11pt; font-weight: bold;">]&gt;&gt;</span></p></td><td style="background-color: rgb(242, 242, 242); border-bottom-color: rgb(0, 0, 0); border-bottom-style: solid; border-bottom-width: 0.75pt; border-left-color: rgb(0, 0, 0); border-left-style: solid; border-left-width: 0.75pt; border-right-color: rgb(0, 0, 0); border-right-style: solid; border-right-width: 0.75pt; border-top-color: rgb(0, 0, 0); border-top-style: solid; border-top-width: 0.75pt; padding-left: 5.03pt; padding-right: 5.03pt; vertical-align: top; width: 102.6pt;"><p style="margin-top: 0pt; margin-right: 0pt; margin-bottom: 0pt; margin-left: 0pt;"><span style="color: rgb(127, 127, 127); font-family: &quot;Courier New&quot;; font-size: 11pt; font-weight: bold;">&lt;&lt;[</span><span style="color: rgb(127, 127, 127); font-family: &quot;Courier New&quot;; font-size: 11pt; font-weight: bold;">getCountry</span><span style="color: rgb(127, 127, 127); font-family: &quot;Courier New&quot;; font-size: 11pt; font-weight: bold;">]&gt;&gt;</span></p></td><td style="background-color: rgb(242, 242, 242); border-bottom-color: rgb(0, 0, 0); border-bottom-style: solid; border-bottom-width: 0.75pt; border-left-color: rgb(0, 0, 0); border-left-style: solid; border-left-width: 0.75pt; border-right-color: rgb(0, 0, 0); border-right-style: solid; border-right-width: 0.75pt; border-top-color: rgb(0, 0, 0); border-top-style: solid; border-top-width: 0.75pt; padding-left: 5.03pt; padding-right: 5.03pt; vertical-align: top; width: 187.35pt;"><p style="margin-top: 0pt; margin-right: 0pt; margin-bottom: 0pt; margin-left: 0pt;"><span style="color: rgb(127, 127, 127); font-family: &quot;Courier New&quot;; font-size: 11pt; font-weight: bold;">&lt;&lt;[</span><span style="color: rgb(127, 127, 127); font-family: &quot;Courier New&quot;; font-size: 11pt; font-weight: bold;">getLocalAddress</span><span style="color: rgb(127, 127, 127); font-family: &quot;Courier New&quot;; font-size: 11pt; font-weight: bold;">]&gt;&gt;&lt;&lt;/foreach&gt;&gt;&lt;&lt;/if&gt;&gt;</span></p></td></tr><tr style="height: 0pt;"><td style="width: 155.7pt; border-top-color: initial; border-top-style: none; border-top-width: initial; border-right-color: initial; border-right-style: none; border-right-width: initial; border-bottom-color: initial; border-bottom-style: none; border-bottom-width: initial; border-left-color: initial; border-left-style: none; border-left-width: initial;"></td><td style="width: 113.4pt; border-top-color: initial; border-top-style: none; border-top-width: initial; border-right-color: initial; border-right-style: none; border-right-width: initial; border-bottom-color: initial; border-bottom-style: none; border-bottom-width: initial; border-left-color: initial; border-left-style: none; border-left-width: initial;"></td><td style="width: 198.15pt; border-top-color: initial; border-top-style: none; border-top-width: initial; border-right-color: initial; border-right-style: none; border-right-width: initial; border-bottom-color: initial; border-bottom-style: none; border-bottom-width: initial; border-left-color: initial; border-left-style: none; border-left-width: initial;"></td></tr></tbody></table>
In case, the corresponding enumeration is empty, the engine produces a report as below:

<table cellspacing="0" cellpadding="0" style="border-collapse: collapse; margin-left: 0pt;"><tbody><tr><td style="background-color: rgb(242, 242, 242); border-bottom-color: rgb(0, 0, 0); border-bottom-style: solid; border-bottom-width: 0.75pt; border-left-color: rgb(0, 0, 0); border-left-style: solid; border-left-width: 0.75pt; border-right-color: rgb(0, 0, 0); border-right-style: solid; border-right-width: 0.75pt; border-top-color: rgb(0, 0, 0); border-top-style: solid; border-top-width: 0.75pt; padding-left: 5.03pt; padding-right: 5.03pt; vertical-align: top; width: 144.9pt;"><p style="margin-top: 0pt; margin-right: 0pt; margin-bottom: 0pt; margin-left: 0pt;"><span style="color: rgb(127, 127, 127); font-family: &quot;Courier New&quot;; font-size: 11pt; font-weight: bold;">Client</span></p></td><td style="background-color: rgb(242, 242, 242); border-bottom-color: rgb(0, 0, 0); border-bottom-style: solid; border-bottom-width: 0.75pt; border-left-color: rgb(0, 0, 0); border-left-style: solid; border-left-width: 0.75pt; border-right-color: rgb(0, 0, 0); border-right-style: solid; border-right-width: 0.75pt; border-top-color: rgb(0, 0, 0); border-top-style: solid; border-top-width: 0.75pt; padding-left: 5.03pt; padding-right: 5.03pt; vertical-align: top; width: 102.6pt;"><p style="margin-top: 0pt; margin-right: 0pt; margin-bottom: 0pt; margin-left: 0pt;"><span style="color: rgb(127, 127, 127); font-family: &quot;Courier New&quot;; font-size: 11pt; font-weight: bold;">getCountry</span></p></td><td style="background-color: rgb(242, 242, 242); border-bottom-color: rgb(0, 0, 0); border-bottom-style: solid; border-bottom-width: 0.75pt; border-left-color: rgb(0, 0, 0); border-left-style: solid; border-left-width: 0.75pt; border-right-color: rgb(0, 0, 0); border-right-style: solid; border-right-width: 0.75pt; border-top-color: rgb(0, 0, 0); border-top-style: solid; border-top-width: 0.75pt; padding-left: 5.03pt; padding-right: 5.03pt; vertical-align: top; width: 187.35pt;"><p style="margin-top: 0pt; margin-right: 0pt; margin-bottom: 0pt; margin-left: 0pt;"><span style="color: rgb(127, 127, 127); font-family: &quot;Courier New&quot;; font-size: 11pt; font-weight: bold;">Local Address</span></p></td></tr><tr><td colspan="3" style="background-color: rgb(242, 242, 242); border-bottom-color: rgb(0, 0, 0); border-bottom-style: solid; border-bottom-width: 0.75pt; border-left-color: rgb(0, 0, 0); border-left-style: solid; border-left-width: 0.75pt; border-right-color: rgb(0, 0, 0); border-right-style: solid; border-right-width: 0.75pt; border-top-color: rgb(0, 0, 0); border-top-style: solid; border-top-width: 0.75pt; padding-left: 5.03pt; padding-right: 5.03pt; vertical-align: top; width: 456.45pt;"><p style="margin-top: 0pt; margin-right: 0pt; margin-bottom: 0pt; margin-left: 0pt; text-align: center;"><span style="color: rgb(127, 127, 127); font-family: &quot;Courier New&quot;; font-size: 11pt; font-weight: bold;">No data</span></p></td></tr><tr style="height: 0pt;"><td style="width: 155.7pt; border-top-color: initial; border-top-style: none; border-top-width: initial; border-right-color: initial; border-right-style: none; border-right-width: initial; border-bottom-color: initial; border-bottom-style: none; border-bottom-width: initial; border-left-color: initial; border-left-style: none; border-left-width: initial;"></td><td style="width: 113.4pt; border-top-color: initial; border-top-style: none; border-top-width: initial; border-right-color: initial; border-right-style: none; border-right-width: initial; border-bottom-color: initial; border-bottom-style: none; border-bottom-width: initial; border-left-color: initial; border-left-style: none; border-left-width: initial;"></td><td style="width: 198.15pt; border-top-color: initial; border-top-style: none; border-top-width: initial; border-right-color: initial; border-right-style: none; border-right-width: initial; border-bottom-color: initial; border-bottom-style: none; border-bottom-width: initial; border-left-color: initial; border-left-style: none; border-left-width: initial;"></td></tr></tbody></table>
{{< alert style="info" >}}**Note:** If tags denoting boundaries of a template option are contained within a single table cell, the option is considered to be a common template option, rather than a table-row one. That is, the option is considered to occupy contents within the cell, rather than the whole row. That is why, a single-cell alternate content in the previous example is located between an opening if and else tags, rather than between an else and closing if tags.{{< /alert >}}

A typical template for LINQ Reporting Engine is composed of common document contents and tags that describe the template’s structure and data bindings. You can form these tags using just running text that can occupy multiple paragraphs to be more descriptive.

