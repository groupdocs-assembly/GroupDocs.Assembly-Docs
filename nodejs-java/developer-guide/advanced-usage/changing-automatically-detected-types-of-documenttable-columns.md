---
id: changing-automatically-detected-types-of-documenttable-columns
url: assembly/nodejs-java/changing-automatically-detected-types-of-documenttable-columns
title: Changing Automatically Detected Types of DocumentTable Columns
weight: 33
description: "Change the type of a DocumentTable column to enable arithmetic operations and aggregates in templates with GroupDocs.Assembly for Node.js via Java."
keywords: documenttable, documenttablecolumn, column type, settype, sum, node.js, javascript
productName: GroupDocs.Assembly for Node.js via Java
hideChildren: False
toc: True
---

## Changing Automatically Detected Types

The type of a `DocumentTable` column is detected automatically when the table is loaded:

*   For spreadsheet documents, the type is detected from cell values (for example, `double` when all cells of a column are numeric).
*   For other documents (word processing and presentation), the type of a column is always `java.lang.String` by default.

`DocumentTableColumn.getType()` returns the column type as a Java `Class`, and `DocumentTableColumn.setType()` changes it. For example, changing the type of a column with numeric text to `double` enables arithmetic operations and aggregates, such as `sum`, on values of the column in templates.

In JavaScript, obtain Java `Class` objects through the `java` package. For primitive types, use the `TYPE` field of the wrapper class, for example `java.import('java.lang.Double').TYPE` for `double`.

### Download

#### Data Source Document

*   [Managers Data.docx](https://github.com/groupdocs-assembly/GroupDocs.Assembly-for-Java/blob/master/Examples/GroupDocs.Assembly.Examples.Java/Data/Data%20Sources/Word%20DataSource/Managers%20Data.docx?raw=true)

#### Template

*   [Changing Document Table Column Type.pptx](https://github.com/groupdocs-assembly/GroupDocs.Assembly-for-Java/blob/master/Examples/GroupDocs.Assembly.Examples.Java/Data/Storage/Presentation%20Templates/Changing%20Document%20Table%20Column%20Type.pptx?raw=true)

The template contains a table with a data row and a total row. The data row cells contain:

```
<<foreach [in Managers]>><<[Manager]>>
```

```
<<[Total_Contract_Price]>><</foreach>>
```

The total row contains:

```
<<[Managers.sum(m => m.Total_Contract_Price)]>>
```

## Changing Document Table Column Type

```javascript
const java = require('java');
const groupdocs = require('@groupdocs/groupdocs.assembly');

// Set table column names to be extracted from the document.
const options = new groupdocs.DocumentTableOptions();
options.setFirstRowContainsColumnNames(true);

const table = new groupdocs.DocumentTable('Managers Data.docx', 1, options);

// NOTE: For non-spreadsheet documents, the type of a document table column is always string by default.
const column = table.getColumns().get('Total_Contract_Price');
console.log(column.getType().getName());   // java.lang.String

// Change the column's type to double, thus enabling arithmetic operations
// on values of the column, such as summing in templates.
column.setType(java.import('java.lang.Double').TYPE);
console.log(column.getType().getName());   // double

// Pass DocumentTable as a data source.
const assembler = new groupdocs.DocumentAssembler();
assembler.assembleDocument('Changing Document Table Column Type.pptx', 'out.pptx',
    new groupdocs.DataSourceInfo(table, 'Managers'));

process.exit(0);
```

The report lists five managers with their total contract prices, followed by the total of `5700000.0`.

{{< alert style="info" >}}In evaluation mode, text read from PPTX templates is truncated, which can make template tags invalid. Apply a license to process presentations without this limitation, or use a template of another format. See [Evaluation Limitations and Licensing](/assembly/nodejs-java/evaluation-limitations-and-licensing/).{{< /alert >}}

## See Also

*   [Using Documents as Data Source](/assembly/nodejs-java/using-documents-as-data-source/)
