---
id: barcode-image-generation-in-presentation-document
url: assembly/python-net/barcode-image-generation-in-presentation-document
title: Barcode Image Generation in Presentation Document
weight: 4
description: "Barcode Image Generation in Presentation Document with GroupDocs.Assembly for Python via .NET: the template, the Python data and the code."
keywords: barcode image generation in presentation document, GroupDocs.Assembly, Python, report generation
productName: GroupDocs.Assembly for Python via .NET
hideChildren: False
---
{{< alert style="info" >}}The example reads the shop data described in [The Business Layer]({{< ref "assembly/python-net/developer-guide/basic-usage/working-with-a-business-case/the-business-layer.md" >}}).{{< /alert >}}

## Barcode Generation in Microsoft PowerPoint

### Template Syntax

*   Add a textbox to your template at the place where you want a barcode image to be inserted.
*   Add the following syntax:

```text
<<barcode [customer.Barcode] -codabar>>
```

{{< alert style="success" >}}For detailed technical information about syntax, expressions and report generation by the engine, please visit: [Working with GroupDocs.Assembly Engine]({{< ref "assembly/python-net/developer-guide/basic-usage/working-with-groupdocs.assembly-engine/_index.md" >}}){{< /alert >}}

### Download Template

Get the template from here.

*   [barcode.pptx](/assembly/python-net/_sample_files/developer-guide/advanced-usage/working-with-barcode-image-generation/barcode-image-generation-in-presentation-document/barcode.pptx)

### The Code

{{< tabs "example1" >}}
{{< tab "Python" >}}
```python
import json

from groupdocs.assembly import DataSourceInfo, DocumentAssembler

with open("customer.json", encoding="utf-8") as f:
    customer = json.load(f)

assembler = DocumentAssembler()
assembler.assemble_document("barcode.pptx", "barcode-report.pptx", DataSourceInfo(customer, "customer"))
```
{{< /tab >}}
{{< tab "barcode.pptx" >}}
{{< tab-text >}}
The following sample file is used in this example: [barcode.pptx](/assembly/python-net/_sample_files/developer-guide/advanced-usage/working-with-barcode-image-generation/barcode-image-generation-in-presentation-document/barcode.pptx)
{{< /tab-text >}}
{{< /tab >}}
{{< tab "customer.json" >}}
{{< tab-text >}}
The following sample file is used in this example: [customer.json](/assembly/python-net/_sample_files/developer-guide/advanced-usage/working-with-barcode-image-generation/barcode-image-generation-in-presentation-document/customer.json)
{{< /tab-text >}}
{{< /tab >}}
{{< tab "barcode-report.pptx" >}}  
```text
Binary file (PPTX, 35 KB)
```
[Download full output](/assembly/python-net/_output_files/developer-guide/advanced-usage/working-with-barcode-image-generation/barcode-image-generation-in-presentation-document/the_code/barcode-report.pptx)
{{< /tab >}}
{{< /tabs >}}
