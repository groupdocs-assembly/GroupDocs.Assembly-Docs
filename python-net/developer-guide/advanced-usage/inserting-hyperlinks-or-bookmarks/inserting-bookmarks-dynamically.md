---
id: inserting-bookmarks-dynamically
url: assembly/python-net/inserting-bookmarks-dynamically
title: Inserting Bookmarks Dynamically
weight: 1
description: "Inserting Bookmarks Dynamically with GroupDocs.Assembly for Python via .NET: the template, the Python data and the code."
keywords: inserting bookmarks dynamically, GroupDocs.Assembly, Python, report generation
productName: GroupDocs.Assembly for Python via .NET
hideChildren: False
---
{{< alert style="info" >}}The example reads the shop data described in [The Business Layer]({{< ref "assembly/python-net/developer-guide/basic-usage/working-with-a-business-case/the-business-layer.md" >}}).{{< /alert >}}

## Inserting Hyperlinks Dynamically

### Dynamic insertion of bookmarks for Word Processing documents and emails with HTML and RTF bodies

You can insert bookmarks to your reports dynamically using bookmark tags. Syntax of a bookmark tag is defined as follows.

```text
<<bookmark [bookmark_expression]>>
bookmarked_content
<</bookmark>>
```

Here, **bookmark\_expression** defines the name of a bookmark to be inserted during run-time. This expression is mandatory and must return a non-empty value. While building a report, **bookmark\_expression** is evaluated and its result is used to construct a bookmark start and end that replace corresponding opening and closing bookmark tags respectively.

{{< alert style="warning" >}}A bookmark tag cannot be used within a chart.{{< /alert >}}

The following code snippet shows how simple you call the document assembler to generate report from the template:

{{< tabs "example1" >}}
{{< tab "Python" >}}
```python
from groupdocs.assembly import DataSourceInfo, DocumentAssembler

assembler = DocumentAssembler()
assembler.assemble_document("inserting-bookmark.docx", "inserting-bookmark-report.docx", [
    DataSourceInfo("hlp_orders", "bookmark_expression"),
    DataSourceInfo("Harbor Lane Provisions", "displayTextExpression"),
])
```
{{< /tab >}}
{{< tab "inserting-bookmark.docx" >}}
{{< tab-text >}}
The following sample file is used in this example: [inserting-bookmark.docx](/assembly/python-net/_sample_files/developer-guide/advanced-usage/inserting-hyperlinks-or-bookmarks/inserting-bookmarks-dynamically/inserting-bookmark.docx)
{{< /tab-text >}}
{{< /tab >}}
{{< tab "inserting-bookmark-report.docx" >}}  
```text
Binary file (DOCX, 10 KB)
```
[Download full output](/assembly/python-net/_output_files/developer-guide/advanced-usage/inserting-hyperlinks-or-bookmarks/inserting-bookmarks-dynamically/dynamic_insertion_of_bookmarks_for_word_processing_documents/inserting-bookmark-report.docx)
{{< /tab >}}
{{< /tabs >}}

### Dynamic naming of cell ranges for Spreadsheet documents

Template syntax and usage of Document Assembler is same as above section for dynamic naming of cell ranges for Spreadsheet documents. The difference is that it results to insertion of named cell ranges instead of bookmarks.

### Download Templates

*   [inserting-bookmark.docx](/assembly/python-net/_sample_files/developer-guide/advanced-usage/inserting-hyperlinks-or-bookmarks/inserting-bookmarks-dynamically/inserting-bookmark.docx)
