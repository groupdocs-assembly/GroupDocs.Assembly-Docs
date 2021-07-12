---
id: groupdocs-assembly-for-java-19-8-release-notes
url: assembly/java/groupdocs-assembly-for-java-19-8-release-notes
title: GroupDocs.Assembly for Java 19.8 Release Notes
weight: 3
description: ""
keywords: 
productName: GroupDocs.Assembly for Java
hideChildren: False
---
{{< alert style="info" >}}This page contains release notes for GroupDocs.Assembly for Java 19.8{{< /alert >}}

## Major Features

Supported saving of assembled Markdown documents to Word Processing formats and saving of assembled Word Processing documents and emails to Markdown.

## Full List of Features Covering all Changes in this Release

| Key | Summary | Category |
| --- | --- | --- |
| ASSEMBLYNET-125  | Support saving of assembled Markdown documents to Word Processing formats  | Feature  |
| ASSEMBLYNET-126  | Support saving of assembled Word Processing documents to Markdown  | Feature  |
| ASSEMBLYNET-127  | Support saving of assembled emails to Markdown  | Feature  |

## Public API and Backward Incompatible Changes 

{{< alert style="info" >}}This section lists public API changes that were introduced in GroupDocs.Assembly for Java 19.8. It includes not only new and obsoleted public methods, but also a description of any changes in the behavior behind the scenes in GroupDocs.Assembly which may affect existing code. Any behavior introduced that could be seen as a regression and modifies existing behavior is especially important and is documented here.{{< /alert >}}

Since version 19.8, the GroupDocs.Assembly provides abilities for saving of assembled Markdown documents to Word Processing formats and saving of assembled Word Processing documents and emails to Markdown. 

{{< alert style="warning" >}}For a moment the following Markdown features are supported:HeadingsBlock quotesHorizontal rulesBold emphasisItalic emphasisThe set of supported Markdown features will be extended in future releases of GroupDocs.Assembly.{{< /alert >}}

### New members of FileFormat

**Java**

```java
/**
  * Specifies the Markdown format.
  */
public static final int MARKDOWN;
```

### Assembled Markdown Document to Word Processing Format 

**Use Case:** Saving an assembled Markdown document to a Word Processing format using file extension.

**Java**

```java
final String description =
    "GroupDocs.Assembly for Java is a class library that enables you to generate documents in popular " +
    "office and email file formats based upon template documents and data obtained from various sources " +
    "including databases, XML, JSON, OData, objects of custom Java types, external documents, and more.";
     
DocumentAssembler assembler = new DocumentAssembler();
 
assembler.assembleDocument(
    "ReadMe.md",
    "ReadMe Out.docx",
    new DataSourceInfo("GroupDocs.Assembly for Java", "product"),
    new DataSourceInfo(description, "description"));
```

### Assembled Word Processing Document or Email to Markdown

**Use Case:** Saving an assembled Word Processing document or email to Markdown using file extension.

**Java**

```java
final String description =
    "GroupDocs.Assembly for Java is a class library that enables you to generate documents in popular " +
    "office and email file formats based upon template documents and data obtained from various sources " +
    "including databases, XML, JSON, OData, objects of custom Java types, external documents, and more.";
 
DocumentAssembler assembler = new DocumentAssembler();
 
assembler.assembleDocument(
    "ReadMe.docx",
    "ReadMe Out.md",
    new DataSourceInfo("GroupDocs.Assembly for Java", "product"),
    new DataSourceInfo(description, "description"));
```

### Assembled Word Processing Document or Email to Markdown (Explicit)

**Use Case:** Saving an assembled Word Processing document or email to Markdown using explicit specifying.

**Java**

```java
InputStream sourceStream = ...;
OutputStream targetStream = ...;
 
DataSourceInfo dataSourceInfo = new DataSourceInfo(...);
DocumentAssembler assembler = new DocumentAssembler();
 
assembler.assembleDocument(sourceStream, targetStream, new LoadSaveOptions(FileFormat.MARKDOWN), dataSourceInfo);
```

{{< alert style="warning" >}}The following attached sample templates were used:ReadMe.mdReadMe.docx{{< /alert >}}
