---
id: single-row-image-in-html-document
url: assembly/python-net/single-row-image-in-html-document
title: Single Row Image in HTML Document
weight: 4
description: "Single Row Image in HTML Document with GroupDocs.Assembly for Python via .NET: the template, the Python data and the code."
keywords: single row image in html document, GroupDocs.Assembly, Python, report generation
productName: GroupDocs.Assembly for Python via .NET
hideChildren: False
---
{{< alert style="info" >}}In this article, we will use GroupDocs.Assembly to generate a Single Row Image report in HTML Document format.{{< /alert >}}

## Single Row Image in HTML Document

### Reporting Requirement

As a report developer, you are required to represent information of first single customer with the following key requirements:

*   Report must show image of the customer
*   It must show Name and Contact Number of the customer
*   Report must be generated in the Presentation Document.

### Adding Syntax to be evaluated by GroupDocs.Assembly Engine

```html
<table>
<tr>
<td>
<img height="100" width="100" src="data:image/jpeg;base64,&lt;&lt;[customer.Photo]&gt;&gt;"/>
</td>
<td>
<table>
<tr>
<td>
<b>Name:</b>
</td>
<td>
<b>&lt;&lt;[customer.CustomerName]&gt;&gt;</b>  
</td>
</tr>
<tr>
<td>
<b>Contact Number:</b>
</td>
<td>
&lt;&lt;[customer.CustomerContactNumber]&gt;&gt;
</td>
</tr>
</table>
```

{{< alert style="success" >}}For detailed technical information about syntax, expressions and report generation by the engine, please visit: [Working with GroupDocs.Assembly Engine]({{< ref "assembly/python-net/developer-guide/basic-usage/working-with-groupdocs.assembly-engine/_index.md" >}}).{{< /alert >}}

### Download Single Row Image Template

Please download the single row image document we created in this article:

*   [single-row.html](/assembly/python-net/_sample_files/developer-guide/advanced-usage/working-with-image-reports-single-row/single-row-image-in-html-document/single-row.html)

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
assembler.assemble_document("single-row.html", "single-row-report.html", DataSourceInfo(customer, "customer"))
```
{{< /tab >}}
{{< tab "single-row.html" >}}
{{< tab-text >}}
The following sample file is used in this example: [single-row.html](/assembly/python-net/_sample_files/developer-guide/advanced-usage/working-with-image-reports-single-row/single-row-image-in-html-document/single-row.html)
{{< /tab-text >}}
{{< /tab >}}
{{< tab "customer.json" >}}
{{< tab-text >}}
The following sample file is used in this example: [customer.json](/assembly/python-net/_sample_files/developer-guide/advanced-usage/working-with-image-reports-single-row/single-row-image-in-html-document/customer.json)
{{< /tab-text >}}
{{< /tab >}}
{{< tab "pictures" >}}
{{< tab-text >}}
The following sample files are used in this example: [quayside-bistro.png](/assembly/python-net/_sample_files/developer-guide/advanced-usage/working-with-image-reports-single-row/single-row-image-in-html-document/quayside-bistro.png), [lantern-street-cafe.png](/assembly/python-net/_sample_files/developer-guide/advanced-usage/working-with-image-reports-single-row/single-row-image-in-html-document/lantern-street-cafe.png), [saltmarsh-deli.png](/assembly/python-net/_sample_files/developer-guide/advanced-usage/working-with-image-reports-single-row/single-row-image-in-html-document/saltmarsh-deli.png), [pier-nine-kitchen.png](/assembly/python-net/_sample_files/developer-guide/advanced-usage/working-with-image-reports-single-row/single-row-image-in-html-document/pier-nine-kitchen.png)
{{< /tab-text >}}
{{< /tab >}}
{{< tab "single-row-report.html" >}}  
```text
<html>
<body>
<table>
<tr>
<td>
<img height="100" width="100" src="data:image/jpeg;base64,quayside-bistro.png"/>
</td>
<td>
<table>
<tr>
[TRUNCATED]
```
[Download full output](/assembly/python-net/_output_files/developer-guide/advanced-usage/working-with-image-reports-single-row/single-row-image-in-html-document/generating_the_report/single-row-report.html)
{{< /tab >}}
{{< /tabs >}}
