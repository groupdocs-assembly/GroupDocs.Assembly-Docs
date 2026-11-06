---
id: bulleted-list-in-text-document
url: assembly/python-net/bulleted-list-in-text-document
title: Bulleted List in Text Document
weight: 5
description: "Bulleted List in Text Document with GroupDocs.Assembly for Python via .NET: the template, the Python data and the code."
keywords: bulleted list in text document, GroupDocs.Assembly, Python, report generation
productName: GroupDocs.Assembly for Python via .NET
hideChildren: False
---
{{< alert style="info" >}}In this article, we will use GroupDocs.Assembly to generate a Bulleted List report in Text Document format.{{< /alert >}}{{< alert style="info" >}}The example reads the shop data described in [The Business Layer]({{< ref "assembly/python-net/developer-guide/basic-usage/working-with-a-business-case/the-business-layer.md" >}}).{{< /alert >}}

## Bulleted List in Text Document

### Creating a Bulleted List

Practicing the following steps you can insert Bulleted List in a Text document.

1.  To add a bulleted list use • as a bullet for each element in the list.
2.  Save your Document.

### Reporting Requirement

As a report developer, you are required to share the following key requirements:

*   A report must show all the products in a bulleted list format.
*   A report must be generated in the Text Document format.

### Adding Syntax to be evaluated by GroupDocs.Assembly Engine

```text
We provide support for the following products:
<<foreach [in product]>>•	<<[ProductName]>>
<</foreach>>

```

{{< alert style="success" >}}For detailed technical information about syntax, expressions and report generation by the engine, please visit: [Working with GroupDocs.Assembly Engine]({{< ref "assembly/python-net/developer-guide/basic-usage/working-with-groupdocs.assembly-engine/_index.md" >}}).{{< /alert >}}

### Download Bulleted List Template

Please download the sample Bulleted List document we created in this article:

*   [bulleted-list.txt](/assembly/python-net/_sample_files/developer-guide/advanced-usage/working-with-list-reports-bulleted/bulleted-list-in-text-document/bulleted-list.txt)

### Generating The Report

{{< tabs "example1" >}}
{{< tab "Python" >}}
```python
import json

from groupdocs.assembly import DataSourceInfo, DocumentAssembler

with open("products.json", encoding="utf-8") as f:
    products = json.load(f)

assembler = DocumentAssembler()
assembler.assemble_document("bulleted-list.txt", "bulleted-list-report.txt", DataSourceInfo(products, "product"))
```
{{< /tab >}}
{{< tab "bulleted-list.txt" >}}
{{< tab-text >}}
The following sample file is used in this example: [bulleted-list.txt](/assembly/python-net/_sample_files/developer-guide/advanced-usage/working-with-list-reports-bulleted/bulleted-list-in-text-document/bulleted-list.txt)
{{< /tab-text >}}
{{< /tab >}}
{{< tab "products.json" >}}
{{< tab-text >}}
The following sample file is used in this example: [products.json](/assembly/python-net/_sample_files/developer-guide/advanced-usage/working-with-list-reports-bulleted/bulleted-list-in-text-document/products.json)
{{< /tab-text >}}
{{< /tab >}}
{{< tab "bulleted-list-report.txt" >}}  
```text
We provide support for the following products:
�	Harbor Blend whole bean coffee
�	Lighthouse Espresso beans
�	Aged harbour cheddar
�	Chestnut honey
�	Oat and honey biscuits
�	Cold-pressed olive oil
�	Smoked sea salt
�	Smoked gouda
�	Autumn Harvest apple butter
[TRUNCATED]
```
[Download full output](/assembly/python-net/_output_files/developer-guide/advanced-usage/working-with-list-reports-bulleted/bulleted-list-in-text-document/generating_the_report/bulleted-list-report.txt)
{{< /tab >}}
{{< /tabs >}}
