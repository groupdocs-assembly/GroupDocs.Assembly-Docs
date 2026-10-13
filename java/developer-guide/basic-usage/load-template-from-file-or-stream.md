---
id: assembly-basic-usage-load-template-java
url: assembly/java/basic-usage-load-template
linktitle: Load Template Documents
title: Load Template Documents from File or Stream
weight: 3
description: "Learn how to load template documents from file paths and streams for document assembly in Java applications."
keywords: load template, file path, stream, InputStream, OutputStream, template document, DOCX, XLSX, PPTX, load from file, load from stream
productName: GroupDocs.Assembly for Java
hideChildren: False
---

## Overview

GroupDocs.Assembly for Java supports loading template documents from both file paths and streams. This flexibility allows you to work with templates stored on disk, in memory, or retrieved from remote sources.

The main class involved is:
- [DocumentAssembler](https://reference.groupdocs.com/assembly/java/com.groupdocs.assembly/documentassembler/) - provides overloads for both file paths and streams

Here are the steps to load and use templates:

* Load template from a file path using a `String` path parameter
* Load template from a stream using an `InputStream` parameter
* Choose the appropriate method based on your use case (file system vs memory/remote)
* Save assembled document to a file path or an `OutputStream` accordingly

{{< alert style="info" >}}
When using streams, ensure proper closing of stream resources. The DocumentAssembler does not close the input and output streams passed to it, so you should manage the stream lifecycle yourself (for example, with try-with-resources).
{{< /alert >}}

## Load Template from File Path

The simplest way to load a template is from a file path:

```java
import com.groupdocs.assembly.*;

public static void loadTemplateFromFile() throws Exception
{
    // Template and output file paths
    String templatePath = "C:\\Templates\\InvoiceTemplate.docx";
    String outputPath = "C:\\Output\\Invoice.docx";

    // Sample data
    InvoiceData invoiceData = new InvoiceData("ABC Corp", 1500.00);

    // Assemble document from file path
    DocumentAssembler assembler = new DocumentAssembler();
    assembler.assembleDocument(templatePath, outputPath,
        new DataSourceInfo(invoiceData, "invoice"));

    System.out.println("Document assembled successfully.");
}

// POJO for the data source
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

## Load Template from Stream

When working with templates in memory or from remote sources, use streams:

```java
import com.groupdocs.assembly.*;
import java.io.*;
import java.nio.file.*;
import java.util.Date;

public static void loadTemplateFromStream() throws Exception
{
    // Load template into memory stream
    byte[] templateBytes = Files.readAllBytes(Paths.get("Template.docx"));
    try (InputStream templateStream = new ByteArrayInputStream(templateBytes);
         // Create output stream
         OutputStream outputStream = new FileOutputStream("Output.docx"))
    {
        ReportData data = new ReportData("Report", new Date());

        DocumentAssembler assembler = new DocumentAssembler();
        assembler.assembleDocument(templateStream, outputStream,
            new DataSourceInfo(data, "report"));

        System.out.println("Document assembled from stream successfully.");
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

## Load Template from Remote Source

You can load templates from URLs or remote sources:

```java
import com.groupdocs.assembly.*;
import java.io.*;
import java.net.URI;

public static void loadTemplateFromRemote() throws Exception
{
    // Download template from remote URL
    try (InputStream templateStream = URI.create(
             "https://example.com/templates/ReportTemplate.docx").toURL().openStream();
         OutputStream outputStream = new FileOutputStream("Output.docx"))
    {
        CompanyData data = new CompanyData("My Company", 2024);

        DocumentAssembler assembler = new DocumentAssembler();
        assembler.assembleDocument(templateStream, outputStream,
            new DataSourceInfo(data, "company"));

        System.out.println("Document assembled from remote template.");
    }
}

// POJO for the data source
public class CompanyData
{
    private final String company;
    private final int year;

    public CompanyData(String company, int year)
    {
        this.company = company;
        this.year = year;
    }

    public String getCompany() { return company; }
    public int getYear() { return year; }
}
```

## Mixed File Path and Stream Usage

You can mix files and streams as needed. `DocumentAssembler` accepts either two paths or two streams, so open the template file as a stream when the output should go to a stream:

```java
import com.groupdocs.assembly.*;
import java.io.*;
import java.nio.file.*;

public static void mixedFileAndStream() throws Exception
{
    // Load template from file path
    String templatePath = "Template.docx";

    // Save output to stream
    try (InputStream templateStream = new FileInputStream(templatePath);
         ByteArrayOutputStream outputStream = new ByteArrayOutputStream())
    {
        ItemData data = new ItemData("Test", 100);

        DocumentAssembler assembler = new DocumentAssembler();
        assembler.assembleDocument(templateStream, outputStream,
            new DataSourceInfo(data, "item"));

        // Use the output stream (e.g., send via HTTP, save to database)
        byte[] outputBytes = outputStream.toByteArray();
        Files.write(Paths.get("Output.docx"), outputBytes);

        System.out.println("Document assembled with mixed file/stream usage.");
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

{{< alert style="warning" >}}
When using streams for output, read the assembled content (for example, via `ByteArrayOutputStream.toByteArray()`) only after `assembleDocument` returns. The output stream is neither closed nor reset by the assembler, so close it yourself when you are done.
{{< /alert >}}

### Advanced Usage Topics

To learn more about working with different template formats, custom document loading, and advanced stream handling, please refer to the [advanced usage section]({{< ref "assembly/java/developer-guide/advanced-usage/_index.md" >}}).

## More resources

### GitHub Examples

You may easily run the code above and see the feature in action in our GitHub examples:

* [GroupDocs.Assembly for Java examples, plugins, and showcase](https://github.com/groupdocs-assembly/GroupDocs.Assembly-for-Java)
* [GroupDocs.Assembly for .NET examples, plugins, and showcase](https://github.com/groupdocs-assembly/GroupDocs.Assembly-for-.NET)
* [GroupDocs.Assembly for Python via .NET examples, plugins, and showcase](https://github.com/groupdocs-assembly/GroupDocs.Assembly-for-Python-via-.NET)

### Free Online Apps

Along with the full-featured Java library, we provide simple but powerful free online apps.

To assemble documents from templates and data sources, you can use the online apps from the **[GroupDocs.Assembly App Product Family](https://products.groupdocs.app/assembly/family)**.
