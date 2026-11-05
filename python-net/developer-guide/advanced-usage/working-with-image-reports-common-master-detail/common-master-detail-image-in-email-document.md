---
id: common-master-detail-image-in-email-document
url: assembly/python-net/common-master-detail-image-in-email-document
title: Common Master-Detail Image in Email Document
weight: 6
description: "Common Master-Detail Image in Email Document with GroupDocs.Assembly for Python via .NET: the template, the Python data and the code."
keywords: common master-detail image in email document, GroupDocs.Assembly, Python, report generation
productName: GroupDocs.Assembly for Python via .NET
hideChildren: False
---
{{< alert style="info" >}}In this article, we will use GroupDocs.Assembly to generate a Common Master-Detail report in Email Document format.{{< /alert >}}

## Common Master-Detail in Email Document

### Creating a Common Master-Detail

Please follow below steps to create Common Master-Detail Template in MS Outlook 2013:

1.  Create a new Email.
2.  Insert two shapes, one for holding image and other for holding other details.
3.  Save the Email.

### Reporting Requirement

As a report developer, you are required to represent the information of the managers and clients with the following key requirements:

*   Report must be in .eml or .msg format.
*   It must add email recipient, css and subject of the email.
*   Report must show customer's name.
*   It must associate the customers with their products.

### Adding Syntax to be evaluated by GroupDocs.Assembly Engine

```text
<<foreach [in customers]>>Customer:
<<[CustomerName]>>
Products: <<foreach [in
Order]>><<[IndexOf() != 0 ? ", " : ""]>><<[Product.ProductName]>><</foreach>>
<</foreach>>
```

{{< alert style="success" >}}For detailed technical information about syntax,expressions and report generation by the engine, please visit: [Working with GroupDocs.Assembly Engine]({{< ref "assembly/python-net/developer-guide/basic-usage/working-with-groupdocs.assembly-engine/_index.md" >}}).{{< /alert >}}

### Download Common Master-Detail Template

Please download the sample Common Master-Detail document we created in this article:

*   [common-master-detail.msg](/assembly/python-net/_sample_files/developer-guide/advanced-usage/working-with-image-reports-common-master-detail/common-master-detail-image-in-email-document/common-master-detail.msg)

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

with open("customers.json", encoding="utf-8") as f:
    customers = json.load(f, object_hook=parse_dates)

assembler = DocumentAssembler()
assembler.assemble_document("common-master-detail.msg", "common-master-detail-report.msg", [
    DataSourceInfo(customers, "customers"),
    DataSourceInfo("Harbor Lane Provisions <orders@harborlane.example>", "sender"),
    DataSourceInfo(["Quayside Bistro <orders@quaysidebistro.example>", "jonas.weber@harborlane.example"], "recipients"),
    DataSourceInfo("amara.osei@harborlane.example", "cc"),
    DataSourceInfo("Common master detail", "subject"),
])
```
{{< /tab >}}
{{< tab "common-master-detail.msg" >}}
{{< tab-text >}}
The following sample file is used in this example: [common-master-detail.msg](/assembly/python-net/_sample_files/developer-guide/advanced-usage/working-with-image-reports-common-master-detail/common-master-detail-image-in-email-document/common-master-detail.msg)
{{< /tab-text >}}
{{< /tab >}}
{{< tab "customers.json" >}}
{{< tab-text >}}
The following sample file is used in this example: [customers.json](/assembly/python-net/_sample_files/developer-guide/advanced-usage/working-with-image-reports-common-master-detail/common-master-detail-image-in-email-document/customers.json)
{{< /tab-text >}}
{{< /tab >}}
{{< tab "common-master-detail-report.msg" >}}  
```text
Binary file (MSG, 39 KB)
```
[Download full output](/assembly/python-net/_output_files/developer-guide/advanced-usage/working-with-image-reports-common-master-detail/common-master-detail-image-in-email-document/generating_the_report/common-master-detail-report.msg)
{{< /tab >}}
{{< /tabs >}}
