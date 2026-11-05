---
id: inserting-hyperlinks-dynamically
url: assembly/python-net/inserting-hyperlinks-dynamically
title: Inserting Hyperlinks Dynamically
weight: 2
description: "Inserting Hyperlinks Dynamically with GroupDocs.Assembly for Python via .NET: the template, the Python data and the code."
keywords: inserting hyperlinks dynamically, GroupDocs.Assembly, Python, report generation
productName: GroupDocs.Assembly for Python via .NET
hideChildren: False
---
{{< alert style="info" >}}The example reads the shop data described in [The Business Layer]({{< ref "assembly/python-net/developer-guide/basic-usage/working-with-a-business-case/the-business-layer.md" >}}).{{< /alert >}}

## Inserting Hyperlinks Dynamically

Using GroupDocs.Assembly, you can insert hyperlinks to your reports dynamically using link tags. The syntax of a link tag is defined as follows:

```text
<<link [uri_expression][display_text_expression]>>
```

Here, **uri\_expression** defines URI for a hyperlink to be inserted dynamically. This expression is mandatory and must return a non-empty value. In turn, **display\_text\_expression** defines text to be displayed for the hyperlink. This expression is optional. If it is omitted or returns an empty value, then during runtime, a value of **uri\_expression** is used as display text as well. Values of both **uri\_expression** and **display\_text\_expression** can be of any types. During runtime, **Object.ToString()** is invoked to get textual representations of these expressions’ values, which is useful for expressions of types like Uri, for example, while building a report, **uri\_expression** and **display\_text\_expression** are evaluated and their results are used to construct a hyperlink that replaces the corresponding link tag then.

### Dynamic insertion of links to bookmarks 

#### Insertion of links for Word Processing documents and Emails

You can also insert links to bookmarks to your reports dynamically using link tags. The syntax of a link tag is defined as follows:

```text
<<link [uri_or_bookmark_expression][display_text_expression]>>
```

Here, **uri\_or\_bookmark\_expression** defines URI or the name of a bookmark within the same document for a hyperlink to be inserted dynamically. This expression is mandatory and must return a non-empty value.In turn, **display\_text\_expression** defines text to be displayed for the hyperlink. This expression is optional. If it is omitted or returns an empty value, then during runtime, a value of **uri\_or\_bookmark\_expression** is used as display text as well.

{{< alert style="warning" >}}

* Values of both uri_or_bookmark_expression and display_text_expression can be of any types. During runtime, Object.ToString() is invoked to get textual representations of these expressions’ values, which is useful for expressions of types like Uri, for example. While building a report, uri_or_bookmark_expression and display_text_expression are evaluated and their results are used to construct a hyperlink that replaces the corresponding link tag then. If uri_or_bookmark_expression returns the name of a bookmark in the same document, then the hyperlink navigates to the bookmark. Otherwise, the hyperlink navigates to a corresponding external resource.

* A link tag cannot be used within a chart.

{{< /alert >}}

#### Insertion of links to cells for Spreadsheet documents

For Spreadsheet documents, behavior of link tags is changed as follows. If an expression defined within a link tag is evaluated to a cell or cell range reference during runtime, then the tag is replaced with a link to the corresponding cell or cell range.

The following table describes supported formats of cell and cell range references.

| Description | Format | Example |
| --- | --- | --- |
| Reference to a cell within the same worksheet | cell\_name | A1 |
| Reference to a cell in another worksheet | worksheet\_name!cell\_name | Sheet1!A1 |
| Reference to a cell range within the same worksheet | start\_cell\_name:end\_cell\_name | A1:B2 |
| Reference to a cell range in another worksheet | worksheet\_name!start\_cell\_name:end\_cell\_name | Sheet1!A1:B2 |

Following is sample syntax, If the insertion of the link to cell A1 is required :

```text
<<link ["A1"] ["Home"]>>
```

#### Insertion of links to slides for Presentation documents

For Presentation documents, behavior of link tags is changed as follows. If an expression defined within a link tag is evaluated to a "SlideN" value, where N is a one-based index of a slide within the same Presentation document, then the tag is replaced with a link to the corresponding slide during run time.

See the example of the syntax as follows:

```text
<<link ["Slide1"] ["Home"]>>
```

## Code Examples and Templates

### Word Processing Documents

{{< tabs "example1" >}}
{{< tab "Python" >}}
```python
from groupdocs.assembly import DataSourceInfo, DocumentAssembler

assembler = DocumentAssembler()
assembler.assemble_document("inserting-hyperlink.docx", "inserting-hyperlink-report.docx", [
    DataSourceInfo("https://harborlane.example/", "uriExpression"),
    DataSourceInfo("Harbor Lane Provisions", "displayTextExpression"),
])
```
{{< /tab >}}
{{< tab "inserting-hyperlink.docx" >}}
{{< tab-text >}}
The following sample file is used in this example: [inserting-hyperlink.docx](/assembly/python-net/_sample_files/developer-guide/advanced-usage/inserting-hyperlinks-or-bookmarks/inserting-hyperlinks-dynamically/inserting-hyperlink.docx)
{{< /tab-text >}}
{{< /tab >}}
{{< tab "inserting-hyperlink-report.docx" >}}  
```text
Binary file (DOCX, 10 KB)
```
[Download full output](/assembly/python-net/_output_files/developer-guide/advanced-usage/inserting-hyperlinks-or-bookmarks/inserting-hyperlinks-dynamically/word_processing_documents/inserting-hyperlink-report.docx)
{{< /tab >}}
{{< /tabs >}}

#### Download

*   [inserting-hyperlink.docx](/assembly/python-net/_sample_files/developer-guide/advanced-usage/inserting-hyperlinks-or-bookmarks/inserting-hyperlinks-dynamically/inserting-hyperlink.docx)
*   [inserting-hyperlink.pptx](/assembly/python-net/_sample_files/developer-guide/advanced-usage/inserting-hyperlinks-or-bookmarks/inserting-hyperlinks-dynamically/inserting-hyperlink.pptx)
*   [inserting-hyperlink.xlsx](/assembly/python-net/_sample_files/developer-guide/advanced-usage/inserting-hyperlinks-or-bookmarks/inserting-hyperlinks-dynamically/inserting-hyperlink.xlsx)
*   [inserting-hyperlink.msg](/assembly/python-net/_sample_files/developer-guide/advanced-usage/inserting-hyperlinks-or-bookmarks/inserting-hyperlinks-dynamically/inserting-hyperlink.msg)

### Presentation Documents 

{{< tabs "example2" >}}
{{< tab "Python" >}}
```python
from groupdocs.assembly import DataSourceInfo, DocumentAssembler

assembler = DocumentAssembler()
assembler.assemble_document("inserting-hyperlink.pptx", "inserting-hyperlink-report.pptx", [
    DataSourceInfo("https://harborlane.example/", "uriExpression"),
    DataSourceInfo("Harbor Lane Provisions", "displayTextExpression"),
])
```
{{< /tab >}}
{{< tab "inserting-hyperlink.pptx" >}}
{{< tab-text >}}
The following sample file is used in this example: [inserting-hyperlink.pptx](/assembly/python-net/_sample_files/developer-guide/advanced-usage/inserting-hyperlinks-or-bookmarks/inserting-hyperlinks-dynamically/inserting-hyperlink.pptx)
{{< /tab-text >}}
{{< /tab >}}
{{< tab "inserting-hyperlink-report.pptx" >}}  
```text
Binary file (PPTX, 37 KB)
```
[Download full output](/assembly/python-net/_output_files/developer-guide/advanced-usage/inserting-hyperlinks-or-bookmarks/inserting-hyperlinks-dynamically/presentation_documents/inserting-hyperlink-report.pptx)
{{< /tab >}}
{{< /tabs >}}

#### Download

### Spreadsheet Documents 

{{< tabs "example3" >}}
{{< tab "Python" >}}
```python
from groupdocs.assembly import DataSourceInfo, DocumentAssembler

assembler = DocumentAssembler()
assembler.assemble_document("inserting-hyperlink.xlsx", "inserting-hyperlink-report.xlsx", [
    DataSourceInfo("https://harborlane.example/", "uriExpression"),
    DataSourceInfo("Harbor Lane Provisions", "displayTextExpression"),
])
```
{{< /tab >}}
{{< tab "inserting-hyperlink.xlsx" >}}
{{< tab-text >}}
The following sample file is used in this example: [inserting-hyperlink.xlsx](/assembly/python-net/_sample_files/developer-guide/advanced-usage/inserting-hyperlinks-or-bookmarks/inserting-hyperlinks-dynamically/inserting-hyperlink.xlsx)
{{< /tab-text >}}
{{< /tab >}}
{{< tab "inserting-hyperlink-report.xlsx" >}}  
```text
Binary file (XLSX, 9 KB)
```
[Download full output](/assembly/python-net/_output_files/developer-guide/advanced-usage/inserting-hyperlinks-or-bookmarks/inserting-hyperlinks-dynamically/spreadsheet_documents/inserting-hyperlink-report.xlsx)
{{< /tab >}}
{{< /tabs >}}

#### Download

### Email Documents

{{< tabs "example4" >}}
{{< tab "Python" >}}
```python
from groupdocs.assembly import DataSourceInfo, DocumentAssembler

assembler = DocumentAssembler()
assembler.assemble_document("inserting-hyperlink.msg", "inserting-hyperlink-report.msg", [
    DataSourceInfo("https://harborlane.example/", "uriExpression"),
    DataSourceInfo("Harbor Lane Provisions", "displayTextExpression"),
    DataSourceInfo("Harbor Lane Provisions <orders@harborlane.example>", "sender"),
    DataSourceInfo(["Quayside Bistro <orders@quaysidebistro.example>", "jonas.weber@harborlane.example"], "recipients"),
    DataSourceInfo("amara.osei@harborlane.example", "cc"),
    DataSourceInfo("Inserting hyperlink", "subject"),
])
```
{{< /tab >}}
{{< tab "inserting-hyperlink.msg" >}}
{{< tab-text >}}
The following sample file is used in this example: [inserting-hyperlink.msg](/assembly/python-net/_sample_files/developer-guide/advanced-usage/inserting-hyperlinks-or-bookmarks/inserting-hyperlinks-dynamically/inserting-hyperlink.msg)
{{< /tab-text >}}
{{< /tab >}}
{{< tab "inserting-hyperlink-report.msg" >}}  
```text
Binary file (MSG, 16 KB)
```
[Download full output](/assembly/python-net/_output_files/developer-guide/advanced-usage/inserting-hyperlinks-or-bookmarks/inserting-hyperlinks-dynamically/email_documents/inserting-hyperlink-report.msg)
{{< /tab >}}
{{< /tabs >}}

#### Download
