---
id: groupdocs-assembly-for-java-20-12-release-notes
url: assembly/java/groupdocs-assembly-for-java-20-12-release-notes
title: GroupDocs.Assembly for Java 20.12 Release Notes
weight: 40
description: ""
keywords: 
productName: GroupDocs.Assembly for Java
hideChildren: False
---
## Major Features

Provided options to control JSON simple values’ recognition and supported working with the XLT Spreadsheet document format.

## Full List of Features Covering all Changes in this Release

| Key             | Summary                                                      | Category |
| :-------------- | :----------------------------------------------------------- | :------- |
| ASSEMBLYNET-174 | Provide a mode where types of JSON simple values are determined from JSON notation itself | Feature  |
| ASSEMBLYNET-175 | Provide a way to parse date-time values using an exact format for JsonDataSource | Feature  |
| ASSEMBLYNET-177 | Support working with XLT format                              | Feature  |

## Public API and Backward Incompatible Changes 

{{< alert style="info" >}}This section lists public API changes that were introduced in GroupDocs.Assembly for Java 20.12. It includes not only new and obsoleted public methods, but also a description of any changes in the behavior behind the scenes in GroupDocs.Assembly which may affect existing code. Any behavior introduced that could be seen as a regression and modifies existing behavior is especially important and is documented here.{{< /alert >}}

### Provided Options to Control JSON Simple Values’ Recognition

A detailed description of this feature can be found in the ["Working with JSON Data Sources"](https://docs.groupdocs.com/assembly/java/working-with-json-data-sources/#recognition-of-json-simple-values) section.

### Supported Working with the XLT Spreadsheet Document Format

Starting from the 20.12 version, GroupDocs.Assembly provides abilities for loading of template XLT Spreadsheet documents and saving of assembled Spreadsheet documents to the XLT format.

{{< alert style="info" >}}For information on supported file formats, see the page ["Supported Document Formats"](https://docs.groupdocs.com/assembly/java/supported-document-formats/#supported-output-file-formats-depending-on-input-file-formats).{{< /alert >}}

#### New members of FileFormat

{{< highlight csharp >}}
/**
	* Specifies the Microsoft Excel 97 - 2007 Binary Template format.
	*/
public static final int XLT;
{{< /highlight >}}

#### UC1: Loading of an XLT template for Spreadsheet document assembly

{{< highlight csharp >}}
DocumentAssembler assembler = new DocumentAssembler();
assembler.assembleDocument("template.xlt", "result.xlsx", ...);
{{< /highlight >}}

#### UC2: Saving an assembled Spreadsheet document to the XLT format using file extension

{{< highlight csharp >}}
DocumentAssembler assembler = new DocumentAssembler();
assembler.assembleDocument("template.xlsx", "result.xlt", ...);
{{< /highlight >}}

#### UC3: Saving an assembled Spreadsheet document to the XLT format using explicit specifying

{{< highlight csharp >}}
InputStream sourceStream = ...;
OutputStream targetStream = ...;

DocumentAssembler assembler = new DocumentAssembler();
assembler.assembleDocument(sourceStream, targetStream, new LoadSaveOptions(FileFormat.XLT), ...);
{{< /highlight >}}