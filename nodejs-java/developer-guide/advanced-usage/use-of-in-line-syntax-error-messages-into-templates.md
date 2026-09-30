---
id: use-of-in-line-syntax-error-messages-into-templates
url: assembly/nodejs-java/use-of-in-line-syntax-error-messages-into-templates
title: Use of In-line Syntax Error Messages into Templates
weight: 38
description: "Write template syntax error messages into the assembled document instead of throwing, using DocumentAssemblyOptions.INLINE_ERROR_MESSAGES in GroupDocs.Assembly for Node.js via Java."
keywords: inline error messages, INLINE_ERROR_MESSAGES, template syntax error, DocumentAssemblyOptions, node.js
productName: GroupDocs.Assembly for Node.js via Java
hideChildren: False
toc: True
---
In-line template syntax error messages are supported for Word Processing, Presentation, Spreadsheet, Email and Plain Text documents.

## Use of in-line syntax error messages

By default, `DocumentAssembler` throws an exception when it encounters a template syntax error. Such an exception provides information on the reason of the error and specifies the tag or expression part where the error is encountered. In most cases, this information is enough to find the place in a template causing the error and fix it. In Node.js, the exception is a JavaScript `Error` whose `message` contains the Java exception text, for example:

```
java.lang.IllegalStateException: An error has been encountered at the end of expression 'name]>'. An assignment operator is expected.
```

However, when dealing with complex templates containing a large number of tags, it becomes harder to find the exact place in a template causing an error. To make things easier, the engine supports the `DocumentAssemblyOptions.INLINE_ERROR_MESSAGES` option that writes a syntax error message into the report at the exact position where the error occurs.

{{< alert style="warning" >}}A template syntax error message is written using a bold font to make it more apparent.{{< /alert >}}

Consider the following template.

```
<<var [name]>>
```

By default, such a template causes the engine to throw an exception while building a report. However, when `DocumentAssemblyOptions.INLINE_ERROR_MESSAGES` is applied, no exception is thrown and the report looks as follows.

```
<<var [name] Error! An assignment operator is expected. >>
```

{{< alert style="warning" >}}Only messages describing errors in template syntax can be in-lined. Messages describing errors encountered during expression evaluation are not in-lined.{{< /alert >}}

When `DocumentAssemblyOptions.INLINE_ERROR_MESSAGES` is applied, the Boolean value returned by `DocumentAssembler.assembleDocument` indicates whether building of a report was finished successfully (`true`) or was interrupted because of a template syntax error (`false`). This enables you to process reports whose building succeeded or failed differently, as shown in the following code snippet.

{{< tabs "inline-error-messages" >}}
{{< tab "JavaScript" >}}
```javascript
const groupdocs = require('@groupdocs/groupdocs.assembly');

// Source template and destination PDF report
const templatePath = "Inline Error Demo.docx";
const reportPath = "Inline Error Demo.pdf";

// Enable in-line error messages
const assembler = new groupdocs.DocumentAssembler();
assembler.setOptions(groupdocs.DocumentAssemblyOptions.INLINE_ERROR_MESSAGES);

const dataSource = new groupdocs.JsonDataSource("ManagerData.json");

// assembleDocument returns false if the template contains a syntax error
const success = assembler.assembleDocument(templatePath, reportPath,
    new groupdocs.LoadSaveOptions(groupdocs.FileFormat.PDF),
    new groupdocs.DataSourceInfo(dataSource, "managers"));

if (success) {
    console.log("No error found in the template.");
} else {
    console.log("Do something with a report containing a template syntax error.");
}

process.exit(0);
```
{{< /tab >}}
{{< /tabs >}}

{{< alert style="warning" >}}This article uses a Word Processing template. The process for the other file formats is the same.{{< /alert >}}

## Download demo file

*   [Inline Error Demo.docx](https://github.com/groupdocs-assembly/GroupDocs.Assembly-for-Java/blob/master/Examples/GroupDocs.Assembly.Examples.Java/Data/Storage/Word%20Templates/Inline%20Error%20Demo.docx?raw=true)
