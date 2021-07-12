---
id: groupdocs-assembly-for-java-19-5-release-notes
url: assembly/java/groupdocs-assembly-for-java-19-5-release-notes
title: GroupDocs.Assembly for Java 19.5 Release Notes
weight: 5
description: ""
keywords: 
productName: GroupDocs.Assembly for Java
hideChildren: False
---
{{< alert style="info" >}}This page contains release notes for GroupDocs.Assembly for Java 19.5.{{< /alert >}}

## Major Features

Supported loading of template documents from HTML with resources and saving of assembled documents to HTML with resources.

## Full List of Features Covering all Changes in this Release

| Key | Summary | Category |
| --- | --- | --- |
| ASSEMBLYNET-86  | Support saving of assembled Word Processing documents to HTML with resources  | Feature  |
| ASSEMBLYNET-87  | Support loading of template documents from HTML with resources  | Feature  |
| ASSEMBLYNET-109  | Support saving of assembled Spreadsheet documents to HTML with resources  | Feature  |
| ASSEMBLYNET-110  | Support saving of assembled Presentation documents to HTML with resources  | Feature  |
| ASSEMBLYNET-111  | Support saving of assembled emails to HTML with resources  | Feature  |
| ASSEMBLYNET-114  | An exception is thrown on saving a document to DOC or PDF assembled from a DOCX template containing charts  | Bug  |
| ASSEMBLYJAVA-13  | Upgrade release JAR to JDK 7 after Java 6 discontinuation  | Enhancement  |

## Public API and Backward Incompatible Changes 

{{< alert style="info" >}}This section lists public API changes that were introduced in GroupDocs.Assembly for Java 19.5. It includes not only new and obsoleted public methods, but also a description of any changes in the behavior behind the scenes in GroupDocs.Assembly which may affect existing code. Any behavior introduced that could be seen as a regression and modifies existing behavior is especially important and is documented here.{{< /alert >}}

### Release JAR was upgraded to JDK 7

Extended Support for Java 6 was officially dropped by Oracle at December 2018. So we have upgraded our release JAR to JDK 7.

### Supported loading of template documents from HTML with resources

From now, the GroupDocs.Assembly supports loading of HTML template documents referencing external resource files to be assembled and saved to non-HTML formats.

#### Changed behavior of DocumentAssembler.assembleDocument overloads accepting file paths

From now, when loading an HTML document from a file, its containing folder is used as a base URI to resolve external resource files' relative URIs to absolute ones by default as shown in the following example.

```java
String myDir = ...
DocumentAssembler assembler = new DocumentAssembler();
 
assembler.assembleDocument(myDir + "TestWordsResourceLoad.htm", myDir + "TestWordsResourceLoad Out.docx", new DataSourceInfo("It should be a jeep image.", "value"));
```

After running the code, the TestWordsResourceLoad Out.docx contains an image, which relative URI is resolved from myDir.

#### Added a new property to LoadSaveOptions

The following property was added.

```java
/**
  * Gets a base URI to resolve external resource files' relative URIs to absolute ones while loading an HTML template document to be assembled and saved to a non-HTML format. The default value is an empty string.
  * <p>
  * When loading an HTML document from a file, its containing folder is used as a base URI by default, which cannot happen when loading an HTML document from a stream. Set this property to specify a base URI when loading an HTML document from a stream or to override the default base URI when loading an HTML document from a file.
  * </p>
  * <p>
  * A value of this property is ignored in the following cases:
  * </p>
  * <ul>
  * <li>
  * An HTML document being loaded contains a BASE HTML element providing a base URI.
  * </li>
  * <li>
  * An HTML document being loaded is to be assembled and saved to HTML (external resource files are not loaded and relative URIs are not changed then).
  * </li>
  * </ul>
  * 
  * @return A base URI to resolve external resource files' relative URIs to absolute ones while loading an HTML template document to be assembled and saved to a non-HTML format.
  */
public String getResourceLoadBaseUri()
 
/**
  * Sets a base URI to resolve external resource files' relative URIs to absolute ones while loading an HTML template document to be assembled and saved to a non-HTML format. The default value is an empty string.
  * <p>
  * When loading an HTML document from a file, its containing folder is used as a base URI by default, which cannot happen when loading an HTML document from a stream. Set this property to specify a base URI when loading an HTML document from a stream or to override the default base URI when loading an HTML document from a file.
  * </p>
  * <p>
  * A value of this property is ignored in the following cases:
  * </p>
  * <ul>
  * <li>
  * An HTML document being loaded contains a BASE HTML element providing a base URI.
  * </li>
  * <li>
  * An HTML document being loaded is to be assembled and saved to HTML (external resource files are not loaded and relative URIs are not changed then).
  * </li>
  * </ul>
  * 
  * @param value A base URI to resolve external resource files' relative URIs to absolute ones while loading an HTML template document to be assembled and saved to a non-HTML format.
  */
public void setResourceLoadBaseUri(String value)
```

In the following example, the default folder used to resolve external resource files' relative URIs is overridden by an explicitly specified folder.

```java
String myDir = ...
DocumentAssembler assembler = new DocumentAssembler();
 
LoadSaveOptions loadSaveOptions = new LoadSaveOptions();
loadSaveOptions.setResourceLoadBaseUri(myDir + "Alternative");
 
assembler.assembleDocument(myDir + "TestWordsResourceLoad.htm", myDir + "TestWordsResourceLoad Out.docx", loadSaveOptions, new DataSourceInfo("It should be a sport car image.", "value"));
```

After running the code, the TestWordsResourceLoad Out.docx contains an image, which relative URI is resolved from the specified alternative folder.

{{< alert style="warning" >}}Download ResourceLoad.zip to get the template documents.{{< /alert >}}

### Supported saving of assembled documents to HTML with resources

From now, the GroupDocs.Assembly supports saving of external resource files while an assembled document loaded from a non-HTML format is being saved to HTML.

#### Changed behavior of DocumentAssembler.assembleDocument overloads accepting file paths

From now, when saving an assembled document to an HTML file, by default, external resource files are stored to a folder having the same name as the HTML file without extension plus the "\_files" suffix. This folder is located in the same folder as the HTML file. The following example illustrates the scenario.

```java
String myDir = ...
DocumentAssembler assembler = new DocumentAssembler();
 
assembler.assembleDocument(myDir + "TestWordsResourceSave.docx", myDir + "TestWordsResourceSave Out.htm", new DataSourceInfo("Hello!", "value"));
```

After running the code, the folder "TestWordsResourceSave Out\_files" is created in myDir and HTML resource files (such as images and stylesheets) are stored in this folder.

#### Added a new property to LoadSaveOptions

The following property was added.

```java
/**
  * Gets a path to a folder to store external resource files while an assembled document loaded from a non-HTML format is being saved to HTML. The default value is an empty string.
  * <p>
  * By default, when saving an assembled document to an HTML file, external resource files are stored to a folder having the same name as the HTML file without extension plus the "_files" suffix. This folder is located in the same folder as the HTML file. However, this cannot be done when saving an assembled document to an HTML stream. Set this property to specify a path to a folder to store external resource files when saving an assembled document to an HTML stream or to override the default folder when saving an assembled document to an HTML file.
  * </p>
  * <p>
  * A value of this property is ignored if an assembled document being saved to HTML was loaded from HTML as well (external resource files are not stored and links to them are not changed then).
  * </p>
  * 
  * @return A path to a folder to store external resource files while an assembled document loaded from a non-HTML format is being saved to HTML.
  */
public String getResourceSaveFolder()
 
/**
  * Sets a path to a folder to store external resource files while an assembled document loaded from a non-HTML format is being saved to HTML. The default value is an empty string.
  * <p>
  * By default, when saving an assembled document to an HTML file, external resource files are stored to a folder having the same name as the HTML file without extension plus the "_files" suffix. This folder is located in the same folder as the HTML file. However, this cannot be done when saving an assembled document to an HTML stream. Set this property to specify a path to a folder to store external resource files when saving an assembled document to an HTML stream or to override the default folder when saving an assembled document to an HTML file.
  * </p>
  * <p>
  * A value of this property is ignored if an assembled document being saved to HTML was loaded from HTML as well (external resource files are not stored and links to them are not changed then).
  * </p>
  * 
  * @param value A path to a folder to store external resource files while an assembled document loaded from a non-HTML format is being saved to HTML.
  */
public void setResourceSaveFolder(String value)
```

In the following example, the default folder used to store HTML resource files is overridden by an explicitly specified folder.

```java
String myDir = ...
DocumentAssembler assembler = new DocumentAssembler();
 
LoadSaveOptions loadSaveOptions = new LoadSaveOptions();
loadSaveOptions.setResourceSaveFolder(myDir + "Alternative");
 
assembler.assembleDocument(myDir + "TestWordsResourceSave.docx", myDir + "TestWordsResourceSave Out.htm", loadSaveOptions, new DataSourceInfo("Hello!", "value"));
```

After running the code, the resource files (such as images and stylesheets) for the saved HTML document are stored to the specified alternative folder.

{{< alert style="warning" >}}Download ResourceSave.zip to get the template documents.{{< /alert >}}
