---
id: using-tables-of-presentation-documents-as-data-sources
url: assembly/nodejs-java/using-tables-of-presentation-documents-as-data-sources
title: Using Tables of Presentation Documents as Data Sources
weight: 2
description: "Load a table of a PowerPoint presentation as a DocumentTable and use it as a data source in GroupDocs.Assembly for Node.js via Java."
keywords: presentation data source, powerpoint, pptx, table, documenttable, documenttableoptions, node.js, javascript
productName: GroupDocs.Assembly for Node.js via Java
hideChildren: False
toc: True
---

A table of a presentation document can be loaded as a `DocumentTable` and used as a data source. Tables are indexed across the whole presentation in document order, starting from zero.

## The Recipe

*   Load the second table of a presentation as a `DocumentTable`, limiting the number of loaded rows
*   Assemble a document using the table as a data source

### Download

#### Data Source Document

*   [Managers Data.pptx](https://github.com/groupdocs-assembly/GroupDocs.Assembly-for-Java/blob/master/Examples/GroupDocs.Assembly.Examples.Java/Data/Data%20Sources/Presentation%20DataSource/Managers%20Data.pptx?raw=true)

The presentation contains two tables. The second one lists managers and their total contract prices, with a `Manager` / `Total Contract Price` header row.

#### Template

*   [Using Presentation as Table of Data.pptx](https://github.com/groupdocs-assembly/GroupDocs.Assembly-for-Java/blob/master/Examples/GroupDocs.Assembly.Examples.Java/Data/Storage/Presentation%20Templates/Using%20Presentation%20as%20Table%20of%20Data.pptx?raw=true)

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
const table = new groupdocs.DocumentTable('Managers Data.pptx', 1, options);

// Check column count and names.
// NOTE: Default column names are used, because the names are not extracted from the first row.
const columns = table.getColumns();
console.log(columns.getCount());         // 2
console.log(columns.get(0).getName());   // Column1
console.log(columns.get(1).getName());   // Column2

const assembler = new groupdocs.DocumentAssembler();
assembler.assembleDocument('Using Presentation as Table of Data.pptx',
    'Using Presentation as Table of Data_report.pptx',
    new groupdocs.DataSourceInfo(table, 'table'));

process.exit(0);
```

The report lists the header row and the first three managers.

{{< alert style="info" >}}In evaluation mode, text read from presentation documents (both templates and data sources) is truncated, which can make template tags in PPTX templates invalid. Apply a license to process presentations without this limitation. See [Evaluation Limitations and Licensing](/assembly/nodejs-java/evaluation-limitations-and-licensing/).{{< /alert >}}
