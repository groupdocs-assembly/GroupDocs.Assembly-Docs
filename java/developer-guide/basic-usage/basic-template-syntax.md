---
id: assembly-basic-usage-template-syntax-basics-java
url: assembly/java/basic-usage-template-syntax-basics
linktitle: Basic Template Syntax
title: Basic Template Syntax - Expression Tags and Fields
weight: 5
description: "Introduction to basic template syntax including expression tags and simple member access in templates using GroupDocs.Assembly for Java."
keywords: template syntax, expression tags, fields, getters, basic syntax, template expressions, assemble, generate, Java
productName: GroupDocs.Assembly for Java
hideChildren: False
---

## Overview

GroupDocs.Assembly for Java uses a simple template syntax that allows you to embed Java expressions directly in your documents, extended with LINQ-style extension methods for collections. Expression tags are the foundation of template syntax, enabling you to output data values and perform calculations.

The main syntax elements are:
- Expression tags `<<[expression]>>` - output expression results
- Data bands `<<foreach>>` - iterate over collections
- Conditional blocks `<<if>>` - display content conditionally

Here are the steps to use basic template syntax:

* Create a template document in Word, Excel, PowerPoint, or HTML format
* Insert expression tags using `<<[expression]>>` syntax
* Call public methods (such as getters) of data source objects in expressions
* Assemble the document with your data source

{{< alert style="info" >}}
Template syntax is case-sensitive and follows Java language rules. Members of Java objects are accessed by calling their public methods, for example `person.getName()`. Expression tags are evaluated at runtime and replaced with their computed values.
{{< /alert >}}

## Basic Expression Tags

Expression tags are the simplest way to output data in templates. They use the syntax `<<[expression]>>`:

```java
import com.groupdocs.assembly.*;

public static void basicExpressionTags() throws Exception
{
    // Sample data
    Person person = new Person("John Doe", 30, "john@example.com");

    // Assemble document
    DocumentAssembler assembler = new DocumentAssembler();
    assembler.assembleDocument("Template.docx", "Output.docx",
        new DataSourceInfo(person, "person"));

    System.out.println("Document assembled with expression tags.");
}

// POJO for the data source
public class Person
{
    private final String name;
    private final int age;
    private final String email;

    public Person(String name, int age, String email)
    {
        this.name = name;
        this.age = age;
        this.email = email;
    }

    public String getName() { return name; }
    public int getAge() { return age; }
    public String getEmail() { return email; }
}
```

## Template Example with Expression Tags

In your template document (Template.docx), use expression tags like this:

```
Name: <<[person.getName()]>>
Age: <<[person.getAge()]>>
Email: <<[person.getEmail()]>>
```

After assembly, the output will be:

```
Name: John Doe
Age: 30
Email: john@example.com
```

## Using Contextual Object Member Access

When using a single data source, you can omit the data source name and use contextual access:

```java
import com.groupdocs.assembly.*;

public static void contextualAccess() throws Exception
{
    Product product = new Product("Laptop", 999.99, 50);

    DocumentAssembler assembler = new DocumentAssembler();
    assembler.assembleDocument("Template.docx", "Output.docx",
        new DataSourceInfo(product));

    System.out.println("Document assembled with contextual access.");
}

// POJO for the data source
public class Product
{
    private final String name;
    private final double price;
    private final int stock;

    public Product(String name, double price, int stock)
    {
        this.name = name;
        this.price = price;
        this.stock = stock;
    }

    public String getName() { return name; }
    public double getPrice() { return price; }
    public int getStock() { return stock; }
}
```

Template with contextual access:

```
Product: <<[getName()]>>
Price: <<[getPrice()]>>
Stock: <<[getStock()]>>
```

## Simple Calculations in Expressions

You can perform calculations directly in expression tags:

```java
import com.groupdocs.assembly.*;

public static void calculationsInExpressions() throws Exception
{
    Order order = new Order(5, 29.99);

    DocumentAssembler assembler = new DocumentAssembler();
    assembler.assembleDocument("Template.docx", "Output.docx",
        new DataSourceInfo(order, "order"));

    System.out.println("Document assembled with calculations.");
}

// POJO for the data source
public class Order
{
    private final int quantity;
    private final double unitPrice;

    public Order(int quantity, double unitPrice)
    {
        this.quantity = quantity;
        this.unitPrice = unitPrice;
    }

    public int getQuantity() { return quantity; }
    public double getUnitPrice() { return unitPrice; }
}
```

Template with calculations:

```
Quantity: <<[order.getQuantity()]>>
Unit Price: <<[order.getUnitPrice()]>>
Total: <<[order.getQuantity() * order.getUnitPrice()]>>
```

{{< alert style="info" >}}
Arithmetic operators in templates work with primitive numeric types such as `int` and `double`. They cannot be applied to `BigDecimal` values, so use primitive types for the values you calculate with in templates.
{{< /alert >}}

## Using String Methods

You can use Java `String` methods in expressions:

```java
import com.groupdocs.assembly.*;

public static void stringMethods() throws Exception
{
    Company company = new Company("ABC Corporation", "www.example.com");

    DocumentAssembler assembler = new DocumentAssembler();
    assembler.assembleDocument("Template.docx", "Output.docx",
        new DataSourceInfo(company, "company"));

    System.out.println("Document assembled with string methods.");
}

// POJO for the data source
public class Company
{
    private final String name;
    private final String website;

    public Company(String name, String website)
    {
        this.name = name;
        this.website = website;
    }

    public String getName() { return name; }
    public String getWebsite() { return website; }
}
```

Template with string methods:

```
Company: <<[company.getName().toUpperCase()]>>
Website: <<[company.getWebsite().toLowerCase()]>>
```

## Expression Tag Formatting

You can format expression results using format strings:

```java
import com.groupdocs.assembly.*;
import java.util.*;

public static void formattedExpressions() throws Exception
{
    Invoice invoice = new Invoice(
        1500.50,
        new GregorianCalendar(2024, Calendar.JANUARY, 15).getTime(),
        0.15);

    DocumentAssembler assembler = new DocumentAssembler();
    assembler.assembleDocument("Template.docx", "Output.docx",
        new DataSourceInfo(invoice, "invoice"));

    System.out.println("Document assembled with formatting.");
}

// POJO for the data source
public class Invoice
{
    private final double amount;
    private final Date date;
    private final double percentage;

    public Invoice(double amount, Date date, double percentage)
    {
        this.amount = amount;
        this.date = date;
        this.percentage = percentage;
    }

    public double getAmount() { return amount; }
    public Date getDate() { return date; }
    public double getPercentage() { return percentage; }
}
```

Template with formatting:

```
Amount: <<[invoice.getAmount()]:"$#,##0.00">>
Date: <<[invoice.getDate()]:"yyyy-MM-dd">>
Percentage: <<[invoice.getPercentage()]:"0.00%">>
```

{{< alert style="warning" >}}
Format strings follow Java formatting conventions: `java.text.DecimalFormat` patterns for numbers (for example, `"$#,##0.00"` for currency or `"0.00%"` for percentage) and `java.text.SimpleDateFormat` patterns for dates. .NET standard format specifiers such as `"C"` or `"P"` are not supported. Decimal and grouping separators depend on the default locale of the JVM.
{{< /alert >}}

### Advanced Usage Topics

To learn more about data bands, conditional blocks, collection extension methods, and advanced template syntax features, please refer to the [advanced usage section]({{< ref "assembly/java/developer-guide/advanced-usage/_index.md" >}}).

## More resources

### GitHub Examples

You may easily run the code above and see the feature in action in our GitHub examples:

* [GroupDocs.Assembly for Java examples, plugins, and showcase](https://github.com/groupdocs-assembly/GroupDocs.Assembly-for-Java)
* [GroupDocs.Assembly for .NET examples, plugins, and showcase](https://github.com/groupdocs-assembly/GroupDocs.Assembly-for-.NET)
* [GroupDocs.Assembly for Python via .NET examples, plugins, and showcase](https://github.com/groupdocs-assembly/GroupDocs.Assembly-for-Python-via-.NET)

### Free Online Apps

Along with the full-featured Java library, we provide simple but powerful free online apps.

To assemble documents from templates and data sources, you can use the online apps from the **[GroupDocs.Assembly App Product Family](https://products.groupdocs.app/assembly/family)**.
