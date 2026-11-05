---
id: multicolored-numbered-list-in-email-document
url: assembly/python-net/multicolored-numbered-list-in-email-document
title: Multicolored Numbered List in Email Document
weight: 5
description: "Multicolored Numbered List in Email Document with GroupDocs.Assembly for Python via .NET: the template, the Python data and the code."
keywords: multicolored numbered list in email document, GroupDocs.Assembly, Python, report generation
productName: GroupDocs.Assembly for Python via .NET
hideChildren: False
---
{{< alert style="info" >}}In this article, we will use GroupDocs.Assembly to generate a Multicolored Numbered List report in Email Document format.{{< /alert >}}{{< alert style="info" >}}The example reads the shop data described in [The Business Layer]({{< ref "assembly/python-net/developer-guide/basic-usage/working-with-a-business-case/the-business-layer.md" >}}).{{< /alert >}}

## Multicolored Numbered List in Email Document

### Creating a Multicolored Numbered List

Practising the following steps you can create Multicolored Numbered List Template in MS Outlook 2013.

1.  In your email, write a sentence like "We provide support for the following clients:".
2.  Start numbered list.
3.  Go to the "Design" tab and select color to make it colored list.
4.  Save the template.

### Reporting Requirement

As a report developer, you are required to represent the following key requirements:

*   The report must be in .eml or .msg format.
*   It must add email recipient, CSS and subject of the email.
*   The report must show the products in the numbered list.
*   It must highlight the products.
*   The report must be generated in the Presentation Document.

### Adding Syntax to be evaluated by GroupDocs.Assembly Engine

We provide support for the following products:

<ol>
<li>&lt;&lt;foreach [in getClients()]>>&lt;&lt;if [indexOf() % 2 == 0]>>      &lt;&lt;[numberOf()]>>.    &lt;&lt;[ProductName]>></li>
<li style="background-color: #ffff00">&lt;&lt;else>>      &lt;&lt;[numberOf()]>>.   &lt;&lt;[ProductName]>></li>
</ol>

<</if>><</foreach>>

{{< alert style="success" >}}For detailed technical information about syntax, expressions and report generation by the engine, please visit: [Working with GroupDocs.Assembly Engine]({{< ref "assembly/python-net/developer-guide/basic-usage/working-with-groupdocs.assembly-engine/_index.md" >}}).{{< /alert >}}

Download Multicolored Numbered List Template

Please download the sample Multicolored Numbered List document we created in this article:

*   [multicolored-numbered-list.msg](/assembly/python-net/_sample_files/developer-guide/advanced-usage/working-with-list-reports-multicolored-numbered/multicolored-numbered-list-in-email-document/multicolored-numbered-list.msg)

### Generating The Report

{{< tabs "example1" >}}
{{< tab "Python" >}}
```python
import json

from groupdocs.assembly import DataSourceInfo, DocumentAssembler

with open("products.json", encoding="utf-8") as f:
    products = json.load(f)

assembler = DocumentAssembler()
assembler.assemble_document("multicolored-numbered-list.msg", "multicolored-numbered-list-report.msg", [
    DataSourceInfo(products, "products"),
    DataSourceInfo("Harbor Lane Provisions <orders@harborlane.example>", "sender"),
    DataSourceInfo(["Quayside Bistro <orders@quaysidebistro.example>", "jonas.weber@harborlane.example"], "recipients"),
    DataSourceInfo("amara.osei@harborlane.example", "cc"),
    DataSourceInfo("Multicolored numbered list", "subject"),
])
```
{{< /tab >}}
{{< tab "multicolored-numbered-list.msg" >}}
{{< tab-text >}}
The following sample file is used in this example: [multicolored-numbered-list.msg](/assembly/python-net/_sample_files/developer-guide/advanced-usage/working-with-list-reports-multicolored-numbered/multicolored-numbered-list-in-email-document/multicolored-numbered-list.msg)
{{< /tab-text >}}
{{< /tab >}}
{{< tab "products.json" >}}
{{< tab-text >}}
The following sample file is used in this example: [products.json](/assembly/python-net/_sample_files/developer-guide/advanced-usage/working-with-list-reports-multicolored-numbered/multicolored-numbered-list-in-email-document/products.json)
{{< /tab-text >}}
{{< /tab >}}
{{< tab "multicolored-numbered-list-report.msg" >}}  
```text
Binary file (MSG, 52 KB)
```
[Download full output](/assembly/python-net/_output_files/developer-guide/advanced-usage/working-with-list-reports-multicolored-numbered/multicolored-numbered-list-in-email-document/generating_the_report/multicolored-numbered-list-report.msg)
{{< /tab >}}
{{< /tabs >}}
