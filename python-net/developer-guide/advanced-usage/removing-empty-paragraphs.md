---
id: removing-empty-paragraphs
url: assembly/python-net/removing-empty-paragraphs
title: Removing Empty Paragraphs
weight: 39
description: "Removing Empty Paragraphs with GroupDocs.Assembly for Python via .NET: the template, the Python data and the code."
keywords: removing empty paragraphs, GroupDocs.Assembly, Python, report generation
productName: GroupDocs.Assembly for Python via .NET
hideChildren: False
---
{{< alert style="info" >}}The example reads the shop data described in [The Business Layer]({{< ref "assembly/python-net/developer-guide/basic-usage/working-with-a-business-case/the-business-layer.md" >}}).{{< /alert >}}

GroupDocs.Assembly for Python via .NET API supports the removal of paragraphs becoming empty after template syntax tags are removed or replaced with empty values. A new member **RemoveEmptyParagraphs** is added to [DocumentAssemblyOptions](https://reference.groupdocs.com/assembly/python-net/groupdocs.assembly/documentassemblyoptions/)**.** When this new option is applied to [DocumentAssembler](https://reference.groupdocs.com/assembly/python-net/groupdocs.assembly/documentassembler/) options through [DocumentAssembler.options](https://reference.groupdocs.com/assembly/python-net/groupdocs.assembly/documentassembler/options/), the engine additionally removes empty paragraphs.

## Removing Empty Paragraphs in Word Processing Document

{{< tabs "example1" >}}
{{< tab "Python" >}}
```python
from groupdocs.assembly import DataSourceInfo, DocumentAssembler, DocumentAssemblyOptions

assembler = DocumentAssembler()
assembler.options = DocumentAssemblyOptions.REMOVE_EMPTY_PARAGRAPHS
assembler.assemble_document("empty-paragraph.docx", "empty-paragraph-report.docx", DataSourceInfo("dummy", "dummy"))
```
{{< /tab >}}
{{< tab "empty-paragraph.docx" >}}
{{< tab-text >}}
The following sample file is used in this example: [empty-paragraph.docx](/assembly/python-net/_sample_files/developer-guide/advanced-usage/removing-empty-paragraphs/empty-paragraph.docx)
{{< /tab-text >}}
{{< /tab >}}
{{< tab "empty-paragraph-report.docx" >}}  
```text
Binary file (DOCX, 10 KB)
```
[Download full output](/assembly/python-net/_output_files/developer-guide/advanced-usage/removing-empty-paragraphs/removing_empty_paragraphs_in_word_processing_document/empty-paragraph-report.docx)
{{< /tab >}}
{{< /tabs >}}

### Download

*   [empty-paragraph.docx](/assembly/python-net/_sample_files/developer-guide/advanced-usage/removing-empty-paragraphs/empty-paragraph.docx)
*   [empty-paragraph.pptx](/assembly/python-net/_sample_files/developer-guide/advanced-usage/removing-empty-paragraphs/empty-paragraph.pptx)
*   [empty-paragraph.msg](/assembly/python-net/_sample_files/developer-guide/advanced-usage/removing-empty-paragraphs/empty-paragraph.msg)

## Removing Empty Paragraphs in Presentation Document

{{< tabs "example2" >}}
{{< tab "Python" >}}
```python
from groupdocs.assembly import DataSourceInfo, DocumentAssembler, DocumentAssemblyOptions

assembler = DocumentAssembler()
assembler.options = DocumentAssemblyOptions.REMOVE_EMPTY_PARAGRAPHS
assembler.assemble_document("empty-paragraph.pptx", "empty-paragraph-report.pptx", DataSourceInfo("dummy", "dummy"))
```
{{< /tab >}}
{{< tab "empty-paragraph.pptx" >}}
{{< tab-text >}}
The following sample file is used in this example: [empty-paragraph.pptx](/assembly/python-net/_sample_files/developer-guide/advanced-usage/removing-empty-paragraphs/empty-paragraph.pptx)
{{< /tab-text >}}
{{< /tab >}}
{{< tab "empty-paragraph-report.pptx" >}}  
```text
Binary file (PPTX, 33 KB)
```
[Download full output](/assembly/python-net/_output_files/developer-guide/advanced-usage/removing-empty-paragraphs/removing_empty_paragraphs_in_presentation_document/empty-paragraph-report.pptx)
{{< /tab >}}
{{< /tabs >}}

### Download

## Removing Empty Paragraphs in Email Document

{{< tabs "example3" >}}
{{< tab "Python" >}}
```python
from groupdocs.assembly import DataSourceInfo, DocumentAssembler, DocumentAssemblyOptions

assembler = DocumentAssembler()
assembler.options = DocumentAssemblyOptions.REMOVE_EMPTY_PARAGRAPHS
assembler.assemble_document("empty-paragraph.msg", "empty-paragraph-report.msg", [
    DataSourceInfo("dummy", "dummy"),
    DataSourceInfo("Harbor Lane Provisions <orders@harborlane.example>", "sender"),
    DataSourceInfo(["Quayside Bistro <orders@quaysidebistro.example>", "jonas.weber@harborlane.example"], "recipients"),
    DataSourceInfo("amara.osei@harborlane.example", "cc"),
    DataSourceInfo("Empty paragraph", "subject"),
])
```
{{< /tab >}}
{{< tab "empty-paragraph.msg" >}}
{{< tab-text >}}
The following sample file is used in this example: [empty-paragraph.msg](/assembly/python-net/_sample_files/developer-guide/advanced-usage/removing-empty-paragraphs/empty-paragraph.msg)
{{< /tab-text >}}
{{< /tab >}}
{{< tab "empty-paragraph-report.msg" >}}  
```text
Binary file (MSG, 16 KB)
```
[Download full output](/assembly/python-net/_output_files/developer-guide/advanced-usage/removing-empty-paragraphs/removing_empty_paragraphs_in_email_document/empty-paragraph-report.msg)
{{< /tab >}}
{{< /tabs >}}

### Download
