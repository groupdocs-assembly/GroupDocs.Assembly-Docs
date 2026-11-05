---
id: in-paragraph-list-in-email-document
url: assembly/python-net/in-paragraph-list-in-email-document
title: In-Paragraph List in Email Document
weight: 6
description: "In-Paragraph List in Email Document with GroupDocs.Assembly for Python via .NET: the template, the Python data and the code."
keywords: in-paragraph list in email document, GroupDocs.Assembly, Python, report generation
productName: GroupDocs.Assembly for Python via .NET
hideChildren: False
---
{{< alert style="info" >}}In this article, we will use GroupDocs.Assembly to generate a In-Paragraph List report in Email Document format.{{< /alert >}}

## In-Paragraph List in Email Document

### Reporting Requirement

As a report developer, you are required to share the following key requirements:

*   Report must be in .eml or .msg format.
*   It must add email recipient, css and subject of the email.
*   A descriptive or informative line like "We provide support for the following products:".
*   Show all the products along with the above sentence.

### Adding Syntax to be evaluated by GroupDocs.Assembly Engine

```text
We provide support for the following products:
<<foreach [in products]>><<[IndexOf() != 0 ? ", " : ""]>>
<<[ProductName]>>
<</foreach>>
```

{{< alert style="success" >}}For detailed technical information about syntax,expressions and report generation by the engine, please visit: [Working with GroupDocs.Assembly Engine]({{< ref "assembly/python-net/developer-guide/basic-usage/working-with-groupdocs.assembly-engine/_index.md" >}}).{{< /alert >}}

### Download In-Paragraph List Template

Please download the sample Common List document we created in this article:

*   [in-paragraph-list.msg](/assembly/python-net/_sample_files/developer-guide/advanced-usage/working-with-paragraph-reports/in-paragraph-list-in-email-document/in-paragraph-list.msg)

### Generating The Report

{{< alert style="info" >}}The example reads the shop data described in [The Business Layer]({{< ref "assembly/python-net/developer-guide/basic-usage/working-with-a-business-case/the-business-layer.md" >}}).{{< /alert >}}

{{< tabs "example1" >}}
{{< tab "Python" >}}
```python
import json

from groupdocs.assembly import DataSourceInfo, DocumentAssembler

with open("products.json", encoding="utf-8") as f:
    products = json.load(f)

assembler = DocumentAssembler()
assembler.assemble_document("in-paragraph-list.msg", "in-paragraph-list-report.msg", [
    DataSourceInfo(products, "products"),
    DataSourceInfo("Harbor Lane Provisions <orders@harborlane.example>", "sender"),
    DataSourceInfo(["Quayside Bistro <orders@quaysidebistro.example>", "jonas.weber@harborlane.example"], "recipients"),
    DataSourceInfo("amara.osei@harborlane.example", "cc"),
    DataSourceInfo("In paragraph list", "subject"),
])
```
{{< /tab >}}
{{< tab "in-paragraph-list.msg" >}}
{{< tab-text >}}
The following sample file is used in this example: [in-paragraph-list.msg](/assembly/python-net/_sample_files/developer-guide/advanced-usage/working-with-paragraph-reports/in-paragraph-list-in-email-document/in-paragraph-list.msg)
{{< /tab-text >}}
{{< /tab >}}
{{< tab "products.json" >}}
{{< tab-text >}}
The following sample file is used in this example: [products.json](/assembly/python-net/_sample_files/developer-guide/advanced-usage/working-with-paragraph-reports/in-paragraph-list-in-email-document/products.json)
{{< /tab-text >}}
{{< /tab >}}
{{< tab "in-paragraph-list-report.msg" >}}  
```text
Binary file (MSG, 32 KB)
```
[Download full output](/assembly/python-net/_output_files/developer-guide/advanced-usage/working-with-paragraph-reports/in-paragraph-list-in-email-document/generating_the_report/in-paragraph-list-report.msg)
{{< /tab >}}
{{< /tabs >}}
