---
id: groupdocs-assembly-for-java-20-3-release-notes
url: assembly/java/groupdocs-assembly-for-java-20-3-release-notes
title: GroupDocs.Assembly for Java 20.3 Release Notes
weight: 100
description: ""
keywords: 
productName: GroupDocs.Assembly for Java
hideChildren: False
---
### Major Features

*   Supported unordered lists for Markdown.
*   Supported access to related DataTable using relation name.
*   Supported dynamic insertion of bookmarks for Word Processing documents and emails with HTML and RTF bodies.
*   Supported dynamic naming of cell ranges for Spreadsheet documents.
*   Supported dynamic insertion of documents and images from Base64-encoded bytes.
*   Supported dynamic checkbox value setting for Word Processing documents.

## Full List of Features Covering all Changes in this Release

### All Changes

| Key | Summary | Category |
| --- | --- | --- |
| ASSEMBLYNET-135  | Support unordered lists for Markdown  | Feature  |
| ASSEMBLYNET-136  | Support access to related DataTable using relation name  | Feature  |
| ASSEMBLYNET-139  | Support dynamic insertion of bookmarks for Word Processing documents  | Feature  |
| ASSEMBLYNET-140  | Support dynamic insertion of bookmarks for emails with HTML and RTF bodies  | Feature  |
| ASSEMBLYNET-141  | Support dynamic naming of cell ranges for Spreadsheet documents  | Feature  |
| ASSEMBLYNET-145  | Support dynamic checkbox value setting for Word Processing documents  | Feature  |
| ASSEMBLYNET-147  | Support dynamic image and document insertion from Base64-encoded bytes  | Feature  |
| ASSEMBLYNET-137  | NullReferenceException is thrown when evaluating a null-conditional operator on missing related DataRow  | Bug  |
| ASSEMBLYNET-138  | Page breaks are removed if DocumentAssemblyOptions.RemoveEmptyParagraphs is used  | Bug  |
| ASSEMBLYNET-142  | Simple-type array with one element does not work for JsonDataSource  | Bug  |
| ASSEMBLYNET-148  | ArgumentException is thrown if image or document expression returns an empty string  | Bug  |

## Public API and Backward Incompatible Changes 

### Supported access to related DataTable using relation name

The Document Assembly Engine enables you to access a data associated with a particular *DataRow* instance in template expressions using the "." operator. See "[Working with DataRow Objects](https://docs.groupdocs.com/assembly/java/template-syntax-part-1-of-2/#using-data-sources)" for more information.

### Supported unordered lists for Markdown

From now on, unordered lists (see chapter 5.3 of [Markdown specification](https://spec.commonmark.org/0.28/)) are supported when saving assembled Markdown documents to Word Processing formats and emails to Markdown.

### Supported dynamic insertion of bookmarks for Word Processing documents and emails with HTML and RTF bodies

You can insert bookmarks to your reports dynamically using bookmark tags. Syntax of a bookmark tag is defined as follows.

```java
<<bookmark [bookmark_expression]>>
bookmarked_content
<</bookmark>>
```

Here, bookmark\_expression defines the name of a bookmark to be inserted during runtime. This expression is mandatory and must return a non-empty value. While building a report, bookmark\_expression is evaluated and its result is used to construct a bookmark start and end that replace corresponding opening and closing bookmark tags respectively.

{{< alert style="warning" >}}A bookmark tag cannot be used within a chart.{{< /alert >}}

### Supported dynamic naming of cell ranges for Spreadsheet documents

Template syntax for dynamic naming of cell ranges for Spreadsheet documents is the same as above point. The difference is that it results to insertion of named cell ranges instead of bookmarks.

### Supported dynamic insertion of documents and images from Base64-encoded bytes and dynamic checkbox value setting

#### Inserting Documents Dynamically

You can insert contents of outer documents to your reports dynamically using doc tags. A doc tag denotes a placeholder within a template for a document to be inserted during runtime.

Syntax of a doc tag is defined as follows.

```java
<<doc [document_expression]>>
```

{{< alert style="warning" >}}A doc tag can be used almost anywhere in a template document except textboxes and charts.{{< /alert >}}

An expression declared within a doc tag is used by the assembler to load a document to be inserted during runtime. The expression must return a value of one of the following types:

*   A byte array containing document data
*   An InputStream[ instance able to read document data](http://msdn.microsoft.com/en-us/library/system.io.stream(v=vs.110).aspx)
*   An instance of the Document class
*   A string containing a document URI, path, or Base64-encoded document data

While building a report, an expression declared within a doc tag is evaluated and its result is used to load a document which content replaces the doc tag then.

{{< alert style="warning" >}}If an expression declared within a doc tag returns a stream object, then the stream is closed by the assembler as soon as a corresponding document is loaded.{{< /alert >}}

By default, a document being inserted is not checked against template syntax and is not populated with data. However, you can enable this by using a build switch as follows.

```java
<<doc [document_expression] -build>>
```

When a build switch is used, the assembler treats a document being inserted as a template that can access the following data available at the scope of a corresponding doc tag:

*   Data sources
*   Variables
*   A contextual object 
*   Known external types 

{{< alert style="warning" >}}Dynamic insertion of documents from Base64-encoded bytes is available for file formats where dynamic document insertion is available for Word Processing documents and emails with HTML and RTF bodies only.{{< /alert >}}

#### Inserting Images Dynamically

You can insert images to your reports dynamically using image tags. To declare a dynamically inserted image within your template, do the following steps:

1.  Add a textbox to your template at the place where you want an image to be inserted.
2.  Set common image attributes such as frame, size, and others for the textbox, making the textbox look like a blank inserted image.
3.  Specify an image tag within the textbox using the following syntax.

```java
<<image [image_expression]>>
```

The expression declared within an image tag is used by the assembler to build an image to be inserted. The expression must return a value of one of the following types:

*   A byte array containing an image data
*   A InputStream instance able to read an image data
*   An BufferredImage object
*   A string containing an image URI, path, or Base64-encoded image data

While building a report, the following procedure is applied to an image tag:

1.  The expression declared within the tag is evaluated and its result is used to form an image.
2.  The corresponding textbox is filled with this image.
3.  The tag is removed from the textbox.

{{< alert style="warning" >}}If the expression declared within an image tag returns a stream object, then it is closed by the assembler as soon as the corresponding image is built. {{< /alert >}}

By default, the assembler stretches an image filling a textbox to the size of the textbox. However, you can change this behavior in the following ways:

*   To keep the width of the textbox and change its height preserving the ratio of the image, use the fitHeight switch as follows.

```java
<<image [image_expression] -fitHeight>>
```

*   To keep the height of the textbox and change its width preserving the ratio of the image, use the fitWidth switch as follows.

```java
<<image [image_expression] -fitWidth>>
```

*   To change the size of the textbox according to the size of the image, use the fitSize switch as follows.

```java
<<image [image_expression] -fitSize>>
```

*   To change the size of the textbox according to the size of the image without increasing the size of the textbox, use the fitSizeLim switch as follows.

```java
<<image [image_expression] -fitSizeLim>>
```

{{< alert style="warning" >}}If the size of the image is greater than the size of the textbox, then the fitSizeLim switch acts like fitHeight or fitWidth. Otherwise, the fitSizeLim switch acts like fitSize.{{< /alert >}}{{< alert style="warning" >}}Dynamic insertion of images from Base64-encoded bytes is available for file formats where dynamic image insertion is available for almost all supported file formats.{{< /alert >}}

#### Setting Checkbox Values Dynamically

You can set checkbox values to either checked or unchecked in your reports dynamically by taking the following steps:

1.  Add a checkbox content control to your template at a place where you want it to appear in a result document.
2.  By editing content control properties, add a check tag to the title of the checkbox content control using the following syntax.

```java
<<check [conditional_expression]>>
```

Here, conditional\_expression defines a condition upon which the value of the checkbox content control is to be set to checked (or unchecked, if the condition is not met). The conditional expression must return a Boolean value.

While building a report, a conditional expression declared within a check tag is evaluated and the value of its containing checkbox content control is set accordingly. The check tag itself is removed then.

{{< alert style="warning" >}}Dynamic checkbox value setting is available for Word Processing documents only.{{< /alert >}}
