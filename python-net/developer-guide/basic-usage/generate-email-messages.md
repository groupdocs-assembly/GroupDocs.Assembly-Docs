---
id: assembly-basic-usage-generate-emails
url: assembly/python-net/basic-usage-generate-emails
aliases:
- /assembly/python-net/email-reports/
linktitle: Generate Email Messages
title: Generate Email Messages from Data
weight: 29
description: "Create email messages whose subject, body, sender and To, CC and BCC recipients come from Python dicts and lists, using EML templates and GroupDocs.Assembly for Python via .NET."
keywords: generate emails, email messages, email subject, email body, email recipients, MSG, EML, compose emails, Python dict, Python
productName: GroupDocs.Assembly for Python via .NET
hideChildren: False
---

## Overview

GroupDocs.Assembly for Python via .NET enables you to generate email messages dynamically from templates. You can set email attributes like subject, body, and recipients (To, CC, BCC) using template syntax, making it easy to create personalized email messages from data sources.

The main classes involved are:
- [DocumentAssembler](https://reference.groupdocs.com/assembly/python-net/groupdocs.assembly/documentassembler/) - assembles email messages
- [DataSourceInfo](https://reference.groupdocs.com/assembly/python-net/groupdocs.assembly/datasourceinfo/) - wraps data sources

Here are the steps to generate email messages:

* Create an email template (MSG or EML format)
* Set email attributes (subject, To, CC, BCC) using template syntax
* Create email body content with data binding
* Assemble the email message with your data source
* Save the assembled email

{{< alert style="info" >}}
Email templates support the same template syntax as Word documents, including expression tags, data bands, conditional blocks, and formatting.
{{< /alert >}}

The templates on this page are EML files: MIME messages in plain text, which any text editor can write. In an EML template, a tag in an address header (`From`, `To`, `Cc`, `Bcc`) sits in a quoted display name, followed by any placeholder address: `To: "<<[email.Recipient]>>" <recipient@harborlane.example>`. The assembled header holds the addresses the tag gives, and the placeholder is dropped. Without the quotes, the header is read as an address list before the tag is evaluated, and the tag is lost. An MSG template made in Outlook takes the same tags in its subject, recipient fields and body.

## Generate Email with Subject and Body

Create a simple email with dynamic subject and body:

{{< tabs "example1" >}}
{{< tab "Python" >}}
```python
from decimal import Decimal

from groupdocs.assembly import DataSourceInfo, DocumentAssembler

email_data = {
    "Recipient": "orders@quaysidebistro.example",
    "Subject": "Invoice #1001",
    "CustomerName": "Quayside Bistro",
    "InvoiceAmount": Decimal("1500.00"),
}

assembler = DocumentAssembler()
assembler.assemble_document("invoice-notification.eml", "invoice-notification-report.eml",
                            DataSourceInfo(email_data, "email"))

print("Email generated successfully.")
```
{{< /tab >}}
{{< tab "invoice-notification.eml" >}}
{{< tab-text >}}
The following sample file is used in this example: [invoice-notification.eml](/assembly/python-net/_sample_files/developer-guide/basic-usage/generate-email-messages/invoice-notification.eml)
{{< /tab-text >}}
{{< /tab >}}
{{< tab "invoice-notification-report.eml" >}}  
```text
Binary file (EML, 786 bytes)
```
[Download full output](/assembly/python-net/_output_files/developer-guide/basic-usage/generate-email-messages/generate_email_with_subject_and_body/invoice-notification-report.eml)
{{< /tab >}}
{{< /tabs >}}

## Email Template Structure

In your email template (invoice-notification.eml), set attributes and body:

**Subject field:**
```text
<<[email.Subject]>>
```

**To field:**
```text
"<<[email.Recipient]>>" <recipient@harborlane.example>
```

**Body:**
```text
Dear <<[email.CustomerName]>>,

Please find your invoice below:

Amount: <<[email.InvoiceAmount]:"C">>

Thank you for your business.
```

## Generate Email with Multiple Recipients

Set multiple recipients using foreach:

{{< tabs "example2" >}}
{{< tab "Python" >}}
```python
from groupdocs.assembly import DataSourceInfo, DocumentAssembler

email_data = {
    "Recipients": [
        "orders@quaysidebistro.example",
        "orders@lanternstreetcafe.example",
    ],
    "Subject": "Important Update",
    "Message": "Our warehouse at 18 Quayside Road closes at noon on Friday, 16 January 2015.",
}

assembler = DocumentAssembler()
assembler.assemble_document("warehouse-update.eml", "warehouse-update-report.eml",
                            DataSourceInfo(email_data, "email"))

print("Email with multiple recipients generated successfully.")
```
{{< /tab >}}
{{< tab "warehouse-update.eml" >}}
{{< tab-text >}}
The following sample file is used in this example: [warehouse-update.eml](/assembly/python-net/_sample_files/developer-guide/basic-usage/generate-email-messages/warehouse-update.eml)
{{< /tab-text >}}
{{< /tab >}}
{{< tab "warehouse-update-report.eml" >}}  
```text
Binary file (EML, 763 bytes)
```
[Download full output](/assembly/python-net/_output_files/developer-guide/basic-usage/generate-email-messages/generate_email_with_multiple_recipients/warehouse-update-report.eml)
{{< /tab >}}
{{< /tabs >}}

Template for multiple recipients:

**To field:**
```text
"<<foreach [r in email.Recipients]>><<[r]>>; <</foreach>>" <recipients@harborlane.example>
```

**Body:**
```text
<<[email.Message]>>
```

The data band writes the addresses separated by semicolons, and the message gets one recipient per address. The list can also be a data source of its own, `DataSourceInfo(addresses, "recipients")`, read by `<<foreach [r in recipients]>>`; an expression tag alone, `<<[recipients]>>`, would write the name of the list type instead of the addresses.

## Generate Email with CC and BCC

Set CC and BCC recipients:

{{< tabs "example3" >}}
{{< tab "Python" >}}
```python
from groupdocs.assembly import DataSourceInfo, DocumentAssembler

email_data = {
    "To": "orders@quaysidebistro.example",
    "Cc": "mei.tanaka@harborlane.example",
    "Bcc": "archive@harborlane.example",
    "Subject": "Invoice",
    "Body": "Please find attached invoice.",
}

assembler = DocumentAssembler()
assembler.assemble_document("invoice-cc-bcc.eml", "invoice-cc-bcc-report.eml",
                            DataSourceInfo(email_data, "email"))

print("Email with CC and BCC generated successfully.")
```
{{< /tab >}}
{{< tab "invoice-cc-bcc.eml" >}}
{{< tab-text >}}
The following sample file is used in this example: [invoice-cc-bcc.eml](/assembly/python-net/_sample_files/developer-guide/basic-usage/generate-email-messages/invoice-cc-bcc.eml)
{{< /tab-text >}}
{{< /tab >}}
{{< tab "invoice-cc-bcc-report.eml" >}}  
```text
Binary file (EML, 742 bytes)
```
[Download full output](/assembly/python-net/_output_files/developer-guide/basic-usage/generate-email-messages/generate_email_with_cc_and_bcc/invoice-cc-bcc-report.eml)
{{< /tab >}}
{{< /tabs >}}

Template:

**To field:**
```text
"<<[email.To]>>" <recipient@harborlane.example>
```

**CC field:**
```text
"<<[email.Cc]>>" <copy@harborlane.example>
```

**BCC field:**
```text
"<<[email.Bcc]>>" <blind-copy@harborlane.example>
```

**Body:**
```text
<<[email.Body]>>
```

## Generate Email with Rich Content

Create emails with lists, totals and formatted content:

{{< tabs "example4" >}}
{{< tab "Python" >}}
```python
from decimal import Decimal

from groupdocs.assembly import DataSourceInfo, DocumentAssembler

order_email = {
    "CustomerName": "Quayside Bistro",
    "Email": "orders@quaysidebistro.example",
    "Subject": "Order Confirmation",
    "Items": [
        {"ProductName": "Harbor Blend whole bean coffee", "Price": Decimal("18.40")},
        {"ProductName": "Aged harbour cheddar", "Price": Decimal("16.50")},
    ],
}

assembler = DocumentAssembler()
assembler.assemble_document("order-confirmation.eml", "order-confirmation-report.eml",
                            DataSourceInfo(order_email, "order"))

print("Rich email generated successfully.")
```
{{< /tab >}}
{{< tab "order-confirmation.eml" >}}
{{< tab-text >}}
The following sample file is used in this example: [order-confirmation.eml](/assembly/python-net/_sample_files/developer-guide/basic-usage/generate-email-messages/order-confirmation.eml)
{{< /tab-text >}}
{{< /tab >}}
{{< tab "order-confirmation-report.eml" >}}  
```text
Binary file (EML, 870 bytes)
```
[Download full output](/assembly/python-net/_output_files/developer-guide/basic-usage/generate-email-messages/generate_email_with_rich_content/order-confirmation-report.eml)
{{< /tab >}}
{{< /tabs >}}

Template body:

```text
Dear <<[order.CustomerName]>>,

Thank you for your order. Here are your items:

<<foreach [in order.Items]>>• <<[ProductName]>> - <<[Price]:"C">>
<</foreach>>
Total: <<[order.Items.Sum(i => i.Price)]:"C">>
```

## Generate Email from Collection

Generate multiple emails from a collection, one `assemble_document` call per item:

{{< tabs "example5" >}}
{{< tab "Python" >}}
```python
from groupdocs.assembly import DataSourceInfo, DocumentAssembler

customers = [
    {
        "Email": "orders@quaysidebistro.example",
        "Name": "Quayside Bistro",
        "Subject": "Personalized Message",
    },
    {
        "Email": "orders@saltmarshdeli.example",
        "Name": "Saltmarsh Deli",
        "Subject": "Personalized Message",
    },
]

# Generate email for each customer
assembler = DocumentAssembler()
for customer in customers:
    output_path = "personal-greeting-{}.eml".format(customer["Name"].lower().replace(" ", "-"))
    assembler.assemble_document("personal-greeting.eml", output_path,
                                DataSourceInfo(customer, "customer"))

print("Emails generated from collection successfully.")
```
{{< /tab >}}
{{< tab "personal-greeting.eml" >}}
{{< tab-text >}}
The following sample file is used in this example: [personal-greeting.eml](/assembly/python-net/_sample_files/developer-guide/basic-usage/generate-email-messages/personal-greeting.eml)
{{< /tab-text >}}
{{< /tab >}}
{{< tab "generate-email-from-collection-outputs.zip" >}}  
```text
personal-greeting-quayside-bistro.eml (897 bytes)
personal-greeting-saltmarsh-deli.eml (895 bytes)
```
[Download full output](/assembly/python-net/_output_files/developer-guide/basic-usage/generate-email-messages/generate_email_from_collection/generate-email-from-collection-outputs.zip)
{{< /tab >}}
{{< /tabs >}}

The template addresses the message to `"<<[customer.Email]>>"`, puts `<<[customer.Subject]>>` in the subject and greets `<<[customer.Name]>>` in the body. The example writes `personal-greeting-quayside-bistro.eml` and `personal-greeting-saltmarsh-deli.eml`.

## Set Email From Address

Set the sender (From) address:

{{< tabs "example6" >}}
{{< tab "Python" >}}
```python
from groupdocs.assembly import DataSourceInfo, DocumentAssembler

email_data = {
    "From": "accounts@harborlane.example",
    "To": "orders@quaysidebistro.example",
    "Subject": "Statement for January 2015",
}

assembler = DocumentAssembler()
assembler.assemble_document("sender-address.eml", "sender-address-report.eml",
                            DataSourceInfo(email_data, "email"))

print("Email with From address generated successfully.")
```
{{< /tab >}}
{{< tab "sender-address.eml" >}}
{{< tab-text >}}
The following sample file is used in this example: [sender-address.eml](/assembly/python-net/_sample_files/developer-guide/basic-usage/generate-email-messages/sender-address.eml)
{{< /tab-text >}}
{{< /tab >}}
{{< tab "sender-address-report.eml" >}}  
```text
Binary file (EML, 725 bytes)
```
[Download full output](/assembly/python-net/_output_files/developer-guide/basic-usage/generate-email-messages/set_email_from_address/sender-address-report.eml)
{{< /tab >}}
{{< /tabs >}}

Template:

**From field:**
```text
"<<[email.From]>>" <sender@harborlane.example>
```

{{< alert style="warning" >}}
Email templates must be in MSG or EML format. The template structure depends on the email client used to create it. Ensure proper formatting for HTML or RTF email bodies.
{{< /alert >}}

### Advanced Usage Topics

To learn more about email attachments, HTML email bodies, email headers, and advanced email generation scenarios, please refer to the [advanced usage section]({{< ref "assembly/python-net/developer-guide/advanced-usage/_index.md" >}}).

## More resources

### GitHub Examples

You may easily run the code above and see the feature in action in our GitHub examples:

* [GroupDocs.Assembly for .NET examples, plugins, and showcase](https://github.com/groupdocs-assembly/GroupDocs.Assembly-for-.NET)
* [GroupDocs.Assembly for Java examples, plugins, and showcase](https://github.com/groupdocs-assembly/GroupDocs.Assembly-for-Java)
* [GroupDocs.Assembly for Python via .NET examples, plugins, and showcase](https://github.com/groupdocs-assembly/GroupDocs.Assembly-for-Python-via-.NET)

### Free Online Apps

Along with the full-featured library, we provide simple but powerful free online apps.

To assemble documents from templates and data sources, you can use the online apps from the **[GroupDocs.Assembly App Product Family](https://products.groupdocs.app/assembly/family)**.
