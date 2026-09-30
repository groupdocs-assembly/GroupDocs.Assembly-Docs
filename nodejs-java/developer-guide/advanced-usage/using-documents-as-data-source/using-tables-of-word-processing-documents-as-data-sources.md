---
id: using-tables-of-word-processing-documents-as-data-sources
url: assembly/nodejs-java/using-tables-of-word-processing-documents-as-data-sources
title: Using Tables of Word Processing Documents as Data Sources
weight: 3
description: "Load a table of a Word document as a DocumentTable and use it as a data source in GroupDocs.Assembly for Node.js via Java."
keywords: word table data source, docx, table, documenttable, documenttableoptions, node.js, javascript
productName: GroupDocs.Assembly for Node.js via Java
hideChildren: False
toc: True
---

A table of a word processing document can be loaded as a `DocumentTable` and used as a data source. Tables are indexed across the whole document in document order, starting from zero. The template can be of any supported format; this example imports a Word table into a presentation.

## The Recipe

*   Load the second table of a Word document as a `DocumentTable`, limiting the number of loaded rows
*   Assemble a document using the table as a data source

### Download

#### Data Source Document

*   [Managers Data.docx](https://github.com/groupdocs-assembly/GroupDocs.Assembly-for-Java/blob/master/Examples/GroupDocs.Assembly.Examples.Java/Data/Data%20Sources/Word%20DataSource/Managers%20Data.docx?raw=true)

The document contains two tables. The second one lists managers and their total contract prices, with a `Manager` / `Total Contract Price` header row.

#### Template

*   [Importing Word Processing Table into Presentation.pptx](https://github.com/groupdocs-assembly/GroupDocs.Assembly-for-Java/blob/master/Examples/GroupDocs.Assembly.Examples.Java/Data/Storage/Presentation%20Templates/Importing%20Word%20Processing%20Table%20into%20Presentation.pptx?raw=true)

The template contains a two-column table. The cells of its row contain:

```
<<foreach [in table]>><<[Column1]>>
```

```
<<[Column2]>><</foreach>>
```

## The Code

```javascript
const groupdocs = require('@groupdocs/groupdocs.assembly');

// Do not extract column names from the first row, so that the first row is treated as a data row.
// Limit the largest row index, so that only the first four rows are loaded.
const options = new groupdocs.DocumentTableOptions();
options.setMaxRowIndex(3);

// Use data of the second table in the document.
const table = new groupdocs.DocumentTable('Managers Data.docx', 1, options);

// Check column count and names.
// NOTE: Default column names are used, because the names are not extracted from the first row.
const columns = table.getColumns();
console.log(columns.getCount());         // 2
console.log(columns.get(0).getName());   // Column1
console.log(columns.get(1).getName());   // Column2

const assembler = new groupdocs.DocumentAssembler();
assembler.assembleDocument('Importing Word Processing Table into Presentation.pptx',
    'Importing Word Processing Table into Presentation_report.pptx',
    new groupdocs.DataSourceInfo(table, 'table'));

process.exit(0);
```

The table in the report contains the header row of the source table followed by the first three managers:

| Column1 | Column2 |
| --- | --- |
| Manager | Total Contract Price |
| John Smith | 2300000 |
| Tony Anderson | 1200000 |
| July James | 800000 |

{{< alert style="info" >}}In evaluation mode, text read from PPTX templates is truncated, which can make template tags invalid. Apply a license to process presentations without this limitation, or use a template of another format. See [Evaluation Limitations and Licensing](/assembly/nodejs-java/evaluation-limitations-and-licensing/).{{< /alert >}}
