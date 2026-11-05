---
id: single-row-image-in-email-document
url: assembly/python-net/single-row-image-in-email-document
title: Single Row Image in Email Document
weight: 6
description: "Single Row Image in Email Document with GroupDocs.Assembly for Python via .NET: the template, the Python data and the code."
keywords: single row image in email document, GroupDocs.Assembly, Python, report generation
productName: GroupDocs.Assembly for Python via .NET
hideChildren: False
---
{{< alert style="info" >}}In this article, we will use GroupDocs.Assembly to generate a Single Row Image report in Email Document format.{{< /alert >}}

## Single Row Image in Email Document

### Reporting Requirement

As a report developer, you are required to represent information of first single manager with the following key requirements:

*   Report must be in .eml or .msg format
*   It must add email recipient, css and subject of the email
*   Report must show image of the manager
*   It must show Name and contact number of customer

### Adding Syntax to be evaluated by GroupDocs.Assembly Engine

```text
Name:	<<[customer.CustomerName]>>
Contact Number:	<<[customer.CustomerContactNumber]>>
```

### Download Single Row Image Template

Please download the sample template we created in this article:

*   [single-row.msg](/assembly/python-net/_sample_files/developer-guide/advanced-usage/working-with-image-reports-single-row/single-row-image-in-email-document/single-row.msg)

{{< alert style="success" >}}For detailed technical information about syntax,expressions and report generation by the engine, please visit: [Working with GroupDocs.Assembly Engine]({{< ref "assembly/python-net/developer-guide/basic-usage/working-with-groupdocs.assembly-engine/_index.md" >}}).{{< /alert >}}

### Generating The Report

{{< alert style="info" >}}The example reads the shop data described in [The Business Layer]({{< ref "assembly/python-net/developer-guide/basic-usage/working-with-a-business-case/the-business-layer.md" >}}).{{< /alert >}}

{{< tabs "example1" >}}
{{< tab "Python" >}}
```python
import json
from datetime import datetime

from groupdocs.assembly import DataSourceInfo, DocumentAssembler

def parse_dates(item):
    # JSON has no dates: turn the order dates into datetime objects for the template
    for key in ("OrderDate", "ShippingDate"):
        if key in item:
            item[key] = datetime.strptime(item[key], "%Y-%m-%dT%H:%M:%S")
    return item

with open("customer.json", encoding="utf-8") as f:
    customer = json.load(f, object_hook=parse_dates)

assembler = DocumentAssembler()
assembler.assemble_document("single-row.msg", "single-row-report.msg", [
    DataSourceInfo(customer, "customer"),
    DataSourceInfo("Harbor Lane Provisions <orders@harborlane.example>", "sender"),
    DataSourceInfo(["Quayside Bistro <orders@quaysidebistro.example>", "jonas.weber@harborlane.example"], "recipients"),
    DataSourceInfo("amara.osei@harborlane.example", "cc"),
    DataSourceInfo("Single row", "subject"),
])
```
{{< /tab >}}
{{< tab "single-row.msg" >}}
{{< tab-text >}}
The following sample file is used in this example: [single-row.msg](/assembly/python-net/_sample_files/developer-guide/advanced-usage/working-with-image-reports-single-row/single-row-image-in-email-document/single-row.msg)
{{< /tab-text >}}
{{< /tab >}}
{{< tab "customer.json" >}}
{{< tab-text >}}
The following sample file is used in this example: [customer.json](/assembly/python-net/_sample_files/developer-guide/advanced-usage/working-with-image-reports-single-row/single-row-image-in-email-document/customer.json)
{{< /tab-text >}}
{{< /tab >}}
{{< tab "single-row-report.msg" >}}  
```text
Binary file (MSG, 36 KB)
```
[Download full output](/assembly/python-net/_output_files/developer-guide/advanced-usage/working-with-image-reports-single-row/single-row-image-in-email-document/generating_the_report/single-row-report.msg)
{{< /tab >}}
{{< /tabs >}}
