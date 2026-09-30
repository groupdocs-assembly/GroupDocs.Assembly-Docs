---
id: working-with-groupdocs-assembly-engine
url: assembly/nodejs-java/working-with-groupdocs-assembly-engine
title: Working with GroupDocs.Assembly Engine
weight: 2
description: "How GroupDocs.Assembly for Node.js via Java processes templates: template syntax, expressions, data bands, conditional blocks and the engine API."
keywords: template syntax, expressions, data bands, conditional blocks, report generation, node.js
productName: GroupDocs.Assembly for Node.js via Java
hideChildren: False
toc: True
---
## About this section

The articles in this section cover the concepts to consider when creating document templates for your reports: the template syntax, composing expressions, and other syntax elements. They also describe how the GroupDocs.Assembly engine reads the syntax, evaluates expressions against your data, and produces the resulting document.

GroupDocs.Assembly for Node.js via Java runs the Java assembly engine. Template syntax is identical to GroupDocs.Assembly for Java, and template expressions follow Java types and semantics. Data is supplied from Node.js through `JsonDataSource`, `XmlDataSource`, `CsvDataSource`, `DataSet`, or `DocumentTable` objects.

## At a glance

### Steps you follow

In a nutshell, you follow these steps when using the GroupDocs.Assembly engine:

1.  Create a data source in one of the supported data formats (for example, a JSON file loaded with `JsonDataSource`).
2.  Create a template conforming to the supported syntax and expressions.
3.  Pass the data source and the template to the engine by calling `DocumentAssembler.assembleDocument`.

```javascript
const groupdocs = require('@groupdocs/groupdocs.assembly');

const dataSource = new groupdocs.JsonDataSource('managers.json');
const assembler = new groupdocs.DocumentAssembler();
assembler.assembleDocument('template.docx', 'report.docx',
    new groupdocs.DataSourceInfo(dataSource, 'managers'));
```

### The actions by GroupDocs.Assembly engine

As a result of passing a template and a data source, the engine performs the following actions:

1.  Sequentially evaluates the expressions against the passed data source object.
2.  Processes the results of the expressions according to their roles.
3.  Replaces the corresponding tags with appropriate contents.

## Articles in this section
