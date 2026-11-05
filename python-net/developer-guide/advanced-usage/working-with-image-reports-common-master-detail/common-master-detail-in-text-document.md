---
id: common-master-detail-in-text-document
url: assembly/python-net/common-master-detail-in-text-document
title: Common Master-Detail in Text Document
weight: 5
description: "Common Master-Detail in Text Document with GroupDocs.Assembly for Python via .NET: the template, the Python data and the code."
keywords: common master-detail in text document, GroupDocs.Assembly, Python, report generation
productName: GroupDocs.Assembly for Python via .NET
hideChildren: False
---
{{< alert style="info" >}}In this article, we will use GroupDocs.Assembly to generate a Common Master-Detail report in Text Document format.{{< /alert >}}

## Common Master-Detail in Text Document

### Reporting Requirement

As a report developer, you are required to represent the information of the customers and products with the following key requirements:

*   It must associate the customers with their products
*   Report must be generated in the HTML Document

### Adding Syntax to be evaluated by GroupDocs.Assembly Engine

```text
<<foreach [in customers]>><<[CustomerName()]>>
Products: <<foreach [in Order]>><<[indexOf() != 0 ? ", " : ""]>><<[Product.ProductName]>><</foreach>>
<</foreach>>
```

{{< alert style="success" >}}For detailed technical information about syntax, expressions and report generation by the engine, please visit: [Working with GroupDocs.Assembly Engine]({{< ref "assembly/python-net/developer-guide/basic-usage/working-with-groupdocs.assembly-engine/_index.md" >}}).{{< /alert >}}

### Download Common Master-Detail Template

Please download the sample Common master-detail document we created in this article:

*   [common-master-detail.txt](/assembly/python-net/_sample_files/developer-guide/advanced-usage/working-with-image-reports-common-master-detail/common-master-detail-in-text-document/common-master-detail.txt)

### Generating The Report

{{< alert style="info" >}}The example reads the shop data described in [The Business Layer]({{< ref "assembly/python-net/developer-guide/basic-usage/working-with-a-business-case/the-business-layer.md" >}}).{{< /alert >}}

{{< tabs "example1" >}}
{{< tab "Python" >}}
```python
import json

from groupdocs.assembly import DataSourceInfo, DocumentAssembler

with open("customers.json", encoding="utf-8") as f:
    customers = json.load(f)

assembler = DocumentAssembler()
assembler.assemble_document("common-master-detail.txt", "common-master-detail-report.txt", DataSourceInfo(customers, "customers"))
```
{{< /tab >}}
{{< tab "common-master-detail.txt" >}}
{{< tab-text >}}
The following sample file is used in this example: [common-master-detail.txt](/assembly/python-net/_sample_files/developer-guide/advanced-usage/working-with-image-reports-common-master-detail/common-master-detail-in-text-document/common-master-detail.txt)
{{< /tab-text >}}
{{< /tab >}}
{{< tab "customers.json" >}}
{{< tab-text >}}
The following sample file is used in this example: [customers.json](/assembly/python-net/_sample_files/developer-guide/advanced-usage/working-with-image-reports-common-master-detail/common-master-detail-in-text-document/customers.json)
{{< /tab-text >}}
{{< /tab >}}
{{< tab "common-master-detail-report.txt" >}}  
```text
Quayside Bistro
Products: Harbor Blend whole bean coffee, Aged harbour cheddar, Cold-pressed olive oil

Lantern Street Café
Products: Lighthouse Espresso beans, Oat and honey biscuits

Saltmarsh Deli
Products: Chestnut honey, Smoked gouda, Autumn Harvest apple butter

Pier Nine Kitchen
[TRUNCATED]
```
[Download full output](/assembly/python-net/_output_files/developer-guide/advanced-usage/working-with-image-reports-common-master-detail/common-master-detail-in-text-document/generating_the_report/common-master-detail-report.txt)
{{< /tab >}}
{{< /tabs >}}
