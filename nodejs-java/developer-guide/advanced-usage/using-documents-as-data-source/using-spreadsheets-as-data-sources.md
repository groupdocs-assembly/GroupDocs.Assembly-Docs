---
id: using-spreadsheets-as-data-sources
url: assembly/nodejs-java/using-spreadsheets-as-data-sources
title: Using Spreadsheets as Data Sources
weight: 1
description: "Load a worksheet of an Excel workbook as a DocumentTable and use it as a data source in GroupDocs.Assembly for Node.js via Java."
keywords: spreadsheet data source, excel, xlsx, documenttable, documenttableoptions, node.js, javascript
productName: GroupDocs.Assembly for Node.js via Java
hideChildren: False
toc: True
---

A worksheet of a spreadsheet document can be loaded as a `DocumentTable` and used as a data source. For spreadsheets, the engine detects column types from cell values, so numeric columns can be used in arithmetic operations and aggregates directly.

## The Recipe

*   Load a worksheet as a `DocumentTable`, extracting column names from the first row
*   Assemble a document using the table as a data source

### Download

#### Data Source Document

*   [Contracts Data.xlsx](https://github.com/groupdocs-assembly/GroupDocs.Assembly-for-Java/blob/master/Examples/GroupDocs.Assembly.Examples.Java/Data/Data%20Sources/Excel%20DataSource/Contracts%20Data.xlsx?raw=true)

The first worksheet contains the `Client`, `Manager` and `Contract Price` columns.

#### Template

*   [Using Spreadsheet as Table of Data.docx](https://github.com/groupdocs-assembly/GroupDocs.Assembly-for-Java/blob/master/Examples/GroupDocs.Assembly.Examples.Java/Data/Storage/Word%20Templates/Using%20Spreadsheet%20as%20Table%20of%20Data.docx?raw=true)

The template contains a two-column table that groups contracts by manager and sums contract prices. The first cell of the data row contains:

```
<<foreach [group in contracts
    .groupBy(c => c.Manager)
    .orderBy(g => g.key)]>><<[group.key]>>
```

The second cell contains:

```
<<[group.sum(
    c => c.Contract_Price)]>><</foreach>>
```

## The Code

```javascript
const groupdocs = require('@groupdocs/groupdocs.assembly');

// Extract column names from the first row.
const options = new groupdocs.DocumentTableOptions();
options.setFirstRowContainsColumnNames(true);

// Use data of the first worksheet.
const table = new groupdocs.DocumentTable('Contracts Data.xlsx', 0, options);

// Check column count, names, and types.
const columns = table.getColumns();
console.log(columns.getCount()); // 3
for (let i = 0; i < columns.getCount(); i++) {
    const column = columns.get(i);
    console.log(column.getName(), column.getType().getName());
}
// Client java.lang.String
// Manager java.lang.String
// Contract_Price double
// NOTE: A space is replaced with an underscore, because spaces are not allowed in column names.
// NOTE: The type of the last column is double, because all its cells contain numeric values.

const assembler = new groupdocs.DocumentAssembler();
assembler.assembleDocument('Using Spreadsheet as Table of Data.docx',
    'Using Spreadsheet as Table of Data_report.docx',
    new groupdocs.DataSourceInfo(table, 'contracts'));

process.exit(0);
```

If column names are not extracted from the first row, the columns are named `A`, `B`, `C`, and so on, the header row is treated as a data row, and all columns get the `java.lang.String` type.
