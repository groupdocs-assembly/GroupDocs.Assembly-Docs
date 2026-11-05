---
id: using-tables-of-word-processing-documents-as-data-sources
url: assembly/python-net/using-tables-of-word-processing-documents-as-data-sources
title: Using Tables of Word Processing Documents as Data Sources
weight: 3
description: "Using Tables of Word Processing Documents as Data Sources with GroupDocs.Assembly for Python via .NET: the template, the Python data and the code."
keywords: using tables of word processing documents as data sources, GroupDocs.Assembly, Python, report generation
productName: GroupDocs.Assembly for Python via .NET
hideChildren: False
---
{{< alert style="info" >}}The example reads the shop data described in [The Business Layer]({{< ref "assembly/python-net/developer-guide/basic-usage/working-with-a-business-case/the-business-layer.md" >}}).{{< /alert >}}

## Using Tables of Word Processing Documents as Data Sources

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

*   [importing-word-processing-table-into-presentation.pptx](/assembly/python-net/_sample_files/developer-guide/advanced-usage/using-documents-as-data-source/using-tables-of-word-processing-documents-as-data-sources/importing-word-processing-table-into-presentation.pptx)

#### Template

## The Code

{{< tabs "example1" >}}
{{< tab "Python" >}}
```python
from groupdocs.assembly import DataSourceInfo, DocumentAssembler
from groupdocs.assembly.data import DocumentTable, DocumentTableOptions

options = DocumentTableOptions()
options.max_row_index = 3
table = DocumentTable("managers.docx", 1, options)

assembler = DocumentAssembler()
assembler.assemble_document("importing-word-processing-table-into-presentation.pptx", "importing-word-processing-table-into-presentation-report.pptx", DataSourceInfo(table, "table"))
```
{{< /tab >}}
{{< tab "importing-word-processing-table-into-presentation.pptx" >}}
{{< tab-text >}}
The following sample file is used in this example: [importing-word-processing-table-into-presentation.pptx](/assembly/python-net/_sample_files/developer-guide/advanced-usage/using-documents-as-data-source/using-tables-of-word-processing-documents-as-data-sources/importing-word-processing-table-into-presentation.pptx)
{{< /tab-text >}}
{{< /tab >}}
{{< tab "managers.docx" >}}
{{< tab-text >}}
The following sample file is used in this example: [managers.docx](/assembly/python-net/_sample_files/developer-guide/advanced-usage/using-documents-as-data-source/using-tables-of-word-processing-documents-as-data-sources/managers.docx)
{{< /tab-text >}}
{{< /tab >}}
{{< tab "importing-word-processing-table-into-presentation-report.pptx" >}}  
```text
Binary file (PPTX, 34 KB)
```
[Download full output](/assembly/python-net/_output_files/developer-guide/advanced-usage/using-documents-as-data-source/using-tables-of-word-processing-documents-as-data-sources/the_code/importing-word-processing-table-into-presentation-report.pptx)
{{< /tab >}}
{{< /tabs >}}
