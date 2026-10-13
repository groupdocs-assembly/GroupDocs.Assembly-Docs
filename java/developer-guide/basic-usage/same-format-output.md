---
id: assembly-basic-usage-same-format-output-java
url: assembly/java/basic-usage-same-format-output
linktitle: Generate Output in Same Format
title: Generate Output in Same Format as Template
weight: 12
description: "Save assembled documents in the same format as the template (e.g., DOCX to DOCX, XLSX to XLSX) using GroupDocs.Assembly for Java."
keywords: same format, output format, save document, preserve format, DOCX output, XLSX output, PPTX output
productName: GroupDocs.Assembly for Java
hideChildren: False
---

## Overview

By default, GroupDocs.Assembly for Java saves assembled documents in the same format as the template. This means a DOCX template produces a DOCX output, an XLSX template produces an XLSX output, and so on. The output format is determined by the file extension of the output path.

The main class involved is:
- [DocumentAssembler](https://reference.groupdocs.com/assembly/java/com.groupdocs.assembly/documentassembler/) - assembles documents and determines output format

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

```java
import com.groupdocs.assembly.*;
import java.util.Date;

public static void generateDocxFromDocx() throws Exception
{
    // Template and output are both DOCX
    String templatePath = "InvoiceTemplate.docx";
    String outputPath = "Invoice.docx";

    InvoiceData invoiceData = new InvoiceData("ABC Corp", 1500.00, new Date());

    DocumentAssembler assembler = new DocumentAssembler();
    assembler.assembleDocument(templatePath, outputPath,
        new DataSourceInfo(invoiceData, "invoice"));

    System.out.println("DOCX document generated from DOCX template.");
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

## Generate XLSX from XLSX Template

Generate an Excel spreadsheet from an Excel template:

```java
import com.groupdocs.assembly.*;

public static void generateXlsxFromXlsx() throws Exception
{
    // Template and output are both XLSX
    String templatePath = "ReportTemplate.xlsx";
    String outputPath = "Report.xlsx";

    ReportData reportData = new ReportData("Monthly Sales", "January 2024");

    DocumentAssembler assembler = new DocumentAssembler();
    assembler.assembleDocument(templatePath, outputPath,
        new DataSourceInfo(reportData, "report"));

    System.out.println("XLSX document generated from XLSX template.");
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

## Generate PPTX from PPTX Template

Generate a PowerPoint presentation from a PowerPoint template:

```java
import com.groupdocs.assembly.*;

public static void generatePptxFromPptx() throws Exception
{
    // Template and output are both PPTX
    String templatePath = "PresentationTemplate.pptx";
    String outputPath = "Presentation.pptx";

    PresentationData presentationData = new PresentationData("Quarterly Review", "Q1 2024");

    DocumentAssembler assembler = new DocumentAssembler();
    assembler.assembleDocument(templatePath, outputPath,
        new DataSourceInfo(presentationData, "presentation"));

    System.out.println("PPTX document generated from PPTX template.");
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

## Generate MSG from MSG Template

Generate an email message from an email template:

```java
import com.groupdocs.assembly.*;

public static void generateMsgFromMsg() throws Exception
{
    // Template and output are both MSG
    String templatePath = "EmailTemplate.msg";
    String outputPath = "Email.msg";

    EmailData emailData = new EmailData("customer@example.com", "Invoice",
        "Please find attached invoice.");

    DocumentAssembler assembler = new DocumentAssembler();
    assembler.assembleDocument(templatePath, outputPath,
        new DataSourceInfo(emailData, "email"));

    System.out.println("MSG document generated from MSG template.");
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

## Using Streams with Same Format

When using streams, the format is still preserved based on the template format:

```java
import com.groupdocs.assembly.*;
import java.io.*;
import java.nio.file.*;

public static void generateSameFormatFromStream() throws Exception
{
    // Load DOCX template from stream
    byte[] templateBytes = Files.readAllBytes(Paths.get("Template.docx"));

    try (InputStream templateStream = new ByteArrayInputStream(templateBytes);
         OutputStream outputStream = new FileOutputStream("Output.docx"))
    {
        ItemData data = new ItemData("Test", 100);

        DocumentAssembler assembler = new DocumentAssembler();
        assembler.assembleDocument(templateStream, outputStream,
            new DataSourceInfo(data, "item"));

        System.out.println("Document generated from stream in same format.");
    }
}

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

To learn more about format conversion, saving to different formats, and format-specific options, please refer to the [advanced usage section]({{< ref "assembly/java/developer-guide/advanced-usage/_index.md" >}}).

## More resources

### GitHub Examples

You may easily run the code above and see the feature in action in our GitHub examples:

* [GroupDocs.Assembly for Java examples, plugins, and showcase](https://github.com/groupdocs-assembly/GroupDocs.Assembly-for-Java)
* [GroupDocs.Assembly for .NET examples, plugins, and showcase](https://github.com/groupdocs-assembly/GroupDocs.Assembly-for-.NET)
* [GroupDocs.Assembly for Python via .NET examples, plugins, and showcase](https://github.com/groupdocs-assembly/GroupDocs.Assembly-for-Python-via-.NET)

### Free Online Apps

Along with the full-featured Java library, we provide simple but powerful free online apps.

To assemble documents from templates and data sources, you can use the online apps from the **[GroupDocs.Assembly App Product Family](https://products.groupdocs.app/assembly/family)**.
