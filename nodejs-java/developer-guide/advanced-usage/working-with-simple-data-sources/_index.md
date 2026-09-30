---
id: working-with-simple-data-sources
url: assembly/nodejs-java/working-with-simple-data-sources
title: Working with Simple Data Sources
weight: 40
description: "Use JSON, XML and CSV files directly as data sources in GroupDocs.Assembly for Node.js via Java with JsonDataSource, XmlDataSource and CsvDataSource."
keywords: json data source, xml data source, csv data source, JsonDataSource, XmlDataSource, CsvDataSource, node.js
productName: GroupDocs.Assembly for Node.js via Java
hideChildren: False
toc: True
---
## Support for simple and standalone data sources

GroupDocs.Assembly for Node.js via Java can read JSON, XML and CSV data directly, without building a `DataSet` first. Each format has its own data source class:

| Class | Data | Load options class |
| --- | --- | --- |
| `JsonDataSource` | JSON file or stream | `JsonDataLoadOptions` |
| `XmlDataSource` | XML file or stream (with an optional XML schema) | `XmlDataLoadOptions` |
| `CsvDataSource` | CSV file or stream | `CsvDataLoadOptions` |

All three classes recognize typed values (numbers, Boolean values, dates) from their string representations, so you can use arithmetic, aggregate extension methods and custom number and date-time formats in templates.

A data source object is wrapped in a `DataSourceInfo` and passed to `DocumentAssembler.assembleDocument`:

```javascript
const groupdocs = require('@groupdocs/groupdocs.assembly');

const dataSource = new groupdocs.JsonDataSource("managers.json");
const assembler = new groupdocs.DocumentAssembler();
assembler.assembleDocument("template.docx", "report.docx",
    new groupdocs.DataSourceInfo(dataSource, "managers"));
```

###### Articles in this section
