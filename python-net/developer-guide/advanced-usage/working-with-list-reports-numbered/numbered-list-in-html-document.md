---
id: numbered-list-in-html-document
url: assembly/python-net/numbered-list-in-html-document
title: Numbered List in HTML Document
weight: 4
description: "Numbered List in HTML Document with GroupDocs.Assembly for Python via .NET: the template, the Python data and the code."
keywords: numbered list in html document, GroupDocs.Assembly, Python, report generation
productName: GroupDocs.Assembly for Python via .NET
hideChildren: False
---
{{< alert style="info" >}}In this article, we will use GroupDocs.Assembly to generate a Numbered List report in HTML Document format.{{< /alert >}}{{< alert style="info" >}}The example reads the shop data described in [The Business Layer]({{< ref "assembly/python-net/developer-guide/basic-usage/working-with-a-business-case/the-business-layer.md" >}}).{{< /alert >}}

## Numbered List in HTML Document

### Reporting Requirement

As a report developer, you are required to describe the services you are providing with the following key requirements:

*   The report must show the products in numbered list.
*   The report must be generated in the HTML Document.

### Adding Syntax to be evaluated by GroupDocs.Assembly Engine

```html
We provide support for the following products:
<ol>
&lt;&lt;foreach [in products]&gt;&gt;
<li>&lt;&lt;[ProductName]&gt;&gt;</li>
&lt;&lt;/foreach&gt;&gt;
</ol>
```

{{< alert style="success" >}}For detailed technical information about syntax, expressions and report generation by the engine, please visit: [Working with GroupDocs.Assembly Engine]({{< ref "assembly/python-net/developer-guide/basic-usage/working-with-groupdocs.assembly-engine/_index.md" >}}).{{< /alert >}}

### Download Numbered List Template

Please download the sample Numbered List document we created in this article:

*   [numbered-list.html](/assembly/python-net/_sample_files/developer-guide/advanced-usage/working-with-list-reports-numbered/numbered-list-in-html-document/numbered-list.html)

### Generating The Report

{{< tabs "example1" >}}
{{< tab "Python" >}}
```python
import json

from groupdocs.assembly import DataSourceInfo, DocumentAssembler

with open("products.json", encoding="utf-8") as f:
    products = json.load(f)

assembler = DocumentAssembler()
assembler.assemble_document("numbered-list.html", "numbered-list-report.html", DataSourceInfo(products, "products"))
```
{{< /tab >}}
{{< tab "numbered-list.html" >}}
{{< tab-text >}}
The following sample file is used in this example: [numbered-list.html](/assembly/python-net/_sample_files/developer-guide/advanced-usage/working-with-list-reports-numbered/numbered-list-in-html-document/numbered-list.html)
{{< /tab-text >}}
{{< /tab >}}
{{< tab "products.json" >}}
{{< tab-text >}}
The following sample file is used in this example: [products.json](/assembly/python-net/_sample_files/developer-guide/advanced-usage/working-with-list-reports-numbered/numbered-list-in-html-document/products.json)
{{< /tab-text >}}
{{< /tab >}}
{{< tab "numbered-list-report.html" >}}  
```text
<html>
<body>
We provide support for the following products:
<ol>

<li>Harbor Blend whole bean coffee</li>

<li>Lighthouse Espresso beans</li>

<li>Aged harbour cheddar</li>
[TRUNCATED]
```
[Download full output](/assembly/python-net/_output_files/developer-guide/advanced-usage/working-with-list-reports-numbered/numbered-list-in-html-document/generating_the_report/numbered-list-report.html)
{{< /tab >}}
{{< /tabs >}}
