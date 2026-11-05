---
id: defining-relations-between-documenttable-instances-loaded-from-a-single-document
url: assembly/python-net/defining-relations-between-documenttable-instances-loaded-from-a-single-document
title: Defining Relations Between DocumentTable Instances Loaded from a Single Document
weight: 34
description: "Defining Relations Between DocumentTable Instances Loaded from a Single Document with GroupDocs.Assembly for Python via .NET: the template, the Python data and the code."
keywords: defining relations between documenttable instances loaded from a single document, GroupDocs.Assembly, Python, report generation
productName: GroupDocs.Assembly for Python via .NET
hideChildren: False
---
## Define Relations Between Document Table Instances

API provides ability to define relations between [DocumentTable](https://reference.groupdocs.com/assembly/python-net/groupdocs.assembly.data/documenttable/) instances loaded from a single document. The following classes of the [GroupDocs.Assembly.Data](https://reference.groupdocs.com/assembly/python-net/groupdocs.assembly.data/) namespace have been added:

*   [DocumentTableRelation](https://reference.groupdocs.com/assembly/python-net/groupdocs.assembly.data/documenttablerelation/)
*   [DocumentTableRelationCollection](https://reference.groupdocs.com/assembly/python-net/groupdocs.assembly.data/documenttablerelationcollection/)

Moreover, the **Relations** property of the [GroupDocs.Assembly.Data.DocumentTableSet](https://reference.groupdocs.com/assembly/python-net/groupdocs.assembly.data/documenttableset/) class has been added.

### Data Source Document

*   [table-relations.docx](/assembly/python-net/_sample_files/developer-guide/advanced-usage/defining-relations-between-documenttable-instances-loaded-from-a-single-document/table-relations.docx)

### Template

## Using Document Table Relations

{{< alert style="info" >}}The example reads the shop data described in [The Business Layer]({{< ref "assembly/python-net/developer-guide/basic-usage/working-with-a-business-case/the-business-layer.md" >}}).{{< /alert >}}

{{< tabs "example1" >}}
{{< tab "Python" >}}
```python
from groupdocs.assembly import DataSourceInfo, DocumentAssembler
from groupdocs.assembly.data import DocumentTableOptions, DocumentTableSet

def load_table(args):
    # The first row of every table holds its column names
    options = DocumentTableOptions()
    options.first_row_contains_column_names = True
    args.options = options

tables = DocumentTableSet("related-tables.xlsx", load_table)
tables.relations.add(tables.tables["CLIENT"].columns["ID"], tables.tables["CONTRACT"].columns["CLIENT_ID"])
tables.relations.add(tables.tables["MANAGER"].columns["ID"], tables.tables["CONTRACT"].columns["MANAGER_ID"])

assembler = DocumentAssembler()
assembler.assemble_document("table-relations.docx", "table-relations-report.docx", DataSourceInfo(tables))
```
{{< /tab >}}
{{< tab "table-relations.docx" >}}
{{< tab-text >}}
The following sample file is used in this example: [table-relations.docx](/assembly/python-net/_sample_files/developer-guide/advanced-usage/defining-relations-between-documenttable-instances-loaded-from-a-single-document/table-relations.docx)
{{< /tab-text >}}
{{< /tab >}}
{{< tab "related-tables.xlsx" >}}
{{< tab-text >}}
The following sample file is used in this example: [related-tables.xlsx](/assembly/python-net/_sample_files/developer-guide/advanced-usage/defining-relations-between-documenttable-instances-loaded-from-a-single-document/related-tables.xlsx)
{{< /tab-text >}}
{{< /tab >}}
{{< tab "table-relations-report.docx" >}}  
```text
Binary file (DOCX, 10 KB)
```
[Download full output](/assembly/python-net/_output_files/developer-guide/advanced-usage/defining-relations-between-documenttable-instances-loaded-from-a-single-document/using_document_table_relations/table-relations-report.docx)
{{< /tab >}}
{{< /tabs >}}
