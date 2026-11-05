---
id: bulleted-list-in-email-document
url: assembly/python-net/bulleted-list-in-email-document
title: Bulleted List in Email Document
weight: 6
description: "Bulleted List in Email Document with GroupDocs.Assembly for Python via .NET: the template, the Python data and the code."
keywords: bulleted list in email document, GroupDocs.Assembly, Python, report generation
productName: GroupDocs.Assembly for Python via .NET
hideChildren: False
---
{{< alert style="info" >}}In this article, we will use GroupDocs.Assembly to generate a Bulleted List report in Email format.{{< /alert >}}{{< alert style="info" >}}The example reads the shop data described in [The Business Layer]({{< ref "assembly/python-net/developer-guide/basic-usage/working-with-a-business-case/the-business-layer.md" >}}).{{< /alert >}}

## Bulleted List in Email

#### Reporting Requirement

As a report developer, you are required to share the following key requirements:

*   A report must be in .eml or .msg format.
*   It must add email recipient, CSS and subject of the email.
*   A report must show all the products in a bulleted list format.

#### Adding Syntax to be evaluated by GroupDocs.Assembly Engine

##### Recipients, Cc and Subject

```text
<<foreach [r in recipients]>><<[r]>>; <</foreach>>
<<[cc]>>
<<[subject]>>

```

##### Body

```text
We provide support for the following clients:
<<foreach[in products]>>  ∙  <<[ProductName]>>
<</foreach>>

```

{{< alert style="success" >}}For detailed technical information about syntax, expressions and report generation by the engine, please visit: [Working with GroupDocs.Assembly Engine]({{< ref "assembly/python-net/developer-guide/basic-usage/working-with-groupdocs.assembly-engine/_index.md" >}}).{{< /alert >}}

#### Download Bulleted List Template

Please download the sample Bulleted List document we used in this article:

*   [bulleted-list.msg](/assembly/python-net/_sample_files/developer-guide/advanced-usage/working-with-list-reports-bulleted/bulleted-list-in-email-document/bulleted-list.msg)

### Generating The Report

{{< tabs "example1" >}}
{{< tab "Python" >}}
```python
import json

from groupdocs.assembly import DataSourceInfo, DocumentAssembler

with open("products.json", encoding="utf-8") as f:
    products = json.load(f)

assembler = DocumentAssembler()
assembler.assemble_document("bulleted-list.msg", "bulleted-list-report.msg", [
    DataSourceInfo(products, "products"),
    DataSourceInfo("Harbor Lane Provisions <orders@harborlane.example>", "sender"),
    DataSourceInfo(["Quayside Bistro <orders@quaysidebistro.example>", "jonas.weber@harborlane.example"], "recipients"),
    DataSourceInfo("amara.osei@harborlane.example", "cc"),
    DataSourceInfo("Bulleted list", "subject"),
])
```
{{< /tab >}}
{{< tab "bulleted-list.msg" >}}
{{< tab-text >}}
The following sample file is used in this example: [bulleted-list.msg](/assembly/python-net/_sample_files/developer-guide/advanced-usage/working-with-list-reports-bulleted/bulleted-list-in-email-document/bulleted-list.msg)
{{< /tab-text >}}
{{< /tab >}}
{{< tab "products.json" >}}
{{< tab-text >}}
The following sample file is used in this example: [products.json](/assembly/python-net/_sample_files/developer-guide/advanced-usage/working-with-list-reports-bulleted/bulleted-list-in-email-document/products.json)
{{< /tab-text >}}
{{< /tab >}}
{{< tab "bulleted-list-report.msg" >}}  
```text
Binary file (MSG, 52 KB)
```
[Download full output](/assembly/python-net/_output_files/developer-guide/advanced-usage/working-with-list-reports-bulleted/bulleted-list-in-email-document/generating_the_report/bulleted-list-report.msg)
{{< /tab >}}
{{< /tabs >}}
