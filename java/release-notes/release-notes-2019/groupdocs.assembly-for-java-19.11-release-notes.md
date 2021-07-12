---
id: groupdocs-assembly-for-java-19-11-release-notes
url: assembly/java/groupdocs-assembly-for-java-19-11-release-notes
title: GroupDocs.Assembly for Java 19.11 Release Notes
weight: 1
description: ""
keywords: 
productName: GroupDocs.Assembly for Java
hideChildren: False
---
{{< alert style="info" >}}This page contains release notes for GroupDocs.Assembly for Java 19.11{{< /alert >}}

## Major Features

Simplified working with JSON data sources, supported dynamic insertion of links to internal document contents, and extended the set of supported Markdown features.

## Full List of Features Covering all Changes in this Release

| Key | Summary | Category |
| --- | --- | --- |
| ASSEMBLYJAVA-14  | Simplify working with JSON data sources  | Feature  |
| ASSEMBLYNET-128  | Support dynamic insertion of links to bookmarks for Word Processing documents  | Feature  |
| ASSEMBLYNET-129  | Support dynamic insertion of links to cells for Spreadsheet documents  | Feature  |
| ASSEMBLYNET-130  | Support dynamic insertion of links to slides for Presentation documents  | Feature  |
| ASSEMBLYNET-131  | Support dynamic insertion of links to bookmarks for emails  | Feature  |
| ASSEMBLYNET-133  | Support code blocks and spans for Markdown  | Feature  |
| ASSEMBLYNET-134  | Support strikethrough text for Markdown  | Feature  |
| ASSEMBLYNET-132  | Valid license files are not accepted  | Bug  |

{{< alert style="info" >}}This section lists public API changes that were introduced in GroupDocs.Assembly for .NET 19.11. It includes not only new and obsoleted public methods, but also a description of any changes in the behavior behind the scenes in GroupDocs.Assembly which may affect existing code. Any behavior introduced that could be seen as a regression and modifies existing behavior is especially important and is documented here.{{< /alert >}}

## Public API and Backward Incompatible Changes 

### Simplified working with JSON data sources

To access JSON data while building a report, you can pass a *JsonDataSource* instance to the engine as a data source.

Using of *JsonDataSource* enables you to work with typed values of JSON elements in template documents. For more convenience, the set of simple JSON types is extended as follows:

*   Integer
*   Long
*   Double
*   Boolean
*   Date
*   String

In template documents, if a top-level JSON element is an array or an object having only one property of an array type, a JsonDataSource instance should be treated in the same way as if it was a DataTable instance (see "[Working with DataTable and DataView Objects](https://docs.groupdocs.com/assembly/java/template-syntax-part-1-of-2/#using-data-sources)" for more information) as shown in the following example.

#### **JSON**

\[ 
   { 
      Name:"John Doe",
      Age:30,
      Birth:"1989-04-01 4:00:00 pm"
   },
   { 
      Name:"Jane Doe",
      Age:27,
      Birth:"1992-01-31 07:00:00 am"
   },
   { 
      Name:"John Smith",
      Age:51,
      Birth:"1968-03-08 1:00:00 pm"
   }
\]

#### Alternative JSON (produces the same result)

{ 
   Persons:\[ 
      { 
         Name:"John Doe",
         Age:30,
         Birth:"1989-04-01 4:00:00 pm"
      },
      { 
         Name:"Jane Doe",
         Age:27,
         Birth:"1992-01-31 07:00:00 am"
      },
      { 
         Name:"John Smith",
         Age:51,
         Birth:"1968-03-08 1:00:00 pm"
      }
   \]
}

#### Template document

<<foreach \[in persons\]>>Name: <<\[Name\]>>, Age: <<\[Age\]>>, Date of Birth: <<\[Birth\]:"dd.MM.yyyy">>
<</foreach>>
Average age: <<\[persons.average(p => p.Age)\]>>

#### Source code

```java
String template_doc_path = ... // Path for template doc
String report_doc_path = ... // path for report doc
JsonDataSource dataSource = ... // Loading JSON.
DocumentAssembler assembler = new DocumentAssembler();
assembler.assembleDocument(template_doc_path, report_doc_path, new DataSourceInfo(dataSource, "persons"));
```

#### Result document

Name: John Doe, Age: 30, Date of Birth: 01.04.1989
Name: Jane Doe, Age: 27, Date of Birth: 31.01.1992
Name: John Smith, Age: 51, Date of Birth: 08.03.1968
Average age: 36

{{< alert style="warning" >}}Using of the custom date-time format becomes possible, because text values of Birth properties are automatically converted to Date.{{< /alert >}}


If a top-level JSON element represents an object, a *JsonDataSource* instance should be treated in template documents in the same way as if it was a *DataRow* instance (see "[Working with *DataRow* and *DataRowView* Objects](https://docs.groupdocs.com/assembly/java/template-syntax-part-1-of-2/#using-data-sources)" for more information). If a top-level JSON object has a single property that is also an object, then this nested object is accessed by the assembler instead. To see how it works, consider the following example.

#### JSON

{ 
   Name:"John Doe",
   Age:30,
   Birth:"1989-04-01 4:00:00 pm",
   Child:\[ 
      "Ann Doe",
      "Charles Doe"
   \]
}

#### Alternative JSON (produces the same result)

{ 
   Person:{ 
      Name:"John Doe",
      Age:30,
      Birth:"1989-04-01 4:00:00 pm",
      Child:\[ 
         "Ann Doe",
         "Charles Doe"
      \]
   }
}

#### Template document

Name: <<\[Name\]>>, Age: <<\[Age\]>>, Date of Birth:
<<\[Birth\]:"dd.MM.yyyy">>
Children:
<<foreach \[in Child\]>><<\[Child\_Text\]>>
<</foreach>>

#### Source code

```java
String template_doc_path = ... // Path for template doc
String report_doc_path = ... // path for report doc
JsonDataSource dataSource = ... // Loading JSON.
DocumentAssembler assembler = new DocumentAssembler();
assembler.assembleDocument(template_doc_path, report_doc_path, new DataSourceInfo(dataSource));
```

#### Result document

Name: John Doe, Age: 30, Date of Birth: 01.04.1989
Children:
Ann Doe
Charles Doe

{{< alert style="warning" >}}To reference a JSON object property that is an array of simple-type values, the name of the property (for example, "Child") should be used in a template document, whereas the same name with the "_Text" suffix (for example, "Child_Text") should be used to reference the value of an item of this array.{{< /alert >}}

The following example sums up typical scenarios involving nested JSON objects and arrays.

#### JSON

\[ 
   { 
      Name:"John Smith",
      Contract:\[ 
         { 
            Client:{ 
               Name:"A Company"
            },
            Price:1200000
         },
         { 
            Client:{ 
               Name:"B Ltd."
            },
            Price:750000
         },
         { 
            Client:{ 
               Name:"C & D"
            },
            Price:350000
         }
      \]
   },
   { 
      Name:"Tony Anderson",
      Contract:\[ 
         { 
            Client:{ 
               Name:"E Corp."
            },
            Price:650000
         },
         { 
            Client:{ 
               Name:"F & Partners"
            },
            Price:550000
         }
      \]
   },
   { 
      Name:"July James",
      Contract:\[ 
         { 
            Client:{ 
               Name:"G & Co."
            },
            Price:350000
         },
         { 
            Client:{ 
               Name:"H Group"
            },
            Price:250000
         },
         { 
            Client:{ 
               Name:"I & Sons"
            },
            Price:100000
         },
         { 
            Client:{ 
               Name:"J Ent."
            },
            Price:100000
         }
      \]
   }
\]

#### Template document

<<foreach \[in managers\]>>Manager: <<\[Name\]>>
Contracts:
<<foreach \[in Contract\]>>- <<\[Client.Name\]>> ($<<\[Price\]>>)
<</foreach>>
<</foreach>>

#### Source code

```java
String template_doc_path = ... // Path for template doc
String report_doc_path = ... // path for report doc
JsonDataSource dataSource = ... // Loading JSON.
DocumentAssembler assembler = new DocumentAssembler();
assembler.assembleDocument(template_doc_path, report_doc_path, new DataSourceInfo(dataSource, "managers"));
```

#### Result document

Manager: John Smith
Contracts:
- A Company ($1200000)
- B Ltd. ($750000)
- C & D ($350000)
Manager: Tony Anderson
Contracts:
- E Corp. ($650000)
- F & Partners ($550000)
Manager: July James
Contracts:
- G & Co. ($350000)
- H Group ($250000)
- I & Sons ($100000)
- J Ent. ($100000)

### Extended the set of supported Markdown features

From now on, the following Markdown features are supported when saving assembled Markdown documents to Word Processing formats and saving assembled Word Processing documents and emails to Markdown:

*   [Indented code blocks ](https://spec.commonmark.org/0.29/#indented-code-blocks)
*   [Fenced code blocks](https://spec.commonmark.org/0.29/#fenced-code-blocks)
*   [Inline code spans](https://spec.commonmark.org/0.29/#code-spans)
*   [Strikethrough text](https://github.com/adam-p/markdown-here/wiki/Markdown-Cheatsheet#emphasis)

### Supported dynamic insertion of links to bookmarks for Word Processing documents and emails

You can also insert links to bookmarks to your reports dynamically using link tags. The syntax of a link tag is defined as follows:

```java
<<link [uri_or_bookmark_expression][display_text_expression]>>

```

Here, **uri\_or\_bookmark\_expression** defines URI or the name of a bookmark within the same document for a hyperlink to be inserted dynamically. This expression is mandatory and must return a non-empty value.In turn, **display\_text\_expression** defines text to be displayed for the hyperlink. This expression is optional. If it is omitted or returns an empty value, then during runtime, a value of **uri\_or\_bookmark\_expression** is used as display text as well.

{{< alert style="warning" >}}Values of both uri_or_bookmark_expression and display_text_expression can be of any types. During runtime, Object.ToString() is invoked to get textual representations of these expressions’ values, which is useful for expressions of types like URI. for example. While building a report, uri_or_bookmark_expression and display_text_expression are evaluated and their results are used to construct a hyperlink that replaces the corresponding link tag then. If uri_or_bookmark_expression returns the name of a bookmark in the same document, then the hyperlink navigates to the bookmark. Otherwise, the hyperlink navigates to a corresponding external resource.A link tag cannot be used within a chart.{{< /alert >}}

### Supported dynamic insertion of links to cells for Spreadsheet documents

For Spreadsheet documents, behavior of link tags is changed as follows. If an expression defined within a link tag is evaluated to a cell or cell range reference during runtime, then the tag is replaced with a link to the corresponding cell or cell range.

The following table describes supported formats of cell and cell range references.

| Description | Format | Example |
| --- | --- | --- |
| Reference to a cell within the same worksheet | cell\_name | A1 |
| Reference to a cell in another worksheet | worksheet\_name!cell\_name | Sheet1!A1 |
| Reference to a cell range within the same worksheet | [start\_cell\_name:end\_cell\_name](http://start_cell_nameend_cell_name) | A1:B2 |
| Reference to a cell range in another worksheet | worksheet\_name![start\_cell\_name:end\_cell\_name](http://start_cell_nameend_cell_name) | Sheet1!A1:B2 |

Following is sample syntax, If the link to cell A1 is required to be inserted:

```java
<<link ["A1"] ["Home"]>>
```

### Supported dynamic insertion of links to slides for Presentation documents

For Presentation documents, behavior of link tags is changed as follows. If an expression defined within a link tag is evaluated to a "SlideN" value, where N is a one-based index of a slide within the same Presentation document, then the tag is replaced with a link to the corresponding slide during runtime.

See the example of the syntax as follows:

```java
<<link ["Slide1"] ["Home"]>>
```
