---
id: numbered-list-in-text-document
url: assembly/python-net/numbered-list-in-text-document
title: Numbered List in Text Document
weight: 5
description: "Numbered List in Text Document with GroupDocs.Assembly for Python via .NET: the template, the Python data and the code."
keywords: numbered list in text document, GroupDocs.Assembly, Python, report generation
productName: GroupDocs.Assembly for Python via .NET
hideChildren: False
---
{{< alert style="info" >}}In this article, we will use GroupDocs.Assembly to generate a Numbered List report in Text Document format.{{< /alert >}}{{< alert style="info" >}}The example reads the shop data described in [The Business Layer]({{< ref "assembly/python-net/developer-guide/basic-usage/working-with-a-business-case/the-business-layer.md" >}}).{{< /alert >}}

## Numbered List in Text Document

### Reporting Requirement

As a report developer, you are required to describe the services you are providing with the following key requirements:

*   The report must show the products in the numbered list.
*   The report must be generated in the Text Document.

### Adding Syntax to be evaluated by GroupDocs.Assembly Engine

```text
We provide support for the following products:
<<foreach [in products]>><<[NumberOf()]>>. <<[ProductName]>>
<</foreach>>
```

{{< alert style="success" >}}For detailed technical information about syntax, expressions and report generation by the engine, please visit: [Working with GroupDocs.Assembly Engine]({{< ref "assembly/python-net/developer-guide/basic-usage/working-with-groupdocs.assembly-engine/_index.md" >}}).{{< /alert >}}

### Download Numbered List Template

Please download the sample Numbered List document we created in this article:

*   [numbered-list.txt](/assembly/python-net/_sample_files/developer-guide/advanced-usage/working-with-list-reports-numbered/numbered-list-in-text-document/numbered-list.txt)

### Generating The Report

{{< tabs "example1" >}}
{{< tab "Python" >}}
```python
import json

from groupdocs.assembly import DataSourceInfo, DocumentAssembler

with open("products.json", encoding="utf-8") as f:
    products = json.load(f)

assembler = DocumentAssembler()
assembler.assemble_document("numbered-list.txt", "numbered-list-report.txt", DataSourceInfo(products, "products"))
```
{{< /tab >}}
{{< tab "numbered-list.txt" >}}
{{< tab-text >}}
The following sample file is used in this example: [numbered-list.txt](/assembly/python-net/_sample_files/developer-guide/advanced-usage/working-with-list-reports-numbered/numbered-list-in-text-document/numbered-list.txt)
{{< /tab-text >}}
{{< /tab >}}
{{< tab "products.json" >}}
{{< tab-text >}}
The following sample file is used in this example: [products.json](/assembly/python-net/_sample_files/developer-guide/advanced-usage/working-with-list-reports-numbered/numbered-list-in-text-document/products.json)
{{< /tab-text >}}
{{< /tab >}}
{{< tab "numbered-list-report.txt" >}}  
```text
We provide support for the following products:
1. Harbor Blend whole bean coffee
2. Lighthouse Espresso beans
3. Aged harbour cheddar
4. Chestnut honey
5. Oat and honey biscuits
6. Cold-pressed olive oil
7. Smoked sea salt
8. Smoked gouda
9. Autumn Harvest apple butter
[TRUNCATED]
```
[Download full output](/assembly/python-net/_output_files/developer-guide/advanced-usage/working-with-list-reports-numbered/numbered-list-in-text-document/generating_the_report/numbered-list-report.txt)
{{< /tab >}}
{{< /tabs >}}
