---
id: assembly-basic-usage-load-template
url: assembly/net/basic-usage-load-template
linktitle: Load Template Documents
title: Load Template Documents from File or Stream
weight: 3
description: "Learn how to load template documents from file paths and streams for document assembly in .NET applications."
keywords: load template, file path, stream, template document, DOCX, XLSX, PPTX, load from file, load from stream
productName: GroupDocs.Assembly for .NET
hideChildren: False
---

## Overview

GroupDocs.Assembly for .NET supports loading template documents from both file paths and streams. This flexibility allows you to work with templates stored on disk, in memory, or retrieved from remote sources.

The main class involved is:
- [DocumentAssembler](https://reference.groupdocs.com/assembly/net/groupdocs.assembly/documentassembler/) - provides overloads for both file paths and streams

Here are the steps to load and use templates:

* Load template from a file path using string path parameter
* Load template from a stream using Stream parameter
* Choose the appropriate method based on your use case (file system vs memory/remote)
* Save assembled document to file path or stream accordingly

{{< alert style="info" >}}
When using streams, ensure proper disposal of stream resources. The DocumentAssembler does not automatically dispose of input streams, so you should manage stream lifecycle yourself.
{{< /alert >}}

## Load Template from File Path

The simplest way to load a template is from a file path:

```csharp
using GroupDocs.Assembly;

public static void LoadTemplateFromFile()
{
    // Template and output file paths
    string templatePath = @"C:\Templates\InvoiceTemplate.docx";
    string outputPath = @"C:\Output\Invoice.docx";
    
    // Sample data
    var invoiceData = new { CustomerName = "ABC Corp", Amount = 1500.00 };
    
    // Assemble document from file path
    DocumentAssembler assembler = new DocumentAssembler();
    assembler.AssembleDocument(templatePath, outputPath, 
        new DataSourceInfo(invoiceData, "invoice"));
    
    Console.WriteLine("Document assembled successfully.");
}
```

## Load Template from Stream

When working with templates in memory or from remote sources, use streams:

```csharp
using GroupDocs.Assembly;
using System.IO;

public static void LoadTemplateFromStream()
{
    // Load template into memory stream
    byte[] templateBytes = File.ReadAllBytes("Template.docx");
    using (MemoryStream templateStream = new MemoryStream(templateBytes))
    {
        // Create output stream
        using (FileStream outputStream = new FileStream("Output.docx", FileMode.Create))
        {
            var data = new { Title = "Report", Date = DateTime.Now };
            
            DocumentAssembler assembler = new DocumentAssembler();
            assembler.AssembleDocument(templateStream, outputStream, 
                new DataSourceInfo(data, "report"));
            
            Console.WriteLine("Document assembled from stream successfully.");
        }
    }
}
```

## Load Template from Remote Source

You can load templates from URLs or remote sources:

```csharp
using GroupDocs.Assembly;
using System.IO;
using System.Net.Http;

public static async void LoadTemplateFromRemote()
{
    // Download template from remote URL
    using (HttpClient client = new HttpClient())
    {
        byte[] templateBytes = await client.GetByteArrayAsync(
            "https://example.com/templates/ReportTemplate.docx");
        
        using (MemoryStream templateStream = new MemoryStream(templateBytes))
        using (FileStream outputStream = new FileStream("Output.docx", FileMode.Create))
        {
            var data = new { Company = "My Company", Year = 2024 };
            
            DocumentAssembler assembler = new DocumentAssembler();
            assembler.AssembleDocument(templateStream, outputStream, 
                new DataSourceInfo(data, "company"));
            
            Console.WriteLine("Document assembled from remote template.");
        }
    }
}
```

## Mixed File Path and Stream Usage

You can mix file paths and streams as needed:

```csharp
using GroupDocs.Assembly;
using System.IO;

public static void MixedFileAndStream()
{
    // Load template from file path
    string templatePath = "Template.docx";
    
    // Save output to stream
    using (MemoryStream outputStream = new MemoryStream())
    {
        var data = new { Name = "Test", Value = 100 };
        
        DocumentAssembler assembler = new DocumentAssembler();
        assembler.AssembleDocument(templatePath, outputStream, 
            new DataSourceInfo(data, "item"));
        
        // Use the output stream (e.g., send via HTTP, save to database)
        byte[] outputBytes = outputStream.ToArray();
        File.WriteAllBytes("Output.docx", outputBytes);
        
        Console.WriteLine("Document assembled with mixed file/stream usage.");
    }
}
```

{{< alert style="warning" >}}
When using streams for output, the stream position is reset after assembly. Make sure to read from the stream after assembly completes, and handle the stream position appropriately.
{{< /alert >}}

### Advanced Usage Topics

To learn more about working with different template formats, custom document loading, and advanced stream handling, please refer to the [advanced usage section]({{< ref "assembly/net/developer-guide/advanced-usage/_index.md" >}}).

## More resources

### GitHub Examples

You may easily run the code above and see the feature in action in our GitHub examples:

* [GroupDocs.Assembly for .NET examples, plugins, and showcase](https://github.com/groupdocs-assembly/GroupDocs.Assembly-for-.NET)
* [GroupDocs.Assembly for Java examples, plugins, and showcase](https://github.com/groupdocs-assembly/GroupDocs.Assembly-for-Java)
* [GroupDocs.Assembly for Python via .NET examples, plugins, and showcase](https://github.com/groupdocs-assembly/GroupDocs.Assembly-for-Python-via-.NET)

### Free Online Apps

Along with the full-featured .NET library, we provide simple but powerful free online apps.

To assemble documents from templates and data sources, you can use the online apps from the **[GroupDocs.Assembly App Product Family](https://products.groupdocs.app/assembly/family)**.

