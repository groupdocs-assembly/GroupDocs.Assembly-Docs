---
id: numbered-list-in-email-document
url: assembly/python-net/numbered-list-in-email-document
title: Numbered List in Email Document
weight: 6
description: "Numbered List in Email Document with GroupDocs.Assembly for Python via .NET: the template, the Python data and the code."
keywords: numbered list in email document, GroupDocs.Assembly, Python, report generation
productName: GroupDocs.Assembly for Python via .NET
hideChildren: False
---
{{< alert style="info" >}}In this article, we will use GroupDocs.Assembly to generate a Numbered List report in Email Document format.{{< /alert >}}{{< alert style="info" >}}The example reads the shop data described in [The Business Layer]({{< ref "assembly/python-net/developer-guide/basic-usage/working-with-a-business-case/the-business-layer.md" >}}).{{< /alert >}}

## Numbered List in Email Document

### Creating a Numbered List

Practising the following steps you can create Numbered List Template in MS Outlook 2013.

1.  Create a new Email.
2.  Write a sentence like "We provide support for the following clients:".
3.  Start numbered list.
4.  Save the template.

### Reporting Requirement

As a report developer, you are required to represent the following key requirements:

*   The report must be in .eml or .msg format.
*   It must add email recipient, CSS and subject of the email.
*   The report must show the products in the numbered list.

### Adding Syntax to be evaluated by GroupDocs.Assembly Engine

```text
We provide support for the following products:
<<foreach [in products]>><<[NumberOf()]>>. <<[ProductName]>>
<</foreach>>
```

{{< alert style="success" >}}For detailed technical information about syntax, expressions and report generation by the engine, please visit: [Working with GroupDocs.Assembly Engine]({{< ref "assembly/python-net/developer-guide/basic-usage/working-with-groupdocs.assembly-engine/_index.md" >}}).{{< /alert >}}

### Download Numbered List Template

Please download the sample Numbered List document we created in this article:

*   [numbered-list.msg](/assembly/python-net/_sample_files/developer-guide/advanced-usage/working-with-list-reports-numbered/numbered-list-in-email-document/numbered-list.msg)
*   [numbered-list-with-restartnum.msg](/assembly/python-net/_sample_files/developer-guide/advanced-usage/working-with-list-reports-numbered/numbered-list-in-email-document/numbered-list-with-restartnum.msg)

### Generating The Report

{{< tabs "example1" >}}
{{< tab "Python" >}}
```python
import json

from groupdocs.assembly import DataSourceInfo, DocumentAssembler

with open("products.json", encoding="utf-8") as f:
    products = json.load(f)

assembler = DocumentAssembler()
assembler.assemble_document("numbered-list.msg", "numbered-list-report.msg", [
    DataSourceInfo(products, "products"),
    DataSourceInfo("Harbor Lane Provisions <orders@harborlane.example>", "sender"),
    DataSourceInfo(["Quayside Bistro <orders@quaysidebistro.example>", "jonas.weber@harborlane.example"], "recipients"),
    DataSourceInfo("amara.osei@harborlane.example", "cc"),
    DataSourceInfo("Numbered list", "subject"),
])
```
{{< /tab >}}
{{< tab "numbered-list.msg" >}}
{{< tab-text >}}
The following sample file is used in this example: [numbered-list.msg](/assembly/python-net/_sample_files/developer-guide/advanced-usage/working-with-list-reports-numbered/numbered-list-in-email-document/numbered-list.msg)
{{< /tab-text >}}
{{< /tab >}}
{{< tab "products.json" >}}
{{< tab-text >}}
The following sample file is used in this example: [products.json](/assembly/python-net/_sample_files/developer-guide/advanced-usage/working-with-list-reports-numbered/numbered-list-in-email-document/products.json)
{{< /tab-text >}}
{{< /tab >}}
{{< tab "numbered-list-report.msg" >}}  
```text
Binary file (MSG, 52 KB)
```
[Download full output](/assembly/python-net/_output_files/developer-guide/advanced-usage/working-with-list-reports-numbered/numbered-list-in-email-document/generating_the_report/numbered-list-report.msg)
{{< /tab >}}
{{< /tabs >}}

{{< tabs "example2" >}}
{{< tab "Python" >}}
```python
import json
from datetime import datetime

from groupdocs.assembly import DataSourceInfo, DocumentAssembler

def parse_dates(item):
    # JSON has no dates: turn the order dates into datetime objects for the template
    for key in ("OrderDate", "ShippingDate"):
        if key in item:
            item[key] = datetime.strptime(item[key], "%Y-%m-%dT%H:%M:%S")
    return item

with open("orders.json", encoding="utf-8") as f:
    orders = json.load(f, object_hook=parse_dates)

assembler = DocumentAssembler()
assembler.assemble_document("numbered-list-with-restartnum.msg", "numbered-list-with-restartnum-report.msg", [
    DataSourceInfo(orders, "orders"),
    DataSourceInfo("Harbor Lane Provisions <orders@harborlane.example>", "sender"),
    DataSourceInfo(["Quayside Bistro <orders@quaysidebistro.example>", "jonas.weber@harborlane.example"], "recipients"),
    DataSourceInfo("amara.osei@harborlane.example", "cc"),
    DataSourceInfo("Numbered list with restartnum", "subject"),
])
```
{{< /tab >}}
{{< tab "numbered-list-with-restartnum.msg" >}}
{{< tab-text >}}
The following sample file is used in this example: [numbered-list-with-restartnum.msg](/assembly/python-net/_sample_files/developer-guide/advanced-usage/working-with-list-reports-numbered/numbered-list-in-email-document/numbered-list-with-restartnum.msg)
{{< /tab-text >}}
{{< /tab >}}
{{< tab "orders.json" >}}
{{< tab-text >}}
The following sample file is used in this example: [orders.json](/assembly/python-net/_sample_files/developer-guide/advanced-usage/working-with-list-reports-numbered/numbered-list-in-email-document/orders.json)
{{< /tab-text >}}
{{< /tab >}}
{{< tab "numbered-list-with-restartnum-report.msg" >}}  
```text
Binary file (MSG, 60 KB)
```
[Download full output](/assembly/python-net/_output_files/developer-guide/advanced-usage/working-with-list-reports-numbered/numbered-list-in-email-document/generating_the_report_2/numbered-list-with-restartnum-report.msg)
{{< /tab >}}
{{< /tabs >}}

## Numbering Restart in Nested Numbered List 

The GroupDocs.Assembly engine allows restart list numbering within your documents dynamically using *<<restartNum>>* tags. In particular, this feature is useful when working with a nested numbered list within a data band.

Assume that we are picking *Order* and *Service* classes as defined in the following *Custom Objects* of our business use case.

Given that orders is an enumeration of Order instances, you could try to use the following template to output information on several orders in one document.

```text
<<foreach [in orders]>><<[Customer.CustomerName]>> (<<[Customer.CustomerContactNumber]>>)
1.	<<foreach [in Services]>><<[ServiceName]>>
<</foreach>><</foreach>>
```

The generated report will look as follows:

```
Jane Doe (+9211874)
	1.	Regular Cleaning
	2.	Oven Cleaning
John Smith (+458789)
	3.	Regular Cleaning
	4.	Oven Cleaning
	5.	Carpet Cleaning
John Smith (+458789)
	6.	Regular Cleaning
	7.	Carpet Cleaning
John Smith (+458789)
	8.	Oven Cleaning
```

However, there would be a single numbered list across all orders, which is not applicable for this scenario. Hence, you can make the list numbering to restart for every order by putting a *<<restartNum>>* tag into your template before a corresponding *<<foreach>>* tag as follows:

```text
<<foreach [in orders]>><<[ Customer.CustomerName]>> (<<[Customer.CustomerContactNumber]>>)
1.	<<restartNum>><<foreach [in Services]>><<[ServiceName]>>
<</foreach>><</foreach>>
```

 Then, the generated report will look as follows:

```
Jane Doe (+9211874)
	1.	Regular Cleaning
	2.	Oven Cleaning
John Smith (+458789)
	1.	Regular Cleaning
	2.	Oven Cleaning
	3.	Carpet Cleaning
John Smith (+458789)
	1.	Regular Cleaning
	2.	Carpet Cleaning
John Smith (+458789)
	1.	Oven Cleaning
```
