---
id: loading-multiple-documenttable-objects-from-a-single-file-as-a-single-operation
url: assembly/nodejs-java/loading-multiple-documenttable-objects-from-a-single-file-as-a-single-operation
title: Loading Multiple DocumentTable Objects from a Single File as a Single Operation
weight: 31
description: "Load all tables of a document at once with DocumentTableSet and control loading of each table with a load handler in GroupDocs.Assembly for Node.js via Java."
keywords: documenttableset, documenttable, idocumenttableloadhandler, documenttableloadargs, multiple tables, node.js, javascript
productName: GroupDocs.Assembly for Node.js via Java
hideChildren: False
toc: True
---

`DocumentTableSet` loads all tables of a document as a single operation. The loaded tables are available through `getTables()`, which returns a collection of `DocumentTable` objects accessible by index or by name.

Each `DocumentTable` provides:

*   `getName()` / `setName()` – the table name. By default, tables are named `Table1`, `Table2`, and so on; for spreadsheets, names are taken from worksheet names.
*   `getIndexInDocument()` – the zero-based index of the table in the document.

To control how each table is loaded, pass an implementation of the Java interface `com.groupdocs.assembly.IDocumentTableLoadHandler`. In JavaScript, create it with `java.newProxy` from the `java` package. The handler's `handle(args)` method receives a `DocumentTableLoadArgs` object with the following members:

*   `getTableIndex()` – the index of the table being loaded.
*   `isLoaded(false)` – skips loading of the table.
*   `getOptions()` / `setOptions()` – the `DocumentTableOptions` used to load the table.

### Download

#### Data Source Document

*   [Multiple Tables Data.docx](https://github.com/groupdocs-assembly/GroupDocs.Assembly-for-Java/blob/master/Examples/GroupDocs.Assembly.Examples.Java/Data/Data%20Sources/Word%20DataSource/Multiple%20Tables%20Data.docx?raw=true)

The document contains three tables with header rows: planets (`Planet`, `Number`), persons (`First Name`, `Last Name`) and companies (`Name`, `Address`).

#### Template

*   [Using Document Table Set as Data Source.pptx](https://github.com/groupdocs-assembly/GroupDocs.Assembly-for-Java/blob/master/Examples/GroupDocs.Assembly.Examples.Java/Data/Storage/Presentation%20Templates/Using%20Document%20Table%20Set%20as%20Data%20Source.pptx?raw=true)

The template contains three tables. Their data rows contain the following tags:

```
<<foreach [in Planets]>><<[Planet]>>  |  <<[Number]>><</foreach>>
<<foreach [in Persons]>><<[First_Name]>>  |  <<[Last_Name]>><</foreach>>
<<foreach [in Companies]>><<[Name]>>  |  <<[Address]>><</foreach>>
```

Here `|` separates table cells.

## Loading DocumentTableSet Using Default Options

```javascript
const groupdocs = require('@groupdocs/groupdocs.assembly');

// Load all document tables using default options.
const tableSet = new groupdocs.DocumentTableSet('Multiple Tables Data.docx');

// Check loading.
const tables = tableSet.getTables();
console.log(tables.getCount());          // 3
console.log(tables.get(0).getName());    // Table1
console.log(tables.get(1).getName());    // Table2
console.log(tables.get(2).getName());    // Table3

process.exit(0);
```

## Loading DocumentTableSet Using Custom Options

The following handler loads the first table with default options, skips the second table, and extracts column names from the first row of the third table:

```javascript
const java = require('java');
const groupdocs = require('@groupdocs/groupdocs.assembly');

const customDocumentTableLoadHandler = java.newProxy('com.groupdocs.assembly.IDocumentTableLoadHandler', {
    handle: function (args) {
        switch (args.getTableIndex()) {
            case 0:
                // Do nothing. The table is loaded with default options.
                break;
            case 1:
                // Discard loading of the table completely.
                args.isLoaded(false);
                break;
            case 2:
                // Load the table with custom options.
                args.setOptions(new groupdocs.DocumentTableOptions());
                args.getOptions().setFirstRowContainsColumnNames(true);
                break;
        }
    }
});

// Load document tables using custom options.
const tableSet = new groupdocs.DocumentTableSet('Multiple Tables Data.docx', customDocumentTableLoadHandler);

// Ensure that the second table is not loaded.
const tables = tableSet.getTables();
console.log(tables.getCount());          // 2
console.log(tables.get(0).getName());    // Table1
console.log(tables.get(1).getName());    // Table3

// Ensure that default options are used to load the first table (default column names are used).
const firstColumns = tables.get(0).getColumns();
console.log(firstColumns.get(0).getName(), firstColumns.get(1).getName());   // Column1 Column2

// Ensure that custom options are used to load the third table (column names are extracted).
const thirdColumns = tables.get(1).getColumns();
console.log(thirdColumns.get(0).getName(), thirdColumns.get(1).getName());   // Name Address

process.exit(0);
```

## Using DocumentTableSet as Data Source

A `DocumentTableSet` can be passed to the engine as a data source without a name. Its tables are then referenced in the template by their names:

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

const tableSet = new groupdocs.DocumentTableSet('Multiple Tables Data.docx',
    columnNameExtractingDocumentTableLoadHandler);

// Set table names for convenience.
tableSet.getTables().get(0).setName('Planets');
tableSet.getTables().get(1).setName('Persons');
tableSet.getTables().get(2).setName('Companies');

// Pass DocumentTableSet as a data source.
const assembler = new groupdocs.DocumentAssembler();
assembler.assembleDocument('Using Document Table Set as Data Source.pptx', 'out.pptx',
    new groupdocs.DataSourceInfo(tableSet));

process.exit(0);
```

{{< alert style="info" >}}In evaluation mode, text read from PPTX templates is truncated, which can make template tags invalid. Apply a license to process presentations without this limitation, or use a template of another format. See [Evaluation Limitations and Licensing](/assembly/nodejs-java/evaluation-limitations-and-licensing/).{{< /alert >}}

## See Also

*   [Defining Relations Between DocumentTable Instances Loaded from a Single Document](/assembly/nodejs-java/defining-relations-between-documenttable-instances-loaded-from-a-single-document/)
*   [Using Documents as Data Source](/assembly/nodejs-java/using-documents-as-data-source/)
