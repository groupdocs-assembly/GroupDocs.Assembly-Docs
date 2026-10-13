---
id: assembly-basic-usage-formatting-java
url: assembly/java/basic-usage-formatting
linktitle: Apply Formatting for various types
title: Apply Formatting to Numbers, Dates, and Text in Java
weight: 22
description: "Format numeric values, date-time values, and text strings in templates using format strings and functions in GroupDocs.Assembly for Java."
keywords: formatting, number format, date format, text format, format strings, numeric formatting, date formatting, DecimalFormat, SimpleDateFormat, Java
productName: GroupDocs.Assembly for Java
hideChildren: False
---

## Overview

GroupDocs.Assembly for Java provides comprehensive formatting capabilities for numbers, dates, and text in templates. You can use format strings (the same patterns as Java's `DecimalFormat` and `SimpleDateFormat`) and built-in text transformation functions to control how data is displayed in your documents.

The main syntax elements are:
- Format strings: `<<[expression]:"format">>` - apply `DecimalFormat` / `SimpleDateFormat` patterns
- Text functions: `upper`, `lower`, `caps`, `firstCap` - transform text case

Here are the steps to apply formatting:

* Use format strings in expression tags for numbers and dates
* Apply text transformation functions for string formatting
* Combine formatting with expressions and calculations
* Test formatting to ensure desired output

{{< alert style="info" >}}
Format strings follow Java formatting conventions: numeric values are formatted with [DecimalFormat](https://docs.oracle.com/javase/8/docs/api/java/text/DecimalFormat.html) patterns (`#,##0.00`, `0.00%`, etc.) and `java.util.Date` values with [SimpleDateFormat](https://docs.oracle.com/javase/8/docs/api/java/text/SimpleDateFormat.html) patterns (`yyyy-MM-dd`, etc.). .NET standard format specifiers such as `C`, `N2`, or `P` are not supported. Decimal and group separators, currency symbols, and month names are taken from the default locale of the JVM; the sample outputs on this page are for the `en-US` locale.
{{< /alert >}}

## Format Numbers

Format numeric values using format strings:

```java
import com.groupdocs.assembly.*;
import java.util.Date;

public class Invoice
{
    private double amount;
    private double percentage;
    private int quantity;
    private Date createdDate;

    public double getAmount() { return amount; }
    public void setAmount(double value) { amount = value; }
    public double getPercentage() { return percentage; }
    public void setPercentage(double value) { percentage = value; }
    public int getQuantity() { return quantity; }
    public void setQuantity(int value) { quantity = value; }
    public Date getCreatedDate() { return createdDate; }
    public void setCreatedDate(Date value) { createdDate = value; }
}

public static void formatNumbers() throws Exception
{
    Invoice invoice = new Invoice();
    invoice.setAmount(1500.75);
    invoice.setPercentage(0.15);
    invoice.setQuantity(25);

    DocumentAssembler assembler = new DocumentAssembler();
    assembler.assembleDocument("FormattingTemplate.docx", "FormattingOutput.docx",
        new DataSourceInfo(invoice, "invoice"));

    System.out.println("Numbers formatted successfully.");
}
```

## Template Examples for Number Formatting

In your template, use format strings:

```
Amount: <<[invoice.getAmount()]:"$#,##0.00">>
Percentage: <<[invoice.getPercentage()]:"0.00%">>
Quantity: <<[invoice.getQuantity()]:"#,##0">>
```

Common numeric format strings:
- `"$#,##0.00"` - Currency with a fixed symbol (e.g., $1,500.75)
- `"¤#,##0.00"` - Currency with the currency symbol of the default locale (e.g., $1,500.75 for en-US)
- `"#,##0.00"` - Number with group separators and two decimals (e.g., 1,500.75)
- `"0.00"` - Fixed-point (e.g., 1500.75)
- `"0.00%"` - Percentage (e.g., 15.00%)
- `"#,##0"` - Integer with group separators (e.g., 1,501)

## Format Dates and Times

Format date-time values:

```java
import com.groupdocs.assembly.*;
import java.util.Calendar;
import java.util.Date;
import java.util.GregorianCalendar;

public class Report
{
    private Date createdDate;
    private Date dueDate;

    public Date getCreatedDate() { return createdDate; }
    public void setCreatedDate(Date value) { createdDate = value; }
    public Date getDueDate() { return dueDate; }
    public void setDueDate(Date value) { dueDate = value; }
}

public static void formatDates() throws Exception
{
    Report report = new Report();
    report.setCreatedDate(new GregorianCalendar(2024, Calendar.JANUARY, 15, 14, 30, 0).getTime());
    report.setDueDate(new GregorianCalendar(2024, Calendar.FEBRUARY, 15).getTime());

    DocumentAssembler assembler = new DocumentAssembler();
    assembler.assembleDocument("FormattingTemplate.docx", "FormattingOutput.docx",
        new DataSourceInfo(report, "report"));

    System.out.println("Dates formatted successfully.");
}
```

## Template Examples for Date Formatting

```
Created: <<[report.getCreatedDate()]:"yyyy-MM-dd HH:mm">>
Due Date: <<[report.getDueDate()]:"MMMM dd, yyyy">>
```

Common date format strings:
- `"yyyy-MM-dd"` - 2024-01-15
- `"MM/dd/yyyy"` - 01/15/2024
- `"MMMM dd, yyyy"` - January 15, 2024
- `"dd.MM.yyyy"` - 15.01.2024
- `"HH:mm"` - 14:30

{{< alert style="info" >}}
Date format strings are applied to `java.util.Date` values. Values of `java.time` types such as `LocalDate` are output using their `toString()` method, and the format string is ignored, so convert them to `java.util.Date` before passing them to the engine.
{{< /alert >}}

## Format Text (Case Transformation)

Transform text case using built-in functions:

```java
import com.groupdocs.assembly.*;

public class Product
{
    private String name;
    private String description;

    public String getName() { return name; }
    public void setName(String value) { name = value; }
    public String getDescription() { return description; }
    public void setDescription(String value) { description = value; }
}

public static void formatText() throws Exception
{
    Product product = new Product();
    product.setName("laptop computer");
    product.setDescription("HIGH-PERFORMANCE DEVICE");

    DocumentAssembler assembler = new DocumentAssembler();
    assembler.assembleDocument("FormattingTemplate.docx", "FormattingOutput.docx",
        new DataSourceInfo(product, "product"));

    System.out.println("Text formatted successfully.");
}
```

## Template Examples for Text Formatting

```
Name: <<[product.getName()]:upper>>
Description: <<[product.getDescription()]:lower>>
Title: <<[product.getName()]:caps>>
```

Text transformation functions:
- `:upper` - Convert to UPPERCASE
- `:lower` - Convert to lowercase
- `:caps` - Capitalize Each Word
- `:firstCap` - Capitalize first letter only

## Combine Formatting with Calculations

Format calculated values:

```java
import com.groupdocs.assembly.*;

public class Order
{
    private int quantity;
    private double unitPrice;

    public int getQuantity() { return quantity; }
    public void setQuantity(int value) { quantity = value; }
    public double getUnitPrice() { return unitPrice; }
    public void setUnitPrice(double value) { unitPrice = value; }
}

public static void formatCalculations() throws Exception
{
    Order order = new Order();
    order.setQuantity(5);
    order.setUnitPrice(29.99);

    DocumentAssembler assembler = new DocumentAssembler();
    assembler.assembleDocument("FormattingTemplate.docx", "FormattingOutput.docx",
        new DataSourceInfo(order, "order"));

    System.out.println("Calculations formatted successfully.");
}
```

Template:

```
Quantity: <<[order.getQuantity()]>>
Unit Price: <<[order.getUnitPrice()]:"$#,##0.00">>
Total: <<[order.getQuantity() * order.getUnitPrice()]:"$#,##0.00">>
```

{{< alert style="info" >}}
Use primitive numeric types (`int`, `double`, etc.) or their wrappers for values involved in template arithmetic. `BigDecimal` values can be output and formatted, but arithmetic operators cannot be applied to them in template expressions.
{{< /alert >}}

## Custom Numeric Formats

Use custom format strings for specific requirements:

```java
import com.groupdocs.assembly.*;

public class NumericData
{
    private long population;
    private int code;
    private double rate;

    public NumericData(long population, int code, double rate)
    {
        this.population = population;
        this.code = code;
        this.rate = rate;
    }

    public long getPopulation() { return population; }
    public int getCode() { return code; }
    public double getRate() { return rate; }
}

public static void customNumericFormats() throws Exception
{
    NumericData data = new NumericData(1234567890L, 42, 0.1234);

    DocumentAssembler assembler = new DocumentAssembler();
    assembler.assembleDocument("FormattingTemplate.docx", "FormattingOutput.docx",
        new DataSourceInfo(data, "data"));

    System.out.println("Custom formats applied successfully.");
}
```

Template with custom formats:

```
Population: <<[data.getPopulation()]:"#,###">>
Code: <<[data.getCode()]:"000">>
Rate: <<[data.getRate()]:"0.00%">>
```

The template above produces "Population: 1,234,567,890", "Code: 042", and "Rate: 12.34%".

{{< alert style="info" >}}
`DecimalFormat` patterns do not support digit masks with literal characters between digits (such as a phone number pattern `(###) ###-####`). Store such values as preformatted strings instead.
{{< /alert >}}

## Formatting in Different Document Types

Formatting works consistently across document types:

```java
import com.groupdocs.assembly.*;
import java.util.Date;

public static void formatInSpreadsheet() throws Exception
{
    Invoice invoice = new Invoice();
    invoice.setAmount(1500.75);
    invoice.setCreatedDate(new Date());

    DocumentAssembler assembler = new DocumentAssembler();
    assembler.assembleDocument("FormattingTemplate.xlsx", "FormattingOutput.xlsx",
        new DataSourceInfo(invoice, "invoice"));

    System.out.println("Formatting applied in spreadsheet successfully.");
}
```

{{< alert style="warning" >}}
Format strings and text function names are case-sensitive. Follow `DecimalFormat` and `SimpleDateFormat` conventions exactly (for example, `MM` means months while `mm` means minutes), and write text functions exactly as `upper`, `lower`, `caps`, and `firstCap`.
{{< /alert >}}

### Advanced Usage Topics

To learn more about custom format providers, culture-specific formatting, and advanced formatting scenarios, please refer to the [advanced usage section]({{< ref "assembly/java/developer-guide/advanced-usage/_index.md" >}}).

## More resources

### GitHub Examples

You may easily run the code above and see the feature in action in our GitHub examples:

* [GroupDocs.Assembly for Java examples, plugins, and showcase](https://github.com/groupdocs-assembly/GroupDocs.Assembly-for-Java)
* [GroupDocs.Assembly for .NET examples, plugins, and showcase](https://github.com/groupdocs-assembly/GroupDocs.Assembly-for-.NET)
* [GroupDocs.Assembly for Python via .NET examples, plugins, and showcase](https://github.com/groupdocs-assembly/GroupDocs.Assembly-for-Python-via-.NET)

### Free Online Apps

Along with the full-featured Java library, we provide simple but powerful free online apps.

To assemble documents from templates and data sources, you can use the online apps from the **[GroupDocs.Assembly App Product Family](https://products.groupdocs.app/assembly/family)**.

