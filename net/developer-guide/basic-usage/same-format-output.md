---
id: assembly-basic-usage-same-format-output
url: assembly/net/basic-usage-same-format-output
linktitle: Generate Output in Same Format
title: Generate Output in Same Format as Template
weight: 12
description: "Save assembled documents in the same format as the template (e.g., DOCX to DOCX, XLSX to XLSX)."
keywords: same format, output format, save document, preserve format, DOCX output, XLSX output, PPTX output
productName: GroupDocs.Assembly for .NET
hideChildren: False
---

## Overview

By default, GroupDocs.Assembly for .NET saves assembled documents in the same format as the template. This means a DOCX template produces a DOCX output, an XLSX template produces an XLSX output, and so on. The output format is determined by the file extension of the output path.

The main class involved is:
- [DocumentAssembler](https://reference.groupdocs.com/assembly/net/groupdocs.assembly/documentassembler/) - assembles documents and determines output format

Here are the steps to generate output in the same format:

* Create a template document in your desired format (DOCX, XLSX, PPTX, etc.)
* Specify an output path with the same file extension as the template
* Assemble the document using DocumentAssembler
* The output will automatically be in the same format as the template

{{< alert style="info" >}}
The output format is automatically determined by the file extension of the output path. No additional configuration is needed to preserve the template format.
{{< /alert >}}

## Generate DOCX from DOCX Template

Generate a Word document from a Word template:

```csharp
using GroupDocs.Assembly;

public static void GenerateDocxFromDocx()
{
    // Template and output are both DOCX
    string templatePath = "InvoiceTemplate.docx";
    string outputPath = "Invoice.docx";
    
    var invoiceData = new { 
        CustomerName = "ABC Corp", 
        Amount = 1500.00m,
        Date = DateTime.Now
    };
    
    DocumentAssembler assembler = new DocumentAssembler();
    assembler.AssembleDocument(templatePath, outputPath, 
        new DataSourceInfo(invoiceData, "invoice"));
    
    Console.WriteLine("DOCX document generated from DOCX template.");
}
```

## Generate XLSX from XLSX Template

Generate an Excel spreadsheet from an Excel template:

```csharp
using GroupDocs.Assembly;

public static void GenerateXlsxFromXlsx()
{
    // Template and output are both XLSX
    string templatePath = "ReportTemplate.xlsx";
    string outputPath = "Report.xlsx";
    
    var reportData = new { 
        Title = "Monthly Sales",
        Month = "January 2024"
    };
    
    DocumentAssembler assembler = new DocumentAssembler();
    assembler.AssembleDocument(templatePath, outputPath, 
        new DataSourceInfo(reportData, "report"));
    
    Console.WriteLine("XLSX document generated from XLSX template.");
}
```

## Generate PPTX from PPTX Template

Generate a PowerPoint presentation from a PowerPoint template:

```csharp
using GroupDocs.Assembly;

public static void GeneratePptxFromPptx()
{
    // Template and output are both PPTX
    string templatePath = "PresentationTemplate.pptx";
    string outputPath = "Presentation.pptx";
    
    var presentationData = new { 
        Title = "Quarterly Review",
        Quarter = "Q1 2024"
    };
    
    DocumentAssembler assembler = new DocumentAssembler();
    assembler.AssembleDocument(templatePath, outputPath, 
        new DataSourceInfo(presentationData, "presentation"));
    
    Console.WriteLine("PPTX document generated from PPTX template.");
}
```

## Generate MSG from MSG Template

Generate an email message from an email template:

```csharp
using GroupDocs.Assembly;

public static void GenerateMsgFromMsg()
{
    // Template and output are both MSG
    string templatePath = "EmailTemplate.msg";
    string outputPath = "Email.msg";
    
    var emailData = new { 
        Recipient = "customer@example.com",
        Subject = "Invoice",
        Body = "Please find attached invoice."
    };
    
    DocumentAssembler assembler = new DocumentAssembler();
    assembler.AssembleDocument(templatePath, outputPath, 
        new DataSourceInfo(emailData, "email"));
    
    Console.WriteLine("MSG document generated from MSG template.");
}
```

## Using Streams with Same Format

When using streams, the format is still preserved based on the template format:

```csharp
using GroupDocs.Assembly;
using System.IO;

public static void GenerateSameFormatFromStream()
{
    // Load DOCX template from stream
    byte[] templateBytes = File.ReadAllBytes("Template.docx");
    
    using (MemoryStream templateStream = new MemoryStream(templateBytes))
    using (FileStream outputStream = new FileStream("Output.docx", FileMode.Create))
    {
        var data = new { Name = "Test", Value = 100 };
        
        DocumentAssembler assembler = new DocumentAssembler();
        assembler.AssembleDocument(templateStream, outputStream, 
            new DataSourceInfo(data, "item"));
        
        Console.WriteLine("Document generated from stream in same format.");
    }
}
```

## Format Compatibility

The following formats support same-format output:

- **Word Processing**: DOCX, DOC, RTF, ODT, OTT
- **Spreadsheet**: XLSX, XLS, XLSM, ODS
- **Presentation**: PPTX, PPT, PPTM, ODP
- **Email**: MSG, EML, EMLX
- **Other**: HTML, TXT, XML

{{< alert style="warning" >}}
Some older formats (like DOC, XLS, PPT) may have limitations compared to their newer counterparts (DOCX, XLSX, PPTX). For best results, use the newer Office Open XML formats.
{{< /alert >}}

### Advanced Usage Topics

To learn more about format conversion, saving to different formats, and format-specific options, please refer to the [advanced usage section]({{< ref "assembly/net/developer-guide/advanced-usage/_index.md" >}}).

## More resources

### GitHub Examples

You may easily run the code above and see the feature in action in our GitHub examples:

* [GroupDocs.Assembly for .NET examples, plugins, and showcase](https://github.com/groupdocs-assembly/GroupDocs.Assembly-for-.NET)
* [GroupDocs.Assembly for Java examples, plugins, and showcase](https://github.com/groupdocs-assembly/GroupDocs.Assembly-for-Java)
* [GroupDocs.Assembly for Python via .NET examples, plugins, and showcase](https://github.com/groupdocs-assembly/GroupDocs.Assembly-for-Python-via-.NET)

### Free Online Apps

Along with the full-featured .NET library, we provide simple but powerful free online apps.

To assemble documents from templates and data sources, you can use the online apps from the **[GroupDocs.Assembly App Product Family](https://products.groupdocs.app/assembly/family)**.

