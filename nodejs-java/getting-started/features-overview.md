---
id: features-overview
url: assembly/nodejs-java/features-overview
title: Features Overview
weight: 2
description: "Overview of GroupDocs.Assembly for Node.js via Java features: supported data sources, template elements, template syntax and output options."
keywords: features, data sources, json, xml, csv, documenttable, template syntax, node.js, javascript
productName: GroupDocs.Assembly for Node.js via Java
hideChildren: False
toc: True
---

GroupDocs.Assembly for Node.js via Java generates documents in popular office and email file formats from template documents and data obtained from JSON, XML, CSV, `DataSet` objects, and tables of other documents. The main features are:

*   Multiple data formats support
*   Formulas and sequential data operations
*   `upper`, `lower`, `caps`, `firstCap` formatting of strings in template syntax
*   Ordinal, cardinal, alphabetic and other numeric formats in template syntax
*   Variables and text comments within template syntax tags
*   Dynamic insertion of outer document content
*   Dynamic background color and barcode generation
*   Dynamic hyperlinks and bookmarks, email attachments and message body attributes
*   Analogue of the Microsoft Word NEXT field
*   Updating fields while assembling word processing documents
*   Calculating formulas while assembling spreadsheet documents
*   Formatting of numeric, text, image, date-time and chart elements
*   Conditional formatting of template text elements
*   LINQ-based template syntax
*   Changing the format of the assembled file by an explicit specification or by the file extension
*   Removal of empty paragraphs
*   Charts, images, tables, lists and other report types
*   In-line template syntax error messages instead of exceptions
*   Loading templates from HTML with resources and saving assembled documents to HTML with resources

The details are given below.

## Data Sources

### Data Formats

| Feature | Support in GroupDocs.Assembly for Node.js via Java |
| --- | --- |
| JSON | Supported (using `JsonDataSource`) |
| XML | Supported (using `XmlDataSource` or `DataSet.readXml`) |
| CSV | Supported (using `CsvDataSource`) |
| Database-like data | Supported (using `DataSet`, `DataTable`, `DataRelation` and related classes) |
| OData and other web services | Supported through the JSON or XML payload returned by the service |
| Custom objects | Not supported (plain JavaScript objects are not Java objects and cannot be used as data sources; use JSON or XML with the same shape instead) |
| Spreadsheet as a table of data | Supported (using `DocumentTable` and `DocumentTableSet`) |
| Word processing table as a table of data | Supported (using `DocumentTable` and `DocumentTableSet`) |
| Presentation table as a table of data | Supported (using `DocumentTable` and `DocumentTableSet`) |

A simple value (a string or a number) can also be passed as a data source and referenced by its name in a template. See [Using Documents as Data Source](/assembly/nodejs-java/using-documents-as-data-source/) for details on `DocumentTable`.

### Data Manipulation Capabilities

| Feature | Support in GroupDocs.Assembly for Node.js via Java |
| --- | --- |
| Formulas | Supported |
| Sequential Data Operations (filtering, ordering, grouping, aggregating, etc.) | Supported (through LINQ-like syntax for data sources of all types; extension method analogues are named using lower camel case) |
| Type Member Invocation | Supported (members of Java types of data values, for example `java.lang.String` methods) |
| Built-In Data Relation Support | Supported (`DataSet` relations, JSON/XML hierarchy, `DocumentTableSet` relations) |
| Data Processing Customization | Limited (custom types cannot be defined in JavaScript) |
| External Document Import | Supported |

### Multiple Data Sources

`DocumentAssembler.assembleDocument` accepts several `DataSourceInfo` objects, so a template can reference multiple data sources by their names:

```javascript
const groupdocs = require('@groupdocs/groupdocs.assembly');

const table = new groupdocs.DocumentTable('Managers Data.docx', 1);

const assembler = new groupdocs.DocumentAssembler();
assembler.assembleDocument('template.docx', 'report.docx',
    new groupdocs.DataSourceInfo('Hello', 'a'),
    new groupdocs.DataSourceInfo('World', 'b'),
    new groupdocs.DataSourceInfo(table, 't'));

process.exit(0);
```

## Template Formats, Elements and Syntax

### Template Document Formats

#### Word Processing Document Formats

Word processing formats, including Microsoft Word and OpenOffice text document formats, are supported. See [Supported Document Formats](/assembly/nodejs-java/supported-document-formats/).

#### Spreadsheet Document Formats

Spreadsheet formats, including Microsoft Excel and OpenOffice spreadsheet formats, are supported. See [Supported Document Formats](/assembly/nodejs-java/supported-document-formats/).

#### Presentation Document Formats

Presentation formats, including Microsoft PowerPoint and OpenOffice presentation formats, are supported. See [Supported Document Formats](/assembly/nodejs-java/supported-document-formats/).

#### More Document Formats

Email, HTML, Markdown, plain text and other formats are also supported. See [Supported Document Formats](/assembly/nodejs-java/supported-document-formats/).

#### Dynamic Merging of Table Cells

Table cells with equal textual contents can be merged dynamically using the `cellMerge` tag.

#### Textual Comments within Template Syntax Tags

An optional comment provides a human-readable explanation that the engine ignores:

```
<<tag_name [expression] –switch1 –switch2 ... // optional_comment >>
```

#### In-lining of Syntax Error Messages into Templates

Syntax error messages can be written into the assembled document instead of throwing an exception. See [Use of In-line Syntax Error Messages into Templates](/assembly/nodejs-java/use-of-in-line-syntax-error-messages-into-templates/).

### Template Elements

| Feature | Support in GroupDocs.Assembly for Node.js via Java |
| --- | --- |
| Formatted Text Blocks | Supported |
| HTML Blocks | Supported |
| Repeated Blocks (including list items and table rows) | Supported |
| Conditional Blocks | Supported (including list items and table rows) |
| Pivot Tables | To be supported |
| Images | Supported |
| Charts | Supported |
| Barcodes | Supported |
| Bound Form Controls | To be supported |
| Hyperlinks to URI or Bookmarks | Supported |

### Template Syntax Formats for Expression Results

#### Specifying String Formats

| String Format | Description |
| --- | --- |
| lower | Converts a string to lower case ("the string") |
| upper | Converts a string to upper case ("THE STRING") |
| caps | Capitalizes a first letter of every word in a string ("The String") |
| firstCap | Capitalizes the first letter of the first word in a string ("The string") |

#### Specifying Numeric Formats

| Number Format | Description |
| --- | --- |
| alphabetic | Formats an integer number as an upper-case letter (A, B, C, ...) |
| roman | Formats an integer number as an upper-case Roman numeral (I, II, III, ...) |
| ordinal | Appends an ordinal suffix to an integer number (1st, 2nd, 3rd, ...) |
| ordinalText | Converts an integer number to its ordinal text representation (First, Second, Third, ...) |
| cardinal | Converts an integer number to its text representation (One, Two, Three, ...) |
| hex | Formats an integer number as hexadecimal (8, 9, A, B, C, D, E, F, 10, 11, ...) |
| arabicDash | Encloses an integer number with dashes (- 1 -, - 2 -, - 3 -, ...) |

#### Variables in Template Documents

Variables can be defined in template documents as follows:

```
<<var [st = "Hello, "]>><<[st]>><<var [st = "World!"]>><<[st]>>
```

### Support for Outer Document Insertion

Contents of outer documents can be inserted into reports dynamically.

### Barcode Image Generation

Barcode images can be generated in reports dynamically.

### Support for Analogue of Microsoft Word NEXT Field

The `<<next>>` tag moves to the next data item. It is supported only within data bands created by the `<<foreach>>` tag.

### Setting Background Color Dynamically

The background color of text can be set dynamically using the `backColor` tag:

```
<<backColor ["red"]>>text with red background<</backColor>>
```

For HTML documents, the `backColor` tag is not supported; use the HTML `style` attribute instead.

### Inserting Images Dynamically

Images can be inserted into reports dynamically using `image` tags:

```
<<image [image_expression]>>
```

### Ability to Update Fields

Fields can be updated while assembling word processing documents. See [Updating Fields While Assembling Word Processing Documents](/assembly/nodejs-java/updating-fields-while-assembling-word-processing-documents/).

### Ability to Calculate Formulas

Formulas can be calculated while assembling spreadsheet documents.

### Template Elements Formatting

| Feature | Support in GroupDocs.Assembly for Node.js via Java |
| --- | --- |
| Numeric/Date-Time Value Formatting | Supported |
| Text Formatting | Supported |
| Conditional Text Formatting | Supported (only through conditional blocks) |
| Image Formatting | Supported (WYSIWYG) |
| Chart Formatting | Supported (WYSIWYG) |

### Template Syntax

| Feature | Support in GroupDocs.Assembly for Node.js via Java |
| --- | --- |
| LINQ-Based | Supported, extension method analogues are named using lower camel case |
| [Mustache](https://mustache.github.io/mustache.5.html) | To be supported |

Expressions in templates use Java syntax and Java types, because the engine runs on the JVM. See [Template Syntax - Part 1 of 2](/assembly/nodejs-java/template-syntax-part-1-of-2/).

### Changing Output File Format

The target format of an assembled document can be defined by the file extension or by an explicit specification. See [Changing Target File Format](/assembly/nodejs-java/changing-target-file-format/).

### Loading HTML and Saving to HTML with External Resource Files

Template documents can be loaded from HTML with resources, and assembled Word, Excel, PowerPoint and email documents can be saved to HTML with external resource files.

### Numbering Restart in Nested Numbered List

List numbering can be restarted dynamically using `<<restartNum>>` tags. This is useful for a nested numbered list within a data band.

### Metered Licensing

The `Metered` class provides metered licensing. See [Evaluation Limitations and Licensing](/assembly/nodejs-java/evaluation-limitations-and-licensing/).
