---
id: quick-start-guide
url: assembly/nodejs-java/quick-start-guide
title: Quick Start Guide
weight: 5
description: "Build your first report with GroupDocs.Assembly for Node.js via Java: create a Word template, load JSON data and generate DOCX and PDF documents."
keywords: quick start, first report, node.js, javascript, json, docx, pdf
productName: GroupDocs.Assembly for Node.js via Java
hideChildren: False
toc: True
---

This guide shows how to generate a Word invoice from a template and JSON data, and how to save the same report as PDF.

Before you start, [install](/assembly/nodejs-java/installation/) the `@groupdocs/groupdocs.assembly` package.

## Prepare the data

Save the following data as `orders.json`:

```json
{
  "Customer": "Northwind Traders",
  "Date": "2026-09-30T00:00:00",
  "Items": [
    { "Product": "Laptop", "Quantity": 2, "Price": 1250.5 },
    { "Product": "Monitor", "Quantity": 3, "Price": 310 },
    { "Product": "Keyboard", "Quantity": 5, "Price": 45.99 }
  ]
}
```

## Create the template

Create a Word document named `invoice-template.docx` with the following content. Template tags are enclosed in `<<` and `>>`, and `order` is the name under which the data source is passed to the engine.

```
Invoice for <<[order.Customer]>>
Date: <<[order.Date]:"yyyy-MM-dd">>
```

Below the text, add a table with a header row, one data row and a total row:

| Product | Quantity | Amount |
| --- | --- | --- |
| `<<foreach [item in order.Items]>><<[item.Product]>>` | `<<[item.Quantity]>>` | `<<[item.Quantity * item.Price]:"0.00">><</foreach>>` |
| Total | | `<<[order.Items.sum(i => i.Quantity * i.Price)]:"0.00">>` |

The `foreach` tag repeats the table row for every item, and the `sum` extension method calculates the total. See [Template Syntax](/assembly/nodejs-java/template-syntax-part-1-of-2/) for the complete syntax reference.

You can also download the ready-to-use [invoice-template.docx](/assembly/nodejs-java/_sample_files/getting-started/quick-start-guide/invoice-template.docx) and [orders.json](/assembly/nodejs-java/_sample_files/getting-started/quick-start-guide/orders.json).

## Generate the report

Create `app.js` next to the template and the data file:

```javascript
'use strict';

const groupdocs = require('@groupdocs/groupdocs.assembly');

// Load data from the JSON file. "order" is the data source name used in the template.
const dataSource = new groupdocs.JsonDataSource("orders.json");
const dataSourceInfo = new groupdocs.DataSourceInfo(dataSource, "order");

// Build the report from the template and the data
const assembler = new groupdocs.DocumentAssembler();
assembler.assembleDocument("invoice-template.docx", "invoice.docx", dataSourceInfo);

console.log("The report is saved to invoice.docx");
process.exit(0);
```

Run the script:

```bash
node app.js
```

The generated [invoice.docx](/assembly/nodejs-java/_sample_files/getting-started/quick-start-guide/invoice.docx) contains:

```
Invoice for Northwind Traders
Date: 2026-09-30
```

| Product | Quantity | Amount |
| --- | --- | --- |
| Laptop | 2 | 2501.00 |
| Monitor | 3 | 930.00 |
| Keyboard | 5 | 229.95 |
| Total | | 3660.95 |

{{< alert style="info" >}}
Number and date formats follow the default locale of the Java virtual machine. Without a license, the report also contains an evaluation watermark; see [Licensing and evaluation](/assembly/nodejs-java/evaluation-limitations-and-licensing/).
{{< /alert >}}

## Save the report as PDF

To save the report in another format, pass `LoadSaveOptions` with the target `FileFormat`. This overload takes the data sources as a Java array, which you can create with the `java` bridge package:

```javascript
'use strict';

const java = require('java');
const groupdocs = require('@groupdocs/groupdocs.assembly');

const dataSource = new groupdocs.JsonDataSource("orders.json");
const dataSourceInfo = new groupdocs.DataSourceInfo(dataSource, "order");
const dataSources = java.newArray('com.groupdocs.assembly.DataSourceInfo', [dataSourceInfo]);

// Save the report as PDF
const saveOptions = new groupdocs.LoadSaveOptions(groupdocs.FileFormat.PDF);

const assembler = new groupdocs.DocumentAssembler();
assembler.assembleDocument("invoice-template.docx", "invoice.pdf", saveOptions, dataSources);

process.exit(0);
```

See [Changing Target File Format](/assembly/nodejs-java/changing-target-file-format/) for more options.

## Next steps

- [Template Syntax - Part 1 of 2](/assembly/nodejs-java/template-syntax-part-1-of-2/)
- [GroupDocs.Assembly Engine APIs](/assembly/nodejs-java/groupdocs-assembly-engine-apis/)
- [Working with JSON, XML and CSV data sources](/assembly/nodejs-java/working-with-simple-data-sources/)
