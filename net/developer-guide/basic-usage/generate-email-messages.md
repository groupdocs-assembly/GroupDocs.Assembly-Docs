---
id: assembly-basic-usage-generate-emails
url: assembly/net/basic-usage-generate-emails
linktitle: Generate Email Messages
title: Generate Email Messages from Data
weight: 29
description: "Create email messages with dynamic subject, body, and recipients from data sources using templates."
keywords: generate emails, email messages, email subject, email body, email recipients, MSG, EML, compose emails
productName: GroupDocs.Assembly for .NET
hideChildren: False
---

## Overview

GroupDocs.Assembly for .NET enables you to generate email messages dynamically from templates. You can set email attributes like subject, body, and recipients (To, CC, BCC) using template syntax, making it easy to create personalized email messages from data sources.

The main classes involved are:
- [DocumentAssembler](https://reference.groupdocs.com/assembly/net/groupdocs.assembly/documentassembler/) - assembles email messages
- [DataSourceInfo](https://reference.groupdocs.com/assembly/net/groupdocs.assembly/datasourceinfo/) - wraps data sources

Here are the steps to generate email messages:

* Create an email template (MSG or EML format)
* Set email attributes (subject, To, CC, BCC) using template syntax
* Create email body content with data binding
* Assemble the email message with your data source
* Save the assembled email

{{< alert style="info" >}}
Email templates support the same template syntax as Word documents, including expression tags, data bands, conditional blocks, and formatting.
{{< /alert >}}

## Generate Email with Subject and Body

Create a simple email with dynamic subject and body:

```csharp
using GroupDocs.Assembly;

public class EmailData
{
    public string Recipient { get; set; }
    public string Subject { get; set; }
    public string CustomerName { get; set; }
    public decimal InvoiceAmount { get; set; }
}

public static void GenerateEmail()
{
    var emailData = new EmailData
    {
        Recipient = "customer@example.com",
        Subject = "Invoice #1001",
        CustomerName = "John Doe",
        InvoiceAmount = 1500.00m
    };
    
    DocumentAssembler assembler = new DocumentAssembler();
    assembler.AssembleDocument("EmailTemplate.msg", "EmailOutput.msg", 
        new DataSourceInfo(emailData, "email"));
    
    Console.WriteLine("Email generated successfully.");
}
```

## Email Template Structure

In your email template (EmailTemplate.msg), set attributes and body:

**Subject field:**
```
<<[email.Subject]>>
```

**To field:**
```
<<[email.Recipient]>>
```

**Body:**
```
Dear <<[email.CustomerName]>>,

Please find your invoice below:

Amount: <<[email.InvoiceAmount]:"C">>

Thank you for your business.
```

## Generate Email with Multiple Recipients

Set multiple recipients using foreach:

```csharp
using GroupDocs.Assembly;
using System.Collections.Generic;

public class EmailData
{
    public List<string> Recipients { get; set; }
    public string Subject { get; set; }
    public string Message { get; set; }
}

public static void GenerateEmailWithMultipleRecipients()
{
    var emailData = new EmailData
    {
        Recipients = new List<string> 
        { 
            "recipient1@example.com", 
            "recipient2@example.com" 
        },
        Subject = "Important Update",
        Message = "This is an important message for all recipients."
    };
    
    DocumentAssembler assembler = new DocumentAssembler();
    assembler.AssembleDocument("EmailTemplate.msg", "EmailOutput.msg", 
        new DataSourceInfo(emailData, "email"));
    
    Console.WriteLine("Email with multiple recipients generated successfully.");
}
```

Template for multiple recipients:

**To field:**
```
<<foreach [r in email.Recipients]>><<[r]>>; <</foreach>>
```

**Body:**
```
<<[email.Message]>>
```

## Generate Email with CC and BCC

Set CC and BCC recipients:

```csharp
using GroupDocs.Assembly;

public class EmailData
{
    public string To { get; set; }
    public string Cc { get; set; }
    public string Bcc { get; set; }
    public string Subject { get; set; }
    public string Body { get; set; }
}

public static void GenerateEmailWithCcBcc()
{
    var emailData = new EmailData
    {
        To = "customer@example.com",
        Cc = "manager@example.com",
        Bcc = "archive@example.com",
        Subject = "Invoice",
        Body = "Please find attached invoice."
    };
    
    DocumentAssembler assembler = new DocumentAssembler();
    assembler.AssembleDocument("EmailTemplate.msg", "EmailOutput.msg", 
        new DataSourceInfo(emailData, "email"));
    
    Console.WriteLine("Email with CC and BCC generated successfully.");
}
```

Template:

**To field:**
```
<<[email.To]>>
```

**CC field:**
```
<<[email.Cc]>>
```

**BCC field:**
```
<<[email.Bcc]>>
```

**Body:**
```
<<[email.Body]>>
```

## Generate Email with Rich Content

Create emails with tables, lists, and formatted content:

```csharp
using GroupDocs.Assembly;
using System.Collections.Generic;

public class OrderEmail
{
    public string CustomerName { get; set; }
    public string Subject { get; set; }
    public List<OrderItem> Items { get; set; }
}

public class OrderItem
{
    public string ProductName { get; set; }
    public decimal Price { get; set; }
}

public static void GenerateRichEmail()
{
    var orderEmail = new OrderEmail
    {
        CustomerName = "John Doe",
        Subject = "Order Confirmation",
        Items = new List<OrderItem>
        {
            new OrderItem { ProductName = "Laptop", Price = 999.99m },
            new OrderItem { ProductName = "Mouse", Price = 29.99m }
        }
    };
    
    DocumentAssembler assembler = new DocumentAssembler();
    assembler.AssembleDocument("EmailTemplate.msg", "EmailOutput.msg", 
        new DataSourceInfo(orderEmail, "order"));
    
    Console.WriteLine("Rich email generated successfully.");
}
```

Template body:

```
Dear <<[order.CustomerName]>>,

Thank you for your order. Here are your items:

<<foreach [in order.Items]>>
• <<[ProductName]>> - <<[Price]:"C">>
<</foreach>>

Total: <<[order.Items.Sum(i => i.Price)]:"C">>
```

## Generate Email from Collection

Generate multiple emails from a collection:

```csharp
using GroupDocs.Assembly;
using System.Collections.Generic;

public class CustomerEmail
{
    public string Email { get; set; }
    public string Name { get; set; }
    public string Subject { get; set; }
}

public static void GenerateEmailsFromCollection()
{
    List<CustomerEmail> customers = new List<CustomerEmail>
    {
        new CustomerEmail 
        { 
            Email = "customer1@example.com", 
            Name = "John Doe",
            Subject = "Personalized Message"
        },
        new CustomerEmail 
        { 
            Email = "customer2@example.com", 
            Name = "Jane Smith",
            Subject = "Personalized Message"
        }
    };
    
    // Generate email for each customer
    DocumentAssembler assembler = new DocumentAssembler();
    foreach (var customer in customers)
    {
        string outputPath = $"Email_{customer.Name.Replace(" ", "_")}.msg";
        assembler.AssembleDocument("EmailTemplate.msg", outputPath, 
            new DataSourceInfo(customer, "customer"));
    }
    
    Console.WriteLine("Emails generated from collection successfully.");
}
```

## Set Email From Address

Set the sender (From) address:

```csharp
using GroupDocs.Assembly;

public class EmailData
{
    public string From { get; set; }
    public string To { get; set; }
    public string Subject { get; set; }
}

public static void GenerateEmailWithFrom()
{
    var emailData = new EmailData
    {
        From = "sender@example.com",
        To = "recipient@example.com",
        Subject = "Test Email"
    };
    
    DocumentAssembler assembler = new DocumentAssembler();
    assembler.AssembleDocument("EmailTemplate.msg", "EmailOutput.msg", 
        new DataSourceInfo(emailData, "email"));
    
    Console.WriteLine("Email with From address generated successfully.");
}
```

Template:

**From field:**
```
<<[email.From]>>
```

{{< alert style="warning" >}}
Email templates must be in MSG or EML format. The template structure depends on the email client used to create it. Ensure proper formatting for HTML or RTF email bodies.
{{< /alert >}}

### Advanced Usage Topics

To learn more about email attachments, HTML email bodies, email headers, and advanced email generation scenarios, please refer to the [advanced usage section]({{< ref "assembly/net/developer-guide/advanced-usage/_index.md" >}}).

## More resources

### GitHub Examples

You may easily run the code above and see the feature in action in our GitHub examples:

* [GroupDocs.Assembly for .NET examples, plugins, and showcase](https://github.com/groupdocs-assembly/GroupDocs.Assembly-for-.NET)
* [GroupDocs.Assembly for Java examples, plugins, and showcase](https://github.com/groupdocs-assembly/GroupDocs.Assembly-for-Java)
* [GroupDocs.Assembly for Python via .NET examples, plugins, and showcase](https://github.com/groupdocs-assembly/GroupDocs.Assembly-for-Python-via-.NET)

### Free Online Apps

Along with the full-featured .NET library, we provide simple but powerful free online apps.

To assemble documents from templates and data sources, you can use the online apps from the **[GroupDocs.Assembly App Product Family](https://products.groupdocs.app/assembly/family)**.

