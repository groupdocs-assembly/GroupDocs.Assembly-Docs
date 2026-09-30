---
id: changing-target-file-format
url: assembly/nodejs-java/changing-target-file-format
title: Changing Target File Format
weight: 36
description: "Save an assembled document in a different format with GroupDocs.Assembly for Node.js via Java, using the output file extension or LoadSaveOptions."
keywords: target file format, convert, pdf, LoadSaveOptions, FileFormat, node.js
productName: GroupDocs.Assembly for Node.js via Java
hideChildren: False
toc: True
---
GroupDocs.Assembly can save an assembled document in a format other than the format of its template. The target file format is determined either by the extension of the output file or by explicit specifying. You can change the target file format when assembling the following kinds of documents:

*   Word Processing documents
*   Spreadsheet documents
*   Presentation documents
*   Email documents
*   Text documents

Supported output file formats depending on input file formats are listed on the [Supported Document Formats](/assembly/nodejs-java/supported-document-formats/) page.

The examples below use the `SimpleDatasetDemo.docx` template and the `ManagerData.json` data described in [Working with JSON Data Sources](/assembly/nodejs-java/working-with-json-data-sources/).

## Changing target file format using file extension

When the output is a file path, the engine picks the format from its extension. Here, a DOCX template is saved as PDF:

{{< tabs "target-format-extension" >}}
{{< tab "JavaScript" >}}
```javascript
const groupdocs = require('@groupdocs/groupdocs.assembly');

const templatePath = "SimpleDatasetDemo.docx";
const reportPath = "SimpleDatasetDemo_report.pdf";

const dataSource = new groupdocs.JsonDataSource("ManagerData.json");

const assembler = new groupdocs.DocumentAssembler();
assembler.assembleDocument(templatePath, reportPath,
    new groupdocs.DataSourceInfo(dataSource, "managers"));

process.exit(0);
```
{{< /tab >}}
{{< /tabs >}}

## Changing target file format using explicit specifying

Pass a `LoadSaveOptions` instance created with a `FileFormat` value to set the target format explicitly. The explicit format takes effect regardless of the output file extension (or its absence).

{{< tabs "target-format-explicit" >}}
{{< tab "JavaScript" >}}
```javascript
const groupdocs = require('@groupdocs/groupdocs.assembly');

const templatePath = "SimpleDatasetDemo.docx";
const reportPath = "SimpleDatasetDemo_report.pdf";

const dataSource = new groupdocs.JsonDataSource("ManagerData.json");
const saveOptions = new groupdocs.LoadSaveOptions(groupdocs.FileFormat.PDF);

const assembler = new groupdocs.DocumentAssembler();
assembler.assembleDocument(templatePath, reportPath, saveOptions,
    new groupdocs.DataSourceInfo(dataSource, "managers"));

process.exit(0);
```
{{< /tab >}}
{{< /tabs >}}

Other values of `FileFormat` include `DOCX`, `ODT`, `RTF`, `HTML`, `MHTML`, `XPS`, `TEXT`, `MARKDOWN`, `XLSX`, `PPTX`, `EML`, `MSG_UNICODE` and more.
