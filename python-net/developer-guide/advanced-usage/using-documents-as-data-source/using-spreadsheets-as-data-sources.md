---
id: using-spreadsheets-as-data-sources
url: assembly/python-net/using-spreadsheets-as-data-sources
title: Using Spreadsheets as Data Sources
weight: 1
description: "Using Spreadsheets as Data Sources with GroupDocs.Assembly for Python via .NET: the template, the Python data and the code."
keywords: using spreadsheets as data sources, GroupDocs.Assembly, Python, report generation
productName: GroupDocs.Assembly for Python via .NET
hideChildren: False
---
{{< alert style="info" >}}The example reads the shop data described in [The Business Layer]({{< ref "assembly/python-net/developer-guide/basic-usage/working-with-a-business-case/the-business-layer.md" >}}).{{< /alert >}}

## Using Spreadsheets as Data Sources

Following classes are added in [GroupDocs.Assembly.Data](https://reference.groupdocs.com/assembly/python-net/groupdocs.assembly.data/) namespace:

*   [DocumentTable](https://reference.groupdocs.com/assembly/python-net/groupdocs.assembly.data/documenttable/)
*   [DocumentTableColumn](https://reference.groupdocs.com/assembly/python-net/groupdocs.assembly.data/documenttablecolumn/)
*   [DocumentTableColumnCollection](https://reference.groupdocs.com/assembly/python-net/groupdocs.assembly.data/documenttablecolumncollection/)
*   [DocumentTableOptions](https://reference.groupdocs.com/assembly/python-net/groupdocs.assembly.data/documenttableoptions/)

## The Recipe

*   Define template and output report documents
*   Assemble a document using the external document table as a data source

### Download

#### Data Source Document

*   [table-row.docx](/assembly/python-net/_sample_files/developer-guide/advanced-usage/using-documents-as-data-source/using-spreadsheets-as-data-sources/table-row.docx)

#### Template

## The Code

{{< tabs "example1" >}}
{{< tab "Python" >}}
```python
from groupdocs.assembly import DataSourceInfo, DocumentAssembler
from groupdocs.assembly.data import DocumentTable, DocumentTableOptions

options = DocumentTableOptions()
options.first_row_contains_column_names = True
table = DocumentTable("contracts.xlsx", 0, options)

assembler = DocumentAssembler()
assembler.assemble_document("table-row.docx", "table-row-report.docx", DataSourceInfo(table, "contracts"))
```
{{< /tab >}}
{{< tab "table-row.docx" >}}
{{< tab-text >}}
The following sample file is used in this example: [table-row.docx](/assembly/python-net/_sample_files/developer-guide/advanced-usage/using-documents-as-data-source/using-spreadsheets-as-data-sources/table-row.docx)
{{< /tab-text >}}
{{< /tab >}}
{{< tab "contracts.xlsx" >}}
{{< tab-text >}}
The following sample file is used in this example: [contracts.xlsx](/assembly/python-net/_sample_files/developer-guide/advanced-usage/using-documents-as-data-source/using-spreadsheets-as-data-sources/contracts.xlsx)
{{< /tab-text >}}
{{< /tab >}}
{{< tab "table-row-report.docx" >}}  
```text
Binary file (DOCX, 10 KB)
```
[Download full output](/assembly/python-net/_output_files/developer-guide/advanced-usage/using-documents-as-data-source/using-spreadsheets-as-data-sources/the_code/table-row-report.docx)
{{< /tab >}}
{{< /tabs >}}
