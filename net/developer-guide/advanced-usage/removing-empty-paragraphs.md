---
id: removing-empty-paragraphs
url: assembly/net/removing-empty-paragraphs
title: Removing Empty Paragraphs
weight: 39
description: ""
keywords: 
productName: GroupDocs.Assembly for .NET
hideChildren: False
---
{{< alert style="info" >}}This feature is supported by version 18.10. or greater.{{< /alert >}}{{< alert style="info" >}}The code uses some of the objects defined in [The Business Layer](https://docs.groupdocs.com/assembly/net/the-business-layer/).{{< /alert >}}

GroupDocs.Assembly for .NET API supports the removal of paragraphs becoming empty after template syntax tags are removed or replaced with empty values. A new member **RemoveEmptyParagraphs** is added to [DocumentAssemblyOptions](https://reference.groupdocs.com/net/assembly/groupdocs.assembly/documentassemblyoptions)**.** When this new option is applied to [DocumentAssembler](https://reference.groupdocs.com/net/assembly/groupdocs.assembly/documentassembler) options through [DocumentAssembler.Options](https://reference.groupdocs.com/net/assembly/groupdocs.assembly/documentassembler/properties/options), the engine additionally removes empty paragraphs.

## Removing Empty Paragraphs in Word Processing Document

{{< gist GroupDocsGists 1baca62f7f2fb6b15feacc8686d431fa >}}

### Download

*   [Empty Paragraph.docx](https://github.com/groupdocs-assembly/GroupDocs.Assembly-for-.NET/blob/master/Examples/Data/Source/Word%20Templates/Empty%20Paragraph.docx)

## Removing Empty Paragraphs in Presentation Document

{{< gist GroupDocsGists 7c9fc9e774e865e047e668ee915fea7e >}}

### Download

*   [Empty Paragraph.pptx](https://github.com/groupdocs-assembly/GroupDocs.Assembly-for-.NET/blob/master/Examples/Data/Source/Presentation%20Templates/Empty%20Paragraph.pptx)

## Removing Empty Paragraphs in Email Document

{{< gist GroupDocsGists 5ba8a40ae2ca44cc4bd4576d5a2648e9 >}}

### Download

*   [Empty Paragraph.msg](https://github.com/groupdocs-assembly/GroupDocs.Assembly-for-.NET/blob/master/Examples/Data/Source/Email%20Templates/Empty%20Paragraph.msg)

## Removing Empty Paragraphs in Spreadsheet and Plain Text Documents

{{< alert style="info" >}}This feature is supported by version 26.11 or greater.{{< /alert >}}

In spreadsheet templates and plain text documents, a paragraph is a line of text: a line of a cell's text, or of a text document, that becomes empty after template tags are removed or replaced with empty values is removed together with its line break. Tags such as `<<if>>` and `<<foreach>>` written on their own lines no longer leave empty lines behind.

```csharp
DocumentAssembler assembler = new DocumentAssembler();
assembler.Options = DocumentAssemblyOptions.RemoveEmptyParagraphs;
assembler.AssembleDocument("Empty paragraph.txt", "result.txt", new DataSourceInfo("dummy", "dummy"));
```

Template:

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

Result:

```
Prefix
Suffix

Prefix
Suffix
```

The same template text in a cell of a spreadsheet gives the same result within the cell. Example: [RemoveEmptyParagraphs.cs](https://github.com/groupdocs-assembly/GroupDocs.Assembly-for-.NET/blob/master/Examples/GroupDocs.Assembly.Examples.CSharp/AdvancedUsage/RemoveEmptyParagraphs.cs), which assembles the DOCX, PPTX, MSG, XLSX and TXT variants.

### Download

*   [Empty paragraph.xlsx](https://github.com/groupdocs-assembly/GroupDocs.Assembly-for-.NET/blob/master/Examples/Data/Templates/Empty%20paragraph.xlsx)
*   [Empty paragraph.txt](https://github.com/groupdocs-assembly/GroupDocs.Assembly-for-.NET/blob/master/Examples/Data/Templates/Empty%20paragraph.txt)

The option in a worked spreadsheet scenario: [Generate Excel reports from a template]({{< ref "/assembly/net/use-cases/generate-excel-reports-from-template.md" >}}).
