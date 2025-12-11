---
id: assembly-basic-usage-ooxml-compliance
url: assembly/net/basic-usage-ooxml-compliance
title: Specify OOXML Compliance Level for Word Documents in C#
weight: 18
description: "Control the OOXML compliance level (Ecma, Transitional, or Strict) when saving Word documents to OOXML formats using GroupDocs.Assembly for .NET."
keywords: OOXML compliance, OoxmlCompliance, Ecma, Transitional, Strict, DOCX compliance, Word document compliance, ISO/IEC 29500
productName: GroupDocs.Assembly for .NET
toc: True
---

## Overview

GroupDocs.Assembly for .NET allows you to control the OOXML compliance level when saving Word documents to OOXML formats (DOCX, DOCM, DOTX, DOTM, FlatOpc, etc.). You can explicitly specify the compliance level or let the system automatically preserve the original document's compliance level.

The main classes involved are:
- [LoadSaveOptions](https://reference.groupdocs.com/assembly/net/groupdocs.assembly/loadsaveoptions/) - contains the OoxmlCompliance property
- [OoxmlCompliance](https://reference.groupdocs.com/assembly/net/groupdocs.assembly/ooxmlcompliance/) - enumeration specifying compliance levels
- [DocumentAssembler](https://reference.groupdocs.com/assembly/net/groupdocs.assembly/documentassembler/) - assembles documents with specified compliance

Here are the steps to specify OOXML compliance:

* Create LoadSaveOptions for your output format
* Set the OoxmlCompliance property to the desired compliance level (or leave null for automatic preservation)
* Use DocumentAssembler with the LoadSaveOptions to assemble the document
* The output document will be saved with the specified compliance level

{{< alert style="info" >}}
The OoxmlCompliance property only applies to OOXML formats (DOCX, DOCM, DOTX, DOTM, FlatOpc, etc.) and is ignored for other file formats. When set to null (default), the system automatically preserves the original document's compliance level if it was Transitional, otherwise uses Strict compliance.
{{< /alert >}}

## Available OOXML Compliance Levels

The `OoxmlCompliance` enumeration provides three compliance levels:

- **Ecma**: Specifies ECMA-376 compliance level
- **Transitional**: Specifies ISO/IEC 29500:2008 Transitional compliance level (commonly used for compatibility)
- **Strict**: Specifies ISO/IEC 29500:2008 Strict compliance level (fully compliant with the standard)

## Specify Explicit OOXML Compliance Level

You can explicitly set the OOXML compliance level when assembling a document:

```csharp
using GroupDocs.Assembly;

public static void SpecifyExplicitCompliance()
{
    DocumentAssembler assembler = new DocumentAssembler();

    // Create LoadSaveOptions with explicit OOXML compliance
    var options = new LoadSaveOptions(FileFormat.Docx);
    options.OoxmlCompliance = OoxmlCompliance.Strict; // or Ecma, Transitional

    var data = new { CompanyName = "ABC Corp", Year = 2024 };
    
    assembler.AssembleDocument("Template.docx", "Output.docx", options,
        new DataSourceInfo(data, "company"));
}
```

## Use Transitional Compliance

For maximum compatibility with older Office versions, use Transitional compliance:

```csharp
using GroupDocs.Assembly;

public static void UseTransitionalCompliance()
{
    DocumentAssembler assembler = new DocumentAssembler();

    var options = new LoadSaveOptions(FileFormat.Docx);
    options.OoxmlCompliance = OoxmlCompliance.Transitional;

    var data = new { CustomerName = "John Doe", OrderNumber = "ORD-12345" };
    
    assembler.AssembleDocument("Template.docx", "Output.docx", options,
        new DataSourceInfo(data, "order"));
}
```

## Use Ecma Compliance

For ECMA-376 standard compliance:

```csharp
using GroupDocs.Assembly;

public static void UseEcmaCompliance()
{
    DocumentAssembler assembler = new DocumentAssembler();

    var options = new LoadSaveOptions(FileFormat.Docx);
    options.OoxmlCompliance = OoxmlCompliance.Ecma;

    var data = new { ReportTitle = "Monthly Report", Month = "January 2024" };
    
    assembler.AssembleDocument("Template.docx", "Output.docx", options,
        new DataSourceInfo(data, "report"));
}
```

## Automatic Preservation of Original Compliance

When `OoxmlCompliance` is not explicitly set (default `null`), the system automatically preserves the original document's compliance level if it was Transitional:

```csharp
using GroupDocs.Assembly;

public static void PreserveOriginalCompliance()
{
    DocumentAssembler assembler = new DocumentAssembler();

    // OoxmlCompliance is null by default - original compliance will be preserved
    var options = new LoadSaveOptions(FileFormat.Docx);
    // options.OoxmlCompliance is null - automatic preservation

    var data = new { Title = "Document Title", Content = "Document content" };
    
    // Output document will maintain Transitional compliance from template if it was Transitional
    assembler.AssembleDocument("Template_Transitional.docx", "Output.docx", options,
        new DataSourceInfo(data, "document"));
}
```

## Using with Different OOXML Formats

The OoxmlCompliance property works with all OOXML formats:

```csharp
using GroupDocs.Assembly;

public static void UseWithDifferentFormats()
{
    DocumentAssembler assembler = new DocumentAssembler();
    var data = new { Name = "Test Document", Value = 100 };
    
    // DOCX format
    var docxOptions = new LoadSaveOptions(FileFormat.Docx);
    docxOptions.OoxmlCompliance = OoxmlCompliance.Strict;
    assembler.AssembleDocument("Template.docx", "Output.docx", docxOptions,
        new DataSourceInfo(data, "item"));
    
    // DOCM format (macro-enabled)
    var docmOptions = new LoadSaveOptions(FileFormat.Docm);
    docmOptions.OoxmlCompliance = OoxmlCompliance.Transitional;
    assembler.AssembleDocument("Template.docm", "Output.docm", docmOptions,
        new DataSourceInfo(data, "item"));
    
    // DOTX format (template)
    var dotxOptions = new LoadSaveOptions(FileFormat.Dotx);
    dotxOptions.OoxmlCompliance = OoxmlCompliance.Strict;
    assembler.AssembleDocument("Template.dotx", "Output.dotx", dotxOptions,
        new DataSourceInfo(data, "item"));
}
```

## Using with Streams

You can also specify OOXML compliance when working with streams:

```csharp
using GroupDocs.Assembly;
using System.IO;

public static void UseComplianceWithStreams()
{
    DocumentAssembler assembler = new DocumentAssembler();

    var options = new LoadSaveOptions(FileFormat.Docx);
    options.OoxmlCompliance = OoxmlCompliance.Strict;

    var data = new { Company = "My Company", Year = 2024 };
    
    using (FileStream templateStream = new FileStream("Template.docx", FileMode.Open))
    using (FileStream outputStream = new FileStream("Output.docx", FileMode.Create))
    {
        assembler.AssembleDocument(templateStream, outputStream, options,
            new DataSourceInfo(data, "company"));
    }
}
```

## Compliance Level Behavior

Understanding how compliance levels work:

- **When explicitly set**: The specified compliance level is used when saving to OOXML formats
- **When null (default)**: 
  - If the original document had Transitional compliance, it is preserved
  - Otherwise, Strict compliance is used
- **For non-OOXML formats**: The property is ignored (e.g., PDF, HTML, RTF)

```csharp
using GroupDocs.Assembly;

public static void DemonstrateComplianceBehavior()
{
    DocumentAssembler assembler = new DocumentAssembler();
    var data = new { Title = "Test", Content = "Content" };
    
    // Explicit Strict compliance
    var strictOptions = new LoadSaveOptions(FileFormat.Docx);
    strictOptions.OoxmlCompliance = OoxmlCompliance.Strict;
    assembler.AssembleDocument("Template.docx", "Output_Strict.docx", strictOptions,
        new DataSourceInfo(data, "doc"));
    
    // Automatic preservation (null)
    var autoOptions = new LoadSaveOptions(FileFormat.Docx);
    // autoOptions.OoxmlCompliance is null - will preserve if Transitional
    assembler.AssembleDocument("Template.docx", "Output_Auto.docx", autoOptions,
        new DataSourceInfo(data, "doc"));
    
    // Note: For PDF output, OoxmlCompliance is ignored
    var pdfOptions = new LoadSaveOptions(FileFormat.Pdf);
    pdfOptions.OoxmlCompliance = OoxmlCompliance.Strict; // Ignored for PDF
    assembler.AssembleDocument("Template.docx", "Output.pdf", pdfOptions,
        new DataSourceInfo(data, "doc"));
}
```

{{< alert style="warning" >}}
The OoxmlCompliance property only affects OOXML formats. When saving to other formats like PDF, HTML, or RTF, this property is ignored. The compliance level is determined by the output format, not the template format.
{{< /alert >}}

### Advanced Usage Topics

To learn more about format-specific options, document conversion settings, and advanced compliance handling, please refer to the [advanced usage section]({{< ref "assembly/net/developer-guide/advanced-usage/_index.md" >}}).

## More resources

### GitHub Examples

You may easily run the code above and see the feature in action in our GitHub examples:

* [GroupDocs.Assembly for .NET examples, plugins, and showcase](https://github.com/groupdocs-assembly/GroupDocs.Assembly-for-.NET)
* [GroupDocs.Assembly for Java examples, plugins, and showcase](https://github.com/groupdocs-assembly/GroupDocs.Assembly-for-Java)
* [GroupDocs.Assembly for Python via .NET examples, plugins, and showcase](https://github.com/groupdocs-assembly/GroupDocs.Assembly-for-Python-via-.NET)

### Free Online Apps

Along with the full-featured .NET library, we provide simple but powerful free online apps.

To assemble documents from templates and data sources, you can use the online apps from the **[GroupDocs.Assembly App Product Family](https://products.groupdocs.app/assembly/family)**.

