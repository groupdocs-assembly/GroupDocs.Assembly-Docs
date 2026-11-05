---
id: barcode-image-generation-in-spreadsheet-document
url: assembly/python-net/barcode-image-generation-in-spreadsheet-document
title: Barcode Image Generation in Spreadsheet Document
weight: 3
description: "Barcode Image Generation in Spreadsheet Document with GroupDocs.Assembly for Python via .NET: the template, the Python data and the code."
keywords: barcode image generation in spreadsheet document, GroupDocs.Assembly, Python, report generation
productName: GroupDocs.Assembly for Python via .NET
hideChildren: False
---
{{< alert style="info" >}}The example reads the shop data described in [The Business Layer]({{< ref "assembly/python-net/developer-guide/basic-usage/working-with-a-business-case/the-business-layer.md" >}}).{{< /alert >}}

## Barcode Generation in Microsoft Spreadsheet

### Template Syntax

*   Add a textbox to your template at the place where you want a barcode image to be inserted.
*   Add the following syntax:

```text
<<barcode [customer.Barcode] -qr>>
```

{{< alert style="success" >}}For detailed technical information about syntax, expressions and report generation by the engine, please visit: [Working with GroupDocs.Assembly Engine]({{< ref "assembly/python-net/developer-guide/basic-usage/working-with-groupdocs.assembly-engine/_index.md" >}}){{< /alert >}}

### Download Template

Get the template from here.

*   [barcode.xlsx](/assembly/python-net/_sample_files/developer-guide/advanced-usage/working-with-barcode-image-generation/barcode-image-generation-in-spreadsheet-document/barcode.xlsx)

### The Code

{{< alert style="warning" >}}On Linux, a QR code needs the workbook's default font (its Normal style font) installed. This sample template is set in Arial, which `ttf-mscorefonts-installer` provides; a template set in Calibri, the Excel default, needs Calibri itself. Without the font the QR code cannot be drawn: the call raises `Value cannot be null. (Parameter 'trueTypeFont')`, and a substitute font such as Carlito is not used. See [System Requirements]({{< ref "assembly/python-net/getting-started/system-requirements.md" >}}).{{< /alert >}}

{{< tabs "example1" >}}
{{< tab "Python" >}}
```python
import json

from groupdocs.assembly import DataSourceInfo, DocumentAssembler

with open("customer.json", encoding="utf-8") as f:
    customer = json.load(f)

assembler = DocumentAssembler()
assembler.assemble_document("barcode.xlsx", "barcode-report.xlsx", DataSourceInfo(customer, "customer"))
```
{{< /tab >}}
{{< tab "barcode.xlsx" >}}
{{< tab-text >}}
The following sample file is used in this example: [barcode.xlsx](/assembly/python-net/_sample_files/developer-guide/advanced-usage/working-with-barcode-image-generation/barcode-image-generation-in-spreadsheet-document/barcode.xlsx)
{{< /tab-text >}}
{{< /tab >}}
{{< tab "customer.json" >}}
{{< tab-text >}}
The following sample file is used in this example: [customer.json](/assembly/python-net/_sample_files/developer-guide/advanced-usage/working-with-barcode-image-generation/barcode-image-generation-in-spreadsheet-document/customer.json)
{{< /tab-text >}}
{{< /tab >}}
{{< tab "barcode-report.xlsx" >}}  
```text
Binary file (XLSX, 13 KB)
```
[Download full output](/assembly/python-net/_output_files/developer-guide/advanced-usage/working-with-barcode-image-generation/barcode-image-generation-in-spreadsheet-document/the_code/barcode-report.xlsx)
{{< /tab >}}
{{< /tabs >}}
