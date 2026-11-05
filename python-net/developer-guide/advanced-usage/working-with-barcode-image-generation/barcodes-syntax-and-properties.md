---
id: barcodes-syntax-and-properties
url: assembly/python-net/barcodes-syntax-and-properties
title: Barcodes Syntax and Properties
weight: 1
description: "Barcode tags in GroupDocs.Assembly for Python via .NET templates: the barcode types, scaling, bar height, colors, text, auto-correction and resolution, with DocumentAssembler.barcode_settings from Python."
keywords: barcode, barcode tag, QR code, CODE 128, EAN-13, barcode_settings, GroupDocs.Assembly, Python
productName: GroupDocs.Assembly for Python via .NET
hideChildren: False
aliases:
  - /assembly/python-net/barcode/
---
{{< alert style="info" >}}The examples read the shop data described in [The Business Layer]({{< ref "assembly/python-net/developer-guide/basic-usage/working-with-a-business-case/the-business-layer.md" >}}).{{< /alert >}}

## Inserting Barcodes Dynamically

You can insert barcode images to your documents dynamically using barcode tags. To declare a dynamically inserted barcode image within your template, perform the following steps:

1.  Add a textbox to your template at the place where you want a barcode image to be inserted.
2.  Set common image attributes such as size, rotation angle, and others for the textbox, making the textbox look like a barcode image without bars and text.
3.  Specify a barcode tag within the textbox using the following syntax:

```text
<<barcode [barcode_expression] -barcode_type>>
```

During run-time, an expression declared within a barcode tag is evaluated, its value is encoded using the specified barcode type, and the tag's containing textbox is filled with a corresponding barcode image. The tag itself is removed from the textbox then.

The following template puts the customer's code into a CODE 128 barcode and the shop's web address into a QR code, then adds a barcode for each of the customer's orders. A barcode tag works inside a data band like any other tag: each order gets its own textbox and barcode.

```text
<<[customer.CustomerName]>>
Customer code, CODE 128:
[textbox] <<barcode [customer.Barcode] -code128>>
Web site, QR code:
[textbox] <<barcode ["https://harborlane.example/"] -qr>>
Orders
<<foreach [o in customer.Order]>>Order <<[o.OrderNumber]>>: <<[o.Product.ProductName]>>
[textbox] <<barcode [o.Barcode] -code128>>
<</foreach>>
```

{{< tabs "example1" >}}
{{< tab "Python" >}}
```python
import json

from groupdocs.assembly import DataSourceInfo, DocumentAssembler

with open("customer.json", encoding="utf-8") as f:
    customer = json.load(f)

assembler = DocumentAssembler()
assembler.assemble_document("customer-barcodes.docx", "customer-barcodes-report.docx", DataSourceInfo(customer, "customer"))
```
{{< /tab >}}
{{< tab "customer-barcodes.docx" >}}
{{< tab-text >}}
The following sample file is used in this example: [customer-barcodes.docx](/assembly/python-net/_sample_files/developer-guide/advanced-usage/working-with-barcode-image-generation/barcodes-syntax-and-properties/customer-barcodes.docx)
{{< /tab-text >}}
{{< /tab >}}
{{< tab "customer.json" >}}
{{< tab-text >}}
The following sample file is used in this example: [customer.json](/assembly/python-net/_sample_files/developer-guide/advanced-usage/working-with-barcode-image-generation/barcodes-syntax-and-properties/customer.json)
{{< /tab-text >}}
{{< /tab >}}
{{< tab "customer-barcodes-report.docx" >}}  
```text
Binary file (DOCX, 17 KB)
```
[Download full output](/assembly/python-net/_output_files/developer-guide/advanced-usage/working-with-barcode-image-generation/barcodes-syntax-and-properties/inserting_barcodes_dynamically/customer-barcodes-report.docx)
{{< /tab >}}
{{< /tabs >}}

To specify a barcode type within a barcode tag, you can use one of the predefined identifiers described in the following table:

| Identifier | Description |
| --- | --- |
| codabar | CODABAR Barcode |
| code11 | CODE 11 barcode |
| code39S | Standard CODE 39 barcode |
| code39E | Extended CODE 39 barcode |
| code93S | Standard CODE 93 barcode |
| code93E | Extended CODE 93 barcode |
| code128 | CODE 128 barcode |
| code128GS1 | GS1 CODE 128 barcode specification. The barcode text must contain parentheses for AI |
| ean8 | EAN-8 barcode |
| ean13 | EAN-13 barcode |
| ean14 | EAN-14 barcode |
| scc14 | SCC-14 barcode |
| sscc18 | SSCC-18 barcode |
| upca | UPC-A barcode |
| upce | UPC-E barcode |
| isbn | ISBN barcode |
| issn | ISSN barcode |
| ismn | ISMN barcode |
| stf | Standard 2 of 5 barcode |
| itf | Interleaved 2 of 5 barcode |
| mtf | Matrix 2 of 5 barcode |
| ip25 | Italian Post 25 barcode |
| iatatf | IATA 2 of 5 barcode. IATA (International Air Transport Association) uses this barcode for the management of air cargo |
| itf14 | ITF14 barcode |
| itf6 | ITF-6 barcode |
| msi | MSI Plessey barcode |
| vin | VIN (Vehicle Identification Number) barcode |
| dpi | Deutschen Post barcode, also known as Identcode, CodeIdentcode, German Postal 2 of 5 Identcode, Deutsche Post AG Identcode, Deutsche Frachtpost Identcode, Deutsche Post AG (DHL) |
| dpl | Deutsche Post Leitcode barcode, also known as German Postal 2 of 5 Leitcode, CodeLeitcode, Leitcode, Deutsche Post AG (DHL) |
| opc | OPC (Optical Product Code) barcode, also known as VCA barcode, VCA OPC, Vision Council of America OPC barcode |
| pzn | PZN barcode, also known as Pharma Zentral Nummer, Pharmazentralnummer |
| code16K | Code 16K barcode |
| pharmacode | Represents Pharmacode barcode, also known as Code32 |
| dm | DataMatrix barcode |
| qr | QR Code barcode |
| aztec | Aztec barcode |
| pdf417 | Pdf417 barcode |
| macroPdf417 | MacroPdf417 barcode |
| dmGS1 | DataMatrix barcode with GS1 string format |
| microPdf417 | MicroPdf417 barcode |
| qrGS1 | QR barcode with GS1 string format |
| maxiCode | MaxiCode barcode |
| dotCode | DotCode barcode |
| ap | Australia Post Customer barcode |
| postnet | Postnet barcode |
| planet | Planet barcode |
| oneCode | USPS OneCode barcode |
| rm4scc | RM4SCC barcode. RM4SCC (Royal Mail 4-state Customer Code) is used for automated mail sort process in UK |
| databarOD | Databar omni-directional barcode |
| databarT | Databar truncated barcode |
| databarL | Databar limited barcode |
| databarE | Databar expanded barcode |
| databarES | Databar expanded stacked barcode |
| databarS | Databar stacked barcode |
| databarSOD | Databar stacked omni-directional barcode |
| sp | Singapore Post barcode |
| ape | Australian Post Domestic eParcel barcode |
| spp | Swiss Post Parcel barcode. Supported types: Domestic Mail, International Mail, Additional Services |
| patchCode | Patch code barcode |
| code32 | Code32 barcode |
| dltf | DataLogic 2 of 5 barcode |
| dkix | Dutch KIX barcode |
| codablockF | Codablock F barcode |
| codablockFGS1 | GS1 Codablock F barcode |
| code128GS1UPCA | GS1-128 AI 8102 Coupon Extended barcode |
| databarGS1UPCA | UPCA & GS1 Databar Coupon barcode |

### Scaling Barcode Symbols

You can scale barcode symbols of dynamically inserted barcode images specifying the scale attribute for a barcode tag as follows.

```text
<<barcode [barcode_expression] -barcode_type scale="scaling_hint">>
```

A scale attribute affects the width and height of a 2D barcode symbol and the width of a 1D barcode symbol. The value of a scale attribute represents the percent of barcode symbol scaling.

The value of a scale attribute, however, is just a hint. That is, actual scaling of a barcode symbol can be not precisely equal to the specified one. The reason is that scaling can damage a barcode symbol in a way it to become unreadable by barcode scanners. That is why, the engine calculates actual scaling not to bring such a damage trying to be as close to the specified scaling as possible at the same time.

A symbol scaled up needs a textbox large enough for it: the engine cuts the image at the textbox's edge.

### Configuring Initial Scaling of Barcode Symbols

You can affect initial scaling of all barcode symbols generated by a single `DocumentAssembler` instance through the `DocumentAssembler.barcode_settings.base_x_dimension` and `DocumentAssembler.barcode_settings.base_y_dimension` properties. These properties define the smallest width and height of the unit of barcode modules respectively. That is, for example, to make all barcode symbols twice larger by default, you can use the following code. A larger symbol needs a larger textbox, so the template of this example gives its CODE 128 barcode a textbox 440 points wide and its QR code one of 200 by 200 points:

```text
Customer code, CODE 128:
[textbox] <<barcode [customer.Barcode] -code128>>
Web site, QR code:
[textbox] <<barcode ["https://harborlane.example/"] -qr>>
```

{{< tabs "example2" >}}
{{< tab "Python" >}}
```python
import json

from groupdocs.assembly import DataSourceInfo, DocumentAssembler

with open("customer.json", encoding="utf-8") as f:
    customer = json.load(f)

assembler = DocumentAssembler()
assembler.barcode_settings.base_x_dimension *= 2
assembler.barcode_settings.base_y_dimension *= 2
assembler.assemble_document("barcode-base-size.docx", "barcode-base-size-report.docx", DataSourceInfo(customer, "customer"))
```
{{< /tab >}}
{{< tab "barcode-base-size.docx" >}}
{{< tab-text >}}
The following sample file is used in this example: [barcode-base-size.docx](/assembly/python-net/_sample_files/developer-guide/advanced-usage/working-with-barcode-image-generation/barcodes-syntax-and-properties/barcode-base-size.docx)
{{< /tab-text >}}
{{< /tab >}}
{{< tab "customer.json" >}}
{{< tab-text >}}
The following sample file is used in this example: [customer.json](/assembly/python-net/_sample_files/developer-guide/advanced-usage/working-with-barcode-image-generation/barcodes-syntax-and-properties/customer.json)
{{< /tab-text >}}
{{< /tab >}}
{{< tab "barcode-base-size-report.docx" >}}  
```text
Binary file (DOCX, 13 KB)
```
[Download full output](/assembly/python-net/_output_files/developer-guide/advanced-usage/working-with-barcode-image-generation/barcodes-syntax-and-properties/configuring_initial_scaling_of_barcode_symbols/barcode-base-size-report.docx)
{{< /tab >}}
{{< /tabs >}}

Values of the `base_x_dimension` and `base_y_dimension` properties are measured in units defined by the `DocumentAssembler.barcode_settings.graphics_unit` property. By default, they are 0.6 and 2, and `graphics_unit` is 6, the millimeter of the .NET `GraphicsUnit` enumeration.

{{< alert style="warning" >}}When the scale attribute is provided for a barcode tag, actual x- and y-dimensions are calculated by the engine as the corresponding percent of base x- and y-dimensions.{{< /alert >}}

### Setting Height of 1D Barcode Symbols

The height of a 1D barcode symbol is not affected by the scale attribute of the corresponding barcode tag. However, you can set the height applying the barHeight attribute as follows:

```text
<<barcode [barcode_expression] -barcode_type barHeight="height">>
```

The value of a barHeight attribute specifies the percent of the overall barcode image height. That is, for example, to set the height of a barcode symbol equal to two thirds of its overall barcode image height, you can use the following barcode tag:

```text
<<barcode ["736192"] -codabar barHeight="67">>
```

The following template shows the customer's code three times: at the default size, scaled to 200% in a textbox twice as wide, and with bars a third of the image high.

```text
Default size:
[textbox] <<barcode [customer.Barcode] -code128>>
Scaled to 200%:
[textbox] <<barcode [customer.Barcode] -code128 scale="200">>
Bars a third of the image height:
[textbox] <<barcode [customer.Barcode] -code128 barHeight="33">>
```

{{< tabs "example3" >}}
{{< tab "Python" >}}
```python
import json

from groupdocs.assembly import DataSourceInfo, DocumentAssembler

with open("customer.json", encoding="utf-8") as f:
    customer = json.load(f)

assembler = DocumentAssembler()
assembler.assemble_document("barcode-sizes.docx", "barcode-sizes-report.docx", DataSourceInfo(customer, "customer"))
```
{{< /tab >}}
{{< tab "barcode-sizes.docx" >}}
{{< tab-text >}}
The following sample file is used in this example: [barcode-sizes.docx](/assembly/python-net/_sample_files/developer-guide/advanced-usage/working-with-barcode-image-generation/barcodes-syntax-and-properties/barcode-sizes.docx)
{{< /tab-text >}}
{{< /tab >}}
{{< tab "customer.json" >}}
{{< tab-text >}}
The following sample file is used in this example: [customer.json](/assembly/python-net/_sample_files/developer-guide/advanced-usage/working-with-barcode-image-generation/barcodes-syntax-and-properties/customer.json)
{{< /tab-text >}}
{{< /tab >}}
{{< tab "barcode-sizes-report.docx" >}}  
```text
Binary file (DOCX, 13 KB)
```
[Download full output](/assembly/python-net/_output_files/developer-guide/advanced-usage/working-with-barcode-image-generation/barcodes-syntax-and-properties/setting_height_of_1d_barcode_symbols/barcode-sizes-report.docx)
{{< /tab >}}
{{< /tabs >}}

### Customizing Fore and Back Colors of Barcode Images

The fore color of a dynamically inserted barcode image is used to render the barcode's symbol and text. This color is derived from the font of the corresponding barcode tag. The background color of the image is derived from the solid fill of the textbox containing the tag.

### Customizing Font and Placement of Barcode Text

The font used to render barcode text of a dynamically inserted barcode image derives the following attributes from the font of the corresponding barcode tag:

*   Name
*   Size
*   Style (bold and italic)
*   Color

The placement of barcode text of a dynamically inserted barcode image – leftward, rightward, or centered – is defined by text alignment of the corresponding barcode tag.

### Using Barcode Text Auto-Correction

For a dynamically inserted barcode image, the engine automatically corrects barcode text that does not conform the barcode's specification, if possible. For example, it replaces the wrong check digit of an EAN-13 text with the right one.

{{< alert style="warning" >}}The auto-correction is not possible for barcodes of some types like Databar.{{< /alert >}}

To disable the auto-correction making the engine throw an exception in case of an invalid barcode text, you can set the `DocumentAssembler.barcode_settings.use_auto_correction` property to `False`. The exception reaches Python as a `RuntimeError`. With the auto-correction disabled, an EAN-13 barcode takes the 12 digits of the number without its check digit, which the engine computes: the following example fails on a 13-digit text and succeeds on the 12 digits. The template holds one tag:

```text
<<[product.ProductName]>>, EAN-13:
[textbox] <<barcode [product.Ean] -ean13>>
```

{{< tabs "example4" >}}
{{< tab "Python" >}}
```python
from groupdocs.assembly import DataSourceInfo, DocumentAssembler

assembler = DocumentAssembler()
assembler.barcode_settings.use_auto_correction = False

for ean in ("5012345678901", "501234567890"):
    product = {"ProductName": "Chestnut honey", "Ean": ean}
    try:
        assembler.assemble_document("product-ean.docx", "product-ean-report.docx", DataSourceInfo(product, "product"))
        print(ean, "assembled")
    except RuntimeError as e:
        print(ean, "rejected:", str(e).splitlines()[0])
```
{{< /tab >}}
{{< tab "product-ean.docx" >}}
{{< tab-text >}}
The following sample file is used in this example: [product-ean.docx](/assembly/python-net/_sample_files/developer-guide/advanced-usage/working-with-barcode-image-generation/barcodes-syntax-and-properties/product-ean.docx)
{{< /tab-text >}}
{{< /tab >}}
{{< tab "product-ean-report.docx" >}}  
```text
Binary file (DOCX, 10 KB)
```
[Download full output](/assembly/python-net/_output_files/developer-guide/advanced-usage/working-with-barcode-image-generation/barcodes-syntax-and-properties/using_barcode_text_auto_correction/product-ean-report.docx)
{{< /tab >}}
{{< /tabs >}}

### Setting Barcode Image Resolution

You can set horizontal and vertical resolution for dynamically inserted barcode images in DPI (dots per inch) using the `DocumentAssembler.barcode_settings.resolution` property. That is, for example, to set both horizontal and vertical resolution to 300 DPI, you can use the following code:

{{< tabs "example5" >}}
{{< tab "Python" >}}
```python
import json

from groupdocs.assembly import DataSourceInfo, DocumentAssembler

with open("customer.json", encoding="utf-8") as f:
    customer = json.load(f)

assembler = DocumentAssembler()
assembler.barcode_settings.resolution = 300
assembler.assemble_document("customer-barcodes.docx", "customer-barcodes-300-dpi.docx", DataSourceInfo(customer, "customer"))
```
{{< /tab >}}
{{< tab "customer-barcodes.docx" >}}
{{< tab-text >}}
The following sample file is used in this example: [customer-barcodes.docx](/assembly/python-net/_sample_files/developer-guide/advanced-usage/working-with-barcode-image-generation/barcodes-syntax-and-properties/customer-barcodes.docx)
{{< /tab-text >}}
{{< /tab >}}
{{< tab "customer.json" >}}
{{< tab-text >}}
The following sample file is used in this example: [customer.json](/assembly/python-net/_sample_files/developer-guide/advanced-usage/working-with-barcode-image-generation/barcodes-syntax-and-properties/customer.json)
{{< /tab-text >}}
{{< /tab >}}
{{< tab "customer-barcodes-300-dpi.docx" >}}  
```text
Binary file (DOCX, 30 KB)
```
[Download full output](/assembly/python-net/_output_files/developer-guide/advanced-usage/working-with-barcode-image-generation/barcodes-syntax-and-properties/setting_barcode_image_resolution/customer-barcodes-300-dpi.docx)
{{< /tab >}}
{{< /tabs >}}

{{< alert style="warning" >}}By default, horizontal and vertical resolution of dynamically inserted barcode images is 96 DPI. The `xresolution` and `yresolution` properties set each of them separately.{{< /alert >}}

### Example with Output

```text
<<barcode ["736192"] -codabar>>
```

The template of the following example holds this tag in a textbox. It reads no data, but `assemble_document` takes at least one data source, so the example passes the customer.

{{< tabs "example6" >}}
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
The following sample file is used in this example: [barcode.docx](/assembly/python-net/_sample_files/developer-guide/advanced-usage/working-with-barcode-image-generation/barcodes-syntax-and-properties/barcode.docx)
{{< /tab-text >}}
{{< /tab >}}
{{< tab "customer.json" >}}
{{< tab-text >}}
The following sample file is used in this example: [customer.json](/assembly/python-net/_sample_files/developer-guide/advanced-usage/working-with-barcode-image-generation/barcodes-syntax-and-properties/customer.json)
{{< /tab-text >}}
{{< /tab >}}
{{< tab "barcode-report.docx" >}}  
```text
Binary file (DOCX, 12 KB)
```
[Download full output](/assembly/python-net/_output_files/developer-guide/advanced-usage/working-with-barcode-image-generation/barcodes-syntax-and-properties/example_with_output/barcode-report.docx)
{{< /tab >}}
{{< /tabs >}}
