---
id: using-markdown-documents
url: assembly/python-net/using-markdown-documents
title: Using Markdown Documents
weight: 41
description: "Using Markdown Documents with GroupDocs.Assembly for Python via .NET: the template, the Python data and the code."
keywords: using markdown documents, GroupDocs.Assembly, Python, report generation
productName: GroupDocs.Assembly for Python via .NET
hideChildren: False
---
{{< alert style="info" >}}The example reads the shop data described in [The Business Layer]({{< ref "assembly/python-net/developer-guide/basic-usage/working-with-a-business-case/the-business-layer.md" >}}).{{< /alert >}}

## Markdown Documents (MD) 

**Markdown** is a [lightweight markup language](https://en.wikipedia.org/wiki/Lightweight_markup_language) intended for one purpose, to be used to format text on the web with plain text formatting syntax. Let it be clear that Markdown is not a replacement for HTML because its syntax is very small, containing a very small subset of HTML tags. The reason behind the Markdown is to make it easy to read, write and edit prose. In other words we can say that HTML is a publishing format while the Markdown is a writing format.

The text files created with Markdown language dialects is saved with **.MD** or **.MARKDOWN** file extension. The MD files are saved in plain text format that uses Markdown language which also includes inline text symbols, defining how a text can be formatted such as indentations, table formatting, fonts, and headers.

## Working with Markdown Documents

Since version 19.8, the GroupDocs.Assembly provides abilities for saving of assembled Markdown documents to Word Processing formats and saving of assembled Word Processing documents and emails to Markdown. 

The API supports the following Markdown features:

*   Headings
*   Block quotes
*   Horizontal rules
*   Bold emphasis
*   Italic emphasis

### Extended the set of supported Markdown features

Since version 19.11, the following Markdown features are supported when saving assembled Markdown documents to Word Processing formats and saving assembled Word Processing documents and emails to Markdown:

*   [Indented code blocks ](https://spec.commonmark.org/0.29/#indented-code-blocks)
*   [Fenced code blocks](https://spec.commonmark.org/0.29/#fenced-code-blocks)
*   [Inline code spans](https://spec.commonmark.org/0.29/#code-spans)
*   [Strikethrough text](https://github.com/adam-p/markdown-here/wiki/Markdown-Cheatsheet#emphasis)
*   Unordered list (v 19.12 or later)

Following sections show that how we can load from and save to Markdown documents:

### Saving an Assembled Markdown Documents to Word Processing Docs

Suppose, we have an assembled Markdown (MD) document as template having the content as shown below:

```text
# <<[product]>>
-----
## Description
<<[description]>>
## Evaluation and Licensing
The library comes up with some limitations in the evaluation mode. 
In order to test full features of <<[product]>>, 
please request a **free 30-day temporary license**.
```

The following code snippet demonstrates the saving this MD document to a Word Processing file.

{{< tabs "example1" >}}
{{< tab "Python" >}}
```python
from groupdocs.assembly import DataSourceInfo, DocumentAssembler

assembler = DocumentAssembler()
assembler.assemble_document("readme.md", "readme-report.md", [
    DataSourceInfo("Harbor Lane Provisions", "product"),
    DataSourceInfo("Specialty food wholesale from the Quayside, Port Ellery.", "description"),
])
```
{{< /tab >}}
{{< tab "readme.md" >}}
{{< tab-text >}}
The following sample file is used in this example: [readme.md](/assembly/python-net/_sample_files/developer-guide/advanced-usage/using-markdown-documents/readme.md)
{{< /tab-text >}}
{{< /tab >}}
{{< tab "readme-report.md" >}}  
```text
# Harbor Lane Provisions
-----
## Description
Specialty food wholesale from the Quayside, Port Ellery.
## Evaluation and Licensing
The library comes up with some limitations in the evaluation mode. In order to test full features of Harbor Lane Provisions, please request a **free 30-day temporary license**.
```
[Download full output](/assembly/python-net/_output_files/developer-guide/advanced-usage/using-markdown-documents/saving_an_assembled_markdown_documents_to_word_processing_do/readme-report.md)
{{< /tab >}}
{{< /tabs >}}

{{< tabs "example2" >}}
{{< tab "Python" >}}
```python
from groupdocs.assembly import DataSourceInfo, DocumentAssembler

assembler = DocumentAssembler()
assembler.assemble_document("readme.docx", "readme-report.docx", [
    DataSourceInfo("Harbor Lane Provisions", "product"),
    DataSourceInfo("Specialty food wholesale from the Quayside, Port Ellery.", "description"),
])
```
{{< /tab >}}
{{< tab "readme.docx" >}}
{{< tab-text >}}
The following sample file is used in this example: [readme.docx](/assembly/python-net/_sample_files/developer-guide/advanced-usage/using-markdown-documents/readme.docx)
{{< /tab-text >}}
{{< /tab >}}
{{< tab "readme-report.docx" >}}  
```text
Binary file (DOCX, 10 KB)
```
[Download full output](/assembly/python-net/_output_files/developer-guide/advanced-usage/using-markdown-documents/saving_an_assembled_markdown_documents_to_word_processing_do_2/readme-report.docx)
{{< /tab >}}
{{< /tabs >}}

{{< tabs "example3" >}}
{{< tab "Python" >}}
```python
from groupdocs.assembly import DataSourceInfo, DocumentAssembler

assembler = DocumentAssembler()
assembler.assemble_document("list.md", "list-report.md", [
    DataSourceInfo("Harbor Lane Provisions", "product"),
    DataSourceInfo("Specialty food wholesale from the Quayside, Port Ellery.", "description"),
])
```
{{< /tab >}}
{{< tab "list.md" >}}
{{< tab-text >}}
The following sample file is used in this example: [list.md](/assembly/python-net/_sample_files/developer-guide/advanced-usage/using-markdown-documents/list.md)
{{< /tab-text >}}
{{< /tab >}}
{{< tab "list-report.md" >}}  
```text
# List Demo
- foo
- foo
+ bar
```
[Download full output](/assembly/python-net/_output_files/developer-guide/advanced-usage/using-markdown-documents/saving_an_assembled_markdown_documents_to_word_processing_do_3/list-report.md)
{{< /tab >}}
{{< /tabs >}}

{{< tabs "example4" >}}
{{< tab "Python" >}}
```python
from groupdocs.assembly import DataSourceInfo, DocumentAssembler

assembler = DocumentAssembler()
assembler.assemble_document("ordered-list.md", "ordered-list-report.md", [
    DataSourceInfo("Harbor Lane Provisions", "product"),
    DataSourceInfo("Specialty food wholesale from the Quayside, Port Ellery.", "description"),
])
```
{{< /tab >}}
{{< tab "ordered-list.md" >}}
{{< tab-text >}}
The following sample file is used in this example: [ordered-list.md](/assembly/python-net/_sample_files/developer-guide/advanced-usage/using-markdown-documents/ordered-list.md)
{{< /tab-text >}}
{{< /tab >}}
{{< tab "ordered-list-report.md" >}}  
```text
# Harbor Lane Provisions
-----
## Description
Specialty food wholesale from the Quayside, Port Ellery.
## Evaluation and Licensing
The library comes up with some limitations in the evaluation mode. In order to test full features of Harbor Lane Provisions, please request a **free 30-day temporary license**.

# List Demo
1. foo
2. bar
[TRUNCATED]
```
[Download full output](/assembly/python-net/_output_files/developer-guide/advanced-usage/using-markdown-documents/saving_an_assembled_markdown_documents_to_word_processing_do_4/ordered-list-report.md)
{{< /tab >}}
{{< /tabs >}}

{{< tabs "example5" >}}
{{< tab "Python" >}}
```python
from groupdocs.assembly import DataSourceInfo, DocumentAssembler

assembler = DocumentAssembler()
assembler.assemble_document("tables.md", "tables-report.md", [
    DataSourceInfo("Harbor Blend whole bean coffee", "product_1_name"),
    DataSourceInfo("30", "product_1_quantity"),
    DataSourceInfo("Aged harbour cheddar", "product_2_name"),
    DataSourceInfo("8", "product_2_quantity"),
])
```
{{< /tab >}}
{{< tab "tables.md" >}}
{{< tab-text >}}
The following sample file is used in this example: [tables.md](/assembly/python-net/_sample_files/developer-guide/advanced-usage/using-markdown-documents/tables.md)
{{< /tab-text >}}
{{< /tab >}}
{{< tab "tables-report.md" >}}  
```text
## Table

| Item | Price |
| - | - |
| Apple | $1.50 |
| Banana | $1.10 |
| Carrot | $0.75 |

## Justified Table

[TRUNCATED]
```
[Download full output](/assembly/python-net/_output_files/developer-guide/advanced-usage/using-markdown-documents/saving_an_assembled_markdown_documents_to_word_processing_do_5/tables-report.md)
{{< /tab >}}
{{< /tabs >}}

{{< tabs "example6" >}}
{{< tab "Python" >}}
```python
from groupdocs.assembly import DataSourceInfo, DocumentAssembler

assembler = DocumentAssembler()
assembler.assemble_document("autolinks.md", "autolinks-report.md", DataSourceInfo("<https://harborlane.example/>", "url"))
```
{{< /tab >}}
{{< tab "autolinks.md" >}}
{{< tab-text >}}
The following sample file is used in this example: [autolinks.md](/assembly/python-net/_sample_files/developer-guide/advanced-usage/using-markdown-documents/autolinks.md)
{{< /tab-text >}}
{{< /tab >}}
{{< tab "autolinks-report.md" >}}  
```text
## URL

<https://www.google.com/>

## Email address

<JohnDoe@sample.com>

## Template that may recieve an inline link

[TRUNCATED]
```
[Download full output](/assembly/python-net/_output_files/developer-guide/advanced-usage/using-markdown-documents/saving_an_assembled_markdown_documents_to_word_processing_do_6/autolinks-report.md)
{{< /tab >}}
{{< /tabs >}}

{{< tabs "example7" >}}
{{< tab "Python" >}}
```python
from groupdocs.assembly import DataSourceInfo, DocumentAssembler

assembler = DocumentAssembler()
assembler.assemble_document("inline-links.md", "inline-links-report.md", [
    DataSourceInfo("Harbor Lane Provisions", "link_text"),
    DataSourceInfo("https://harborlane.example/", "link"),
])
```
{{< /tab >}}
{{< tab "inline-links.md" >}}
{{< tab-text >}}
The following sample file is used in this example: [inline-links.md](/assembly/python-net/_sample_files/developer-guide/advanced-usage/using-markdown-documents/inline-links.md)
{{< /tab-text >}}
{{< /tab >}}
{{< tab "inline-links-report.md" >}}  
```text
## URL

[Click here to visit the Google home page](https://www.google.com/)

## Email address

[Click here to send an email](JohnDoe@sample.com)

## Custom link

[TRUNCATED]
```
[Download full output](/assembly/python-net/_output_files/developer-guide/advanced-usage/using-markdown-documents/saving_an_assembled_markdown_documents_to_word_processing_do_7/inline-links-report.md)
{{< /tab >}}
{{< /tabs >}}

{{< tabs "example8" >}}
{{< tab "Python" >}}
```python
from groupdocs.assembly import DataSourceInfo, DocumentAssembler

assembler = DocumentAssembler()
assembler.assemble_document("inline-image.md", "inline-image-report.md", [
    DataSourceInfo("Harbor Lane Provisions logo", "alt_text"),
    DataSourceInfo("logo.png", "image_URI"),
])
```
{{< /tab >}}
{{< tab "inline-image.md" >}}
{{< tab-text >}}
The following sample file is used in this example: [inline-image.md](/assembly/python-net/_sample_files/developer-guide/advanced-usage/using-markdown-documents/inline-image.md)
{{< /tab-text >}}
{{< /tab >}}
{{< tab "logo.png" >}}
{{< tab-text >}}
The following sample file is used in this example: [logo.png](/assembly/python-net/_sample_files/developer-guide/advanced-usage/using-markdown-documents/logo.png)
{{< /tab-text >}}
{{< /tab >}}
{{< tab "inline-image-report.md" >}}  
```text
## Local file system image

![Image from the local file system](images/Logo.jpg)

## Image URL

![Image from the web](https://www.aspose.cloud/templates/aspose/App_Themes/V3/images/words/header/aspose_words-for-net.png)

## Custom inline image

[TRUNCATED]
```
[Download full output](/assembly/python-net/_output_files/developer-guide/advanced-usage/using-markdown-documents/saving_an_assembled_markdown_documents_to_word_processing_do_8/inline-image-report.md)
{{< /tab >}}
{{< /tabs >}}

The resultant Word document is produced by the code snippet above.

### Saving an Assembled Word Processing Document or Email to Markdown

{{< alert style="info" >}}The version 19.8 supports only assembled emails and Word Processing documents to save into Markdown format.{{< /alert >}}

Suppose, we have a Word Processing template having the same content as above Markdown template.

The following code snippet demonstrates the saving this assembled Word Processing document to a Markdown file.

The resultant Markdown document is produced by the code snippet above.

### Saving an Assembled Word Processing Document or Email to Markdown (Explicit)

The following code snippet shows the saving of an assembled Word Processing document or email to Markdown using explicit specifying:
