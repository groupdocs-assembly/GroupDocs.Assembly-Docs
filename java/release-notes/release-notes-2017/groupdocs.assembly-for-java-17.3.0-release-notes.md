---
id: groupdocs-assembly-for-java-17-3-0-release-notes
url: assembly/java/groupdocs-assembly-for-java-17-3-0-release-notes
title: GroupDocs.Assembly for Java 17.3.0 Release Notes
weight: 6
description: ""
keywords: 
productName: GroupDocs.Assembly for Java
hideChildren: False
---
{{< alert style="info" >}}This page contains release notes for GroupDocs.Assembly for Java 17.3.0{{< /alert >}}

## Major Features

Supported document assembly for Plain Text, HTML, and XML file formats.

### All Changes

| Key | Summary | Category |
| --- | --- | --- |
| ASSEMBLYNET-30 | Support document assembly for Plain Text file formats | Feature |
| ASSEMBLYNET-31 | Support document assembly for HTML file formats | Feature |
| ASSEMBLYNET-36 | Support document assembly for XML files of general form | Feature |

## Public API and Backward Incompatible Changes

{{< alert style="info" >}}This section lists public API changes that were introduced in GroupDocs.Assembly for Java 17.3.0 It includes not only new and obsoleted public methods, but also a description of any changes in the behavior behind the scenes in GroupDocs.Assembly which may affect existing code. Any behavior introduced that could be seen as a regression and modifies existing behavior is especially important and is documented here.{{< /alert >}}

### Added Support for HTML, XML, and Plain Text File Formats

#### Supported Features for HTML, XML, and Plain Text File Formats

The following table provides information on those GroupDocs.Assembly features that are partially supported or not supported at all for HTML, XML, and plain text file formats.

| Feature | HTML Status | XML Status | Plain Text Status |
| --- | --- | --- | --- |
| Inserting Charts Dynamically | Not available | Not available | Not available |
| Inserting Documents Dynamically | To be supported | Not supported | Not supported |
| Inserting Images Dynamically | Supported, to be extended | Not available | Not available |

{{< alert style="warning" >}}The rest of GroupDocs.Assembly features provided for other file formats are available for HTML, XML, and plain text file formats to the full extent.{{< /alert >}}

#### Specifics of Working with HTML and XML File Formats

GroupDocs.Assembly treats HTML and XML tags in template documents as common text. That is, to output HTML or XML tags using a data band or conditional block, these tags must be included to the body of the corresponding data band or conditional block as in the following example. Given that items is an enumeration of strings "Item1", "Item2", and "Item3", you can use the following HTML template to output the items in a bulleted list.

```java
<html>
<body>
<ul>
<<foreach [item in items]>>
<li><<[item]>></li>
<</foreach>>
</ul>
</body>
</html>

```

In this case, GroupDocs.Assembly produces the following result document.

```java
<html>
<body>
<ul>

<li>Item1</li>

<li>Item2</li>

<li>Item3</li>

</ul>
</body>
</html>

```

The resulting document looks in a web browser as follows.

*   Item1
*   Item2
*   Item3

### Escaping Special Characters

GroupDocs.Assembly does not require you to escape special characters such as '<', '>', and others in HTML and XML templates while declaring GroupDocs.Assembly tags. However, if you need your HTML and XML templates to be correctly viewed by web browsers, you can escape special characters in accordance with HTML and XML standards. GroupDocs.Assembly understands both unescaped and escaped characters in HTML and XML templates. For example, the following two template fragments produce the same results.

**Fragment 1**

```java
<<[value]>>

```

**Fragment 2**

```java
&lt;&lt;[value]&gt;&gt;

```

{{< alert style="warning" >}}GroupDocs.Assembly supports all numeric and named character references defined in latest HTML and XML specifications.{{< /alert >}}

### Inserting Images Dynamically (HTML only)

You can insert images into HTML documents dynamically using a combination of HTML and GroupDocs.Assembly tags. Basically there are the following two options to achieve this.

**Option 1. Specifying Image URL**

To specify an image URL dynamically, you can use the following syntax.

```java
<img src="<<[url_expression]>>"/>

```

Here, `url_expression` stands for an expression returning a URL string like "/images/foo.png".

**Option 2. Embedding Image Data**

To embed an image into an HTML document, you can use syntax as in the following example.

```java
<img src="data:image_mime_type;base64,<<[ImageUtil.GetBytesAsBase64(path)]>>"/>

```

Here, `image_mime_type` stands for an image mime type like "image/png", `path` stands for the local path to an image file to be embedded, and `ImageUtil` stands for an external class defined in your application as follows.

```java
public class ImageUtil
{
    public static String GetBytesAsBase64(String path) throws Exception
    {
        java.io.ByteArrayOutputStream stream = new java.io.ByteArrayOutputStream();
        java.nio.file.Files.copy(java.nio.file.Paths.get(path), stream);
        return java.util.Base64.getEncoder().encodeToString(stream.toByteArray());
    }
} 

```

{{< alert style="warning" >}}Although in this example ImageUtil loads an image from a local file, it can be easily extended to load images from streams, for example.{{< /alert >}}

To make this example work, the type of ImageUtil must be set known for a `DocumentAssembler` instance before assembling a document like in the following code snippet.

```java
DocumentAssembler assembler = new DocumentAssembler();
assembler.getKnownTypes().add(ImageUtil.class);
assembler.assembleDocument(...);
```
