---
id: assembly-basic-usage-ooxml-compliance
url: assembly/java/basic-usage-ooxml-compliance
linktitle: Specify OOXML Compliance
title: Specify OOXML Compliance Level for Word Documents
weight: 19
description: "Control the OOXML compliance level (Ecma, Transitional, or Strict) when saving Word documents to OOXML formats using GroupDocs.Assembly for Java."
keywords: OOXML compliance, OoxmlCompliance, Ecma, Transitional, Strict, DOCX compliance, Word document compliance, ISO/IEC 29500
productName: GroupDocs.Assembly for Java
hideChildren: False
---

## Overview

GroupDocs.Assembly for Java allows you to control the OOXML compliance level when saving Word documents to OOXML formats (DOCX, DOCM, DOTX, DOTM, FlatOpc, etc.). You can explicitly specify the compliance level or let the system automatically preserve the original document's compliance level.

The main classes involved are:
- [LoadSaveOptions](https://reference.groupdocs.com/assembly/java/groupdocs.assembly/loadsaveoptions/) - contains the OoxmlCompliance property
- [DocumentAssembler](https://reference.groupdocs.com/assembly/java/groupdocs.assembly/documentassembler/) - assembles documents with specified compliance

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

```java
import com.groupdocs.assembly.*;

public static void specifyExplicitCompliance() throws Exception
{
    DocumentAssembler assembler = new DocumentAssembler();

    // Create LoadSaveOptions with explicit OOXML compliance
    LoadSaveOptions options = new LoadSaveOptions(FileFormat.DOCX);
    options.setOoxmlCompliance(OoxmlCompliance.STRICT); // or OoxmlCompliance.ECMA, OoxmlCompliance.TRANSITIONAL

    // Data object (Java has no anonymous types; use a POJO or Map)
    CompanyData data = new CompanyData();
    data.setCompanyName("ABC Corp");
    data.setYear(2026);

    assembler.assembleDocument("Template.docx", "Output.docx", options,
        new DataSourceInfo(data, "company"));
}

// Simple POJO for the data source (getters required for assembly engine)
static class CompanyData
{
    private String companyName;
    private int year;

    public String getCompanyName() { return companyName; }
    public void setCompanyName(String value) { this.companyName = value; }
    public int getYear() { return year; }
    public void setYear(int value) { this.year = value; }
}
```

## Use Transitional Compliance

For maximum compatibility with older Office versions, use Transitional compliance:

```java
import com.groupdocs.assembly;

public static void useTransitionalCompliance() throws Exception
{
    DocumentAssembler assembler = new DocumentAssembler();

    LoadSaveOptions options = new LoadSaveOptions(FileFormat.DOCX);
    options.setOoxmlCompliance(OoxmlCompliance.TRANSITIONAL);

    OrderData data = new OrderData();
    data.setCustomerName("John Doe");
    data.setOrderNumber("ORD-12345");

    assembler.assembleDocument("Template.docx", "Output.docx", options,
        new DataSourceInfo(data, "order"));
}

// POJO for the data source
static class OrderData
{
    private String customerName;
    private String orderNumber;

    public String getCustomerName() { return customerName; }
    public void setCustomerName(String value) { this.customerName = value; }
    public String getOrderNumber() { return orderNumber; }
    public void setOrderNumber(String value) { this.orderNumber = value; }
}
```

## Use Ecma Compliance

For ECMA-376 standard compliance:

```java
import com.groupdocs.assembly.*;

public static void useEcmaCompliance() throws Exception
{
    DocumentAssembler assembler = new DocumentAssembler();

    LoadSaveOptions options = new LoadSaveOptions(FileFormat.DOCX);
    options.setOoxmlCompliance(OoxmlCompliance.ECMA);

    ReportData data = new ReportData();
    data.setReportTitle("Monthly Report");
    data.setMonth("January 2026");

    assembler.assembleDocument("Template.docx", "Output.docx", options,
        new DataSourceInfo(data, "report"));
}

// POJO for the data source
static class ReportData
{
    private String reportTitle;
    private String month;

    public String getReportTitle() { return reportTitle; }
    public void setReportTitle(String value) { this.reportTitle = value; }
    public String getMonth() { return month; }
    public void setMonth(String value) { this.month = value; }
}
```

## Automatic Preservation of Original Compliance

When `OoxmlCompliance` is not explicitly set (default `null`), the system automatically preserves the original document's compliance level if it was Transitional:

```java
import com.groupdocs.assembly.*;

public static void preserveOriginalCompliance() throws Exception
{
    DocumentAssembler assembler = new DocumentAssembler();

    // OoxmlCompliance is null by default - original compliance will be preserved
    LoadSaveOptions options = new LoadSaveOptions(FileFormat.DOCX);
    // options.getOoxmlCompliance() is null - automatic preservation

    DocumentData data = new DocumentData();
    data.setTitle("Document Title");
    data.setContent("Document content");

    // Output document will maintain Transitional compliance from template if it was Transitional
    assembler.assembleDocument("Template_Transitional.docx", "Output.docx", options,
        new DataSourceInfo(data, "document"));
}

// POJO for the data source
static class DocumentData
{
    private String title;
    private String content;

    public String getTitle() { return title; }
    public void setTitle(String value) { this.title = value; }
    public String getContent() { return content; }
    public void setContent(String value) { this.content = value; }
}
```

## Using with Different OOXML Formats

The OoxmlCompliance property works with all OOXML formats:

```java
import com.groupdocs.assembly.*;

public static void useWithDifferentFormats() throws Exception
{
    DocumentAssembler assembler = new DocumentAssembler();

    ItemData data = new ItemData();
    data.setName("Test Document");
    data.setValue(100);

    // DOCX format
    LoadSaveOptions docxOptions = new LoadSaveOptions(FileFormat.DOCX);
    docxOptions.setOoxmlCompliance(OoxmlCompliance.STRICT);
    assembler.assembleDocument("Template.docx", "Output.docx", docxOptions,
        new DataSourceInfo(data, "item"));

    // DOCM format (macro-enabled)
    LoadSaveOptions docmOptions = new LoadSaveOptions(FileFormat.DOCM);
    docmOptions.setOoxmlCompliance(OoxmlCompliance.TRANSITIONAL);
    assembler.assembleDocument("Template.docm", "Output.docm", docmOptions,
        new DataSourceInfo(data, "item"));

    // DOTX format (template)
    LoadSaveOptions dotxOptions = new LoadSaveOptions(FileFormat.DOTX);
    dotxOptions.setOoxmlCompliance(OoxmlCompliance.STRICT);
    assembler.assembleDocument("Template.dotx", "Output.dotx", dotxOptions,
        new DataSourceInfo(data, "item"));
}

// POJO for the data source
static class ItemData
{
    private String name;
    private int value;

    public String getName() { return name; }
    public void setName(String value) { this.name = value; }
    public int getValue() { return value; }
    public void setValue(int value) { this.value = value; }
}
```

## Using with Streams

You can also specify OOXML compliance when working with streams:

```java
import com.groupdocs.assembly.*;
import java.io.*;

public static void useComplianceWithStreams() throws Exception
{
    DocumentAssembler assembler = new DocumentAssembler();

    LoadSaveOptions options = new LoadSaveOptions(FileFormat.DOCX);
    options.setOoxmlCompliance(OoxmlCompliance.STRICT);

    CompanyData data = new CompanyData();
    data.setCompany("My Company");
    data.setYear(2024);

    try (InputStream templateStream = new FileInputStream("Template.docx");
         OutputStream outputStream = new FileOutputStream("Output.docx"))
    {
        assembler.assembleDocument(templateStream, outputStream, options,
            new DataSourceInfo(data, "company"));
    }
}

// POJO for the data source
static class CompanyData
{
    private String company;
    private int year;

    public String getCompany() { return company; }
    public void setCompany(String value) { this.company = value; }
    public int getYear() { return year; }
    public void setYear(int value) { this.year = value; }
}
```

## Compliance Level Behavior

Understanding how compliance levels work:

- **When explicitly set**: The specified compliance level is used when saving to OOXML formats
- **When null (default)**: 
  - If the original document had Transitional compliance, it is preserved
  - Otherwise, Strict compliance is used
- **For non-OOXML formats**: The property is ignored (e.g., PDF, HTML, RTF)

```java
import com.groupdocs.assembly.*;

public static void demonstrateComplianceBehavior() throws Exception
{
    DocumentAssembler assembler = new DocumentAssembler();

    DocData data = new DocData();
    data.setTitle("Test");
    data.setContent("Content");

    // Explicit Strict compliance
    LoadSaveOptions strictOptions = new LoadSaveOptions(FileFormat.DOCX);
    strictOptions.setOoxmlCompliance(OoxmlCompliance.STRICT);
    assembler.assembleDocument("Template.docx", "Output_Strict.docx", strictOptions,
        new DataSourceInfo(data, "doc"));

    // Automatic preservation (null)
    LoadSaveOptions autoOptions = new LoadSaveOptions(FileFormat.DOCX);
    // autoOptions.getOoxmlCompliance() is null - will preserve if Transitional
    assembler.assembleDocument("Template.docx", "Output_Auto.docx", autoOptions,
        new DataSourceInfo(data, "doc"));

    // Note: For PDF output, OoxmlCompliance is ignored
    LoadSaveOptions pdfOptions = new LoadSaveOptions(FileFormat.PDF);
    pdfOptions.setOoxmlCompliance(OoxmlCompliance.STRICT); // Ignored for PDF
    assembler.assembleDocument("Template.docx", "Output.pdf", pdfOptions,
        new DataSourceInfo(data, "doc"));
}

// POJO for the data source
static class DocData
{
    private String title;
    private String content;

    public String getTitle() { return title; }
    public void setTitle(String value) { this.title = value; }
    public String getContent() { return content; }
    public void setContent(String value) { this.content = value; }
}
```

{{< alert style="warning" >}}
The OoxmlCompliance property only affects OOXML formats. When saving to other formats like PDF, HTML, or RTF, this property is ignored. The compliance level is determined by the output format, not the template format.
{{< /alert >}}

### Advanced Usage Topics

To learn more about format-specific options, document conversion settings, and advanced compliance handling, please refer to the [advanced usage section]({{< ref "assembly/java/developer-guide/advanced-usage/_index.md" >}}).

## More resources

### GitHub Examples

You may easily run the code above and see the feature in action in our GitHub examples:

* [GroupDocs.Assembly for Java examples, plugins, and showcase](https://github.com/groupdocs-assembly/GroupDocs.Assembly-for-Java)
* [GroupDocs.Assembly for .NET examples, plugins, and showcase](https://github.com/groupdocs-assembly/GroupDocs.Assembly-for-.NET)
* [GroupDocs.Assembly for Python via .NET examples, plugins, and showcase](https://github.com/groupdocs-assembly/GroupDocs.Assembly-for-Python-via-.NET)

### Free Online Apps

Along with the full-featured Java library, we provide simple but powerful free online apps.

To assemble documents from templates and data sources, you can use the online apps from the **[GroupDocs.Assembly App Product Family](https://products.groupdocs.app/assembly/family)**.

