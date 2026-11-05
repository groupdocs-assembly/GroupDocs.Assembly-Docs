---
id: common-list-image-in-html-document
url: assembly/python-net/common-list-image-in-html-document
title: Common List Image in HTML Document
weight: 4
description: "Common List Image in HTML Document with GroupDocs.Assembly for Python via .NET: the template, the Python data and the code."
keywords: common list image in html document, GroupDocs.Assembly, Python, report generation
productName: GroupDocs.Assembly for Python via .NET
hideChildren: False
---
{{< alert style="info" >}}In this article, we will use GroupDocs.Assembly to generate a Common List report in HTML Document format.{{< /alert >}}{{< alert style="info" >}}The example reads the shop data described in [The Business Layer]({{< ref "assembly/python-net/developer-guide/basic-usage/working-with-a-business-case/the-business-layer.md" >}}).{{< /alert >}}

## Common List in HTML Document

### Reporting Requirement

As a report developer, you are required to share the following key requirements:

*   A report must show multiple customers' picture and name.
*   A report must be generated in the HTML Document format.

### Adding Syntax to be evaluated by GroupDocs.Assembly Engine

<img src="/assembly/net/images/common-list-image-word-processing-document.png" alt="common-list-image-word-processing-document" style="width:230px"/>

### Download Common List Template

Please download the sample Common List document we created in this article:

*   [common-list.html](/assembly/python-net/_sample_files/developer-guide/advanced-usage/working-with-image-reports-common-list/common-list-image-in-html-document/common-list.html)

### Generating The Report

{{< tabs "example1" >}}
{{< tab "Python" >}}
```python
import json

from groupdocs.assembly import DataSourceInfo, DocumentAssembler

with open("customers.json", encoding="utf-8") as f:
    customers = json.load(f)

assembler = DocumentAssembler()
assembler.assemble_document("common-list.html", "common-list-report.html", DataSourceInfo(customers, "customers"))
```
{{< /tab >}}
{{< tab "common-list.html" >}}
{{< tab-text >}}
The following sample file is used in this example: [common-list.html](/assembly/python-net/_sample_files/developer-guide/advanced-usage/working-with-image-reports-common-list/common-list-image-in-html-document/common-list.html)
{{< /tab-text >}}
{{< /tab >}}
{{< tab "customers.json" >}}
{{< tab-text >}}
The following sample file is used in this example: [customers.json](/assembly/python-net/_sample_files/developer-guide/advanced-usage/working-with-image-reports-common-list/common-list-image-in-html-document/customers.json)
{{< /tab-text >}}
{{< /tab >}}
{{< tab "pictures" >}}
{{< tab-text >}}
The following sample files are used in this example: [quayside-bistro.png](/assembly/python-net/_sample_files/developer-guide/advanced-usage/working-with-image-reports-common-list/common-list-image-in-html-document/quayside-bistro.png), [lantern-street-cafe.png](/assembly/python-net/_sample_files/developer-guide/advanced-usage/working-with-image-reports-common-list/common-list-image-in-html-document/lantern-street-cafe.png), [saltmarsh-deli.png](/assembly/python-net/_sample_files/developer-guide/advanced-usage/working-with-image-reports-common-list/common-list-image-in-html-document/saltmarsh-deli.png), [pier-nine-kitchen.png](/assembly/python-net/_sample_files/developer-guide/advanced-usage/working-with-image-reports-common-list/common-list-image-in-html-document/pier-nine-kitchen.png)
{{< /tab-text >}}
{{< /tab >}}
{{< tab "common-list-report.html" >}}  
```text
<html>
<body>

<img height="100" width="100" src="data:image/jpeg;base64,quayside-bistro.png"/>
<h2>Quayside Bistro</h2>

<img height="100" width="100" src="data:image/jpeg;base64,lantern-street-cafe.png"/>
<h2>Lantern Street Café</h2>

<img height="100" width="100" src="data:image/jpeg;base64,saltmarsh-deli.png"/>
[TRUNCATED]
```
[Download full output](/assembly/python-net/_output_files/developer-guide/advanced-usage/working-with-image-reports-common-list/common-list-image-in-html-document/generating_the_report/common-list-report.html)
{{< /tab >}}
{{< /tabs >}}
