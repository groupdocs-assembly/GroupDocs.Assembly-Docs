---
id: updating-fields-while-assembling-word-processing-documents
url: assembly/nodejs-java/updating-fields-while-assembling-word-processing-documents
title: Updating Fields while Assembling Word Processing Documents
weight: 28
description: "Recalculate fields and formulas while assembling Word documents with DocumentAssemblyOptions.UPDATE_FIELDS_AND_FORMULAS in GroupDocs.Assembly for Node.js via Java."
keywords: update fields, formulas, UPDATE_FIELDS_AND_FORMULAS, DocumentAssemblyOptions, word, docx, node.js
productName: GroupDocs.Assembly for Node.js via Java
hideChildren: False
toc: True
---
## Updating fields

By default, fields in a Word Processing template (for example, `=SUM(ABOVE)` formulas in tables) keep the result values stored in the template. Apply the `DocumentAssemblyOptions.UPDATE_FIELDS_AND_FORMULAS` option to make the engine recalculate them while assembling the report.

### The recipe

*   Set up the source template path
*   Set up the destination report path
*   Instantiate the `DocumentAssembler` class
*   Set the `DocumentAssemblyOptions.UPDATE_FIELDS_AND_FORMULAS` option
*   Generate the report

### The template

The template contains a list of clients built from data and a table with a formula field in the last cell:

```
We provide support for the following clients:
<<foreach [in clients]>><<[Name]>>
<</foreach>>
```

| Model | Price |
| --- | --- |
| Lumia 640 XL | 18000 |
| Lumia 550 | 12500 |
| Total | `{ =SUM(ABOVE) \# "#,##0" }` |

The data is a JSON array:

```
[ { "Name": "A Company" }, { "Name": "B Ltd." }, { "Name": "C & D" } ]
```

### The code

{{< tabs "update-fields" >}}
{{< tab "JavaScript" >}}
```javascript
const groupdocs = require('@groupdocs/groupdocs.assembly');

const templatePath = "Update field.docx";
const reportPath = "Update field_report.docx";

const assembler = new groupdocs.DocumentAssembler();
// Recalculate fields and formulas while assembling
assembler.setOptions(groupdocs.DocumentAssemblyOptions.UPDATE_FIELDS_AND_FORMULAS);

const dataSource = new groupdocs.JsonDataSource("clients.json");
assembler.assembleDocument(templatePath, reportPath,
    new groupdocs.DataSourceInfo(dataSource, "clients"));

process.exit(0);
```
{{< /tab >}}
{{< /tabs >}}

In the report, the Total cell shows the recalculated value `30,500` (the number format follows the current culture). Without the option, the field keeps the value that was stored in the template.
