---
id: bulleted-list-in-html-document
url: assembly/python-net/bulleted-list-in-html-document
title: Bulleted List in HTML Document
weight: 4
description: "Bulleted List in HTML Document with GroupDocs.Assembly for Python via .NET: the template, the Python data and the code."
keywords: bulleted list in html document, GroupDocs.Assembly, Python, report generation
productName: GroupDocs.Assembly for Python via .NET
hideChildren: False
---
{{< alert style="info" >}}In this article, we will use GroupDocs.Assembly to generate a Bulleted List report in HTML Document format.{{< /alert >}}{{< alert style="info" >}}The example reads the shop data described in [The Business Layer]({{< ref "assembly/python-net/developer-guide/basic-usage/working-with-a-business-case/the-business-layer.md" >}}).{{< /alert >}}

## Bulleted List in HTML Document

### Creating a Bulleted List

Practising the following steps you can insert Bulleted List in an HTML document.

1.  To add a bulleted list start and end your list with `<ul></ul>` tag and list all the elements by enclosing them between `<li></li>` tag.
2.  Save your Document.

### Reporting Requirement

As a report developer, you are required to share the following key requirements:

*   A report must show all the products in a bulleted list format.
*   A report must be generated in the HTML Document.

### Adding Syntax to be evaluated by GroupDocs.Assembly Engine

```html
We provide support for the following products:
<ul>
&lt;&lt;foreach [in product]&gt;&gt;
<li>&lt;&lt;[ProductName]&gt;&gt;</li>
&lt;&lt;/foreach&gt;&gt;
</ul>
```

{{< alert style="success" >}}For detailed technical information about syntax, expressions and report generation by the engine, please visit: [Working with GroupDocs.Assembly Engine]({{< ref "assembly/python-net/developer-guide/basic-usage/working-with-groupdocs.assembly-engine/_index.md" >}}).{{< /alert >}}

### Download Bulleted List Template

Please download the sample Bulleted List document we created in this article:

*   [bulleted-list.html](/assembly/python-net/_sample_files/developer-guide/advanced-usage/working-with-list-reports-bulleted/bulleted-list-in-html-document/bulleted-list.html)

### Generating The Report

{{< tabs "example1" >}}
{{< tab "Python" >}}
```python
import json

from groupdocs.assembly import DataSourceInfo, DocumentAssembler

with open("products.json", encoding="utf-8") as f:
    products = json.load(f)

assembler = DocumentAssembler()
assembler.assemble_document("bulleted-list.html", "bulleted-list-report.html", DataSourceInfo(products, "product"))
```
{{< /tab >}}
{{< tab "bulleted-list.html" >}}
{{< tab-text >}}
The following sample file is used in this example: [bulleted-list.html](/assembly/python-net/_sample_files/developer-guide/advanced-usage/working-with-list-reports-bulleted/bulleted-list-in-html-document/bulleted-list.html)
{{< /tab-text >}}
{{< /tab >}}
{{< tab "products.json" >}}
{{< tab-text >}}
The following sample file is used in this example: [products.json](/assembly/python-net/_sample_files/developer-guide/advanced-usage/working-with-list-reports-bulleted/bulleted-list-in-html-document/products.json)
{{< /tab-text >}}
{{< /tab >}}
{{< tab "bulleted-list-report.html" >}}  
```text
<html>
<body>
We provide support for the following products:
<ul>

<li>Harbor Blend whole bean coffee</li>

<li>Lighthouse Espresso beans</li>

<li>Aged harbour cheddar</li>
[TRUNCATED]
```
[Download full output](/assembly/python-net/_output_files/developer-guide/advanced-usage/working-with-list-reports-bulleted/bulleted-list-in-html-document/generating_the_report/bulleted-list-report.html)
{{< /tab >}}
{{< /tabs >}}
