---
id: barcode-image-generation-in-word-processing-document
url: assembly/python-net/barcode-image-generation-in-word-processing-document
title: Barcode Image Generation in Word Processing Document
weight: 2
description: "Barcode Image Generation in Word Processing Document with GroupDocs.Assembly for Python via .NET: the template, the Python data and the code."
keywords: barcode image generation in word processing document, GroupDocs.Assembly, Python, report generation
productName: GroupDocs.Assembly for Python via .NET
hideChildren: False
---
{{< alert style="info" >}}The example reads the shop data described in [The Business Layer]({{< ref "assembly/python-net/developer-guide/basic-usage/working-with-a-business-case/the-business-layer.md" >}}).{{< /alert >}}

## Barcode Generation in Microsoft Word

### Template Syntax

*   Add a textbox to your template at the place where you want a barcode image to be inserted.
*   Add the following syntax:

```text
<<barcode [customer.Barcode] -codabar>>
```

{{< alert style="success" >}}For detailed technical information about syntax, expressions and report generation by the engine, please visit: [Working with GroupDocs.Assembly Engine]({{< ref "assembly/python-net/developer-guide/basic-usage/working-with-groupdocs.assembly-engine/_index.md" >}}){{< /alert >}}

### Download Template

Get the template from here.

*   [barcode.docx](/assembly/python-net/_sample_files/developer-guide/advanced-usage/working-with-barcode-image-generation/barcode-image-generation-in-word-processing-document/barcode.docx)

### The Code

{{< tabs "example1" >}}
{{< tab "Python" >}}
```python
import json

from groupdocs.assembly import DataSourceInfo, DocumentAssembler

with open("customer.json", encoding="utf-8") as f:
    customer = json.load(f)

assembler = DocumentAssembler()
assembler.assemble_document("barcode.docx", "barcode-report.docx", DataSourceInfo(customer, "customer"))
```
{{< /tab >}}
{{< tab "barcode.docx" >}}
{{< tab-text >}}
The following sample file is used in this example: [barcode.docx](/assembly/python-net/_sample_files/developer-guide/advanced-usage/working-with-barcode-image-generation/barcode-image-generation-in-word-processing-document/barcode.docx)
{{< /tab-text >}}
{{< /tab >}}
{{< tab "customer.json" >}}
{{< tab-text >}}
The following sample file is used in this example: [customer.json](/assembly/python-net/_sample_files/developer-guide/advanced-usage/working-with-barcode-image-generation/barcode-image-generation-in-word-processing-document/customer.json)
{{< /tab-text >}}
{{< /tab >}}
{{< tab "barcode-report.docx" >}}  
```text
Binary file (DOCX, 12 KB)
```
[Download full output](/assembly/python-net/_output_files/developer-guide/advanced-usage/working-with-barcode-image-generation/barcode-image-generation-in-word-processing-document/the_code/barcode-report.docx)
{{< /tab >}}
{{< /tabs >}}
