---
id: defining-relations-between-documenttable-instances-loaded-from-a-single-document
url: assembly/nodejs-java/defining-relations-between-documenttable-instances-loaded-from-a-single-document
title: Defining Relations Between DocumentTable Instances Loaded from a Single Document
weight: 32
description: "Define parent-child relations between tables of a DocumentTableSet and navigate them in templates with GroupDocs.Assembly for Node.js via Java."
keywords: documenttableset, documenttablerelation, relations, master-detail, spreadsheet, node.js, javascript
productName: GroupDocs.Assembly for Node.js via Java
hideChildren: False
toc: True
---

Relations can be defined between `DocumentTable` instances loaded from a single document into a `DocumentTableSet`. `DocumentTableSet.getRelations()` returns a `DocumentTableRelationCollection`; its `add(parentColumn, childColumn)` method creates a `DocumentTableRelation` between a column of a parent table and a column of a child table.

Once a relation is defined, a template can navigate from a child row to the related parent row by the parent table name (for example, `Manager.Name`), and from a parent row to its child rows.

### Download

#### Data Source Document

*   [Related Tables Data.xlsx](https://github.com/groupdocs-assembly/GroupDocs.Assembly-for-Java/blob/master/Examples/GroupDocs.Assembly.Examples.Java/Data/Data%20Sources/Excel%20DataSource/Related%20Tables%20Data.xlsx?raw=true)

The workbook contains three worksheets:

| Worksheet | Columns |
| --- | --- |
| `MANAGER` | `ID`, `NAME` |
| `CLIENT` | `ID`, `NAME` |
| `CONTRACT` | `ID`, `CLIENT_ID`, `MANAGER_ID`, `PRICE` |

#### Template

*   [Using Document Table Relations.docx](https://github.com/groupdocs-assembly/GroupDocs.Assembly-for-Java/blob/master/Examples/GroupDocs.Assembly.Examples.Java/Data/Storage/Word%20Templates/Using%20Document%20Table%20Relations.docx?raw=true)

The template contains a three-column table. The cells of its data row contain:

```
<<foreach [in Contract]>><<[Manager.Name]>>
```

```
<<[Client.Name]>>
```

```
<<[Price]>><</foreach>>
```

## Using Document Table Relations

```javascript
const java = require('java');
const groupdocs = require('@groupdocs/groupdocs.assembly');

// Extract column names from the first row of every table.
const columnNameExtractingDocumentTableLoadHandler = java.newProxy('com.groupdocs.assembly.IDocumentTableLoadHandler', {
    handle: function (args) {
        args.setOptions(new groupdocs.DocumentTableOptions());
        args.getOptions().setFirstRowContainsColumnNames(true);
    }
});

const tableSet = new groupdocs.DocumentTableSet('Related Tables Data.xlsx',
    columnNameExtractingDocumentTableLoadHandler);

// Define relations between tables.
// NOTE: For spreadsheet documents, table names are extracted from worksheet names.
const tables = tableSet.getTables();
tableSet.getRelations().add(
    tables.get('CLIENT').getColumns().get('ID'),
    tables.get('CONTRACT').getColumns().get('CLIENT_ID'));
tableSet.getRelations().add(
    tables.get('MANAGER').getColumns().get('ID'),
    tables.get('CONTRACT').getColumns().get('MANAGER_ID'));

// Pass DocumentTableSet as a data source.
const assembler = new groupdocs.DocumentAssembler();
assembler.assembleDocument('Using Document Table Relations.docx', 'out.docx',
    new groupdocs.DataSourceInfo(tableSet));

process.exit(0);
```

The report lists every contract with its manager name, client name and price, for example:

| Manager | Client | Contract Price |
| --- | --- | --- |
| John Smith | A Company | 1200000.0 |
| John Smith | B Ltd. | 750000.0 |
| Tony Anderson | E Corp. | 650000.0 |

Table and column names in template expressions are case-insensitive, so `Contract`, `Manager.Name` and `Price` match the `CONTRACT` table and its `NAME` and `PRICE` columns.

## See Also

*   [Loading Multiple DocumentTable Objects from a Single File as a Single Operation](/assembly/nodejs-java/loading-multiple-documenttable-objects-from-a-single-file-as-a-single-operation/)
*   [Using Documents as Data Source](/assembly/nodejs-java/using-documents-as-data-source/)
