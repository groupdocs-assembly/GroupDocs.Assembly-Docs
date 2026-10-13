---
id: assembly-basic-usage-generate-emails-java
url: assembly/java/basic-usage-generate-emails
linktitle: Generate Email Messages
title: Generate Email Messages from Data
weight: 29
description: "Create email messages with dynamic subject, body, and recipients from data sources using templates in GroupDocs.Assembly for Java."
keywords: generate emails, email messages, email subject, email body, email recipients, MSG, EML, EMLX, MHTML, compose emails, Java
productName: GroupDocs.Assembly for Java
hideChildren: False
---

## Overview

GroupDocs.Assembly for Java enables you to generate email messages dynamically from templates. You can set email attributes like subject, body, and recipients (To, CC, BCC) using template syntax, making it easy to create personalized email messages from data sources.

The main classes involved are:
- [DocumentAssembler](https://reference.groupdocs.com/assembly/java/com.groupdocs.assembly/documentassembler/) - assembles email messages
- [DataSourceInfo](https://reference.groupdocs.com/assembly/java/com.groupdocs.assembly/datasourceinfo/) - wraps data sources

Here are the steps to generate email messages:

* Create an email template (MSG, EML, EMLX, or MHTML format)
* Set email attributes (subject, From, To, CC, BCC) using template syntax
* Create email body content with data binding
* Assemble the email message with your data source
* Save the assembled email

{{< alert style="info" >}}
Email templates support the same template syntax as Word documents, including expression tags, data bands, conditional blocks, and formatting.
{{< /alert >}}

## Generate Email with Subject and Body

Create a simple email with dynamic subject and body:

```java
import com.groupdocs.assembly.*;

public class EmailData
{
    private String recipient;
    private String subject;
    private String customerName;
    private double invoiceAmount;

    public String getRecipient() { return recipient; }
    public void setRecipient(String value) { this.recipient = value; }
    public String getSubject() { return subject; }
    public void setSubject(String value) { this.subject = value; }
    public String getCustomerName() { return customerName; }
    public void setCustomerName(String value) { this.customerName = value; }
    public double getInvoiceAmount() { return invoiceAmount; }
    public void setInvoiceAmount(double value) { this.invoiceAmount = value; }
}

public static void generateEmail() throws Exception
{
    EmailData emailData = new EmailData();
    emailData.setRecipient("customer@example.com");
    emailData.setSubject("Invoice #1001");
    emailData.setCustomerName("John Doe");
    emailData.setInvoiceAmount(1500.00);

    DocumentAssembler assembler = new DocumentAssembler();
    assembler.assembleDocument("EmailTemplate.msg", "EmailOutput.msg",
        new DataSourceInfo(emailData, "email"));

    System.out.println("Email generated successfully.");
}
```

## Email Template Structure

In your email template (EmailTemplate.msg), set attributes and body:

**Subject field:**
```
<<[email.getSubject()]>>
```

**To field:**
```
<<[email.getRecipient()]>>
```

**Body:**
```
Dear <<[email.getCustomerName()]>>,

Please find your invoice below:

Amount: <<[email.getInvoiceAmount()]:"$#,##0.00">>

Thank you for your business.
```

{{< alert style="info" >}}
Number and date format strings follow Java conventions (`java.text.DecimalFormat` and `java.text.SimpleDateFormat` patterns). The .NET-specific `"C"` currency format is not supported; use a pattern such as `"$#,##0.00"` instead.
{{< /alert >}}

## Generate Email with Multiple Recipients

Set multiple recipients using foreach:

```java
import com.groupdocs.assembly.*;
import java.util.*;

public class MultiRecipientEmailData
{
    private List<String> recipients;
    private String subject;
    private String message;

    public List<String> getRecipients() { return recipients; }
    public void setRecipients(List<String> value) { this.recipients = value; }
    public String getSubject() { return subject; }
    public void setSubject(String value) { this.subject = value; }
    public String getMessage() { return message; }
    public void setMessage(String value) { this.message = value; }
}

public static void generateEmailWithMultipleRecipients() throws Exception
{
    MultiRecipientEmailData emailData = new MultiRecipientEmailData();
    emailData.setRecipients(Arrays.asList(
        "recipient1@example.com",
        "recipient2@example.com"));
    emailData.setSubject("Important Update");
    emailData.setMessage("This is an important message for all recipients.");

    DocumentAssembler assembler = new DocumentAssembler();
    assembler.assembleDocument("EmailTemplate.msg", "EmailOutput.msg",
        new DataSourceInfo(emailData, "email"));

    System.out.println("Email with multiple recipients generated successfully.");
}
```

Template for multiple recipients:

**To field:**
```
<<foreach [r in email.getRecipients()]>><<[r]>>; <</foreach>>
```

**Body:**
```
<<[email.getMessage()]>>
```

## Generate Email with CC and BCC

Set CC and BCC recipients:

```java
import com.groupdocs.assembly.*;

public class CcBccEmailData
{
    private String to;
    private String cc;
    private String bcc;
    private String subject;
    private String body;

    public String getTo() { return to; }
    public void setTo(String value) { this.to = value; }
    public String getCc() { return cc; }
    public void setCc(String value) { this.cc = value; }
    public String getBcc() { return bcc; }
    public void setBcc(String value) { this.bcc = value; }
    public String getSubject() { return subject; }
    public void setSubject(String value) { this.subject = value; }
    public String getBody() { return body; }
    public void setBody(String value) { this.body = value; }
}

public static void generateEmailWithCcBcc() throws Exception
{
    CcBccEmailData emailData = new CcBccEmailData();
    emailData.setTo("customer@example.com");
    emailData.setCc("manager@example.com");
    emailData.setBcc("archive@example.com");
    emailData.setSubject("Invoice");
    emailData.setBody("Please find attached invoice.");

    DocumentAssembler assembler = new DocumentAssembler();
    assembler.assembleDocument("EmailTemplate.msg", "EmailOutput.msg",
        new DataSourceInfo(emailData, "email"));

    System.out.println("Email with CC and BCC generated successfully.");
}
```

Template:

**To field:**
```
<<[email.getTo()]>>
```

**CC field:**
```
<<[email.getCc()]>>
```

**BCC field:**
```
<<[email.getBcc()]>>
```

**Body:**
```
<<[email.getBody()]>>
```

## Generate Email with Rich Content

Create emails with tables, lists, and formatted content:

```java
import com.groupdocs.assembly.*;
import java.util.*;

public class OrderEmail
{
    private String customerName;
    private String subject;
    private List<OrderItem> items;

    public String getCustomerName() { return customerName; }
    public void setCustomerName(String value) { this.customerName = value; }
    public String getSubject() { return subject; }
    public void setSubject(String value) { this.subject = value; }
    public List<OrderItem> getItems() { return items; }
    public void setItems(List<OrderItem> value) { this.items = value; }
}

public class OrderItem
{
    private String productName;
    private double price;

    public OrderItem(String productName, double price)
    {
        this.productName = productName;
        this.price = price;
    }

    public String getProductName() { return productName; }
    public double getPrice() { return price; }
}

public static void generateRichEmail() throws Exception
{
    OrderEmail orderEmail = new OrderEmail();
    orderEmail.setCustomerName("John Doe");
    orderEmail.setSubject("Order Confirmation");
    orderEmail.setItems(Arrays.asList(
        new OrderItem("Laptop", 999.99),
        new OrderItem("Mouse", 29.99)));

    DocumentAssembler assembler = new DocumentAssembler();
    assembler.assembleDocument("EmailTemplate.msg", "EmailOutput.msg",
        new DataSourceInfo(orderEmail, "order"));

    System.out.println("Rich email generated successfully.");
}
```

Template body:

```
Dear <<[order.getCustomerName()]>>,

Thank you for your order. Here are your items:

<<foreach [in order.getItems()]>>
• <<[getProductName()]>> - <<[getPrice()]:"$#,##0.00">>
<</foreach>>

Total: <<[order.getItems().sum(i => i.getPrice())]:"$#,##0.00">>
```

## Generate Email from Collection

Generate multiple emails from a collection:

```java
import com.groupdocs.assembly.*;
import java.util.*;

public class CustomerEmail
{
    private String email;
    private String name;
    private String subject;

    public CustomerEmail(String email, String name, String subject)
    {
        this.email = email;
        this.name = name;
        this.subject = subject;
    }

    public String getEmail() { return email; }
    public String getName() { return name; }
    public String getSubject() { return subject; }
}

public static void generateEmailsFromCollection() throws Exception
{
    List<CustomerEmail> customers = Arrays.asList(
        new CustomerEmail("customer1@example.com", "John Doe", "Personalized Message"),
        new CustomerEmail("customer2@example.com", "Jane Smith", "Personalized Message"));

    // Generate email for each customer
    DocumentAssembler assembler = new DocumentAssembler();
    for (CustomerEmail customer : customers)
    {
        String outputPath = "Email_" + customer.getName().replace(" ", "_") + ".msg";
        assembler.assembleDocument("EmailTemplate.msg", outputPath,
            new DataSourceInfo(customer, "customer"));
    }

    System.out.println("Emails generated from collection successfully.");
}
```

## Set Email From Address

Set the sender (From) address:

```java
import com.groupdocs.assembly.*;

public class SenderEmailData
{
    private String from;
    private String to;
    private String subject;

    public String getFrom() { return from; }
    public void setFrom(String value) { this.from = value; }
    public String getTo() { return to; }
    public void setTo(String value) { this.to = value; }
    public String getSubject() { return subject; }
    public void setSubject(String value) { this.subject = value; }
}

public static void generateEmailWithFrom() throws Exception
{
    SenderEmailData emailData = new SenderEmailData();
    emailData.setFrom("sender@example.com");
    emailData.setTo("recipient@example.com");
    emailData.setSubject("Test Email");

    DocumentAssembler assembler = new DocumentAssembler();
    assembler.assembleDocument("EmailTemplate.msg", "EmailOutput.msg",
        new DataSourceInfo(emailData, "email"));

    System.out.println("Email with From address generated successfully.");
}
```

Template:

**From field:**
```
<<[email.getFrom()]>>
```

{{< alert style="warning" >}}
Email templates must be in MSG, EML, EMLX, or MHTML format. The template structure depends on the email client used to create it. Ensure proper formatting for HTML or RTF email bodies. The output email format is determined by the output file extension, or can be set explicitly with `new LoadSaveOptions(FileFormat.MSG_UNICODE)` (also `FileFormat.MSG_ASCII`, `FileFormat.EML`, `FileFormat.EMLX`, `FileFormat.MHTML`).
{{< /alert >}}

### Advanced Usage Topics

To learn more about email attachments, HTML email bodies, email headers, and advanced email generation scenarios, please refer to the [advanced usage section]({{< ref "assembly/java/developer-guide/advanced-usage/_index.md" >}}).

## More resources

### GitHub Examples

You may easily run the code above and see the feature in action in our GitHub examples:

* [GroupDocs.Assembly for Java examples, plugins, and showcase](https://github.com/groupdocs-assembly/GroupDocs.Assembly-for-Java)
* [GroupDocs.Assembly for .NET examples, plugins, and showcase](https://github.com/groupdocs-assembly/GroupDocs.Assembly-for-.NET)
* [GroupDocs.Assembly for Python via .NET examples, plugins, and showcase](https://github.com/groupdocs-assembly/GroupDocs.Assembly-for-Python-via-.NET)

### Free Online Apps

Along with the full-featured Java library, we provide simple but powerful free online apps.

To assemble documents from templates and data sources, you can use the online apps from the **[GroupDocs.Assembly App Product Family](https://products.groupdocs.app/assembly/family)**.
