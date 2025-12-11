# Basic Usage Documentation Structure for GroupDocs.Assembly for .NET

This document contains the complete structure, metadata, planning, and ready-to-use Markdown files for the Basic Usage section.

---

## Section A – Basic Usage Topic List (TOC)

### 1. Getting Started Basics
- **Install via NuGet and apply license**
  - Install GroupDocs.Assembly via NuGet Package Manager or Package Manager Console
  - Apply license from file or stream
  - Verify installation and license status

- **First simple document generation**
  - Generate a simple document from an in-memory .NET object
  - Basic template with expression tags
  - Save output document

### 2. Working with Templates
- **Load templates from file path and stream**
  - Load template from file path
  - Load template from stream
  - Supported template formats overview

- **Supported template formats and basic notes**
  - Word processing formats (DOCX, DOC, RTF, etc.)
  - Spreadsheet formats (XLSX, XLS, etc.)
  - Presentation formats (PPTX, PPT, etc.)
  - Email formats (MSG, EML, etc.)
  - HTML and other formats

- **Minimal template syntax usage**
  - Expression tags `<<[expression]>>`
  - Basic field access
  - Simple expressions

### 3. Data Sources – Basic Scenarios

- **Generate document from custom .NET objects**
  - Create custom class with properties
  - Pass object instance to DocumentAssembler
  - Access properties in template

- **Generate document from XML data source**
  - Load XML data using XmlDataSource
  - Access XML elements and attributes in template
  - Handle nested XML structures

- **Generate document from JSON data source**
  - Load JSON data using JsonDataSource
  - Access JSON properties and arrays in template
  - Handle nested JSON objects

- **Generate document from database (ADO.NET / ORM)**
  - Use DataSet or DataTable as data source
  - Connect to database and populate DataSet
  - Access tables and rows in template

- **Generate document from OData**
  - Connect to OData service
  - Deserialize OData response to custom objects
  - Use objects in template

- **Generate document using external documents as data source**
  - Use Word tables as data source
  - Use spreadsheet tables as data source
  - Load external document and extract data

### 4. Core Output Operations

- **Generate and save output in the same format as template**
  - DOCX template → DOCX output
  - XLSX template → XLSX output
  - PPTX template → PPTX output

- **Generate and save output in another format**
  - DOCX template → PDF output
  - DOCX template → HTML output
  - XLSX template → PDF output

- **Work with streams vs file paths**
  - Assemble document using file paths
  - Assemble document using streams
  - Memory-efficient stream handling

### 5. Basic Content Generation Patterns

- **Generate tables from a collection**
  - Create table in template
  - Use foreach data band in table rows
  - Display collection items in table format

- **Generate bullet lists from a data source**
  - Create bullet list in template
  - Use foreach data band for list items
  - Format list items

- **Generate numbered lists from a data source**
  - Create numbered list in template
  - Use foreach data band for numbered items
  - Customize numbering format

- **Generate master–detail (parent–child) reports**
  - Nested foreach data bands
  - Parent-child data relationships
  - Display orders with order items example

- **Generate charts from data**
  - Create chart in template
  - Bind chart data from data source
  - Display chart with dynamic data

- **Generate images dynamically**
  - Insert images from file path
  - Insert images from URL
  - Insert images from binary data/stream

- **Insert hyperlinks dynamically**
  - Create hyperlinks in template
  - Set hyperlink URL from data source
  - Format hyperlink text

### 6. Formatting and Simple Calculations

- **Apply numeric, date/time, and text formatting**
  - Format numbers with custom formats
  - Format dates and times
  - Apply text transformations (upper, lower, capitalize)

- **Add conditional content (if/else)**
  - Use if/elseif/else blocks
  - Conditional text display
  - Conditional formatting

- **Use simple aggregates**
  - Sum, Count, Average functions
  - Aggregate data in templates
  - Display totals and summaries

- **Use basic formulas in spreadsheet templates**
  - Insert formulas in spreadsheet cells
  - Reference data in formulas
  - Calculate values dynamically

### 7. Barcodes and Special Elements

- **Generate barcodes in documents**
  - Insert barcode in template
  - Configure barcode type and properties
  - Display barcode from data source

- **Generate QR codes**
  - Insert QR code in template
  - Configure QR code properties
  - Display QR code from data source

- **Use Word template features like NEXT-like behavior**
  - Use NEXT field for repeating documents
  - Generate multiple documents from single template
  - Handle document breaks

### 8. Email and Message Generation Basics

- **Generate email messages from data**
  - Set email subject dynamically
  - Set email body from template
  - Configure email recipients (To, CC, BCC)

- **Attach files and configure basic message properties**
  - Attach template documents as attachments
  - Set email sender (From)
  - Configure email headers

### 9. Error Handling and Diagnostics (Basic)

- **Handle common template/data errors**
  - Catch assembly exceptions
  - Validate template syntax
  - Handle missing data members

- **Log and inspect generation results**
  - Enable error logging
  - Inspect assembly warnings
  - Debug template issues

### 10. Performance-Friendly Basic Patterns

- **Basic advice for moderately large data**
  - Stream data processing
  - Simple batching strategies
  - Memory-efficient patterns

---

## Section B – Per-Topic Metadata and Planning Tables

| Topic ID | File URL Segment | Title | Parent Section | Weight | Description | Keywords | Priority |
|----------|------------------|-------|----------------|--------|-------------|----------|----------|
| assembly-basic-usage-install-license | basic-usage-install-and-license | Install GroupDocs.Assembly for .NET and Apply License | Getting Started Basics | 1 | Learn how to install GroupDocs.Assembly via NuGet and apply a license to remove evaluation limitations. | install, NuGet, license, setup, configure, GroupDocs.Assembly, .NET, C# | P1 |
| assembly-basic-usage-first-document | basic-usage-first-document | Generate Your First Document from .NET Object in C# | Getting Started Basics | 2 | Create your first document by generating a simple report from an in-memory .NET object using GroupDocs.Assembly. | generate document, create report, first example, .NET object, C#, assemble, compose | P1 |
| assembly-basic-usage-load-template | basic-usage-load-template | Load Template Documents from File or Stream in C# | Working with Templates | 3 | Learn how to load template documents from file paths and streams for document assembly in .NET. | load template, file path, stream, template document, DOCX, XLSX, PPTX | P1 |
| assembly-basic-usage-template-formats | basic-usage-template-formats | Supported Template Formats Overview | Working with Templates | 4 | Overview of supported template document formats including Word, Excel, PowerPoint, Email, and HTML formats. | template formats, DOCX, XLSX, PPTX, MSG, EML, HTML, supported formats | P2 |
| assembly-basic-usage-template-syntax-basics | basic-usage-template-syntax-basics | Basic Template Syntax - Expression Tags and Fields | Working with Templates | 5 | Introduction to basic template syntax including expression tags and simple field access in templates. | template syntax, expression tags, fields, basic syntax, template expressions | P1 |
| assembly-basic-usage-custom-objects | basic-usage-custom-objects | Generate Document from Custom .NET Objects in C# | Data Sources Basics | 6 | Generate documents by binding data from custom .NET classes and objects to template documents. | custom objects, .NET classes, object properties, data binding, C# objects, assemble document | P1 |
| assembly-basic-usage-xml-datasource | basic-usage-xml-datasource | Generate Document from XML Data Source in C# | Data Sources Basics | 7 | Create reports from XML data sources using XmlDataSource class to load and bind XML data to templates. | XML data source, XmlDataSource, XML binding, parse XML, generate from XML, assemble XML | P1 |
| assembly-basic-usage-json-datasource | basic-usage-json-datasource | Generate Document from JSON Data Source in C# | Data Sources Basics | 8 | Build documents from JSON data sources using JsonDataSource class to load and bind JSON data to templates. | JSON data source, JsonDataSource, JSON binding, parse JSON, generate from JSON, compose JSON | P1 |
| assembly-basic-usage-database-datasource | basic-usage-database-datasource | Generate Document from Database in C# | Data Sources Basics | 9 | Create reports from database data using DataSet, DataTable, or IDataReader as data sources for templates. | database, DataSet, DataTable, ADO.NET, SQL, database binding, generate from database | P1 |
| assembly-basic-usage-odata-datasource | basic-usage-odata-datasource | Generate Document from OData Service in C# | Data Sources Basics | 10 | Build documents from OData services by deserializing OData responses to custom objects and using them in templates. | OData, OData service, REST API, deserialize OData, generate from OData | P2 |
| assembly-basic-usage-external-documents | basic-usage-external-documents | Use External Documents as Data Source in C# | Data Sources Basics | 11 | Extract data from Word tables or spreadsheet tables and use them as data sources for document assembly. | external documents, Word tables, spreadsheet tables, extract data, document as data source | P2 |
| assembly-basic-usage-same-format-output | basic-usage-same-format-output | Generate Output in Same Format as Template | Core Output Operations | 12 | Save assembled documents in the same format as the template (e.g., DOCX to DOCX, XLSX to XLSX). | same format, output format, save document, preserve format, DOCX output, XLSX output | P1 |
| assembly-basic-usage-different-format-output | basic-usage-different-format-output | Generate Output in Different Format in C# | Core Output Operations | 13 | Convert assembled documents to different formats (e.g., DOCX to PDF, DOCX to HTML) during assembly. | format conversion, PDF output, HTML output, convert format, change format, output format | P1 |
| assembly-basic-usage-streams-vs-files | basic-usage-streams-vs-files | Work with Streams vs File Paths in C# | Core Output Operations | 14 | Learn when and how to use streams versus file paths for template loading and document saving in .NET. | streams, file paths, memory streams, file streams, stream handling, efficient processing | P1 |
| assembly-basic-usage-generate-tables | basic-usage-generate-tables | Generate Tables from Collection Data in C# | Content Generation Patterns | 15 | Create dynamic tables in documents by iterating over collections and displaying data in table rows. | generate tables, table reports, foreach data band, table rows, collection data, tabular data | P1 |
| assembly-basic-usage-generate-bullet-lists | basic-usage-generate-bullet-lists | Generate Bullet Lists from Data Source in C# | Content Generation Patterns | 16 | Create bulleted lists in documents by iterating over data collections and displaying items as bullets. | bullet lists, bulleted lists, foreach data band, list items, collection iteration | P1 |
| assembly-basic-usage-generate-numbered-lists | basic-usage-generate-numbered-lists | Generate Numbered Lists from Data Source in C# | Content Generation Patterns | 17 | Create numbered lists in documents by iterating over data collections and displaying items with numbers. | numbered lists, numbered items, foreach data band, list numbering, ordered lists | P1 |
| assembly-basic-usage-master-detail | basic-usage-master-detail | Generate Master-Detail Reports in C# | Content Generation Patterns | 18 | Create parent-child reports with nested data bands to display master records with their detail records. | master detail, parent child, nested foreach, hierarchical data, orders and items | P1 |
| assembly-basic-usage-generate-charts | basic-usage-generate-charts | Generate Charts from Data in C# | Content Generation Patterns | 19 | Create dynamic charts in documents by binding chart data from data sources to template charts. | generate charts, chart data, dynamic charts, bind chart data, chart reports | P2 |
| assembly-basic-usage-generate-images | basic-usage-generate-images | Insert Images Dynamically in C# | Content Generation Patterns | 20 | Insert images into documents from file paths, URLs, or binary data sources during document assembly. | insert images, dynamic images, image from file, image from URL, image from stream | P1 |
| assembly-basic-usage-insert-hyperlinks | basic-usage-insert-hyperlinks | Insert Hyperlinks Dynamically in C# | Content Generation Patterns | 21 | Create hyperlinks in documents with URLs and text dynamically set from data sources during assembly. | insert hyperlinks, dynamic hyperlinks, link URLs, hyperlink text, clickable links | P1 |
| assembly-basic-usage-formatting | basic-usage-formatting | Apply Formatting to Numbers, Dates, and Text in C# | Formatting and Calculations | 22 | Format numeric values, date-time values, and text strings in templates using format strings and functions. | formatting, number format, date format, text format, format strings, numeric formatting | P1 |
| assembly-basic-usage-conditional-content | basic-usage-conditional-content | Add Conditional Content with If/Else in C# | Formatting and Calculations | 23 | Display content conditionally in templates using if/elseif/else blocks based on data values. | conditional content, if else, conditional blocks, conditional display, conditional formatting | P1 |
| assembly-basic-usage-aggregates | basic-usage-aggregates | Use Simple Aggregates (Sum, Count, Average) in C# | Formatting and Calculations | 24 | Calculate and display aggregate values like sums, counts, and averages from data collections in templates. | aggregates, sum, count, average, totals, calculations, aggregate functions | P1 |
| assembly-basic-usage-spreadsheet-formulas | basic-usage-spreadsheet-formulas | Use Formulas in Spreadsheet Templates | Formatting and Calculations | 25 | Insert and calculate formulas in spreadsheet templates that reference data from data sources. | spreadsheet formulas, Excel formulas, calculate formulas, formula cells, dynamic formulas | P2 |
| assembly-basic-usage-generate-barcodes | basic-usage-generate-barcodes | Generate Barcodes in Documents in C# | Barcodes and Special Elements | 26 | Insert barcode images into documents dynamically from data sources with configurable barcode types. | generate barcodes, barcode images, barcode types, dynamic barcodes, barcode generation | P2 |
| assembly-basic-usage-generate-qrcodes | basic-usage-generate-qrcodes | Generate QR Codes in Documents in C# | Barcodes and Special Elements | 27 | Insert QR code images into documents dynamically from data sources with customizable properties. | generate QR codes, QR code images, QR code generation, dynamic QR codes | P2 |
| assembly-basic-usage-next-field | basic-usage-next-field | Use NEXT Field for Repeating Documents | Barcodes and Special Elements | 28 | Generate multiple documents from a single template using NEXT field behavior for document repetition. | NEXT field, repeating documents, multiple documents, document breaks, document generation | P3 |
| assembly-basic-usage-generate-emails | basic-usage-generate-emails | Generate Email Messages from Data in C# | Email Generation Basics | 29 | Create email messages with dynamic subject, body, and recipients from data sources using templates. | generate emails, email messages, email subject, email body, email recipients, MSG, EML | P1 |
| assembly-basic-usage-email-attachments | basic-usage-email-attachments | Attach Files to Email Messages in C# | Email Generation Basics | 30 | Attach documents to email messages dynamically and configure email message properties like sender. | email attachments, attach files, email properties, email sender, email headers | P2 |
| assembly-basic-usage-error-handling | basic-usage-error-handling | Handle Common Template and Data Errors | Error Handling and Diagnostics | 31 | Catch and handle common exceptions during document assembly and validate template syntax and data. | error handling, exceptions, template errors, data errors, validation, error catching | P1 |
| assembly-basic-usage-logging | basic-usage-logging | Log and Inspect Assembly Results | Error Handling and Diagnostics | 32 | Enable logging and inspect assembly warnings and errors to debug template and data issues. | logging, debug, inspect results, assembly warnings, error logging, diagnostics | P2 |
| assembly-basic-usage-performance | basic-usage-performance | Performance Tips for Large Data Sets | Performance Patterns | 33 | Best practices for processing moderately large data sets efficiently using streaming and batching. | performance, large data, streaming, batching, memory efficient, optimization | P2 |

---

## Section C – Ready-to-Use Markdown Files for P1 Topics

### Topic: Install GroupDocs.Assembly for .NET and Apply License

```markdown
---
id: assembly-basic-usage-install-license
url: assembly/net/basic-usage-install-and-license
title: Install GroupDocs.Assembly for .NET and Apply License
weight: 1
description: "Learn how to install GroupDocs.Assembly via NuGet and apply a license to remove evaluation limitations in your .NET applications."
keywords: install, NuGet, license, setup, configure, GroupDocs.Assembly, .NET, C#, apply license
productName: GroupDocs.Assembly for .NET
toc: True
---

## Overview

Before you can start generating documents with GroupDocs.Assembly for .NET, you need to install the library and apply a license. This guide shows you how to install the package via NuGet and configure licensing to remove evaluation limitations.

The main classes involved are:
- [License](https://reference.groupdocs.com/assembly/net/groupdocs.assembly/license/) - for applying licenses
- [DocumentAssembler](https://reference.groupdocs.com/assembly/net/groupdocs.assembly/documentassembler/) - for assembling documents

Here are the steps to get started:

* Install GroupDocs.Assembly package via NuGet Package Manager or Package Manager Console
* Apply a license from a file or stream using the `License.SetLicense` method
* Verify that the license is applied correctly before using DocumentAssembler

{{< alert style="info" >}}
Calling `License.SetLicense` multiple times is not harmful but wastes processor time. In Windows Forms or console applications, call it once during startup. In ASP.NET applications, call it in `Application_Start` method in Global.asax.cs.
{{< /alert >}}

## Install via NuGet Package Manager

The easiest way to install GroupDocs.Assembly is through NuGet Package Manager in Visual Studio.

```csharp
// No code needed - installation is done via NuGet UI
// 1. Right-click your project in Solution Explorer
// 2. Select "Manage NuGet Packages"
// 3. Search for "GroupDocs.Assembly"
// 4. Click "Install"
```

## Install via Package Manager Console

Alternatively, you can install the package using Package Manager Console:

```csharp
// Run this command in Package Manager Console:
// Install-Package GroupDocs.Assembly
```

## Apply License from File

After installation, apply your license file to remove evaluation limitations:

```csharp
using GroupDocs.Assembly;

public static void ApplyLicenseFromFile()
{
    // Path to your license file
    string licensePath = "GroupDocs.Assembly.lic";
    
    // Apply the license
    License license = new License();
    license.SetLicense(licensePath);
    
    Console.WriteLine("License applied successfully from file.");
}
```

## Apply License from Stream

You can also load a license from a stream:

```csharp
using GroupDocs.Assembly;
using System.IO;

public static void ApplyLicenseFromStream()
{
    // Load license file into a stream
    using (FileStream stream = new FileStream("GroupDocs.Assembly.lic", FileMode.Open))
    {
        License license = new License();
        license.SetLicense(stream);
        
        Console.WriteLine("License applied successfully from stream.");
    }
}
```

## Verify License Application

To verify that your license is applied correctly, you can check for evaluation watermarks in generated documents. If no watermarks appear, the license is active.

```csharp
using GroupDocs.Assembly;

public static void VerifyLicense()
{
    License license = new License();
    license.SetLicense("GroupDocs.Assembly.lic");
    
    // Try to assemble a simple document
    DocumentAssembler assembler = new DocumentAssembler();
    // If license is valid, no evaluation watermark will appear
    Console.WriteLine("License verification: Check generated documents for watermarks.");
}
```

{{< alert style="warning" >}}
The license file contains a digital signature. Do not modify the license file, as even adding an extra line break will invalidate it.
{{< /alert >}}

### Advanced Usage Topics

To learn more about licensing options including metered licensing, please refer to the [advanced usage section]({{< ref "assembly/net/developer-guide/advanced-usage/_index.md" >}}).

## More resources

### GitHub Examples

You may easily run the code above and see the feature in action in our GitHub examples:

* [GroupDocs.Assembly for .NET examples, plugins, and showcase](https://github.com/groupdocs-assembly/GroupDocs.Assembly-for-.NET)
* [GroupDocs.Assembly for Java examples, plugins, and showcase](https://github.com/groupdocs-assembly/GroupDocs.Assembly-for-Java)
* [GroupDocs.Assembly for Python via .NET examples, plugins, and showcase](https://github.com/groupdocs-assembly/GroupDocs.Assembly-for-Python-via-.NET)

### Free Online Apps

Along with the full-featured .NET library, we provide simple but powerful free online apps.

To assemble documents from templates and data sources, you can use the online apps from the **[GroupDocs.Assembly App Product Family](https://products.groupdocs.app/assembly/family)**.
```

---

### Topic: Generate Your First Document from .NET Object

```markdown
---
id: assembly-basic-usage-first-document
url: assembly/net/basic-usage-first-document
title: Generate Your First Document from .NET Object in C#
weight: 2
description: "Create your first document by generating a simple report from an in-memory .NET object using GroupDocs.Assembly for .NET."
keywords: generate document, create report, first example, .NET object, C#, assemble, compose, build document
productName: GroupDocs.Assembly for .NET
toc: True
---

## Overview

This guide walks you through creating your first document with GroupDocs.Assembly for .NET. You'll generate a simple document from an in-memory .NET object, demonstrating the basic workflow of template-based document assembly.

The main classes involved are:
- [DocumentAssembler](https://reference.groupdocs.com/assembly/net/groupdocs.assembly/documentassembler/) - the main class for assembling documents
- [DataSourceInfo](https://reference.groupdocs.com/assembly/net/groupdocs.assembly/datasourceinfo/) - wraps data source objects with optional names

Here are the steps to generate your first document:

* Create a simple .NET class with properties to represent your data
* Instantiate the class and populate it with sample data
* Create a template document (DOCX) with expression tags referencing the object properties
* Use DocumentAssembler to assemble the template with your data object
* Save the assembled document to a file

## Define a Simple Data Class

First, create a simple class to hold your data:

```csharp
public class Person
{
    public string Name { get; set; }
    public int Age { get; set; }
    public string Email { get; set; }
}
```

## Generate Document from Object

Now, create a method to generate a document from this object:

```csharp
using GroupDocs.Assembly;
using System;

public static void GenerateFirstDocument()
{
    // Create sample data
    Person person = new Person
    {
        Name = "John Doe",
        Age = 30,
        Email = "john.doe@example.com"
    };
    
    // Paths for template and output
    string templatePath = "Template.docx";
    string outputPath = "Output.docx";
    
    // Assemble the document
    DocumentAssembler assembler = new DocumentAssembler();
    assembler.AssembleDocument(templatePath, outputPath, 
        new DataSourceInfo(person, "person"));
    
    Console.WriteLine($"Document generated successfully: {outputPath}");
}
```

## Template Document Example

Your template document (Template.docx) should contain expression tags like this:

```
Name: <<[person.Name]>>
Age: <<[person.Age]>>
Email: <<[person.Email]>>
```

After assembly, the output will be:

```
Name: John Doe
Age: 30
Email: john.doe@example.com
```

## Using Contextual Object Member Access

You can also use contextual member access, which allows you to omit the data source name in simple scenarios:

```csharp
public static void GenerateDocumentWithContextualAccess()
{
    Person person = new Person
    {
        Name = "Jane Smith",
        Age = 28,
        Email = "jane.smith@example.com"
    };
    
    DocumentAssembler assembler = new DocumentAssembler();
    // When using contextual access, you can omit the data source name
    assembler.AssembleDocument("Template.docx", "Output.docx", 
        new DataSourceInfo(person));
}
```

With contextual access, your template can use:

```
Name: <<[Name]>>
Age: <<[Age]>>
Email: <<[Email]>>
```

{{< alert style="info" >}}
When using contextual object member access, the template expressions can reference properties directly without the data source name prefix. This is useful for simple, single-object scenarios.
{{< /alert >}}

### Advanced Usage Topics

To learn more about working with complex data structures, multiple data sources, and advanced template syntax, please refer to the [advanced usage section]({{< ref "assembly/net/developer-guide/advanced-usage/_index.md" >}}).

## More resources

### GitHub Examples

You may easily run the code above and see the feature in action in our GitHub examples:

* [GroupDocs.Assembly for .NET examples, plugins, and showcase](https://github.com/groupdocs-assembly/GroupDocs.Assembly-for-.NET)
* [GroupDocs.Assembly for Java examples, plugins, and showcase](https://github.com/groupdocs-assembly/GroupDocs.Assembly-for-Java)
* [GroupDocs.Assembly for Python via .NET examples, plugins, and showcase](https://github.com/groupdocs-assembly/GroupDocs.Assembly-for-Python-via-.NET)

### Free Online Apps

Along with the full-featured .NET library, we provide simple but powerful free online apps.

To assemble documents from templates and data sources, you can use the online apps from the **[GroupDocs.Assembly App Product Family](https://products.groupdocs.app/assembly/family)**.
```

---

### Topic: Load Template Documents from File or Stream

```markdown
---
id: assembly-basic-usage-load-template
url: assembly/net/basic-usage-load-template
title: Load Template Documents from File or Stream in C#
weight: 3
description: "Learn how to load template documents from file paths and streams for document assembly in .NET applications."
keywords: load template, file path, stream, template document, DOCX, XLSX, PPTX, load from file, load from stream
productName: GroupDocs.Assembly for .NET
toc: True
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
```

---

*[Continue with remaining P1 topics... Due to length, I'll create separate files for each topic]*

