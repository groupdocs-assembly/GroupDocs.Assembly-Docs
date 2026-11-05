---
id: common-list-image-in-email-document
url: assembly/python-net/common-list-image-in-email-document
title: Common List Image in Email Document
weight: 6
description: "Common List Image in Email Document with GroupDocs.Assembly for Python via .NET: the template, the Python data and the code."
keywords: common list image in email document, GroupDocs.Assembly, Python, report generation
productName: GroupDocs.Assembly for Python via .NET
hideChildren: False
---
{{< alert style="info" >}}In this article, we will use GroupDocs.Assembly to generate a Common List report in Email Document format.{{< /alert >}}{{< alert style="info" >}}The example reads the shop data described in [The Business Layer]({{< ref "assembly/python-net/developer-guide/basic-usage/working-with-a-business-case/the-business-layer.md" >}}).{{< /alert >}}

## Common List in Email Document

### Reporting Requirement

As a report developer, you are required to share the following key requirements:

*   A report must be in .eml or .msg format
*   It must add email recipient, CSS and subject of the email
*   A report must show multiple customers' name

### Adding Syntax to be evaluated by GroupDocs.Assembly Engine

```text
<<foreach [in customers]>><<[CustomerName]>>
<</foreach>>
```

{{< alert style="success" >}}For detailed technical information about syntax, expressions and report generation by the engine, please visit: [Working with GroupDocs.Assembly Engine]({{< ref "assembly/python-net/developer-guide/basic-usage/working-with-groupdocs.assembly-engine/_index.md" >}}).{{< /alert >}}

Download Common List Template

Please download the sample Common List document we used in this article:

*   [common-list.msg](/assembly/python-net/_sample_files/developer-guide/advanced-usage/working-with-image-reports-common-list/common-list-image-in-email-document/common-list.msg)

### Generating The Report

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

with open("customers.json", encoding="utf-8") as f:
    customers = json.load(f, object_hook=parse_dates)

assembler = DocumentAssembler()
assembler.assemble_document("common-list.msg", "common-list-report.msg", [
    DataSourceInfo(customers, "customers"),
    DataSourceInfo("Harbor Lane Provisions <orders@harborlane.example>", "sender"),
    DataSourceInfo(["Quayside Bistro <orders@quaysidebistro.example>", "jonas.weber@harborlane.example"], "recipients"),
    DataSourceInfo("amara.osei@harborlane.example", "cc"),
    DataSourceInfo("Common list", "subject"),
])
```
{{< /tab >}}
{{< tab "common-list.msg" >}}
{{< tab-text >}}
The following sample file is used in this example: [common-list.msg](/assembly/python-net/_sample_files/developer-guide/advanced-usage/working-with-image-reports-common-list/common-list-image-in-email-document/common-list.msg)
{{< /tab-text >}}
{{< /tab >}}
{{< tab "customers.json" >}}
{{< tab-text >}}
The following sample file is used in this example: [customers.json](/assembly/python-net/_sample_files/developer-guide/advanced-usage/working-with-image-reports-common-list/common-list-image-in-email-document/customers.json)
{{< /tab-text >}}
{{< /tab >}}
{{< tab "common-list-report.msg" >}}  
```text
Binary file (MSG, 34 KB)
```
[Download full output](/assembly/python-net/_output_files/developer-guide/advanced-usage/working-with-image-reports-common-list/common-list-image-in-email-document/generating_the_report/common-list-report.msg)
{{< /tab >}}
{{< /tabs >}}
