---
id: changing-automatically-detected-types-of-documenttable-columns
url: assembly/python-net/changing-automatically-detected-types-of-documenttable-columns
title: Changing Automatically Detected Types of DocumentTable Columns
weight: 35
description: "Changing Automatically Detected Types of DocumentTable Columns with GroupDocs.Assembly for Python via .NET: the template, the Python data and the code."
keywords: changing automatically detected types of documenttable columns, GroupDocs.Assembly, Python, report generation
productName: GroupDocs.Assembly for Python via .NET
hideChildren: False
---
API provides the ability to change automatically detected types of DocumentTable columns. The **Type** property setter has been added to the [GroupDocs.Assembly.Data.DocumentTableColumn](https://reference.groupdocs.com/assembly/python-net/groupdocs.assembly.data/documenttablecolumn/) class.

Moreover, The **Relations** property of the [GroupDocs.Assembly.Data.DocumentTableSet](https://reference.groupdocs.com/assembly/python-net/groupdocs.assembly.data/documenttableset/) class has been added.

## Data Source Document

*   [changed-column-type.pptx](/assembly/python-net/_sample_files/developer-guide/advanced-usage/changing-automatically-detected-types-of-documenttable-columns/changed-column-type.pptx)

## Template

## Changing Document Table Column Type

{{< alert style="info" >}}The example reads the shop data described in [The Business Layer]({{< ref "assembly/python-net/developer-guide/basic-usage/working-with-a-business-case/the-business-layer.md" >}}).{{< /alert >}}

{{< tabs "example1" >}}
{{< tab "Python" >}}
```python
from groupdocs.assembly import DataSourceInfo, DocumentAssembler
from groupdocs.assembly.data import DocumentTable, DocumentTableOptions

options = DocumentTableOptions()
options.first_row_contains_column_names = True
table = DocumentTable("managers.docx", 1, options)
table.columns["Total_Contract_Price"].type = float

assembler = DocumentAssembler()
assembler.assemble_document("changed-column-type.pptx", "changed-column-type-report.pptx", DataSourceInfo(table, "Managers"))
```
{{< /tab >}}
{{< tab "changed-column-type.pptx" >}}
{{< tab-text >}}
The following sample file is used in this example: [changed-column-type.pptx](/assembly/python-net/_sample_files/developer-guide/advanced-usage/changing-automatically-detected-types-of-documenttable-columns/changed-column-type.pptx)
{{< /tab-text >}}
{{< /tab >}}
{{< tab "managers.docx" >}}
{{< tab-text >}}
The following sample file is used in this example: [managers.docx](/assembly/python-net/_sample_files/developer-guide/advanced-usage/changing-automatically-detected-types-of-documenttable-columns/managers.docx)
{{< /tab-text >}}
{{< /tab >}}
{{< tab "changed-column-type-report.pptx" >}}  
```text
Binary file (PPTX, 36 KB)
```
[Download full output](/assembly/python-net/_output_files/developer-guide/advanced-usage/changing-automatically-detected-types-of-documenttable-columns/changing_document_table_column_type/changed-column-type-report.pptx)
{{< /tab >}}
{{< /tabs >}}
