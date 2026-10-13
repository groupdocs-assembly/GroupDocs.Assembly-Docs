---
id: assembly-basic-usage-conditional-content-java
url: assembly/java/basic-usage-conditional-content
linktitle: Add Conditional Content
title: Add Conditional Content with If/Else
weight: 23
description: "Display content conditionally in templates using if/elseif/else blocks based on data values with GroupDocs.Assembly for Java."
keywords: conditional content, if else, conditional blocks, conditional display, conditional formatting, if elseif, Java
productName: GroupDocs.Assembly for Java
hideChildren: False
---

## Overview

Conditional blocks allow you to display different content in your documents based on data values. GroupDocs.Assembly for Java supports if/elseif/else syntax similar to Java, enabling you to create dynamic documents that adapt their content based on conditions.

The main syntax elements are:
- `<<if [condition]>>` - display content if condition is true
- `<<elseif [condition]>>` - display content if previous conditions are false and this condition is true
- `<<else>>` - display content if all conditions are false
- `<</if>>` - closing tag

Here are the steps to use conditional content:

* Create a template with conditional blocks
* Define conditions using expressions that return boolean values
* Provide content for each condition branch
* Assemble the document with your data

{{< alert style="info" >}}
Conditional expressions must return boolean values. You can use comparison operators (==, !=, <, >, <=, >=), logical operators (&&, ||, !), and method calls that return boolean.
{{< /alert >}}

## Simple If/Else Block

Display content based on a simple condition:

```java
import com.groupdocs.assembly.*;

public class Customer
{
    private String name;
    private double balance;

    public String getName() { return name; }
    public void setName(String value) { name = value; }
    public double getBalance() { return balance; }
    public void setBalance(double value) { balance = value; }
}

public static void simpleConditional() throws Exception
{
    Customer customer = new Customer();
    customer.setName("John Doe");
    customer.setBalance(1500.00);

    DocumentAssembler assembler = new DocumentAssembler();
    assembler.assembleDocument("ConditionalTemplate.docx", "ConditionalOutput.docx",
        new DataSourceInfo(customer, "customer"));

    System.out.println("Conditional content generated successfully.");
}
```

## Template Example for Simple If/Else

In your template (ConditionalTemplate.docx):

```
Customer: <<[customer.getName()]>>

<<if [customer.getBalance() > 1000]>>
Status: Premium Customer
You have a high balance and qualify for special benefits.
<<else>>
Status: Standard Customer
Thank you for your business.
<</if>>
```

## If/Elseif/Else Block

Use multiple conditions with elseif:

```java
import com.groupdocs.assembly.*;

public class Order
{
    private double amount;

    public double getAmount() { return amount; }
    public void setAmount(double value) { amount = value; }
}

public static void multipleConditions() throws Exception
{
    Order order = new Order();
    order.setAmount(750.00);

    DocumentAssembler assembler = new DocumentAssembler();
    assembler.assembleDocument("ConditionalTemplate.docx", "ConditionalOutput.docx",
        new DataSourceInfo(order, "order"));

    System.out.println("Multiple conditions processed successfully.");
}
```

Template with elseif:

```
Order Amount: <<[order.getAmount()]:"$#,##0.00">>

<<if [order.getAmount() > 1000]>>
Discount: 10% (Large order discount)
<<elseif [order.getAmount() > 500]>>
Discount: 5% (Medium order discount)
<<else>>
Discount: No discount available
<</if>>
```

## Conditional Content with Collections

Check if collections have items:

```java
import com.groupdocs.assembly.*;
import java.util.Arrays;
import java.util.List;

public class Report
{
    private List<String> items;

    public List<String> getItems() { return items; }
    public void setItems(List<String> value) { items = value; }
}

public static void conditionalWithCollections() throws Exception
{
    Report report = new Report();
    report.setItems(Arrays.asList("Item 1", "Item 2", "Item 3"));

    DocumentAssembler assembler = new DocumentAssembler();
    assembler.assembleDocument("ConditionalTemplate.docx", "ConditionalOutput.docx",
        new DataSourceInfo(report, "report"));

    System.out.println("Conditional content with collections generated successfully.");
}
```

Template:

```
<<if [report.getItems().any()]>>
Items:
<<foreach [item in report.getItems()]>>
- <<[item]>>
<</foreach>>
<<else>>
No items available.
<</if>>
```

## Conditional Content in Data Bands

Use conditional blocks within foreach loops:

```java
import com.groupdocs.assembly.*;

public class Product
{
    private String name;
    private double price;
    private boolean inStock;

    public Product(String name, double price, boolean inStock)
    {
        this.name = name;
        this.price = price;
        this.inStock = inStock;
    }

    public String getName() { return name; }
    public double getPrice() { return price; }
    public boolean isInStock() { return inStock; }
}

public static void conditionalInDataBand() throws Exception
{
    // Pass an array (or a POJO with a typed List<Product> getter) so that the engine
    // knows the item type; a raw java.util.List passed directly loses its element type
    Product[] products = new Product[]
    {
        new Product("Laptop", 999.99, true),
        new Product("Mouse", 29.99, false),
        new Product("Keyboard", 79.99, true)
    };

    DocumentAssembler assembler = new DocumentAssembler();
    assembler.assembleDocument("ConditionalTemplate.docx", "ConditionalOutput.docx",
        new DataSourceInfo(products, "products"));

    System.out.println("Conditional content in data band generated successfully.");
}
```

Template:

```
<<foreach [in products]>>
<<[getName()]>> - <<[getPrice()]:"$#,##0.00">>
<<if [isInStock()]>>
✓ In Stock
<<else>>
✗ Out of Stock
<</if>>

<</foreach>>
```

## Complex Conditions

Use logical operators for complex conditions:

```java
import com.groupdocs.assembly.*;

public class Employee
{
    private int yearsOfService;
    private double salary;
    private String department;

    public int getYearsOfService() { return yearsOfService; }
    public void setYearsOfService(int value) { yearsOfService = value; }
    public double getSalary() { return salary; }
    public void setSalary(double value) { salary = value; }
    public String getDepartment() { return department; }
    public void setDepartment(String value) { department = value; }
}

public static void complexConditions() throws Exception
{
    Employee employee = new Employee();
    employee.setYearsOfService(5);
    employee.setSalary(75000);
    employee.setDepartment("Engineering");

    DocumentAssembler assembler = new DocumentAssembler();
    assembler.assembleDocument("ConditionalTemplate.docx", "ConditionalOutput.docx",
        new DataSourceInfo(employee, "employee"));

    System.out.println("Complex conditions processed successfully.");
}
```

Template with complex conditions:

```
<<if [employee.getYearsOfService() >= 5 && employee.getSalary() > 70000]>>
Eligible for promotion
<<elseif [employee.getDepartment() == "Engineering"]>>
Consider for technical leadership
<<else>>
Standard review process
<</if>>
```

{{< alert style="info" >}}
In template expressions, the `==` operator compares strings by value, so you do not need to call `equals()`.
{{< /alert >}}

## Conditional Formatting

Apply different formatting based on conditions:

```java
import com.groupdocs.assembly.*;

public class Invoice
{
    private double amount;
    private boolean paid;

    public double getAmount() { return amount; }
    public void setAmount(double value) { amount = value; }
    public boolean isPaid() { return paid; }
    public void setPaid(boolean value) { paid = value; }
}

public static void conditionalFormatting() throws Exception
{
    Invoice invoice = new Invoice();
    invoice.setAmount(1500.00);
    invoice.setPaid(false);

    DocumentAssembler assembler = new DocumentAssembler();
    assembler.assembleDocument("ConditionalTemplate.docx", "ConditionalOutput.docx",
        new DataSourceInfo(invoice, "invoice"));

    System.out.println("Conditional formatting applied successfully.");
}
```

Template:

```
Amount: <<[invoice.getAmount()]:"$#,##0.00">>

<<if [invoice.isPaid()]>>
Status: PAID
<<else>>
Status: UNPAID - Payment Required
<</if>>
```

## Using Methods in Conditions

Call methods that return boolean values:

```java
import com.groupdocs.assembly.*;
import java.util.Arrays;
import java.util.List;

public class OrderWithItems
{
    private List<OrderItem> items;

    public List<OrderItem> getItems() { return items; }
    public void setItems(List<OrderItem> value) { items = value; }

    public boolean hasItems()
    {
        return items != null && items.size() > 0;
    }
}

public class OrderItem
{
    private String name;

    public OrderItem(String name) { this.name = name; }

    public String getName() { return name; }
}

public static void conditionalWithMethods() throws Exception
{
    OrderWithItems order = new OrderWithItems();
    order.setItems(Arrays.asList(new OrderItem("Product")));

    DocumentAssembler assembler = new DocumentAssembler();
    assembler.assembleDocument("ConditionalTemplate.docx", "ConditionalOutput.docx",
        new DataSourceInfo(order, "order"));

    System.out.println("Conditional with methods processed successfully.");
}
```

Template:

```
<<if [order.hasItems()]>>
Order contains items.
<<else>>
Order is empty.
<</if>>
```

{{< alert style="warning" >}}
Conditional blocks must be properly closed with `<</if>>`. Nested conditional blocks are supported, but ensure proper nesting and closing of all blocks.
{{< /alert >}}

### Advanced Usage Topics

To learn more about table-row conditional blocks, conditional formatting in different document types, and advanced conditional scenarios, please refer to the [advanced usage section]({{< ref "assembly/java/developer-guide/advanced-usage/_index.md" >}}).

## More resources

### GitHub Examples

You may easily run the code above and see the feature in action in our GitHub examples:

* [GroupDocs.Assembly for Java examples, plugins, and showcase](https://github.com/groupdocs-assembly/GroupDocs.Assembly-for-Java)
* [GroupDocs.Assembly for .NET examples, plugins, and showcase](https://github.com/groupdocs-assembly/GroupDocs.Assembly-for-.NET)
* [GroupDocs.Assembly for Python via .NET examples, plugins, and showcase](https://github.com/groupdocs-assembly/GroupDocs.Assembly-for-Python-via-.NET)

### Free Online Apps

Along with the full-featured Java library, we provide simple but powerful free online apps.

To assemble documents from templates and data sources, you can use the online apps from the **[GroupDocs.Assembly App Product Family](https://products.groupdocs.app/assembly/family)**.

