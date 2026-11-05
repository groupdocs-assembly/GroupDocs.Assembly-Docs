---
id: using-tables-of-presentation-documents-as-data-sources
url: assembly/python-net/using-tables-of-presentation-documents-as-data-sources
title: Using Tables of Presentation Documents as Data Sources
weight: 2
description: "Using Tables of Presentation Documents as Data Sources with GroupDocs.Assembly for Python via .NET: the template, the Python data and the code."
keywords: using tables of presentation documents as data sources, GroupDocs.Assembly, Python, report generation
productName: GroupDocs.Assembly for Python via .NET
hideChildren: False
---
{{< alert style="info" >}}The example reads the shop data described in [The Business Layer]({{< ref "assembly/python-net/developer-guide/basic-usage/working-with-a-business-case/the-business-layer.md" >}}).{{< /alert >}}

## Using Tables of Presentation Documents as Data Sources

Following classes are added in **[GroupDocs.Assembly.Data](https://reference.groupdocs.com/assembly/python-net/groupdocs.assembly.data/)** namespace:

*   [DocumentTable](https://reference.groupdocs.com/assembly/python-net/groupdocs.assembly.data/documenttable/)
*   [DocumentTableColumn](https://reference.groupdocs.com/assembly/python-net/groupdocs.assembly.data/documenttablecolumn/)
*   [DocumentTableColumnCollection](https://reference.groupdocs.com/assembly/python-net/groupdocs.assembly.data/documenttablecolumncollection/)
*   [DocumentTableOptions](https://reference.groupdocs.com/assembly/python-net/groupdocs.assembly.data/documenttableoptions/)

## The Recipe

*   Define template and output report documents
*   Assemble a document using the external document table as a data source

### Download

#### Data Source Document

*   [table-row.pptx](/assembly/python-net/_sample_files/developer-guide/advanced-usage/using-documents-as-data-source/using-tables-of-presentation-documents-as-data-sources/table-row.pptx)

#### Template

## The Code

{{< tabs "example1" >}}
{{< tab "Python" >}}
```python
from groupdocs.assembly import DataSourceInfo, DocumentAssembler
from groupdocs.assembly.data import DocumentTable, DocumentTableOptions

options = DocumentTableOptions()
options.max_row_index = 3
table = DocumentTable("managers.pptx", 1, options)

assembler = DocumentAssembler()
assembler.assemble_document("table-row.pptx", "table-row-report.pptx", DataSourceInfo(table, "table"))
```
{{< /tab >}}
{{< tab "table-row.pptx" >}}
{{< tab-text >}}
The following sample file is used in this example: [table-row.pptx](/assembly/python-net/_sample_files/developer-guide/advanced-usage/using-documents-as-data-source/using-tables-of-presentation-documents-as-data-sources/table-row.pptx)
{{< /tab-text >}}
{{< /tab >}}
{{< tab "managers.pptx" >}}
{{< tab-text >}}
The following sample file is used in this example: [managers.pptx](/assembly/python-net/_sample_files/developer-guide/advanced-usage/using-documents-as-data-source/using-tables-of-presentation-documents-as-data-sources/managers.pptx)
{{< /tab-text >}}
{{< /tab >}}
{{< tab "table-row-report.pptx" >}}  
```text
Binary file (PPTX, 34 KB)
```
[Download full output](/assembly/python-net/_output_files/developer-guide/advanced-usage/using-documents-as-data-source/using-tables-of-presentation-documents-as-data-sources/the_code/table-row-report.pptx)
{{< /tab >}}
{{< /tabs >}}
