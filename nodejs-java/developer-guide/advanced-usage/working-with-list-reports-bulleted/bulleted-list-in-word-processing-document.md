---
id: bulleted-list-in-word-processing-document
url: assembly/nodejs-java/bulleted-list-in-word-processing-document
title: Bulleted List in Word Processing Document
weight: 1
description: "Generate a bulleted list report in a Word document from JSON data using GroupDocs.Assembly for Node.js via Java."
keywords: bulleted list, word, docx, foreach, json, node.js, javascript
productName: GroupDocs.Assembly for Node.js via Java
hideChildren: False
toc: True
---
{{< alert style="info" >}}In this article, we use GroupDocs.Assembly for Node.js via Java to generate a bulleted list report in a Word document.{{< /alert >}}

## Bulleted list in a Microsoft Word document

### Creating a bulleted list

To add a bulleted list to a Word document:

1.  Place the cursor where the list should appear.
2.  On the **Home** tab, click **Bullets**.
3.  Type the template tags described below and save the document.

### Reporting requirement

As a report developer, you need to meet the following requirements:

*   The report must show all clients in a bulleted list.
*   The report must be generated as a Word document.

### Data source

Save the clients as `clients.json`:

```json
[
  { "Name": "A Company" },
  { "Name": "B Ltd." },
  { "Name": "C & D" },
  { "Name": "E Corp." }
]
```

### Adding syntax to be evaluated by GroupDocs.Assembly engine

Put the opening `foreach` tag and the client name into a bulleted paragraph, and the closing tag into the next paragraph:

```
We provide support for the following clients:
• <<foreach [client in clients]>><<[client.Name]>>
<</foreach>>
```

The engine repeats the bulleted paragraph for every client, so the report contains one bullet per client.

### Download the bulleted list template

Download the sample files used in this article:

*   [bulleted-list-template.docx](/assembly/nodejs-java/_sample_files/developer-guide/bulleted-list-in-word-processing-document/bulleted-list-template.docx)
*   [clients.json](/assembly/nodejs-java/_sample_files/developer-guide/bulleted-list-in-word-processing-document/clients.json)

### Generating the report

```javascript
'use strict';

const groupdocs = require('@groupdocs/groupdocs.assembly');

// "clients" is the data source name used in the template
const dataSource = new groupdocs.JsonDataSource("clients.json");
const dataSourceInfo = new groupdocs.DataSourceInfo(dataSource, "clients");

const assembler = new groupdocs.DocumentAssembler();
assembler.assembleDocument("bulleted-list-template.docx", "bulleted-list-report.docx", dataSourceInfo);

process.exit(0);
```

### Result

The generated [bulleted-list-report.docx](/assembly/nodejs-java/_sample_files/developer-guide/bulleted-list-in-word-processing-document/bulleted-list-report.docx) contains:

We provide support for the following clients:

*   A Company
*   B Ltd.
*   C & D
*   E Corp.

## Bulleted list in an OpenDocument text document

The same template syntax works in ODT documents created with Microsoft Word, LibreOffice or Apache OpenOffice. Save the template as `.odt` and use an `.odt` output file name, or save the report to another format as described in [Changing Target File Format](/assembly/nodejs-java/changing-target-file-format/).
