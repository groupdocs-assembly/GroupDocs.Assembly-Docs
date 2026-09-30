---
id: removing-empty-paragraphs
url: assembly/nodejs-java/removing-empty-paragraphs
title: Removing Empty Paragraphs
weight: 37
description: "Remove paragraphs that become empty after template tags are processed, using DocumentAssemblyOptions.REMOVE_EMPTY_PARAGRAPHS in GroupDocs.Assembly for Node.js via Java."
keywords: empty paragraphs, REMOVE_EMPTY_PARAGRAPHS, DocumentAssemblyOptions, setOptions, node.js
productName: GroupDocs.Assembly for Node.js via Java
hideChildren: False
toc: True
---
GroupDocs.Assembly can remove paragraphs that become empty after template syntax tags are removed or replaced with empty values. To enable this, apply the `DocumentAssemblyOptions.REMOVE_EMPTY_PARAGRAPHS` option to a `DocumentAssembler` instance through `DocumentAssembler.setOptions()`.

`DocumentAssemblyOptions` members are exposed in Node.js as plain numbers (bit flags), so several options can be combined with the bitwise OR operator:

```javascript
assembler.setOptions(groupdocs.DocumentAssemblyOptions.REMOVE_EMPTY_PARAGRAPHS
    | groupdocs.DocumentAssemblyOptions.INLINE_ERROR_MESSAGES);
```

Consider a template with the following paragraphs:

```
Prefix
<<[""]>>
Suffix

Prefix
<<if [false]>>
Text to be removed
<</if>>
Suffix
```

Without the option, the paragraphs that held the `<<[""]>>` and `<<if>>` tags stay in the report as empty lines. With `REMOVE_EMPTY_PARAGRAPHS` applied, they are removed, while paragraphs that were already empty in the template are kept:

```
Prefix
Suffix

Prefix
Suffix
```

## Removing empty paragraphs in a Word Processing document

The template does not reference any data, so a dummy data source is passed.

{{< tabs "empty-paragraphs-word" >}}
{{< tab "JavaScript" >}}
```javascript
const groupdocs = require('@groupdocs/groupdocs.assembly');

const templatePath = "Empty Paragraph.docx";
const reportPath = "Empty Paragraph_report.docx";

const assembler = new groupdocs.DocumentAssembler();
assembler.setOptions(groupdocs.DocumentAssemblyOptions.REMOVE_EMPTY_PARAGRAPHS);
assembler.assembleDocument(templatePath, reportPath,
    new groupdocs.DataSourceInfo("dummy", "dummy"));

process.exit(0);
```
{{< /tab >}}
{{< /tabs >}}

### Download

*   [Empty Paragraph.docx](https://github.com/groupdocs-assembly/GroupDocs.Assembly-for-Java/blob/master/Examples/GroupDocs.Assembly.Examples.Java/Data/Storage/Word%20Templates/Empty%20Paragraph.docx?raw=true)

## Removing empty paragraphs in a Presentation document

The option works the same way for presentation templates: use the code above with a PPTX template (for example, `Empty Paragraph.pptx`) and a PPTX output file.

### Download

*   [Empty Paragraph.pptx](https://github.com/groupdocs-assembly/GroupDocs.Assembly-for-Java/blob/master/Examples/GroupDocs.Assembly.Examples.Java/Data/Storage/Presentation%20Templates/Empty%20Paragraph.pptx?raw=true)

## Removing empty paragraphs in an Email document

{{< tabs "empty-paragraphs-email" >}}
{{< tab "JavaScript" >}}
```javascript
const groupdocs = require('@groupdocs/groupdocs.assembly');

const templatePath = "Empty Paragraph.msg";
const reportPath = "Empty Paragraph_report.msg";

const assembler = new groupdocs.DocumentAssembler();
assembler.setOptions(groupdocs.DocumentAssemblyOptions.REMOVE_EMPTY_PARAGRAPHS);
assembler.assembleDocument(templatePath, reportPath,
    new groupdocs.DataSourceInfo("dummy", "dummy"));

process.exit(0);
```
{{< /tab >}}
{{< /tabs >}}

### Download

*   [Empty Paragraph.msg](https://github.com/groupdocs-assembly/GroupDocs.Assembly-for-Java/blob/master/Examples/GroupDocs.Assembly.Examples.Java/Data/Storage/Email%20Templates/Empty%20Paragraph.msg?raw=true)
