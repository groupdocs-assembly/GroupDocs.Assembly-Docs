---
id: using-markdown-documents
url: assembly/java/using-markdown-documents
title: Using Markdown Documents
weight: 39
description: ""
keywords: 
productName: GroupDocs.Assembly for Java
hideChildren: False
---
{{< alert style="info" >}}This feature is supported by version 19.8 or greater.{{< /alert >}}{{< alert style="info" >}}The code uses some of the objects defined in [The Business Layer](https://docs.groupdocs.com/assembly/java/the-business-layer/).{{< /alert >}}

## Markdown Documents (MD) 

**Markdown** is a [lightweight markup language](https://en.wikipedia.org/wiki/Lightweight_markup_language) intended for one purpose, to be used to format text on the web with plain text formatting syntax. Let it be clear that Markdown is not a replacement for HTML because its syntax is very small, containing a very small subset of HTML tags. The reason behind the Markdown is to make it easy to read, write and edit prose. In other words we can say that HTML is a publishing format while the Markdown is a writing format.

The text files created with Markdown language dialects is saved with **.MD** or **.MARKDOWN** file extension. The MD files are saved in plain text format that uses Markdown language which also includes inline text symbols, defining how a text can be formatted such as indentations, table formatting, fonts, and headers.

## Working with Markdown Documents

Since version 19.8, the GroupDocs.Assembly provides abilities for saving of assembled Markdown documents to Word Processing formats and saving of assembled Word Processing documents and emails to Markdown. 

The API supports the following Markdown features:

*   Headings
*   Block quotes
*   Horizontal rules
*   Bold emphasis
*   Italic emphasis

### Extended the set of supported Markdown features

{{< alert style="info" >}}This feature is supported by version 19.11 or greater.{{< /alert >}}

Since version 19.11, the following Markdown features are supported when saving assembled Markdown documents to Word Processing formats and saving assembled Word Processing documents and emails to Markdown:

*   [Indented code blocks ](https://spec.commonmark.org/0.29/#indented-code-blocks)
*   [Fenced code blocks](https://spec.commonmark.org/0.29/#fenced-code-blocks)
*   [Inline code spans](https://spec.commonmark.org/0.29/#code-spans)
*   [Strikethrough text](https://github.com/adam-p/markdown-here/wiki/Markdown-Cheatsheet#emphasis)
*   Unordered list (version 20.3 or later)

Following sections show that how we can load from and save to Markdown documents:

### Saving an Assembled Markdown Documents to Word Processing Docs

Suppose, we have an assembled Markdown (MD) document ([ReadMe.md](https://docs.groupdocs.com/download/attachments/85230860/ReadMe.md?version=1&modificationDate=1566999867974&api=v2)) as template having the content as shown below:

```java
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

{{< gist GroupDocsGists a71a5d818455bbb866dc60349138fcd5 saveMdtoWord_UsingExtension_19.8.java >}}

The resultant word document ([ReadMe Out.docx](https://docs.groupdocs.com/download/attachments/85230860/ReadMe%20Out.docx?version=1&modificationDate=1566999867970&api=v2)) is available for download.

### Saving an Assembled Word Processing Document or Email to Markdown

{{< alert style="info" >}}The version 19.8 supports only assembled emails and Word Processing documents to save into Markdown format.{{< /alert >}}

Suppose, we have a Word Processing template([ReadMe.docx](https://docs.groupdocs.com/download/attachments/85230860/ReadMe.docx?version=1&modificationDate=1567001059552&api=v2)) having the same content as above Markdown template.

 The following code snippet demonstrates the saving this assembled Word Processing document to a Markdown file.

{{< gist GroupDocsGists a71a5d818455bbb866dc60349138fcd5 saveWordOrEmailtoMD_UsingExtension_19.8.java >}}

The resultant word document ([ReadMe Out.md](https://docs.groupdocs.com/download/attachments/85230860/ReadMe%20Out.md?version=1&modificationDate=1567001143475&api=v2)) is available for download.

### Saving an Assembled Word Processing Document or Email to Markdown (Explicit)

The following code snippet shows the saving of an assembled Word Processing document or email to Markdown using explicit specifying:

{{< gist GroupDocsGists a71a5d818455bbb866dc60349138fcd5 saveWordOrEmailtoMD_Explicit_19.8.java >}}


