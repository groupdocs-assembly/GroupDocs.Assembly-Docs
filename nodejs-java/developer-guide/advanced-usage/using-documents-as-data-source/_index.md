---
id: using-documents-as-data-source
url: assembly/nodejs-java/using-documents-as-data-source
title: Using Documents as Data Source
weight: 25
description: "Use tables of spreadsheet, word processing and presentation documents as data sources in GroupDocs.Assembly for Node.js via Java with DocumentTable and DocumentTableSet."
keywords: documenttable, documenttableset, documenttableoptions, spreadsheet data source, word table, presentation table, node.js, javascript
productName: GroupDocs.Assembly for Node.js via Java
hideChildren: False
toc: True
---

GroupDocs.Assembly for Node.js via Java can use a table from another document as a data source. The following classes are used:

| Class | Purpose |
| --- | --- |
| `DocumentTable` | A single table loaded from a spreadsheet worksheet, a word processing table or a presentation table. |
| `DocumentTableOptions` | Options for loading a table: whether the first row contains column names, and the row and column index limits. |
| `DocumentTableSet` | All tables of a document loaded as a single operation, with optional relations between them. |

A `DocumentTable` is passed to the engine like any other data source and is treated as a list of rows in templates:

```javascript
const groupdocs = require('@groupdocs/groupdocs.assembly');

const options = new groupdocs.DocumentTableOptions();
options.setFirstRowContainsColumnNames(true);

// Load the first table (worksheet) of the document.
const table = new groupdocs.DocumentTable('Contracts Data.xlsx', 0, options);

const assembler = new groupdocs.DocumentAssembler();
assembler.assembleDocument('template.docx', 'report.docx',
    new groupdocs.DataSourceInfo(table, 'contracts'));

process.exit(0);
```

Key points:

- The second constructor argument is the zero-based index of the table in the document (for spreadsheets, the index of the worksheet).
- When `setFirstRowContainsColumnNames(true)` is not set, the first row is treated as data and default column names are used: `A`, `B`, `C`, ... for spreadsheets and `Column1`, `Column2`, ... for other documents.
- Spaces in column names are replaced with underscores, for example `Contract Price` becomes `Contract_Price`.
- For spreadsheets, a column type is detected from cell values (for example, `double` when all cells are numeric). For other documents, columns are `java.lang.String` by default. See [Changing Automatically Detected Types of DocumentTable Columns](/assembly/nodejs-java/changing-automatically-detected-types-of-documenttable-columns/).
- `setMinRowIndex`, `setMaxRowIndex`, `setMinColumnIndex` and `setMaxColumnIndex` of `DocumentTableOptions` limit the loaded range.
- `DocumentTable` and `DocumentTableSet` also have constructors that accept a Java `InputStream` instead of a file path.

## Articles in this section

- [Using Spreadsheets as Data Sources](/assembly/nodejs-java/using-spreadsheets-as-data-sources/)
- [Using Tables of Presentation Documents as Data Sources](/assembly/nodejs-java/using-tables-of-presentation-documents-as-data-sources/)
- [Using Tables of Word Processing Documents as Data Sources](/assembly/nodejs-java/using-tables-of-word-processing-documents-as-data-sources/)

## Related articles

- [Loading Multiple DocumentTable Objects from a Single File as a Single Operation](/assembly/nodejs-java/loading-multiple-documenttable-objects-from-a-single-file-as-a-single-operation/)
- [Defining Relations Between DocumentTable Instances Loaded from a Single Document](/assembly/nodejs-java/defining-relations-between-documenttable-instances-loaded-from-a-single-document/)
- [Changing Automatically Detected Types of DocumentTable Columns](/assembly/nodejs-java/changing-automatically-detected-types-of-documenttable-columns/)
