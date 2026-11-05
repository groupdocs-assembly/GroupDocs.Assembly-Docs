---
id: assembly-basic-usage-insert-hyperlinks
url: assembly/python-net/basic-usage-insert-hyperlinks
linktitle: Insert Hyperlinks Dynamically
title: Insert Hyperlinks Dynamically
weight: 21
description: "Insert hyperlinks to web addresses, bookmarks, cells and slides into documents with link tags whose address and text come from Python dicts, using GroupDocs.Assembly for Python via .NET."
keywords: insert hyperlinks, dynamic hyperlinks, link URLs, hyperlink text, clickable links, bookmarks, generate links, Python
productName: GroupDocs.Assembly for Python via .NET
hideChildren: False
---

## Overview

GroupDocs.Assembly for Python via .NET enables you to insert hyperlinks dynamically into documents using link tags. Hyperlinks can point to external URLs, bookmarks within the document, or specific cells/slides depending on the document type.

The main classes involved are:
- [DocumentAssembler](https://reference.groupdocs.com/assembly/python-net/groupdocs.assembly/documentassembler/) - assembles documents
- [DataSourceInfo](https://reference.groupdocs.com/assembly/python-net/groupdocs.assembly/datasourceinfo/) - wraps data sources

Here are the steps to insert hyperlinks dynamically:

* Create a template document with link tags
* Use the syntax `<<link [uri_expression][display_text_expression]>>`
* Provide URI and optional display text from your data source
* Assemble the document

{{< alert style="info" >}}
Link tags are replaced with clickable hyperlinks during document assembly. The URI expression is mandatory, while display text is optional.
{{< /alert >}}

## Insert Hyperlink with URL and Text

Insert a hyperlink with both URL and display text:

{{< tabs "example1" >}}
{{< tab "Python" >}}
```python
from groupdocs.assembly import DataSourceInfo, DocumentAssembler

website = {
    "Name": "Visit our website",
    "Url": "https://harborlane.example/",
}

assembler = DocumentAssembler()
assembler.assemble_document("website-link.docx", "website-link-report.docx",
                            DataSourceInfo(website, "website"))

print("Hyperlink inserted successfully.")
```
{{< /tab >}}
{{< tab "website-link.docx" >}}
{{< tab-text >}}
The following sample file is used in this example: [website-link.docx](/assembly/python-net/_sample_files/developer-guide/basic-usage/insert-hyperlinks-dynamically/website-link.docx)
{{< /tab-text >}}
{{< /tab >}}
{{< tab "website-link-report.docx" >}}  
```text
Binary file (DOCX, 7 KB)
```
[Download full output](/assembly/python-net/_output_files/developer-guide/basic-usage/insert-hyperlinks-dynamically/insert_hyperlink_with_url_and_text/website-link-report.docx)
{{< /tab >}}
{{< /tabs >}}

## Template Structure for Hyperlinks

In your template (website-link.docx), use link tags:

```text
Please <<link [website.Url][website.Name]>> for more information.
```

After assembly:

```text
Please Visit our website for more information.
```

(The text "Visit our website" will be a clickable hyperlink to https://harborlane.example/.)

## Hyperlink with URL Only

If you omit the display text, the URL is used as the display text:

{{< tabs "example2" >}}
{{< tab "Python" >}}
```python
from groupdocs.assembly import DataSourceInfo, DocumentAssembler

website = {"Url": "https://harborlane.example/"}

assembler = DocumentAssembler()
assembler.assemble_document("website-url-link.docx", "website-url-link-report.docx",
                            DataSourceInfo(website, "website"))

print("Hyperlink with URL only inserted successfully.")
```
{{< /tab >}}
{{< tab "website-url-link.docx" >}}
{{< tab-text >}}
The following sample file is used in this example: [website-url-link.docx](/assembly/python-net/_sample_files/developer-guide/basic-usage/insert-hyperlinks-dynamically/website-url-link.docx)
{{< /tab-text >}}
{{< /tab >}}
{{< tab "website-url-link-report.docx" >}}  
```text
Binary file (DOCX, 7 KB)
```
[Download full output](/assembly/python-net/_output_files/developer-guide/basic-usage/insert-hyperlinks-dynamically/hyperlink_with_url_only/website-url-link-report.docx)
{{< /tab >}}
{{< /tabs >}}

Template:

```text
Visit <<link [website.Url]>> for more information.
```

## Insert Multiple Hyperlinks from Collection

Insert hyperlinks for each item in a collection:

{{< tabs "example3" >}}
{{< tab "Python" >}}
```python
from groupdocs.assembly import DataSourceInfo, DocumentAssembler

websites = [
    {"Name": "Home", "Url": "https://harborlane.example/"},
    {"Name": "Products", "Url": "https://harborlane.example/products"},
    {"Name": "Contact", "Url": "https://harborlane.example/contact"},
]

assembler = DocumentAssembler()
assembler.assemble_document("website-links.docx", "website-links-report.docx",
                            DataSourceInfo(websites, "websites"))

print("Hyperlinks inserted from collection successfully.")
```
{{< /tab >}}
{{< tab "website-links.docx" >}}
{{< tab-text >}}
The following sample file is used in this example: [website-links.docx](/assembly/python-net/_sample_files/developer-guide/basic-usage/insert-hyperlinks-dynamically/website-links.docx)
{{< /tab-text >}}
{{< /tab >}}
{{< tab "website-links-report.docx" >}}  
```text
Binary file (DOCX, 7 KB)
```
[Download full output](/assembly/python-net/_output_files/developer-guide/basic-usage/insert-hyperlinks-dynamically/insert_multiple_hyperlinks_from_collection/website-links-report.docx)
{{< /tab >}}
{{< /tabs >}}

Template with foreach:

```text
Links:
<<foreach [in websites]>>- <<link [Url][Name]>>
<</foreach>>
```

## Hyperlink to Bookmark (Word Documents)

Link to bookmarks within the same document. When the URI expression gives a bookmark name instead of an address, the link jumps to that bookmark:

{{< tabs "example4" >}}
{{< tab "Python" >}}
```python
from groupdocs.assembly import DataSourceInfo, DocumentAssembler

section = {
    "Title": "Go to Introduction",
    "BookmarkName": "Introduction",
}

assembler = DocumentAssembler()
assembler.assemble_document("bookmark-link.docx", "bookmark-link-report.docx",
                            DataSourceInfo(section, "section"))

print("Bookmark hyperlink inserted successfully.")
```
{{< /tab >}}
{{< tab "bookmark-link.docx" >}}
{{< tab-text >}}
The following sample file is used in this example: [bookmark-link.docx](/assembly/python-net/_sample_files/developer-guide/basic-usage/insert-hyperlinks-dynamically/bookmark-link.docx)
{{< /tab-text >}}
{{< /tab >}}
{{< tab "bookmark-link-report.docx" >}}  
```text
Binary file (DOCX, 7 KB)
```
[Download full output](/assembly/python-net/_output_files/developer-guide/basic-usage/insert-hyperlinks-dynamically/hyperlink_to_bookmark_word_documents/bookmark-link-report.docx)
{{< /tab >}}
{{< /tabs >}}

Template:

```text
<<link [section.BookmarkName][section.Title]>>
```

In this template, the bookmark is on the heading of the second page, and the template creates it too, with a bookmark tag: `<<bookmark [section.BookmarkName]>>Introduction<</bookmark>>`. A bookmark set in Word works the same way.

## Hyperlink to Cell (Spreadsheet Documents)

Link to cells in spreadsheet documents:

{{< tabs "example5" >}}
{{< tab "Python" >}}
```python
from groupdocs.assembly import DataSourceInfo, DocumentAssembler

data = {"CellReference": "A1", "DisplayText": "Go to Home"}

assembler = DocumentAssembler()
assembler.assemble_document("cell-link.xlsx", "cell-link-report.xlsx",
                            DataSourceInfo(data, "data"))

print("Cell hyperlink inserted successfully.")
```
{{< /tab >}}
{{< tab "cell-link.xlsx" >}}
{{< tab-text >}}
The following sample file is used in this example: [cell-link.xlsx](/assembly/python-net/_sample_files/developer-guide/basic-usage/insert-hyperlinks-dynamically/cell-link.xlsx)
{{< /tab-text >}}
{{< /tab >}}
{{< tab "cell-link-report.xlsx" >}}  
```text
Binary file (XLSX, 7 KB)
```
[Download full output](/assembly/python-net/_output_files/developer-guide/basic-usage/insert-hyperlinks-dynamically/hyperlink_to_cell_spreadsheet_documents/cell-link-report.xlsx)
{{< /tab >}}
{{< /tabs >}}

Template (cell A3):

```text
<<link [data.CellReference][data.DisplayText]>>
```

The link gets the text "Go to Home" and points to cell A1 of the same worksheet (`Sheet1!A1`). The tag can also hold the reference itself: `<<link ["A1"]["Go to Home"]>>`.

## Hyperlink to Slide (Presentation Documents)

Link to slides in presentation documents:

{{< tabs "example6" >}}
{{< tab "Python" >}}
```python
from groupdocs.assembly import DataSourceInfo, DocumentAssembler

data = {"SlideNumber": "Slide1", "DisplayText": "Go to First Slide"}

assembler = DocumentAssembler()
assembler.assemble_document("slide-link.pptx", "slide-link-report.pptx",
                            DataSourceInfo(data, "data"))

print("Slide hyperlink inserted successfully.")
```
{{< /tab >}}
{{< tab "slide-link.pptx" >}}
{{< tab-text >}}
The following sample file is used in this example: [slide-link.pptx](/assembly/python-net/_sample_files/developer-guide/basic-usage/insert-hyperlinks-dynamically/slide-link.pptx)
{{< /tab-text >}}
{{< /tab >}}
{{< tab "slide-link-report.pptx" >}}  
```text
Binary file (PPTX, 31 KB)
```
[Download full output](/assembly/python-net/_output_files/developer-guide/basic-usage/insert-hyperlinks-dynamically/hyperlink_to_slide_presentation_documents/slide-link-report.pptx)
{{< /tab >}}
{{< /tabs >}}

Template (second slide):

```text
<<link [data.SlideNumber][data.DisplayText]>>
```

The link on the second slide jumps to the first one. The tag can also hold the target itself: `<<link ["Slide1"]["Go to First Slide"]>>`.

## Using Uri Objects

A .NET program can pass a `System.Uri` object as the address. A Python dict holds the address as a `str`, as all the examples above do; the template needs nothing else.

{{< alert style="warning" >}}
Link tags cannot be used within charts. For hyperlinks in charts, use alternative approaches or place links outside chart elements.
{{< /alert >}}

### Advanced Usage Topics

To learn more about bookmark creation, complex hyperlink scenarios, and advanced link formatting, please refer to the [advanced usage section]({{< ref "assembly/python-net/developer-guide/advanced-usage/_index.md" >}}).

## More resources

### GitHub Examples

You may easily run the code above and see the feature in action in our GitHub examples:

* [GroupDocs.Assembly for .NET examples, plugins, and showcase](https://github.com/groupdocs-assembly/GroupDocs.Assembly-for-.NET)
* [GroupDocs.Assembly for Java examples, plugins, and showcase](https://github.com/groupdocs-assembly/GroupDocs.Assembly-for-Java)
* [GroupDocs.Assembly for Python via .NET examples, plugins, and showcase](https://github.com/groupdocs-assembly/GroupDocs.Assembly-for-Python-via-.NET)

### Free Online Apps

Along with the full-featured library, we provide simple but powerful free online apps.

To assemble documents from templates and data sources, you can use the online apps from the **[GroupDocs.Assembly App Product Family](https://products.groupdocs.app/assembly/family)**.
