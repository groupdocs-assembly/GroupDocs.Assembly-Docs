---
id: common-list-in-text-document
url: assembly/python-net/common-list-in-text-document
title: Common List in Text Document
weight: 5
description: "Common List in Text Document with GroupDocs.Assembly for Python via .NET: the template, the Python data and the code."
keywords: common list in text document, GroupDocs.Assembly, Python, report generation
productName: GroupDocs.Assembly for Python via .NET
hideChildren: False
---
{{< alert style="info" >}}In this article, we will use GroupDocs.Assembly to generate a Common List report in Text Document format.{{< /alert >}}{{< alert style="info" >}}The example reads the shop data described in [The Business Layer]({{< ref "assembly/python-net/developer-guide/basic-usage/working-with-a-business-case/the-business-layer.md" >}}).{{< /alert >}}

## Common List in Text Document

### Reporting Requirement

As a report developer, you are required to share the following key requirements:

*   The report must be generated in the Text Document format

### Adding Syntax to be evaluated by GroupDocs.Assembly Engine

```text
<<foreach [in customers]>><<[CustomerName]>>
<</foreach>>
```

### Download Common List Template

Please download the sample Common List document we created in this article:

*   [common-list.txt](/assembly/python-net/_sample_files/developer-guide/advanced-usage/working-with-image-reports-common-list/common-list-in-text-document/common-list.txt)

### Generating The Report

{{< tabs "example1" >}}
{{< tab "Python" >}}
```python
import json

from groupdocs.assembly import DataSourceInfo, DocumentAssembler

with open("customers.json", encoding="utf-8") as f:
    customers = json.load(f)

assembler = DocumentAssembler()
assembler.assemble_document("common-list.txt", "common-list-report.txt", DataSourceInfo(customers, "customers"))
```
{{< /tab >}}
{{< tab "common-list.txt" >}}
{{< tab-text >}}
The following sample file is used in this example: [common-list.txt](/assembly/python-net/_sample_files/developer-guide/advanced-usage/working-with-image-reports-common-list/common-list-in-text-document/common-list.txt)
{{< /tab-text >}}
{{< /tab >}}
{{< tab "customers.json" >}}
{{< tab-text >}}
The following sample file is used in this example: [customers.json](/assembly/python-net/_sample_files/developer-guide/advanced-usage/working-with-image-reports-common-list/common-list-in-text-document/customers.json)
{{< /tab-text >}}
{{< /tab >}}
{{< tab "common-list-report.txt" >}}  
```text
Quayside Bistro
Lantern Street Café
Saltmarsh Deli
Pier Nine Kitchen
```
[Download full output](/assembly/python-net/_output_files/developer-guide/advanced-usage/working-with-image-reports-common-list/common-list-in-text-document/generating_the_report/common-list-report.txt)
{{< /tab >}}
{{< /tabs >}}
