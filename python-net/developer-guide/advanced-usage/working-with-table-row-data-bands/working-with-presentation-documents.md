---
id: working-with-presentation-documents
url: assembly/python-net/working-with-presentation-documents
title: Working with Presentation Documents
weight: 3
description: "Working with Presentation Documents with GroupDocs.Assembly for Python via .NET: the template, the Python data and the code."
keywords: working with presentation documents, GroupDocs.Assembly, Python, report generation
productName: GroupDocs.Assembly for Python via .NET
hideChildren: False
---
{{< alert style="info" >}}The example reads the shop data described in [The Business Layer]({{< ref "assembly/python-net/developer-guide/basic-usage/working-with-a-business-case/the-business-layer.md" >}}).{{< /alert >}}

## Working with Presentation Documents

GroupDocs.Assembly allows you to use data bands in table rows in **Presentation**** Documents**. A table-row data band is a data band which body occupies single or multiple rows of a single document table. The body of such a band starts at the beginning of the first occupied row and ends at the end of the last occupied row as follows. The syntax for using data bands in presentation document is as follows:

<table class="gd-assembly">
	<tbody>
		<tr>
			<td>Manager</td>
			<td>Manager</td>
			<td>Contract Price</td>
		</tr>
		<tr>
			<td>&lt;&lt;foreach [c in ds]>>&lt;&lt;[c.Client]>></td>
			<td>&lt;&lt;[c.Manager]>></td>
			<td>&lt;&lt;[c.Price]>>&lt;&lt;/foreach>></td>
		</tr>
	</tbody>
</table>

### Working with Table-Row Conditional Blocks

You can also use a table-row conditional block which body occupies single or multiple rows of a single document table. The body of such a block (as well as the body of its every template option) starts at the beginning of the first occupied row and ends at the end of the last occupied row as follows:

|                        |         |                 |
| ---------------------- | ------- | --------------- |
| **&lt;&lt;if ...>> ...**     | **...** | **...**         |
| **...**                | **...** | **...**         |
| **&lt;&lt;elseif ...>> ...** | **...** | **...**         |
| **...**                | **...** | **...**         |
| **&lt;&lt;else>> ...**       | **...** | **...**         |
| **...**                | **...** | **...**         |
| **...**                | **...** | **... &lt;&lt;/if>>** |
|                        |         |                 |

### Download

#### Data Source Document

*   [data-table.pptx](/assembly/python-net/_sample_files/developer-guide/advanced-usage/working-with-table-row-data-bands/working-with-presentation-documents/data-table.pptx)

#### Template

### The Code

{{< tabs "example1" >}}
{{< tab "Python" >}}
```python
from groupdocs.assembly import DataSourceInfo, DocumentAssembler
from groupdocs.assembly.data import DocumentTable, DocumentTableOptions

options = DocumentTableOptions()
options.first_row_contains_column_names = True
table = DocumentTable("contracts.xlsx", 0, options)

assembler = DocumentAssembler()
assembler.assemble_document("data-table.pptx", "data-table-report.pptx", DataSourceInfo(table, "ds"))
```
{{< /tab >}}
{{< tab "data-table.pptx" >}}
{{< tab-text >}}
The following sample file is used in this example: [data-table.pptx](/assembly/python-net/_sample_files/developer-guide/advanced-usage/working-with-table-row-data-bands/working-with-presentation-documents/data-table.pptx)
{{< /tab-text >}}
{{< /tab >}}
{{< tab "contracts.xlsx" >}}
{{< tab-text >}}
The following sample file is used in this example: [contracts.xlsx](/assembly/python-net/_sample_files/developer-guide/advanced-usage/working-with-table-row-data-bands/working-with-presentation-documents/contracts.xlsx)
{{< /tab-text >}}
{{< /tab >}}
{{< tab "data-table-report.pptx" >}}  
```text
Binary file (PPTX, 37 KB)
```
[Download full output](/assembly/python-net/_output_files/developer-guide/advanced-usage/working-with-table-row-data-bands/working-with-presentation-documents/the_code/data-table-report.pptx)
{{< /tab >}}
{{< /tabs >}}
