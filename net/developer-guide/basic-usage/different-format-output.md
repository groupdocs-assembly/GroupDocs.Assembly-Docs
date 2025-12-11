---
id: assembly-basic-usage-different-format-output
url: assembly/net/basic-usage-different-format-output
title: Generate Output in Different Format in C#
weight: 13
description: "Convert assembled documents to different formats (e.g., DOCX to PDF, DOCX to HTML) during assembly."
keywords: format conversion, PDF output, HTML output, convert format, change format, output format, DOCX to PDF
productName: GroupDocs.Assembly for .NET
toc: True
---

## Overview

GroupDocs.Assembly for .NET allows you to generate output documents in a different format than the template. For example, you can create a DOCX template but output a PDF, or create an XLSX template but output HTML. The output format is determined by the file extension of the output path.

The main class involved is:
- [DocumentAssembler](https://reference.groupdocs.com/assembly/net/groupdocs.assembly/documentassembler/) - assembles documents and converts to output format

Here are the steps to generate output in a different format:

* Create a template document in one format (e.g., DOCX)
* Specify an output path with a different file extension (e.g., .pdf, .html)
* Assemble the document using DocumentAssembler
* The output will be automatically converted to the specified format

{{< alert style="info" >}}
Format conversion is automatic based on the output file extension. Supported conversions depend on the template format - Word templates can convert to PDF, HTML, and more, while spreadsheet templates have more limited conversion options.
{{< /alert >}}

## Convert DOCX Template to PDF

Generate a PDF from a Word template:

```csharp
using GroupDocs.Assembly;

public static void ConvertDocxToPdf()
{
    // DOCX template, PDF output
    string templatePath = "InvoiceTemplate.docx";
    string outputPath = "Invoice.pdf";
    
    var invoiceData = new { 
        CustomerName = "ABC Corp", 
        Amount = 1500.00m,
        Date = DateTime.Now
    };
    
    DocumentAssembler assembler = new DocumentAssembler();
    assembler.AssembleDocument(templatePath, outputPath, 
        new DataSourceInfo(invoiceData, "invoice"));
    
    Console.WriteLine("PDF generated from DOCX template.");
}
```

## Convert DOCX Template to HTML

Generate an HTML file from a Word template:

```csharp
using GroupDocs.Assembly;

public static void ConvertDocxToHtml()
{
    // DOCX template, HTML output
    string templatePath = "ReportTemplate.docx";
    string outputPath = "Report.html";
    
    var reportData = new { 
        Title = "Monthly Report",
        Month = "January 2024"
    };
    
    DocumentAssembler assembler = new DocumentAssembler();
    assembler.AssembleDocument(templatePath, outputPath, 
        new DataSourceInfo(reportData, "report"));
    
    Console.WriteLine("HTML generated from DOCX template.");
}
```

## Convert DOCX Template to XPS

Generate an XPS document from a Word template:

```csharp
using GroupDocs.Assembly;

public static void ConvertDocxToXps()
{
    // DOCX template, XPS output
    string templatePath = "DocumentTemplate.docx";
    string outputPath = "Document.xps";
    
    var documentData = new { 
        Title = "Document Title",
        Content = "Document content"
    };
    
    DocumentAssembler assembler = new DocumentAssembler();
    assembler.AssembleDocument(templatePath, outputPath, 
        new DataSourceInfo(documentData, "document"));
    
    Console.WriteLine("XPS generated from DOCX template.");
}
```

## Convert XLSX Template to PDF

Generate a PDF from an Excel template:

```csharp
using GroupDocs.Assembly;

public static void ConvertXlsxToPdf()
{
    // XLSX template, PDF output
    string templatePath = "SpreadsheetTemplate.xlsx";
    string outputPath = "Spreadsheet.pdf";
    
    var data = new { 
        ReportTitle = "Sales Report",
        Quarter = "Q1 2024"
    };
    
    DocumentAssembler assembler = new DocumentAssembler();
    assembler.AssembleDocument(templatePath, outputPath, 
        new DataSourceInfo(data, "report"));
    
    Console.WriteLine("PDF generated from XLSX template.");
}
```

## Convert PPTX Template to PDF

Generate a PDF from a PowerPoint template:

```csharp
using GroupDocs.Assembly;

public static void ConvertPptxToPdf()
{
    // PPTX template, PDF output
    string templatePath = "PresentationTemplate.pptx";
    string outputPath = "Presentation.pdf";
    
    var presentationData = new { 
        Title = "Quarterly Review",
        Quarter = "Q1 2024"
    };
    
    DocumentAssembler assembler = new DocumentAssembler();
    assembler.AssembleDocument(templatePath, outputPath, 
        new DataSourceInfo(presentationData, "presentation"));
    
    Console.WriteLine("PDF generated from PPTX template.");
}
```

## Convert Email Template to PDF

Generate a PDF from an email template:

```csharp
using GroupDocs.Assembly;

public static void ConvertEmailToPdf()
{
    // MSG template, PDF output
    string templatePath = "EmailTemplate.msg";
    string outputPath = "Email.pdf";
    
    var emailData = new { 
        Recipient = "customer@example.com",
        Subject = "Invoice",
        Body = "Please find attached invoice."
    };
    
    DocumentAssembler assembler = new DocumentAssembler();
    assembler.AssembleDocument(templatePath, outputPath, 
        new DataSourceInfo(emailData, "email"));
    
    Console.WriteLine("PDF generated from email template.");
}
```

## Supported Format Conversions

The following conversions are supported:

**From Word Processing (DOCX, DOC, RTF, etc.):**
- PDF, XPS, HTML, MHTML, EPUB, TIFF, SVG, PS, PCL, Markdown, TXT, XAML

**From Spreadsheet (XLSX, XLS, etc.):**
- PDF, XPS, HTML, MHTML, TIFF

**From Presentation (PPTX, PPT, etc.):**
- PDF, XPS, TIFF

**From Email (MSG, EML, etc.):**
- PDF, XPS, HTML, MHTML, Markdown, TXT, XAML

{{< alert style="warning" >}}
Not all format combinations are supported. Word processing templates have the most conversion options, while spreadsheet and presentation templates have more limited output formats.
{{< /alert >}}

### Advanced Usage Topics

To learn more about format-specific options, conversion settings, and advanced format handling, please refer to the [advanced usage section]({{< ref "assembly/net/developer-guide/advanced-usage/_index.md" >}}).

## More resources

### GitHub Examples

You may easily run the code above and see the feature in action in our GitHub examples:

* [GroupDocs.Assembly for .NET examples, plugins, and showcase](https://github.com/groupdocs-assembly/GroupDocs.Assembly-for-.NET)
* [GroupDocs.Assembly for Java examples, plugins, and showcase](https://github.com/groupdocs-assembly/GroupDocs.Assembly-for-Java)
* [GroupDocs.Assembly for Python via .NET examples, plugins, and showcase](https://github.com/groupdocs-assembly/GroupDocs.Assembly-for-Python-via-.NET)

### Free Online Apps

Along with the full-featured .NET library, we provide simple but powerful free online apps.

To assemble documents from templates and data sources, you can use the online apps from the **[GroupDocs.Assembly App Product Family](https://products.groupdocs.app/assembly/family)**.

