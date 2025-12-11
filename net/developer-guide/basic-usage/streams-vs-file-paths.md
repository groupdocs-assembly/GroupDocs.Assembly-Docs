---
id: assembly-basic-usage-streams-vs-files
url: assembly/net/basic-usage-streams-vs-files
title: Work with Streams vs File Paths in C#
weight: 14
description: "Learn when and how to use streams versus file paths for template loading and document saving in .NET."
keywords: streams, file paths, memory streams, file streams, stream handling, efficient processing, memory efficient
productName: GroupDocs.Assembly for .NET
toc: True
---

## Overview

GroupDocs.Assembly for .NET supports both file paths and streams for template loading and document saving. Understanding when to use each approach helps you build efficient, scalable applications. File paths are simpler for local file system operations, while streams are essential for memory-based processing, remote templates, and web applications.

The main class involved is:
- [DocumentAssembler](https://reference.groupdocs.com/assembly/net/groupdocs.assembly/documentassembler/) - provides overloads for both file paths and streams

Here are the considerations for choosing between streams and file paths:

* Use file paths for simple local file system operations
* Use streams for memory-based processing, remote templates, or web applications
* Mix file paths and streams as needed for your scenario
* Always properly dispose of streams to avoid resource leaks

{{< alert style="info" >}}
DocumentAssembler provides multiple overloads supporting various combinations of file paths and streams for both input templates and output documents.
{{< /alert >}}

## When to Use File Paths

File paths are ideal for:
- Simple local file system operations
- Templates stored on disk
- Output documents saved to disk
- Desktop applications with direct file access

```csharp
using GroupDocs.Assembly;

public static void UseFilePaths()
{
    // Simple file path approach
    string templatePath = @"C:\Templates\InvoiceTemplate.docx";
    string outputPath = @"C:\Output\Invoice.docx";
    
    var data = new { CustomerName = "ABC Corp", Amount = 1500.00m };
    
    DocumentAssembler assembler = new DocumentAssembler();
    assembler.AssembleDocument(templatePath, outputPath, 
        new DataSourceInfo(data, "invoice"));
    
    Console.WriteLine("Document assembled using file paths.");
}
```

## When to Use Streams

Streams are essential for:
- Memory-based processing (no disk I/O)
- Templates loaded from databases or remote sources
- Web applications serving documents directly
- Processing templates in memory for performance

```csharp
using GroupDocs.Assembly;
using System.IO;

public static void UseStreams()
{
    // Load template into memory
    byte[] templateBytes = File.ReadAllBytes("Template.docx");
    
    using (MemoryStream templateStream = new MemoryStream(templateBytes))
    using (MemoryStream outputStream = new MemoryStream())
    {
        var data = new { Title = "Report", Date = DateTime.Now };
        
        DocumentAssembler assembler = new DocumentAssembler();
        assembler.AssembleDocument(templateStream, outputStream, 
            new DataSourceInfo(data, "report"));
        
        // Use output stream (e.g., send via HTTP, save to database)
        byte[] outputBytes = outputStream.ToArray();
        File.WriteAllBytes("Output.docx", outputBytes);
        
        Console.WriteLine("Document assembled using streams.");
    }
}
```

## Mixed Approach: File Path Input, Stream Output

Load template from file, save to stream:

```csharp
using GroupDocs.Assembly;
using System.IO;

public static void FilePathInputStreamOutput()
{
    // Template from file path
    string templatePath = "Template.docx";
    
    // Output to memory stream
    using (MemoryStream outputStream = new MemoryStream())
    {
        var data = new { Name = "Test", Value = 100 };
        
        DocumentAssembler assembler = new DocumentAssembler();
        assembler.AssembleDocument(templatePath, outputStream, 
            new DataSourceInfo(data, "item"));
        
        // Use output stream (e.g., send via HTTP response)
        byte[] outputBytes = outputStream.ToArray();
        
        Console.WriteLine($"Document assembled, output size: {outputBytes.Length} bytes");
    }
}
```

## Mixed Approach: Stream Input, File Path Output

Load template from stream, save to file:

```csharp
using GroupDocs.Assembly;
using System.IO;

public static void StreamInputFilePathOutput()
{
    // Template from memory stream
    byte[] templateBytes = File.ReadAllBytes("Template.docx");
    
    using (MemoryStream templateStream = new MemoryStream(templateBytes))
    {
        // Output to file path
        string outputPath = "Output.docx";
        
        var data = new { Title = "Report", Date = DateTime.Now };
        
        DocumentAssembler assembler = new DocumentAssembler();
        assembler.AssembleDocument(templateStream, outputPath, 
            new DataSourceInfo(data, "report"));
        
        Console.WriteLine("Document assembled from stream to file.");
    }
}
```

## Web Application Example

In web applications, streams are typically preferred:

```csharp
using GroupDocs.Assembly;
using System.IO;

public static byte[] GenerateDocumentForWeb(byte[] templateBytes, object data)
{
    using (MemoryStream templateStream = new MemoryStream(templateBytes))
    using (MemoryStream outputStream = new MemoryStream())
    {
        DocumentAssembler assembler = new DocumentAssembler();
        assembler.AssembleDocument(templateStream, outputStream, 
            new DataSourceInfo(data, "data"));
        
        return outputStream.ToArray();
    }
}
```

## Loading Template from Remote Source

Streams enable loading templates from URLs or remote sources:

```csharp
using GroupDocs.Assembly;
using System.IO;
using System.Net.Http;

public static async Task<byte[]> LoadTemplateFromUrl(string url, object data)
{
    using (HttpClient client = new HttpClient())
    {
        // Download template
        byte[] templateBytes = await client.GetByteArrayAsync(url);
        
        using (MemoryStream templateStream = new MemoryStream(templateBytes))
        using (MemoryStream outputStream = new MemoryStream())
        {
            DocumentAssembler assembler = new DocumentAssembler();
            assembler.AssembleDocument(templateStream, outputStream, 
                new DataSourceInfo(data, "data"));
            
            return outputStream.ToArray();
        }
    }
}
```

## Stream Disposal Best Practices

Always properly dispose of streams:

```csharp
using GroupDocs.Assembly;
using System.IO;

public static void ProperStreamDisposal()
{
    // Good: Using statement ensures disposal
    using (FileStream templateStream = new FileStream("Template.docx", FileMode.Open))
    using (FileStream outputStream = new FileStream("Output.docx", FileMode.Create))
    {
        var data = new { Name = "Test" };
        
        DocumentAssembler assembler = new DocumentAssembler();
        assembler.AssembleDocument(templateStream, outputStream, 
            new DataSourceInfo(data, "item"));
    } // Streams are automatically disposed here
    
    Console.WriteLine("Streams properly disposed.");
}
```

{{< alert style="warning" >}}
DocumentAssembler does not automatically dispose of input streams. Always use `using` statements or manually dispose streams to avoid resource leaks. Output streams are managed by the assembler.
{{< /alert >}}

## Performance Considerations

- **File Paths**: Simpler but require disk I/O
- **Streams**: More flexible, can be faster for memory operations
- **Memory Streams**: Best for small to medium documents
- **File Streams**: Better for large documents to avoid memory pressure

### Advanced Usage Topics

To learn more about advanced stream handling, custom stream implementations, and performance optimization, please refer to the [advanced usage section]({{< ref "assembly/net/developer-guide/advanced-usage/_index.md" >}}).

## More resources

### GitHub Examples

You may easily run the code above and see the feature in action in our GitHub examples:

* [GroupDocs.Assembly for .NET examples, plugins, and showcase](https://github.com/groupdocs-assembly/GroupDocs.Assembly-for-.NET)
* [GroupDocs.Assembly for Java examples, plugins, and showcase](https://github.com/groupdocs-assembly/GroupDocs.Assembly-for-Java)
* [GroupDocs.Assembly for Python via .NET examples, plugins, and showcase](https://github.com/groupdocs-assembly/GroupDocs.Assembly-for-Python-via-.NET)

### Free Online Apps

Along with the full-featured .NET library, we provide simple but powerful free online apps.

To assemble documents from templates and data sources, you can use the online apps from the **[GroupDocs.Assembly App Product Family](https://products.groupdocs.app/assembly/family)**.

