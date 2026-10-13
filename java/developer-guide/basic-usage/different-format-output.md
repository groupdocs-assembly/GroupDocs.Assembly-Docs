---
id: assembly-basic-usage-different-format-output-java
url: assembly/java/basic-usage-different-format-output
linktitle: Generate Output in Different Format
title: Generate Output in Different Format
weight: 13
description: "Convert assembled documents to different formats (e.g., DOCX to PDF, DOCX to HTML) during assembly using GroupDocs.Assembly for Java."
keywords: format conversion, PDF output, HTML output, convert format, change format, output format, DOCX to PDF
productName: GroupDocs.Assembly for Java
hideChildren: False
---

## Overview

GroupDocs.Assembly for Java allows you to generate output documents in a different format than the template. For example, you can create a DOCX template but output a PDF, or create an XLSX template but output HTML. The output format is determined by the file extension of the output path.

The main class involved is:
- [DocumentAssembler](https://reference.groupdocs.com/assembly/java/com.groupdocs.assembly/documentassembler/) - assembles documents and converts to output format

Here are the steps to generate output in a different format:

* Create a template document in one format (e.g., DOCX)
* Specify an output path with a different file extension (e.g., .pdf, .html)
* Assemble the document using DocumentAssembler
* The output will be automatically converted to the specified format

{{< alert style="info" >}}
Format conversion is automatic based on the output file extension. Supported conversions depend on the template format - Word templates can convert to PDF, HTML, and more, while spreadsheet templates have more limited conversion options. When writing the result to an `OutputStream`, or to override the format implied by the extension, pass [LoadSaveOptions](https://reference.groupdocs.com/assembly/java/com.groupdocs.assembly/loadsaveoptions/) with the required [FileFormat](https://reference.groupdocs.com/assembly/java/com.groupdocs.assembly/fileformat/), for example `new LoadSaveOptions(FileFormat.PDF)`.
{{< /alert >}}

## Convert DOCX Template to PDF

Generate a PDF from a Word template:

```java
import com.groupdocs.assembly.*;
import java.util.Date;

public static void convertDocxToPdf() throws Exception
{
    // DOCX template, PDF output
    String templatePath = "InvoiceTemplate.docx";
    String outputPath = "Invoice.pdf";

    InvoiceData invoiceData = new InvoiceData("ABC Corp", 1500.00, new Date());

    DocumentAssembler assembler = new DocumentAssembler();
    assembler.assembleDocument(templatePath, outputPath,
        new DataSourceInfo(invoiceData, "invoice"));

    System.out.println("PDF generated from DOCX template.");
}

// Data source type (must be public; members are accessed in templates through getters,
// e.g. <<[invoice.getCustomerName()]>>)
public class InvoiceData
{
    private final String customerName;
    private final double amount;
    private final Date date;

    public InvoiceData(String customerName, double amount, Date date)
    {
        this.customerName = customerName;
        this.amount = amount;
        this.date = date;
    }

    public String getCustomerName() { return customerName; }
    public double getAmount() { return amount; }
    public Date getDate() { return date; }
}
```

## Convert DOCX Template to HTML

Generate an HTML file from a Word template:

```java
import com.groupdocs.assembly.*;

public static void convertDocxToHtml() throws Exception
{
    // DOCX template, HTML output
    String templatePath = "ReportTemplate.docx";
    String outputPath = "Report.html";

    ReportData reportData = new ReportData("Monthly Report", "January 2024");

    DocumentAssembler assembler = new DocumentAssembler();
    assembler.assembleDocument(templatePath, outputPath,
        new DataSourceInfo(reportData, "report"));

    System.out.println("HTML generated from DOCX template.");
}

public class ReportData
{
    private final String title;
    private final String month;

    public ReportData(String title, String month)
    {
        this.title = title;
        this.month = month;
    }

    public String getTitle() { return title; }
    public String getMonth() { return month; }
}
```

## Convert DOCX Template to XPS

Generate an XPS document from a Word template:

```java
import com.groupdocs.assembly.*;

public static void convertDocxToXps() throws Exception
{
    // DOCX template, XPS output
    String templatePath = "DocumentTemplate.docx";
    String outputPath = "Document.xps";

    DocumentData documentData = new DocumentData("Document Title", "Document content");

    DocumentAssembler assembler = new DocumentAssembler();
    assembler.assembleDocument(templatePath, outputPath,
        new DataSourceInfo(documentData, "document"));

    System.out.println("XPS generated from DOCX template.");
}

public class DocumentData
{
    private final String title;
    private final String content;

    public DocumentData(String title, String content)
    {
        this.title = title;
        this.content = content;
    }

    public String getTitle() { return title; }
    public String getContent() { return content; }
}
```

## Convert XLSX Template to PDF

Generate a PDF from an Excel template:

```java
import com.groupdocs.assembly.*;

public static void convertXlsxToPdf() throws Exception
{
    // XLSX template, PDF output
    String templatePath = "SpreadsheetTemplate.xlsx";
    String outputPath = "Spreadsheet.pdf";

    SalesReportData data = new SalesReportData("Sales Report", "Q1 2024");

    DocumentAssembler assembler = new DocumentAssembler();
    assembler.assembleDocument(templatePath, outputPath,
        new DataSourceInfo(data, "report"));

    System.out.println("PDF generated from XLSX template.");
}

public class SalesReportData
{
    private final String reportTitle;
    private final String quarter;

    public SalesReportData(String reportTitle, String quarter)
    {
        this.reportTitle = reportTitle;
        this.quarter = quarter;
    }

    public String getReportTitle() { return reportTitle; }
    public String getQuarter() { return quarter; }
}
```

## Convert PPTX Template to PDF

Generate a PDF from a PowerPoint template:

```java
import com.groupdocs.assembly.*;

public static void convertPptxToPdf() throws Exception
{
    // PPTX template, PDF output
    String templatePath = "PresentationTemplate.pptx";
    String outputPath = "Presentation.pdf";

    PresentationData presentationData = new PresentationData("Quarterly Review", "Q1 2024");

    DocumentAssembler assembler = new DocumentAssembler();
    assembler.assembleDocument(templatePath, outputPath,
        new DataSourceInfo(presentationData, "presentation"));

    System.out.println("PDF generated from PPTX template.");
}

public class PresentationData
{
    private final String title;
    private final String quarter;

    public PresentationData(String title, String quarter)
    {
        this.title = title;
        this.quarter = quarter;
    }

    public String getTitle() { return title; }
    public String getQuarter() { return quarter; }
}
```

## Convert Email Template to PDF

Generate a PDF from an email template:

```java
import com.groupdocs.assembly.*;

public static void convertEmailToPdf() throws Exception
{
    // MSG template, PDF output
    String templatePath = "EmailTemplate.msg";
    String outputPath = "Email.pdf";

    EmailData emailData = new EmailData("customer@example.com", "Invoice",
        "Please find attached invoice.");

    DocumentAssembler assembler = new DocumentAssembler();
    assembler.assembleDocument(templatePath, outputPath,
        new DataSourceInfo(emailData, "email"));

    System.out.println("PDF generated from email template.");
}

public class EmailData
{
    private final String recipient;
    private final String subject;
    private final String body;

    public EmailData(String recipient, String subject, String body)
    {
        this.recipient = recipient;
        this.subject = subject;
        this.body = body;
    }

    public String getRecipient() { return recipient; }
    public String getSubject() { return subject; }
    public String getBody() { return body; }
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

To learn more about format-specific options, conversion settings, and advanced format handling, please refer to the [advanced usage section]({{< ref "assembly/java/developer-guide/advanced-usage/_index.md" >}}).

## More resources

### GitHub Examples

You may easily run the code above and see the feature in action in our GitHub examples:

* [GroupDocs.Assembly for Java examples, plugins, and showcase](https://github.com/groupdocs-assembly/GroupDocs.Assembly-for-Java)
* [GroupDocs.Assembly for .NET examples, plugins, and showcase](https://github.com/groupdocs-assembly/GroupDocs.Assembly-for-.NET)
* [GroupDocs.Assembly for Python via .NET examples, plugins, and showcase](https://github.com/groupdocs-assembly/GroupDocs.Assembly-for-Python-via-.NET)

### Free Online Apps

Along with the full-featured Java library, we provide simple but powerful free online apps.

To assemble documents from templates and data sources, you can use the online apps from the **[GroupDocs.Assembly App Product Family](https://products.groupdocs.app/assembly/family)**.
