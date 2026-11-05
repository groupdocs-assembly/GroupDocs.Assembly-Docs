---
id: product-overview
url: assembly/python-net/product-overview
title: GroupDocs.Assembly for Python via .NET Overview
linkTitle: Product overview
weight: 1
description: "GroupDocs.Assembly for Python via .NET builds reports and documents from Word, Excel, PowerPoint, email, HTML, Markdown and text templates, filled with Python dicts and lists, JSON, XML and CSV files, or document tables, and saves them as DOCX, XLSX, PPTX, PDF, HTML, email and more."
keywords: report generation, document automation, document assembly, template, mail merge, python dict, json, xml, csv, docx, xlsx, pptx, pdf, email, python
productName: GroupDocs.Assembly for Python via .NET
toc: True
structuredData:
  showOrganization: True
  application:
    name: Document Assembly and Report Generation Tool
    description: The product builds documents and reports from templates of Word, Excel, PowerPoint, email, HTML, Markdown and text formats, filled with data from Python objects, JSON, XML, CSV and document tables.
    productCode: assembly
    productPlatform: python-net
---
## What is GroupDocs.Assembly?
GroupDocs.Assembly for Python via .NET is a native Python library for [document automation](https://en.wikipedia.org/wiki/Document_automation): it builds reports and documents from templates. A template is an ordinary Word, Excel, PowerPoint, OpenDocument, email, HTML, Markdown or text document in which tags such as `<<[customer.Name]>>` and `<<foreach [o in orders]>>` mark where the data goes. GroupDocs.Assembly fills the tags with your data - Python dicts and lists, JSON, XML and CSV files, or the tables of other documents - and saves the report in the template's format or another one, such as PDF. No Microsoft Office installation is required.

Typical uses include:
- **Business documents** - invoices, contracts, offers and letters from one template per document type.
- **Reports** - tables, lists and charts of sales, orders or any other data, with totals, grouping, filtering and sorting done in the template.
- **Email** - messages whose recipients, subject and body come from data.
- **Mail merge** - one document per customer, employee or record.

## Key Capabilities

| Capability | Description |
|---|---|
| **Python data** | [Dicts and lists]({{< ref "assembly/python-net/developer-guide/basic-usage/generate-from-custom-objects.md" >}}) as they are, with their types: numbers, strings, dates, `Decimal`, nested dicts and lists. |
| **Data files and documents** | [JSON, XML and CSV]({{< ref "assembly/python-net/developer-guide/advanced-usage/working-with-simple-data-sources/_index.md" >}}) files, and the tables of [Word, Excel and PowerPoint documents]({{< ref "assembly/python-net/developer-guide/advanced-usage/using-documents-as-data-source/_index.md" >}}). |
| **Template syntax** | [Expressions, formatting and data bands]({{< ref "assembly/python-net/developer-guide/basic-usage/working-with-groupdocs.assembly-engine/template-syntax-part-1-of-2.md" >}}), with `Sum`, `Where`, `GroupBy`, `OrderBy` and other [sequence operations]({{< ref "assembly/python-net/developer-guide/advanced-usage/enumeration-extension-methods.md" >}}) in the template. |
| **Tables and lists** | [Table reports]({{< ref "assembly/python-net/developer-guide/advanced-usage/working-with-table-reports/_index.md" >}}) with totals, master-detail, highlighting and merged cells, and [bulleted]({{< ref "assembly/python-net/developer-guide/basic-usage/generate-bullet-lists.md" >}}) and [numbered]({{< ref "assembly/python-net/developer-guide/basic-usage/generate-numbered-lists.md" >}}) lists. |
| **Charts** | [Pie]({{< ref "assembly/python-net/developer-guide/advanced-usage/working-with-chart-reports-pie/_index.md" >}}), [bubble]({{< ref "assembly/python-net/developer-guide/advanced-usage/working-with-chart-reports-bubble/_index.md" >}}), [scatter]({{< ref "assembly/python-net/developer-guide/advanced-usage/working-with-chart-reports-scatter/_index.md" >}}) and column charts with series, points and colors from data. |
| **Images, barcodes, links** | [Images]({{< ref "assembly/python-net/developer-guide/advanced-usage/inserting-images-dynamically.md" >}}), [barcodes]({{< ref "assembly/python-net/developer-guide/advanced-usage/working-with-barcode-image-generation/_index.md" >}}), [hyperlinks and bookmarks]({{< ref "assembly/python-net/developer-guide/advanced-usage/inserting-hyperlinks-or-bookmarks/_index.md" >}}) and [whole documents]({{< ref "assembly/python-net/developer-guide/advanced-usage/inserting-documents-dynamically.md" >}}) inserted from data. |
| **Email** | [MSG and EML templates]({{< ref "assembly/python-net/developer-guide/basic-usage/generate-email-messages.md" >}}) with sender, recipients, subject and body from data. |
| **Formats** | [More than 40 template formats]({{< ref "assembly/python-net/getting-started/supported-document-formats.md" >}}), and reports [saved to another format]({{< ref "assembly/python-net/developer-guide/advanced-usage/changing-target-file-format.md" >}}) such as PDF, HTML or XPS. |
| **On-premise** | No cloud calls, no Microsoft Office install, no network traffic. |

## Quick Example

Fill a Word template with the orders of a customer from a JSON file, and save the report as PDF:

{{< tabs "product-overview-quick-example" >}}
{{< tab "quick_example.py" >}}
```python
import json

from groupdocs.assembly import DataSourceInfo, DocumentAssembler

def quick_example():
    # The data: one customer and its orders, read from JSON into a dict
    with open("customer.json", encoding="utf-8") as f:
        customer = json.load(f)

    # Fill the template's tags and save the report as PDF
    assembler = DocumentAssembler()
    assembler.assemble_document("customer-summary.docx", "customer-summary.pdf", DataSourceInfo(customer, "customer"))
    print("Orders in the report:", len(customer["Order"]))

if __name__ == "__main__":
    quick_example()
```
{{< /tab >}}
{{< tab "customer-summary.docx" >}}
{{< tab-text >}}
The following sample file is used in this example: [customer-summary.docx](/assembly/python-net/_sample_files/product-overview/customer-summary.docx)
{{< /tab-text >}}
{{< /tab >}}
{{< tab "customer.json" >}}
{{< tab-text >}}
The following sample file is used in this example: [customer.json](/assembly/python-net/_sample_files/product-overview/customer.json)
{{< /tab-text >}}
{{< /tab >}}
{{< tab "customer-summary.pdf" >}}  
```text
Binary file (PDF, 37 KB)
```
[Download full output](/assembly/python-net/_output_files/product-overview/quick_example/customer-summary.pdf)
{{< /tab >}}
{{< /tabs >}}

The template holds the customer's name and address, a table whose row repeats for each order, and the total:

```text
<<[customer.CustomerName]>>
<<[customer.ShippingAddress]>>, <<[customer.CustomerContactNumber]>>
| Product                                              | Quantity                  | Price, USD                    |
| <<foreach [o in customer.Order]>><<[o.Product.ProductName]>> | <<[o.ProductQuantity]>> | <<[o.Price]>><</foreach>> |
Total: <<[customer.Order.Sum(o => o.Price)]>> USD
```

## Where to next

- [Hello, World!]({{< ref "assembly/python-net/getting-started/hello-world.md" >}}) and the [Quick Start Guide]({{< ref "assembly/python-net/getting-started/quick-start-guide.md" >}}) - your first reports.
- [Features Overview]({{< ref "assembly/python-net/getting-started/features-overview.md" >}}) - everything GroupDocs.Assembly can do, with links to each topic.
- [Developer Guide]({{< ref "assembly/python-net/developer-guide/_index.md" >}}) - the template syntax, the data sources and every kind of report.
- [API Reference](https://reference.groupdocs.com/assembly/python-net/) - the classes and their members.
- [AI agents and LLM integration]({{< ref "assembly/python-net/agents-and-llm-integration.md" >}}) - the package's `AGENTS.md` and the documentation for AI coding assistants.
