---
id: assembly-basic-usage-custom-objects-java
url: assembly/java/basic-usage-custom-objects
linktitle: Generate from Custom Objects
title: Generate Document from Custom Java Objects
weight: 6
description: "Generate documents by binding data from custom Java classes and objects to template documents."
keywords: custom objects, Java classes, POJO, getters, data binding, Java objects, assemble document, generate from objects
productName: GroupDocs.Assembly for Java
hideChildren: False
---

## Overview

One of the most common scenarios in document assembly is generating reports from custom Java objects. GroupDocs.Assembly for Java makes it easy to bind your business objects directly to templates, allowing you to create type-safe, maintainable document generation code.

The main classes involved are:
- [DocumentAssembler](https://reference.groupdocs.com/assembly/java/com.groupdocs.assembly/documentassembler/) - assembles documents from templates
- [DataSourceInfo](https://reference.groupdocs.com/assembly/java/com.groupdocs.assembly/datasourceinfo/) - wraps data source objects

Here are the steps to generate documents from custom objects:

* Define your custom public Java class with public getters
* Create an instance of the class and populate it with data
* Create a template document with expression tags calling the object's getters
* Use DocumentAssembler to assemble the template with your object
* Save the assembled document

{{< alert style="info" >}}
Custom classes must be public, and their members must be public methods (such as getters) or public fields to be accessible in templates. Methods are called in templates explicitly, for example `customer.getName()`. Private members are not accessible by the template engine.
{{< /alert >}}

## Define a Custom Class

Start by defining a class with getters you want to use in your template:

```java
import java.util.Date;

public class Customer
{
    private String name;
    private String email;
    private String address;
    private Date registrationDate;
    private double balance;

    public Customer()
    {
    }

    public Customer(String name, String email, double balance)
    {
        this.name = name;
        this.email = email;
        this.balance = balance;
    }

    public String getName() { return name; }
    public void setName(String value) { this.name = value; }
    public String getEmail() { return email; }
    public void setEmail(String value) { this.email = value; }
    public String getAddress() { return address; }
    public void setAddress(String value) { this.address = value; }
    public Date getRegistrationDate() { return registrationDate; }
    public void setRegistrationDate(Date value) { this.registrationDate = value; }
    public double getBalance() { return balance; }
    public void setBalance(double value) { this.balance = value; }
}
```

## Generate Document from Single Object

Generate a document from a single object instance:

```java
import com.groupdocs.assembly.*;
import java.util.*;

public static void generateFromSingleObject() throws Exception
{
    // Create and populate object
    Customer customer = new Customer();
    customer.setName("John Doe");
    customer.setEmail("john.doe@example.com");
    customer.setAddress("123 Main St, New York, NY 10001");
    customer.setRegistrationDate(new GregorianCalendar(2023, Calendar.JANUARY, 15).getTime());
    customer.setBalance(1250.75);

    // Assemble document
    DocumentAssembler assembler = new DocumentAssembler();
    assembler.assembleDocument("CustomerTemplate.docx", "CustomerReport.docx",
        new DataSourceInfo(customer, "customer"));

    System.out.println("Document generated from custom object successfully.");
}
```

## Template Example

Your template (CustomerTemplate.docx) can call object getters:

```
Customer Information

Name: <<[customer.getName()]>>
Email: <<[customer.getEmail()]>>
Address: <<[customer.getAddress()]>>
Registration Date: <<[customer.getRegistrationDate()]:"yyyy-MM-dd">>
Balance: <<[customer.getBalance()]:"$#,##0.00">>
```

{{< alert style="info" >}}
Format strings follow Java conventions: `java.text.SimpleDateFormat` patterns for dates and `java.text.DecimalFormat` patterns for numbers.
{{< /alert >}}

## Generate Document from Object Collection

You can also generate documents from collections of objects:

```java
import com.groupdocs.assembly.*;

public static void generateFromCollection() throws Exception
{
    // Create collection of objects
    Customer[] customers = new Customer[]
    {
        new Customer("John Doe", "john@example.com", 1000),
        new Customer("Jane Smith", "jane@example.com", 2500),
        new Customer("Bob Johnson", "bob@example.com", 750)
    };

    DocumentAssembler assembler = new DocumentAssembler();
    assembler.assembleDocument("CustomersTemplate.docx", "CustomersReport.docx",
        new DataSourceInfo(customers, "customers"));

    System.out.println("Document generated from collection successfully.");
}
```

Template for collection (using data band):

```
Customers List:

<<foreach [in customers]>>
<<[getName()]>> - <<[getEmail()]>> - Balance: <<[getBalance()]:"$#,##0.00">>
<</foreach>>
```

{{< alert style="info" >}}
Because of Java type erasure, the engine cannot determine the item type of a `java.util.List` passed directly as a data source, so calling item methods such as `getName()` fails. Pass an array (as shown above), or expose the list through a getter of a wrapper object (for example, `public List<Customer> getCustomers()`) and iterate over it in the template: `<<foreach [in data.getCustomers()]>>`.
{{< /alert >}}

## Using Nested Objects

Custom objects can contain nested objects:

```java
import com.groupdocs.assembly.*;
import java.util.Date;

public class Order
{
    private int orderId;
    private Date orderDate;
    private Customer customer;
    private double totalAmount;

    public int getOrderId() { return orderId; }
    public void setOrderId(int value) { this.orderId = value; }
    public Date getOrderDate() { return orderDate; }
    public void setOrderDate(Date value) { this.orderDate = value; }
    public Customer getCustomer() { return customer; }
    public void setCustomer(Customer value) { this.customer = value; }
    public double getTotalAmount() { return totalAmount; }
    public void setTotalAmount(double value) { this.totalAmount = value; }
}

public static void generateFromNestedObjects() throws Exception
{
    Customer customer = new Customer();
    customer.setName("John Doe");
    customer.setEmail("john@example.com");

    Order order = new Order();
    order.setOrderId(1001);
    order.setOrderDate(new Date());
    order.setCustomer(customer);
    order.setTotalAmount(599.99);

    DocumentAssembler assembler = new DocumentAssembler();
    assembler.assembleDocument("OrderTemplate.docx", "OrderReport.docx",
        new DataSourceInfo(order, "order"));

    System.out.println("Document generated from nested objects successfully.");
}
```

Template with nested object access:

```
Order #<<[order.getOrderId()]>>
Date: <<[order.getOrderDate()]:"yyyy-MM-dd">>

Customer:
Name: <<[order.getCustomer().getName()]>>
Email: <<[order.getCustomer().getEmail()]>>

Total: <<[order.getTotalAmount()]:"$#,##0.00">>
```

## Using Object Methods

You can call methods on objects in templates:

```java
import com.groupdocs.assembly.*;

public class Product
{
    private String name;
    private double price;
    private int quantity;

    public String getName() { return name; }
    public void setName(String value) { this.name = value; }
    public double getPrice() { return price; }
    public void setPrice(double value) { this.price = value; }
    public int getQuantity() { return quantity; }
    public void setQuantity(int value) { this.quantity = value; }

    public double getTotal()
    {
        return price * quantity;
    }
}

public static void generateWithMethods() throws Exception
{
    Product product = new Product();
    product.setName("Laptop");
    product.setPrice(999.99);
    product.setQuantity(2);

    DocumentAssembler assembler = new DocumentAssembler();
    assembler.assembleDocument("ProductTemplate.docx", "ProductReport.docx",
        new DataSourceInfo(product, "product"));

    System.out.println("Document generated with method calls successfully.");
}
```

Template using method:

```
Product: <<[product.getName()]>>
Price: <<[product.getPrice()]:"$#,##0.00">>
Quantity: <<[product.getQuantity()]>>
Total: <<[product.getTotal()]:"$#,##0.00">>
```

{{< alert style="warning" >}}
Methods called in templates must be public and should not have side effects. The template engine may call methods multiple times during document assembly.
{{< /alert >}}

### Advanced Usage Topics

To learn more about working with complex object hierarchies, collections, collection extension methods on objects, and performance optimization, please refer to the [advanced usage section]({{< ref "assembly/java/developer-guide/advanced-usage/_index.md" >}}).

## More resources

### GitHub Examples

You may easily run the code above and see the feature in action in our GitHub examples:

* [GroupDocs.Assembly for Java examples, plugins, and showcase](https://github.com/groupdocs-assembly/GroupDocs.Assembly-for-Java)
* [GroupDocs.Assembly for .NET examples, plugins, and showcase](https://github.com/groupdocs-assembly/GroupDocs.Assembly-for-.NET)
* [GroupDocs.Assembly for Python via .NET examples, plugins, and showcase](https://github.com/groupdocs-assembly/GroupDocs.Assembly-for-Python-via-.NET)

### Free Online Apps

Along with the full-featured Java library, we provide simple but powerful free online apps.

To assemble documents from templates and data sources, you can use the online apps from the **[GroupDocs.Assembly App Product Family](https://products.groupdocs.app/assembly/family)**.
