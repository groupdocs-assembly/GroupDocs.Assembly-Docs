---
id: updating-fields-while-assembling-word-processing-documents
url: assembly/python-net/updating-fields-while-assembling-word-processing-documents
title: Updating Fields while Assembling Word Processing Documents
weight: 30
description: "Updating Fields while Assembling Word Processing Documents with GroupDocs.Assembly for Python via .NET: the template, the Python data and the code."
keywords: updating fields while assembling word processing documents, GroupDocs.Assembly, Python, report generation
productName: GroupDocs.Assembly for Python via .NET
hideChildren: False
---
{{< alert style="info" >}}The example reads the shop data described in [The Business Layer]({{< ref "assembly/python-net/developer-guide/basic-usage/working-with-a-business-case/the-business-layer.md" >}}).{{< /alert >}}

### The Recipe

*   Set up the source document template path
*   Set up destination report path
*   Instantiate DocumentAssembler class
*   Set options, **[DocumentAssemblyOptions.UPDATE_FIELDS_AND_FORMULAS](https://reference.groupdocs.com/assembly/python-net/groupdocs.assembly/documentassemblyoptions/)**
*   Generate report

### Download Template

Get the template from here.

*   [update-field.docx](/assembly/python-net/_sample_files/developer-guide/advanced-usage/updating-fields-while-assembling-word-processing-documents/update-field.docx)

### The Code

{{< tabs "example1" >}}
{{< tab "Python" >}}
```python
import json

from groupdocs.assembly import DataSourceInfo, DocumentAssembler, DocumentAssemblyOptions

with open("products.json", encoding="utf-8") as f:
    products = json.load(f)

assembler = DocumentAssembler()
assembler.options = DocumentAssemblyOptions.UPDATE_FIELDS_AND_FORMULAS
assembler.assemble_document("update-field.docx", "update-field-report.docx", DataSourceInfo(products, "product"))
```
{{< /tab >}}
{{< tab "update-field.docx" >}}
{{< tab-text >}}
The following sample file is used in this example: [update-field.docx](/assembly/python-net/_sample_files/developer-guide/advanced-usage/updating-fields-while-assembling-word-processing-documents/update-field.docx)
{{< /tab-text >}}
{{< /tab >}}
{{< tab "products.json" >}}
{{< tab-text >}}
The following sample file is used in this example: [products.json](/assembly/python-net/_sample_files/developer-guide/advanced-usage/updating-fields-while-assembling-word-processing-documents/products.json)
{{< /tab-text >}}
{{< /tab >}}
{{< tab "update-field-report.docx" >}}  
```text
Binary file (DOCX, 11 KB)
```
[Download full output](/assembly/python-net/_output_files/developer-guide/advanced-usage/updating-fields-while-assembling-word-processing-documents/the_code/update-field-report.docx)
{{< /tab >}}
{{< /tabs >}}
