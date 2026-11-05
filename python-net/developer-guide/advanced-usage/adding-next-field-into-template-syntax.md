---
id: adding-next-field-into-template-syntax
url: assembly/python-net/adding-next-field-into-template-syntax
title: Adding NEXT Field into Template Syntax
weight: 32
description: "Adding NEXT Field into Template Syntax with GroupDocs.Assembly for Python via .NET: the template, the Python data and the code."
keywords: adding next field into template syntax, GroupDocs.Assembly, Python, report generation
productName: GroupDocs.Assembly for Python via .NET
hideChildren: False
---
{{< alert style="info" >}}The example reads the shop data described in [The Business Layer]({{< ref "assembly/python-net/developer-guide/basic-usage/working-with-a-business-case/the-business-layer.md" >}}).{{< /alert >}}

## Adding Syntax to be evaluated by GroupDocs.Assembly Engine

**Template Syntax**

```text
We provide support for the following products:
. <<foreach [in products]>><<next>><<[ProductName]>>
<</foreach>>
```

## The Recipe

*   Set up the source document template path
*   Set up destination report path
*   Instantiate [DocumentAssembler](https://reference.groupdocs.com/assembly/python-net/groupdocs.assembly/documentassembler/) class
*   Generate report

### Download Template

Get the template from here.

*   [next-field.docx](/assembly/python-net/_sample_files/developer-guide/advanced-usage/adding-next-field-into-template-syntax/next-field.docx)

### The Code

{{< tabs "example1" >}}
{{< tab "Python" >}}
```python
import json

from groupdocs.assembly import DataSourceInfo, DocumentAssembler

with open("products.json", encoding="utf-8") as f:
    products = json.load(f)

assembler = DocumentAssembler()
assembler.assemble_document("next-field.docx", "next-field-report.docx", DataSourceInfo(products, "product"))
```
{{< /tab >}}
{{< tab "next-field.docx" >}}
{{< tab-text >}}
The following sample file is used in this example: [next-field.docx](/assembly/python-net/_sample_files/developer-guide/advanced-usage/adding-next-field-into-template-syntax/next-field.docx)
{{< /tab-text >}}
{{< /tab >}}
{{< tab "products.json" >}}
{{< tab-text >}}
The following sample file is used in this example: [products.json](/assembly/python-net/_sample_files/developer-guide/advanced-usage/adding-next-field-into-template-syntax/products.json)
{{< /tab-text >}}
{{< /tab >}}
{{< tab "next-field-report.docx" >}}  
```text
Binary file (DOCX, 11 KB)
```
[Download full output](/assembly/python-net/_output_files/developer-guide/advanced-usage/adding-next-field-into-template-syntax/the_code/next-field-report.docx)
{{< /tab >}}
{{< /tabs >}}
