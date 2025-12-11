---
id: assembly-basic-usage-custom-objects
url: assembly/net/basic-usage-custom-objects
title: Generate Document from Custom .NET Objects in C#
weight: 6
description: "Generate documents by binding data from custom .NET classes and objects to template documents."
keywords: custom objects, .NET classes, object properties, data binding, C# objects, assemble document, generate from objects
productName: GroupDocs.Assembly for .NET
toc: True
---

## Overview

One of the most common scenarios in document assembly is generating reports from custom .NET objects. GroupDocs.Assembly for .NET makes it easy to bind your business objects directly to templates, allowing you to create type-safe, maintainable document generation code.

The main classes involved are:
- [DocumentAssembler](https://reference.groupdocs.com/assembly/net/groupdocs.assembly/documentassembler/) - assembles documents from templates
- [DataSourceInfo](https://reference.groupdocs.com/assembly/net/groupdocs.assembly/datasourceinfo/) - wraps data source objects

Here are the steps to generate documents from custom objects:

* Define your custom .NET class with public properties
* Create an instance of the class and populate it with data
* Create a template document with expression tags referencing object properties
* Use DocumentAssembler to assemble the template with your object
* Save the assembled document

{{< alert style="info" >}}
Custom objects must have public properties or fields to be accessible in templates. Private members are not accessible by the template engine.
{{< /alert >}}

## Define a Custom Class

Start by defining a class with properties you want to use in your template:

```csharp
public class Customer
{
    public string Name { get; set; }
    public string Email { get; set; }
    public string Address { get; set; }
    public DateTime RegistrationDate { get; set; }
    public decimal Balance { get; set; }
}
```

## Generate Document from Single Object

Generate a document from a single object instance:

```csharp
using GroupDocs.Assembly;

public static void GenerateFromSingleObject()
{
    // Create and populate object
    Customer customer = new Customer
    {
        Name = "John Doe",
        Email = "john.doe@example.com",
        Address = "123 Main St, New York, NY 10001",
        RegistrationDate = new DateTime(2023, 1, 15),
        Balance = 1250.75m
    };
    
    // Assemble document
    DocumentAssembler assembler = new DocumentAssembler();
    assembler.AssembleDocument("CustomerTemplate.docx", "CustomerReport.docx", 
        new DataSourceInfo(customer, "customer"));
    
    Console.WriteLine("Document generated from custom object successfully.");
}
```

## Template Example

Your template (CustomerTemplate.docx) can reference object properties:

```
Customer Information

Name: <<[customer.Name]>>
Email: <<[customer.Email]>>
Address: <<[customer.Address]>>
Registration Date: <<[customer.RegistrationDate]:"yyyy-MM-dd">>
Balance: <<[customer.Balance]:"C">>
```

## Generate Document from Object Collection

You can also generate documents from collections of objects:

```csharp
using GroupDocs.Assembly;
using System.Collections.Generic;

public static void GenerateFromCollection()
{
    // Create collection of objects
    List<Customer> customers = new List<Customer>
    {
        new Customer { Name = "John Doe", Email = "john@example.com", Balance = 1000m },
        new Customer { Name = "Jane Smith", Email = "jane@example.com", Balance = 2500m },
        new Customer { Name = "Bob Johnson", Email = "bob@example.com", Balance = 750m }
    };
    
    DocumentAssembler assembler = new DocumentAssembler();
    assembler.AssembleDocument("CustomersTemplate.docx", "CustomersReport.docx", 
        new DataSourceInfo(customers, "customers"));
    
    Console.WriteLine("Document generated from collection successfully.");
}
```

Template for collection (using data band):

```
Customers List:

<<foreach [in customers]>>
<<[Name]>> - <<[Email]>> - Balance: <<[Balance]:"C">>
<</foreach>>
```

## Using Nested Objects

Custom objects can contain nested objects:

```csharp
public class Order
{
    public int OrderId { get; set; }
    public DateTime OrderDate { get; set; }
    public Customer Customer { get; set; }
    public decimal TotalAmount { get; set; }
}

public static void GenerateFromNestedObjects()
{
    Order order = new Order
    {
        OrderId = 1001,
        OrderDate = DateTime.Now,
        Customer = new Customer 
        { 
            Name = "John Doe", 
            Email = "john@example.com" 
        },
        TotalAmount = 599.99m
    };
    
    DocumentAssembler assembler = new DocumentAssembler();
    assembler.AssembleDocument("OrderTemplate.docx", "OrderReport.docx", 
        new DataSourceInfo(order, "order"));
    
    Console.WriteLine("Document generated from nested objects successfully.");
}
```

Template with nested object access:

```
Order #<<[order.OrderId]>>
Date: <<[order.OrderDate]:"yyyy-MM-dd">>

Customer:
Name: <<[order.Customer.Name]>>
Email: <<[order.Customer.Email]>>

Total: <<[order.TotalAmount]:"C">>
```

## Using Object Methods

You can call methods on objects in templates:

```csharp
public class Product
{
    public string Name { get; set; }
    public decimal Price { get; set; }
    public int Quantity { get; set; }
    
    public decimal GetTotal()
    {
        return Price * Quantity;
    }
}

public static void GenerateWithMethods()
{
    Product product = new Product
    {
        Name = "Laptop",
        Price = 999.99m,
        Quantity = 2
    };
    
    DocumentAssembler assembler = new DocumentAssembler();
    assembler.AssembleDocument("ProductTemplate.docx", "ProductReport.docx", 
        new DataSourceInfo(product, "product"));
    
    Console.WriteLine("Document generated with method calls successfully.");
}
```

Template using method:

```
Product: <<[product.Name]>>
Price: <<[product.Price]:"C">>
Quantity: <<[product.Quantity]>>
Total: <<[product.GetTotal()]:"C">>
```

{{< alert style="warning" >}}
Methods called in templates must be public and should not have side effects. The template engine may call methods multiple times during document assembly.
{{< /alert >}}

### Advanced Usage Topics

To learn more about working with complex object hierarchies, collections, LINQ queries on objects, and performance optimization, please refer to the [advanced usage section]({{< ref "assembly/net/developer-guide/advanced-usage/_index.md" >}}).

## More resources

### GitHub Examples

You may easily run the code above and see the feature in action in our GitHub examples:

* [GroupDocs.Assembly for .NET examples, plugins, and showcase](https://github.com/groupdocs-assembly/GroupDocs.Assembly-for-.NET)
* [GroupDocs.Assembly for Java examples, plugins, and showcase](https://github.com/groupdocs-assembly/GroupDocs.Assembly-for-Java)
* [GroupDocs.Assembly for Python via .NET examples, plugins, and showcase](https://github.com/groupdocs-assembly/GroupDocs.Assembly-for-Python-via-.NET)

### Free Online Apps

Along with the full-featured .NET library, we provide simple but powerful free online apps.

To assemble documents from templates and data sources, you can use the online apps from the **[GroupDocs.Assembly App Product Family](https://products.groupdocs.app/assembly/family)**.

