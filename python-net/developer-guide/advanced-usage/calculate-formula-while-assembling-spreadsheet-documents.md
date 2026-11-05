---
id: calculate-formula-while-assembling-spreadsheet-documents
url: assembly/python-net/calculate-formula-while-assembling-spreadsheet-documents
title: Calculate Formula while Assembling Spreadsheet Documents
weight: 31
description: "Calculate Formula while Assembling Spreadsheet Documents with GroupDocs.Assembly for Python via .NET: the template, the Python data and the code."
keywords: calculate formula while assembling spreadsheet documents, GroupDocs.Assembly, Python, report generation
productName: GroupDocs.Assembly for Python via .NET
hideChildren: False
---
{{< alert style="info" >}}The example reads the shop data described in [The Business Layer]({{< ref "assembly/python-net/developer-guide/basic-usage/working-with-a-business-case/the-business-layer.md" >}}).{{< /alert >}}

### The Recipe

*   Set up the source document template path
*   Set up destination report path
*   Instantiate DocumentAssembler class
*   Set options, [DocumentAssemblyOptions.UPDATE_FIELDS_AND_FORMULAS](https://reference.groupdocs.com/assembly/python-net/groupdocs.assembly/documentassemblyoptions/)
*   Generate report

### Download Template

Get the template from here.

*   [update-field.xlsx](/assembly/python-net/_sample_files/developer-guide/advanced-usage/calculate-formula-while-assembling-spreadsheet-documents/update-field.xlsx)

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
assembler.assemble_document("update-field.xlsx", "update-field-report.xlsx", DataSourceInfo(products, "product"))
```
{{< /tab >}}
{{< tab "update-field.xlsx" >}}
{{< tab-text >}}
The following sample file is used in this example: [update-field.xlsx](/assembly/python-net/_sample_files/developer-guide/advanced-usage/calculate-formula-while-assembling-spreadsheet-documents/update-field.xlsx)
{{< /tab-text >}}
{{< /tab >}}
{{< tab "products.json" >}}
{{< tab-text >}}
The following sample file is used in this example: [products.json](/assembly/python-net/_sample_files/developer-guide/advanced-usage/calculate-formula-while-assembling-spreadsheet-documents/products.json)
{{< /tab-text >}}
{{< /tab >}}
{{< tab "update-field-report.xlsx" >}}  
```text
Binary file (XLSX, 9 KB)
```
[Download full output](/assembly/python-net/_output_files/developer-guide/advanced-usage/calculate-formula-while-assembling-spreadsheet-documents/the_code/update-field-report.xlsx)
{{< /tab >}}
{{< /tabs >}}
