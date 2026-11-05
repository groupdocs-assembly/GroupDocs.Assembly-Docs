---
id: single-row-in-text-document
url: assembly/python-net/single-row-in-text-document
title: Single Row in Text Document
weight: 5
description: "Single Row in Text Document with GroupDocs.Assembly for Python via .NET: the template, the Python data and the code."
keywords: single row in text document, GroupDocs.Assembly, Python, report generation
productName: GroupDocs.Assembly for Python via .NET
hideChildren: False
---
{{< alert style="info" >}}In this article, we will use GroupDocs.Assembly to generate a Single Row report in Text Document format.{{< /alert >}}

## Single Row in Text Document

### Reporting Requirement

As a report developer, you are required to represent information of first single customer with the following key requirements:

*   It must show Name and Contact Number of the customer
*   Report must be generated in the Text Document

### Adding Syntax to be evaluated by GroupDocs.Assembly Engine

```text
Name:	<<[customer.CustomerName]>>
Contact Number:	<<[customer.CustomerContactNumber]>>
```

{{< alert style="success" >}}For detailed technical information about syntax, expressions and report generation by the engine, please visit: [Working with GroupDocs.Assembly Engine]({{< ref "assembly/python-net/developer-guide/basic-usage/working-with-groupdocs.assembly-engine/_index.md" >}}).{{< /alert >}}

### Download Single Row Image Template

Please download the single row image document we created in this article:

*   [single-row.txt](/assembly/python-net/_sample_files/developer-guide/advanced-usage/working-with-image-reports-single-row/single-row-in-text-document/single-row.txt)

### Generating The Report

{{< alert style="info" >}}The example reads the shop data described in [The Business Layer]({{< ref "assembly/python-net/developer-guide/basic-usage/working-with-a-business-case/the-business-layer.md" >}}).{{< /alert >}}

{{< tabs "example1" >}}
{{< tab "Python" >}}
```python
import json

from groupdocs.assembly import DataSourceInfo, DocumentAssembler

with open("customer.json", encoding="utf-8") as f:
    customer = json.load(f)

assembler = DocumentAssembler()
assembler.assemble_document("single-row.txt", "single-row-report.txt", DataSourceInfo(customer, "customer"))
```
{{< /tab >}}
{{< tab "single-row.txt" >}}
{{< tab-text >}}
The following sample file is used in this example: [single-row.txt](/assembly/python-net/_sample_files/developer-guide/advanced-usage/working-with-image-reports-single-row/single-row-in-text-document/single-row.txt)
{{< /tab-text >}}
{{< /tab >}}
{{< tab "customer.json" >}}
{{< tab-text >}}
The following sample file is used in this example: [customer.json](/assembly/python-net/_sample_files/developer-guide/advanced-usage/working-with-image-reports-single-row/single-row-in-text-document/customer.json)
{{< /tab-text >}}
{{< /tab >}}
{{< tab "single-row-report.txt" >}}  
```text
Name:	Quayside Bistro
Age:	+1 555 0142 811
```
[Download full output](/assembly/python-net/_output_files/developer-guide/advanced-usage/working-with-image-reports-single-row/single-row-in-text-document/generating_the_report/single-row-report.txt)
{{< /tab >}}
{{< /tabs >}}
