---
id: "groupdocs-assembly-for-net-25-12-release-notes"
slug: "groupdocs-assembly-for-net-25-12-release-notes"
linktitle: "GroupDocs.Assembly for .NET 25.12 Release Notes"
title: "GroupDocs.Assembly for .NET 25.12 Release Notes"
productName: "GroupDocs.Assembly for .NET"
weight: 100
description: "GroupDocs.Assembly for .NET 25.12 Release Notes – the latest updates and fixes."
type: "repository"
layout: "release"
hideChildren: false
toc: false
family_listing_page_title: "GroupDocs.Assembly for .NET 25.12 Release Notes"
menuItemWithNoContent: false
---

## Major Features, Enhancement and Fixes

The **GroupDocs.Assembly for .NET 25.12** release introduces significant enhancements for OOXML compliance handling and fixes critical issues with template expression processing and barcode generation.

**OOXML Compliance Support**: This release adds comprehensive support for OOXML compliance levels in Word documents. You can now explicitly specify the compliance level (Ecma, Transitional, or Strict) when saving documents, and the system automatically preserves the original document's compliance when appropriate.

**Template Expression Processing**: Fixed an issue where template expressions inside inline content controls (SdtRun) were not being processed, ensuring all template expressions are correctly replaced regardless of their location in the document.

**Barcode Generation Reliability**: Improved barcode generation on Linux platforms by properly handling transparent colors and enforcing minimum dimensions for Codabar barcodes, ensuring barcodes render correctly across all platforms.

## Full List of Features Covering all Changes in this Release

| Key             | Category | Summary                                                      |
| :-------------- | :------- | :----------------------------------------------------------- |
| ASSEMBLYNET-70 | ★ Feature | Implement explicit OOXML compliance specification for Words documents |
| ASSEMBLYNET-69 | ✜ Enhancement | Implement automatic preservation of original Words document compliance |
| ASSEMBLYNET-68 | ✜ Enhancement | Implement OOXML compliance support for Words documents |
| ASSEMBLYNET-75 | ✜ Enhancement | Improved Codabar barcode generation reliability by enforcing minimum X Dimension |
| ASSEMBLYNET-76 | ✜ Enhancement | Improved Barcode generation reliability to avoid transparent colors usage |
| ASSEMBLYNET-73 | 🔧 Fix | Missing replacement of template expressions inside SdtRun |
| ASSEMBLYNET-60 | 🔧 Fix | Barcodes render blank when assembling on Linux (.NET 8) |

## Public API and Backward Incompatible Changes

{{< alert style="info" >}}This section outlines public API changes introduced in GroupDocs.Assembly for .NET 25.13. It includes new and deprecated methods, as well as internal behavioral changes that may affect existing implementations. Any regression or modified behavior is highlighted here.{{< /alert >}}

### 1. New Public Enumeration: OoxmlCompliance

A new public enumeration `OoxmlCompliance` has been added to specify the OOXML compliance level when saving Word documents to OOXML formats:

```csharp
namespace GroupDocs.Assembly
{
    /// <summary>
    /// Specifies the OOXML compliance level to use when saving Word documents to OOXML formats.
    /// </summary>
    public enum OoxmlCompliance
    {
        /// <summary>
        /// Specifies ECMA-376 compliance level.
        /// </summary>
        Ecma,
        
        /// <summary>
        /// Specifies ISO/IEC 29500:2008 Transitional compliance level.
        /// </summary>
        Transitional,
        
        /// <summary>
        /// Specifies ISO/IEC 29500:2008 Strict compliance level.
        /// </summary>
        Strict
    }
}
```

**Available Options:**
- `Ecma`: Specifies ECMA-376 compliance level
- `Transitional`: Specifies ISO/IEC 29500:2008 Transitional compliance level (commonly used for compatibility)
- `Strict`: Specifies ISO/IEC 29500:2008 Strict compliance level (fully compliant with the standard)

### 2. New Property in LoadSaveOptions: OoxmlCompliance

A new nullable property `OoxmlCompliance` has been added to the `LoadSaveOptions` class:

```csharp
public class LoadSaveOptions
{
    /// <summary>
    /// Gets or sets the OOXML compliance level to use when saving Word documents to OOXML formats.
    /// The default value is null, which means the compliance level will be determined automatically.
    /// </summary>
    public OoxmlCompliance? OoxmlCompliance { get; set; }
}
```

**Usage:**
- When set to `null` (default): The system automatically preserves the original document's compliance level if it was Transitional, otherwise uses Strict compliance
- When explicitly set: The specified compliance level will be used when saving to OOXML formats
- This property only applies to OOXML formats (DOCX, DOCM, DOTX, DOTM, FlatOpc, etc.) and is ignored for other file formats

### How to Specify Explicit OOXML Compliance Level

The following code snippet demonstrates how to explicitly specify the OOXML compliance level when assembling a Word document:

```csharp
var source = "template.docx";
var target = "output.docx";
var data = "data.json";

// Create LoadSaveOptions with explicit OOXML compliance
var options = new LoadSaveOptions(FileFormat.Docx);
options.OoxmlCompliance = OoxmlCompliance.Strict; // or Ecma, Transitional

var dataSourceInfo = new DataSourceInfo(new JsonDataSource(data));
var assembler = new DocumentAssembler();
assembler.AssembleDocument(source, target, options, dataSourceInfo);
```

### How to Preserve Original Document Compliance Automatically

When `OoxmlCompliance` is not explicitly set (default `null`), the system automatically preserves the original document's compliance level if it was Transitional:

```csharp
var source = "template_transitional.docx"; // Document with Transitional compliance
var target = "output.docx";
var data = "data.json";

// OoxmlCompliance is null by default - original compliance will be preserved
var options = new LoadSaveOptions(FileFormat.Docx);
// options.OoxmlCompliance is null - automatic preservation

var dataSourceInfo = new DataSourceInfo(new JsonDataSource(data));
var assembler = new DocumentAssembler();
assembler.AssembleDocument(source, target, options, dataSourceInfo);
// Output document will maintain Transitional compliance
```

### How to Process Template Expressions in Inline Content Controls

Template expressions inside inline content controls (SdtRun) are now properly processed. The following example demonstrates that expressions work correctly in all content control types:

```csharp
var source = "template_with_sdtrun.docx";
var target = "output.docx";
var data = "data.json";

// Template document contains:
// - SdtBlock: <<[field1]>>
// - SdtRun (Inline): <<[field2]>>  // Now properly processed
// - Regular text: <<[field3]>>

var options = new LoadSaveOptions(FileFormat.Docx);
var dataSourceInfo = new DataSourceInfo(new JsonDataSource(data));
var assembler = new DocumentAssembler();
assembler.AssembleDocument(source, target, options, dataSourceInfo);
// All template expressions are now correctly replaced, including those in SdtRun
```
