---
id: assembly-basic-usage-streams-vs-files-java
url: assembly/java/basic-usage-streams-vs-files
linktitle: Work with Streams vs File Paths
title: Work with Streams vs File Paths
weight: 14
description: "Learn when and how to use streams versus file paths for template loading and document saving in Java."
keywords: streams, file paths, input streams, output streams, file streams, stream handling, efficient processing, memory efficient
productName: GroupDocs.Assembly for Java
hideChildren: False
---

## Overview

GroupDocs.Assembly for Java supports both file paths and streams for template loading and document saving. Understanding when to use each approach helps you build efficient, scalable applications. File paths are simpler for local file system operations, while streams are essential for memory-based processing, remote templates, and web applications.

The main class involved is:
- [DocumentAssembler](https://reference.groupdocs.com/assembly/java/com.groupdocs.assembly/documentassembler/) - provides overloads for both file paths and streams

Here are the considerations for choosing between streams and file paths:

* Use file paths for simple local file system operations
* Use streams for memory-based processing, remote templates, or web applications
* Mix file paths and streams as needed for your scenario
* Always properly close streams to avoid resource leaks

{{< alert style="info" >}}
DocumentAssembler provides two kinds of overloads: one accepts a template path and a result path (`String`, `String`), the other accepts a template stream and a result stream (`InputStream`, `OutputStream`). Both optionally take `LoadSaveOptions`. To combine a file path with a stream, open the file as a `FileInputStream` or `FileOutputStream` and use the stream overload.
{{< /alert >}}

## When to Use File Paths

File paths are ideal for:
- Simple local file system operations
- Templates stored on disk
- Output documents saved to disk
- Desktop applications with direct file access

```java
import com.groupdocs.assembly.*;

public static void useFilePaths() throws Exception
{
    // Simple file path approach
    String templatePath = "C:\\Templates\\InvoiceTemplate.docx";
    String outputPath = "C:\\Output\\Invoice.docx";

    InvoiceData data = new InvoiceData("ABC Corp", 1500.00);

    DocumentAssembler assembler = new DocumentAssembler();
    assembler.assembleDocument(templatePath, outputPath,
        new DataSourceInfo(data, "invoice"));

    System.out.println("Document assembled using file paths.");
}

// POJO for the data source (Java has no anonymous types)
public class InvoiceData
{
    private final String customerName;
    private final double amount;

    public InvoiceData(String customerName, double amount)
    {
        this.customerName = customerName;
        this.amount = amount;
    }

    public String getCustomerName() { return customerName; }
    public double getAmount() { return amount; }
}
```

## When to Use Streams

Streams are essential for:
- Memory-based processing (no disk I/O)
- Templates loaded from databases or remote sources
- Web applications serving documents directly
- Processing templates in memory for performance

```java
import com.groupdocs.assembly.*;
import java.io.*;
import java.nio.file.*;
import java.util.Date;

public static void useStreams() throws Exception
{
    // Load template into memory
    byte[] templateBytes = Files.readAllBytes(Paths.get("Template.docx"));

    try (ByteArrayInputStream templateStream = new ByteArrayInputStream(templateBytes);
         ByteArrayOutputStream outputStream = new ByteArrayOutputStream())
    {
        ReportData data = new ReportData("Report", new Date());

        DocumentAssembler assembler = new DocumentAssembler();
        assembler.assembleDocument(templateStream, outputStream,
            new DataSourceInfo(data, "report"));

        // Use output stream (e.g., send via HTTP, save to database)
        byte[] outputBytes = outputStream.toByteArray();
        Files.write(Paths.get("Output.docx"), outputBytes);

        System.out.println("Document assembled using streams.");
    }
}

// POJO for the data source
public class ReportData
{
    private final String title;
    private final Date date;

    public ReportData(String title, Date date)
    {
        this.title = title;
        this.date = date;
    }

    public String getTitle() { return title; }
    public Date getDate() { return date; }
}
```

## Mixed Approach: File Path Input, Stream Output

Load template from file, save to stream. Since `assembleDocument` accepts either two paths or two streams, open the template file as a `FileInputStream`:

```java
import com.groupdocs.assembly.*;
import java.io.*;

public static void filePathInputStreamOutput() throws Exception
{
    // Template from file path
    String templatePath = "Template.docx";

    // Output to memory stream
    try (InputStream templateStream = new FileInputStream(templatePath);
         ByteArrayOutputStream outputStream = new ByteArrayOutputStream())
    {
        ItemData data = new ItemData("Test", 100);

        DocumentAssembler assembler = new DocumentAssembler();
        assembler.assembleDocument(templateStream, outputStream,
            new DataSourceInfo(data, "item"));

        // Use output stream (e.g., send via HTTP response)
        byte[] outputBytes = outputStream.toByteArray();

        System.out.println("Document assembled, output size: " + outputBytes.length + " bytes");
    }
}

// POJO for the data source
public class ItemData
{
    private final String name;
    private final int value;

    public ItemData(String name, int value)
    {
        this.name = name;
        this.value = value;
    }

    public String getName() { return name; }
    public int getValue() { return value; }
}
```

## Mixed Approach: Stream Input, File Path Output

Load template from stream, save to file. Open the result file as a `FileOutputStream`:

```java
import com.groupdocs.assembly.*;
import java.io.*;
import java.nio.file.*;
import java.util.Date;

public static void streamInputFilePathOutput() throws Exception
{
    // Template from memory stream
    byte[] templateBytes = Files.readAllBytes(Paths.get("Template.docx"));

    // Output to file path
    String outputPath = "Output.docx";

    try (ByteArrayInputStream templateStream = new ByteArrayInputStream(templateBytes);
         OutputStream outputStream = new FileOutputStream(outputPath))
    {
        ReportData data = new ReportData("Report", new Date());

        DocumentAssembler assembler = new DocumentAssembler();
        assembler.assembleDocument(templateStream, outputStream,
            new DataSourceInfo(data, "report"));

        System.out.println("Document assembled from stream to file.");
    }
}
```

## Web Application Example

In web applications, streams are typically preferred:

```java
import com.groupdocs.assembly.*;
import java.io.*;

public static byte[] generateDocumentForWeb(byte[] templateBytes, Object data) throws Exception
{
    try (ByteArrayInputStream templateStream = new ByteArrayInputStream(templateBytes);
         ByteArrayOutputStream outputStream = new ByteArrayOutputStream())
    {
        DocumentAssembler assembler = new DocumentAssembler();
        assembler.assembleDocument(templateStream, outputStream,
            new DataSourceInfo(data, "data"));

        return outputStream.toByteArray();
    }
}
```

## Loading Template from Remote Source

Streams enable loading templates from URLs or remote sources:

```java
import com.groupdocs.assembly.*;
import java.io.*;
import java.net.URL;

public static byte[] loadTemplateFromUrl(String url, Object data) throws Exception
{
    // Read the template directly from the remote source
    try (InputStream templateStream = new URL(url).openStream();
         ByteArrayOutputStream outputStream = new ByteArrayOutputStream())
    {
        DocumentAssembler assembler = new DocumentAssembler();
        assembler.assembleDocument(templateStream, outputStream,
            new DataSourceInfo(data, "data"));

        return outputStream.toByteArray();
    }
}
```

## Stream Disposal Best Practices

Always properly close streams:

```java
import com.groupdocs.assembly.*;
import java.io.*;

public static void properStreamDisposal() throws Exception
{
    // Good: try-with-resources ensures the streams are closed
    try (InputStream templateStream = new FileInputStream("Template.docx");
         OutputStream outputStream = new FileOutputStream("Output.docx"))
    {
        ItemData data = new ItemData("Test", 0);

        DocumentAssembler assembler = new DocumentAssembler();
        assembler.assembleDocument(templateStream, outputStream,
            new DataSourceInfo(data, "item"));
    } // Streams are automatically closed here

    System.out.println("Streams properly closed.");
}
```

{{< alert style="warning" >}}
DocumentAssembler does not close the streams passed to it, neither the template input stream nor the result output stream. Always use try-with-resources statements or close the streams manually to avoid resource leaks.
{{< /alert >}}

## Performance Considerations

- **File Paths**: Simpler but require disk I/O
- **Streams**: More flexible, can be faster for memory operations
- **In-Memory Streams** (`ByteArrayInputStream`/`ByteArrayOutputStream`): Best for small to medium documents
- **File Streams**: Better for large documents to avoid memory pressure

### Advanced Usage Topics

To learn more about advanced stream handling, custom stream implementations, and performance optimization, please refer to the [advanced usage section]({{< ref "assembly/java/developer-guide/advanced-usage/_index.md" >}}).

## More resources

### GitHub Examples

You may easily run the code above and see the feature in action in our GitHub examples:

* [GroupDocs.Assembly for Java examples, plugins, and showcase](https://github.com/groupdocs-assembly/GroupDocs.Assembly-for-Java)
* [GroupDocs.Assembly for .NET examples, plugins, and showcase](https://github.com/groupdocs-assembly/GroupDocs.Assembly-for-.NET)
* [GroupDocs.Assembly for Python via .NET examples, plugins, and showcase](https://github.com/groupdocs-assembly/GroupDocs.Assembly-for-Python-via-.NET)

### Free Online Apps

Along with the full-featured Java library, we provide simple but powerful free online apps.

To assemble documents from templates and data sources, you can use the online apps from the **[GroupDocs.Assembly App Product Family](https://products.groupdocs.app/assembly/family)**.
