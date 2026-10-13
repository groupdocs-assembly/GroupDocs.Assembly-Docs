---
id: assembly-basic-usage-master-detail-java
url: assembly/java/basic-usage-master-detail
linktitle: Generate Master-Detail Reports
title: Generate Master-Detail Reports
weight: 18
description: "Create parent-child reports with nested data bands to display master records with their detail records using GroupDocs.Assembly for Java."
keywords: master detail, parent child, nested foreach, hierarchical data, orders and items, generate master detail
productName: GroupDocs.Assembly for Java
hideChildren: False
---

## Overview

Master-detail reports display hierarchical data where each master record (parent) has associated detail records (children). GroupDocs.Assembly for Java supports master-detail reports through nested foreach data bands, allowing you to display parent records with their related child records.

The main classes involved are:
- [DocumentAssembler](https://reference.groupdocs.com/assembly/java/com.groupdocs.assembly/documentassembler/) - assembles documents
- [DataSourceInfo](https://reference.groupdocs.com/assembly/java/com.groupdocs.assembly/datasourceinfo/) - wraps data sources

Here are the steps to generate master-detail reports:

* Define data structures with parent-child relationships
* Create a template with nested foreach data bands
* Outer foreach iterates over master records
* Inner foreach iterates over detail records for each master
* Assemble the document with your hierarchical data

{{< alert style="info" >}}
Nested foreach data bands allow you to create complex hierarchical reports. The outer band processes master records, while inner bands process related detail records.
{{< /alert >}}

## Define Master-Detail Data Structure

Start by defining classes with parent-child relationships:

```java
import java.util.Date;
import java.util.List;

public class Order
{
    private final int orderId;
    private final Date orderDate;
    private final String customerName;
    private final List<OrderItem> items;

    public Order(int orderId, Date orderDate, String customerName, List<OrderItem> items)
    {
        this.orderId = orderId;
        this.orderDate = orderDate;
        this.customerName = customerName;
        this.items = items;
    }

    public Order(int orderId, String customerName, List<OrderItem> items)
    {
        this(orderId, null, customerName, items);
    }

    public int getOrderId() { return orderId; }
    public Date getOrderDate() { return orderDate; }
    public String getCustomerName() { return customerName; }
    public List<OrderItem> getItems() { return items; }
}

public class OrderItem
{
    private final String productName;
    private final int quantity;
    private final double price;

    public OrderItem(String productName, int quantity, double price)
    {
        this.productName = productName;
        this.quantity = quantity;
        this.price = price;
    }

    public String getProductName() { return productName; }
    public int getQuantity() { return quantity; }
    public double getPrice() { return price; }
}
```

{{< alert style="info" >}}
Because of Java type erasure, the engine cannot determine the item type of a `java.util.List` passed directly as a data source. That is why the master records are passed as an array (`Order[]`) below. Detail collections returned by getters such as `List<OrderItem> getItems()` work fine, because the engine reads the item type from the getter's declared return type.
{{< /alert >}}

## Generate Master-Detail Report

Create a master-detail report from hierarchical data:

```java
import com.groupdocs.assembly.*;
import java.util.*;
import java.util.Date;

public static void generateMasterDetailReport() throws Exception
{
    // Create sample data with master-detail relationship
    Order[] orders =
    {
        new Order(
            1001,
            new GregorianCalendar(2024, Calendar.JANUARY, 15).getTime(),
            "John Doe",
            Arrays.asList(
                new OrderItem("Laptop", 1, 999.99),
                new OrderItem("Mouse", 2, 29.99)
            )),
        new Order(
            1002,
            new GregorianCalendar(2024, Calendar.JANUARY, 16).getTime(),
            "Jane Smith",
            Arrays.asList(
                new OrderItem("Keyboard", 1, 79.99)
            ))
    };

    // Assemble document
    DocumentAssembler assembler = new DocumentAssembler();
    assembler.assembleDocument("MasterDetailTemplate.docx", "MasterDetailOutput.docx",
        new DataSourceInfo(orders, "orders"));

    System.out.println("Master-detail report generated successfully.");
}
```

## Template Structure for Master-Detail

In your template (MasterDetailTemplate.docx), use nested foreach data bands:

```
<<foreach [in orders]>>Order #<<[getOrderId()]>>
Date: <<[getOrderDate()]:"yyyy-MM-dd">>
Customer: <<[getCustomerName()]>>

Items:
<<foreach [in getItems()]>>  - <<[getProductName()]>> (Qty: <<[getQuantity()]>>, Price: <<[getPrice()]:"$#,##0.00">>)
<</foreach>>
Total: <<[getItems().sum(i => i.getPrice() * i.getQuantity())]:"$#,##0.00">>

<</foreach>>
```

Members of Java objects are accessed through their getter methods. Date format strings follow the `java.text.SimpleDateFormat` pattern syntax, and number format strings follow the `java.text.DecimalFormat` pattern syntax (decimal and grouping separators depend on the current locale). After assembly, you'll get:

```
Order #1001
Date: 2024-01-15
Customer: John Doe

Items:
  - Laptop (Qty: 1, Price: $999.99)
  - Mouse (Qty: 2, Price: $29.99)

Total: $1,059.97

Order #1002
Date: 2024-01-16
Customer: Jane Smith

Items:
  - Keyboard (Qty: 1, Price: $79.99)

Total: $79.99
```

## Master-Detail in Tables

You can also create master-detail reports in table format:

```java
import com.groupdocs.assembly.*;
import java.util.*;

public static void generateMasterDetailTable() throws Exception
{
    Order[] orders =
    {
        new Order(
            1001,
            "John Doe",
            Arrays.asList(
                new OrderItem("Laptop", 1, 999.99),
                new OrderItem("Mouse", 2, 29.99)
            ))
    };

    DocumentAssembler assembler = new DocumentAssembler();
    assembler.assembleDocument("MasterDetailTableTemplate.docx", "MasterDetailTableOutput.docx",
        new DataSourceInfo(orders, "orders"));

    System.out.println("Master-detail table generated successfully.");
}
```

Template table structure:

| Order ID | Customer | Product | Quantity | Price |
|----------|----------|---------|----------|-------|
| `<<foreach [in orders]>><<[getOrderId()]>>` | `<<[getCustomerName()]>>` | | | |
| `<<foreach [in getItems()]>>` | | `<<[getProductName()]>>` | `<<[getQuantity()]>>` | `<<[getPrice()]:"$#,##0.00">><</foreach>><</foreach>>` |

The outer table-row data band spans both rows: it starts at the beginning of the first cell of the master row and ends at the end of the last cell of the detail row. The inner data band covers the detail row only, so it is repeated for each order item.

## Using Aggregates in Master-Detail

Calculate totals and aggregates for each master record:

```java
import com.groupdocs.assembly.*;
import java.util.*;

public static void generateMasterDetailWithAggregates() throws Exception
{
    Order[] orders =
    {
        new Order(
            1001,
            "John Doe",
            Arrays.asList(
                new OrderItem("Laptop", 1, 999.99),
                new OrderItem("Mouse", 2, 29.99)
            ))
    };

    DocumentAssembler assembler = new DocumentAssembler();
    assembler.assembleDocument("MasterDetailAggregatesTemplate.docx", "MasterDetailAggregatesOutput.docx",
        new DataSourceInfo(orders, "orders"));

    System.out.println("Master-detail report with aggregates generated successfully.");
}
```

Template with aggregates (MasterDetailAggregatesTemplate.docx):

```
<<foreach [in orders]>>Order #<<[getOrderId()]>> - <<[getCustomerName()]>>

Items:
<<foreach [in getItems()]>>  <<[getProductName()]>> - <<[getQuantity()]>> x <<[getPrice()]:"$#,##0.00">> = <<[getQuantity() * getPrice()]:"$#,##0.00">>
<</foreach>>
Subtotal: <<[getItems().sum(i => i.getPrice() * i.getQuantity())]:"$#,##0.00">>
Item Count: <<[getItems().count()]>>
<</foreach>>
```

{{< alert style="warning" >}}
When using nested foreach data bands, ensure proper closing tags. Each opening `<<foreach>>` tag must have a corresponding closing `<</foreach>>` tag.
{{< /alert >}}

### Advanced Usage Topics

To learn more about complex hierarchical structures, multiple levels of nesting, and advanced master-detail patterns, please refer to the [advanced usage section]({{< ref "assembly/java/developer-guide/advanced-usage/_index.md" >}}).

## More resources

### GitHub Examples

You may easily run the code above and see the feature in action in our GitHub examples:

* [GroupDocs.Assembly for Java examples, plugins, and showcase](https://github.com/groupdocs-assembly/GroupDocs.Assembly-for-Java)
* [GroupDocs.Assembly for .NET examples, plugins, and showcase](https://github.com/groupdocs-assembly/GroupDocs.Assembly-for-.NET)
* [GroupDocs.Assembly for Python via .NET examples, plugins, and showcase](https://github.com/groupdocs-assembly/GroupDocs.Assembly-for-Python-via-.NET)

### Free Online Apps

Along with the full-featured Java library, we provide simple but powerful free online apps.

To assemble documents from templates and data sources, you can use the online apps from the **[GroupDocs.Assembly App Product Family](https://products.groupdocs.app/assembly/family)**.
