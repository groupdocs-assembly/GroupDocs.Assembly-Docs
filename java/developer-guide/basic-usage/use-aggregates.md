---
id: assembly-basic-usage-aggregates-java
url: assembly/java/basic-usage-aggregates
linktitle: Use Simple Aggregates
title: Use Simple Aggregates (Sum, Count, Average)
weight: 24
description: "Calculate and display aggregate values like sums, counts, and averages from data collections in templates using GroupDocs.Assembly for Java."
keywords: aggregates, sum, count, average, totals, calculations, aggregate functions, enumeration extension methods, Java
productName: GroupDocs.Assembly for Java
hideChildren: False
---

## Overview

GroupDocs.Assembly for Java supports LINQ-like aggregate extension methods that allow you to calculate sums, counts, averages, and other aggregate values directly in templates. These functions work with collections and enable you to display totals, summaries, and statistical information in your documents.

The main aggregate functions are:
- `sum()` - calculate sum of numeric values
- `count()` - count number of items
- `average()` - calculate average of numeric values
- `min()` - find minimum value
- `max()` - find maximum value

Here are the steps to use aggregates:

* Create a template with aggregate expressions
* Use aggregate extension methods on collections
* Reference aggregate results in your template
* Assemble the document with your data

{{< alert style="info" >}}
Aggregate functions use LINQ-like syntax with lambda expressions (`i => i.getPrice()`) and work with any enumerable collection, including arrays, `java.util` collections, `DataTable` objects, and other `Iterable` implementations. See [Enumeration Extension Methods]({{< ref "assembly/java/developer-guide/advanced-usage/enumeration-extension-methods.md" >}}) for the full list of available methods.
{{< /alert >}}

## Calculate Sum

Calculate the sum of values in a collection:

```java
import com.groupdocs.assembly.*;

public class OrderItem
{
    private String productName;
    private double price;
    private int quantity;

    public OrderItem(String productName, double price, int quantity)
    {
        this.productName = productName;
        this.price = price;
        this.quantity = quantity;
    }

    public String getProductName() { return productName; }
    public double getPrice() { return price; }
    public int getQuantity() { return quantity; }
}

public static void calculateSum() throws Exception
{
    // Pass an array (or a POJO with a typed List<OrderItem> getter) so that the engine
    // knows the item type; a raw java.util.List passed directly loses its element type
    OrderItem[] items = new OrderItem[]
    {
        new OrderItem("Laptop", 999.99, 1),
        new OrderItem("Mouse", 29.99, 2),
        new OrderItem("Keyboard", 79.99, 1)
    };

    DocumentAssembler assembler = new DocumentAssembler();
    assembler.assembleDocument("AggregatesTemplate.docx", "AggregatesOutput.docx",
        new DataSourceInfo(items, "items"));

    System.out.println("Sum calculated successfully.");
}
```

## Template Example for Sum

In your template (AggregatesTemplate.docx):

```
Items:
<<foreach [in items]>>
<<[getProductName()]>> - <<[getPrice()]:"$#,##0.00">> x <<[getQuantity()]>>
<</foreach>>

Total: <<[items.sum(i => i.getPrice() * i.getQuantity())]:"$#,##0.00">>
```

## Calculate Count

Count the number of items in a collection:

```java
import com.groupdocs.assembly.*;
import java.util.Arrays;
import java.util.List;

public static void calculateCount() throws Exception
{
    List<String> products = Arrays.asList(
        "Laptop",
        "Mouse",
        "Keyboard",
        "Monitor");

    DocumentAssembler assembler = new DocumentAssembler();
    assembler.assembleDocument("AggregatesTemplate.docx", "AggregatesOutput.docx",
        new DataSourceInfo(products, "products"));

    System.out.println("Count calculated successfully.");
}
```

Template:

```
Products:
<<foreach [product in products]>>
- <<[product]>>
<</foreach>>

Total Products: <<[products.count()]>>
```

## Calculate Average

Calculate the average of numeric values:

```java
import com.groupdocs.assembly.*;

public class Sale
{
    private double amount;

    public Sale(double amount) { this.amount = amount; }

    public double getAmount() { return amount; }
}

public static void calculateAverage() throws Exception
{
    Sale[] sales = new Sale[]
    {
        new Sale(1000.00),
        new Sale(1500.00),
        new Sale(800.00),
        new Sale(1200.00)
    };

    DocumentAssembler assembler = new DocumentAssembler();
    assembler.assembleDocument("AggregatesTemplate.docx", "AggregatesOutput.docx",
        new DataSourceInfo(sales, "sales"));

    System.out.println("Average calculated successfully.");
}
```

Template:

```
Sales:
<<foreach [in sales]>>
<<[getAmount()]:"$#,##0.00">>
<</foreach>>

Average Sale: <<[sales.average(s => s.getAmount())]:"$#,##0.00">>
```

## Calculate Min and Max

Find minimum and maximum values:

```java
import com.groupdocs.assembly.*;

public static void calculateMinMax() throws Exception
{
    Sale[] sales = new Sale[]
    {
        new Sale(1000.00),
        new Sale(1500.00),
        new Sale(800.00)
    };

    DocumentAssembler assembler = new DocumentAssembler();
    assembler.assembleDocument("AggregatesTemplate.docx", "AggregatesOutput.docx",
        new DataSourceInfo(sales, "sales"));

    System.out.println("Min and max calculated successfully.");
}
```

Template:

```
Minimum Sale: <<[sales.min(s => s.getAmount())]:"$#,##0.00">>
Maximum Sale: <<[sales.max(s => s.getAmount())]:"$#,##0.00">>
```

## Multiple Aggregates

Use multiple aggregates in the same template:

```java
import com.groupdocs.assembly.*;

public static void multipleAggregates() throws Exception
{
    OrderItem[] items = new OrderItem[]
    {
        new OrderItem("Laptop", 999.99, 1),
        new OrderItem("Mouse", 29.99, 2),
        new OrderItem("Keyboard", 79.99, 1)
    };

    DocumentAssembler assembler = new DocumentAssembler();
    assembler.assembleDocument("AggregatesTemplate.docx", "AggregatesOutput.docx",
        new DataSourceInfo(items, "items"));

    System.out.println("Multiple aggregates calculated successfully.");
}
```

Template:

```
Items:
<<foreach [in items]>>
<<[getProductName()]>> - <<[getPrice()]:"$#,##0.00">> x <<[getQuantity()]>>
<</foreach>>

Summary:
Total Items: <<[items.count()]>>
Total Quantity: <<[items.sum(i => i.getQuantity())]>>
Total Amount: <<[items.sum(i => i.getPrice() * i.getQuantity())]:"$#,##0.00">>
Average Price: <<[items.average(i => i.getPrice())]:"$#,##0.00">>
```

## Aggregates with Conditions

Use aggregates with filtered data:

```java
import com.groupdocs.assembly.*;

public static void aggregatesWithConditions() throws Exception
{
    OrderItem[] items = new OrderItem[]
    {
        new OrderItem("Laptop", 999.99, 1),
        new OrderItem("Mouse", 29.99, 2),
        new OrderItem("Keyboard", 79.99, 1)
    };

    DocumentAssembler assembler = new DocumentAssembler();
    assembler.assembleDocument("AggregatesTemplate.docx", "AggregatesOutput.docx",
        new DataSourceInfo(items, "items"));

    System.out.println("Conditional aggregates calculated successfully.");
}
```

Template:

```
High-value items (Price > 100):
<<foreach [in items.where(i => i.getPrice() > 100)]>>
<<[getProductName()]>> - <<[getPrice()]:"$#,##0.00">>
<</foreach>>

Total High-value: <<[items.where(i => i.getPrice() > 100).sum(i => i.getPrice())]:"$#,##0.00">>
```

## Aggregates in Master-Detail Reports

Calculate aggregates for detail records within master records:

```java
import com.groupdocs.assembly.*;
import java.util.Arrays;
import java.util.List;

public class Order
{
    private int orderId;
    private List<OrderItem> items;

    public Order(int orderId, List<OrderItem> items)
    {
        this.orderId = orderId;
        this.items = items;
    }

    public int getOrderId() { return orderId; }
    public List<OrderItem> getItems() { return items; }
}

public static void aggregatesInMasterDetail() throws Exception
{
    Order[] orders = new Order[]
    {
        new Order(1001, Arrays.asList(
            new OrderItem("Laptop", 999.99, 1),
            new OrderItem("Mouse", 29.99, 2)))
    };

    DocumentAssembler assembler = new DocumentAssembler();
    assembler.assembleDocument("AggregatesTemplate.docx", "AggregatesOutput.docx",
        new DataSourceInfo(orders, "orders"));

    System.out.println("Master-detail aggregates calculated successfully.");
}
```

Template:

```
<<foreach [in orders]>>
Order #<<[getOrderId()]>>
Items:
<<foreach [in getItems()]>>
  <<[getProductName()]>> - <<[getPrice()]:"$#,##0.00">> x <<[getQuantity()]>>
<</foreach>>
Order Total: <<[getItems().sum(i => i.getPrice() * i.getQuantity())]:"$#,##0.00">>
<</foreach>>
```

{{< alert style="info" >}}
A `List<OrderItem>` returned by a getter keeps its item type (the engine reads the generic return type of the getter), so lambdas such as `i => i.getPrice()` work on it. A raw `java.util.List` of POJOs passed directly to `DataSourceInfo` does not keep its item type; pass an array or wrap the list in a POJO instead.
{{< /alert >}}

{{< alert style="warning" >}}
Aggregate functions require collections. Ensure your data source is a collection type (array, `java.util` collection, `DataTable`, etc.) when using aggregates.
{{< /alert >}}

### Advanced Usage Topics

To learn more about grouping, filtering with aggregates, custom aggregate functions, and performance optimization, please refer to the [advanced usage section]({{< ref "assembly/java/developer-guide/advanced-usage/_index.md" >}}).

## More resources

### GitHub Examples

You may easily run the code above and see the feature in action in our GitHub examples:

* [GroupDocs.Assembly for Java examples, plugins, and showcase](https://github.com/groupdocs-assembly/GroupDocs.Assembly-for-Java)
* [GroupDocs.Assembly for .NET examples, plugins, and showcase](https://github.com/groupdocs-assembly/GroupDocs.Assembly-for-.NET)
* [GroupDocs.Assembly for Python via .NET examples, plugins, and showcase](https://github.com/groupdocs-assembly/GroupDocs.Assembly-for-Python-via-.NET)

### Free Online Apps

Along with the full-featured Java library, we provide simple but powerful free online apps.

To assemble documents from templates and data sources, you can use the online apps from the **[GroupDocs.Assembly App Product Family](https://products.groupdocs.app/assembly/family)**.

