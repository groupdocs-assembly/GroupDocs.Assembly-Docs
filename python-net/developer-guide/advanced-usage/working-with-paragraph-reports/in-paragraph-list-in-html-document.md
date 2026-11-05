---
id: in-paragraph-list-in-html-document
url: assembly/python-net/in-paragraph-list-in-html-document
title: In-Paragraph List in HTML Document
weight: 4
description: "In-Paragraph List in HTML Document with GroupDocs.Assembly for Python via .NET: the template, the Python data and the code."
keywords: in-paragraph list in html document, GroupDocs.Assembly, Python, report generation
productName: GroupDocs.Assembly for Python via .NET
hideChildren: False
---
{{< alert style="info" >}}In this article, we will use GroupDocs.Assembly to generate a In-Paragraph List report in HTML Document format.{{< /alert >}}

## In-Paragraph List in HTML Document

### Reporting Requirement

As a report developer, you are required to describe the services you are providing with the following key requirements:

*   A descriptive or informative line like "We provide support for the following products:".
*   Show all the products along with the above sentence.
*   Report must be generated in the HTML Document.

### Adding Syntax to be evaluated by GroupDocs.Assembly Engine

```text
We provide support for the following products: <<foreach [in products]>>
<<[indexOf() != 0 ? ", " : ""]>><<[ProductName]>><</foreach>>
```

{{< alert style="success" >}}For detailed technical information about syntax, expressions and report generation by the engine, please visit: [Working with GroupDocs.Assembly Engine]({{< ref "assembly/python-net/developer-guide/basic-usage/working-with-groupdocs.assembly-engine/_index.md" >}}).{{< /alert >}}

### Download In-Paragraph List Template

Please download the sample Common List document we created in this article:

*   [in-paragraph-list.html](/assembly/python-net/_sample_files/developer-guide/advanced-usage/working-with-paragraph-reports/in-paragraph-list-in-html-document/in-paragraph-list.html)

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
assembler.assemble_document("in-paragraph-list.html", "in-paragraph-list-report.html", DataSourceInfo(products, "products"))
```
{{< /tab >}}
{{< tab "in-paragraph-list.html" >}}
{{< tab-text >}}
The following sample file is used in this example: [in-paragraph-list.html](/assembly/python-net/_sample_files/developer-guide/advanced-usage/working-with-paragraph-reports/in-paragraph-list-in-html-document/in-paragraph-list.html)
{{< /tab-text >}}
{{< /tab >}}
{{< tab "products.json" >}}
{{< tab-text >}}
The following sample file is used in this example: [products.json](/assembly/python-net/_sample_files/developer-guide/advanced-usage/working-with-paragraph-reports/in-paragraph-list-in-html-document/products.json)
{{< /tab-text >}}
{{< /tab >}}
{{< tab "in-paragraph-list-report.html" >}}  
```text
<html>
<body>
We provide support for the following products: Harbor Blend whole bean coffee, Lighthouse Espresso beans, Aged harbour cheddar, Chestnut honey, Oat and honey biscuits, Cold-pressed olive oil, Smoked sea salt, Smoked gouda, Autumn Harvest apple butter, Autumn Harvest spiced roast
</body>
</html>
```
[Download full output](/assembly/python-net/_output_files/developer-guide/advanced-usage/working-with-paragraph-reports/in-paragraph-list-in-html-document/generating_the_report/in-paragraph-list-report.html)
{{< /tab >}}
{{< /tabs >}}
