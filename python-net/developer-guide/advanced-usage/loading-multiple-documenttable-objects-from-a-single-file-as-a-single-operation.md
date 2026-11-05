---
id: loading-multiple-documenttable-objects-from-a-single-file-as-a-single-operation
url: assembly/python-net/loading-multiple-documenttable-objects-from-a-single-file-as-a-single-operation
title: Loading Multiple DocumentTable Objects from a Single File as a Single Operation
weight: 33
description: "Loading Multiple DocumentTable Objects from a Single File as a Single Operation with GroupDocs.Assembly for Python via .NET: the template, the Python data and the code."
keywords: loading multiple documenttable objects from a single file as a single operation, GroupDocs.Assembly, Python, report generation
productName: GroupDocs.Assembly for Python via .NET
hideChildren: False
---
{{< alert style="info" >}}The example reads the shop data described in [The Business Layer]({{< ref "assembly/python-net/developer-guide/basic-usage/working-with-a-business-case/the-business-layer.md" >}}).{{< /alert >}}

## Loading Multiple DocumentTable Objects

GroupDocs.Assembly for Python via .NET API provides the ability to load multiple DocumentTable objects from a single file as a single operation. Following classes and interfaces of the [GroupDocs.Assembly.Data](https://reference.groupdocs.com/assembly/python-net/groupdocs.assembly.data/) namespace have been added:

*   [DocumentTableSet](https://reference.groupdocs.com/assembly/python-net/groupdocs.assembly.data/documenttableset/)
*   [DocumentTableCollection](https://reference.groupdocs.com/assembly/python-net/groupdocs.assembly.data/documenttablecollection/)
*   [IDocumentTableLoadHandler](https://reference.groupdocs.com/assembly/python-net/groupdocs.assembly.data/idocumenttableloadhandler/)
*   [DocumentTableLoadArgs.](https://reference.groupdocs.com/assembly/python-net/groupdocs.assembly.data/documenttableloadargs/)

Moreover, following properties of the [GroupDocs.Assembly.Data.DocumentTable](https://reference.groupdocs.com/assembly/python-net/groupdocs.assembly.data/documenttable/) class have been added:

*   Name
*   IndexInDocument

### Data Source Document

*   [several-tables.pptx](/assembly/python-net/_sample_files/developer-guide/advanced-usage/loading-multiple-documenttable-objects-from-a-single-file-as-a-single-operation/several-tables.pptx)

### Template

## Loading DocumentTableSet using Default Options

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

tables = DocumentTableSet("multiple-tables.docx", load_table)
tables.tables[0].name = "Planets"
tables.tables[1].name = "Persons"
tables.tables[2].name = "Companies"

assembler = DocumentAssembler()
assembler.assemble_document("several-tables.pptx", "several-tables-report.pptx", DataSourceInfo(tables))
```
{{< /tab >}}
{{< tab "several-tables.pptx" >}}
{{< tab-text >}}
The following sample file is used in this example: [several-tables.pptx](/assembly/python-net/_sample_files/developer-guide/advanced-usage/loading-multiple-documenttable-objects-from-a-single-file-as-a-single-operation/several-tables.pptx)
{{< /tab-text >}}
{{< /tab >}}
{{< tab "multiple-tables.docx" >}}
{{< tab-text >}}
The following sample file is used in this example: [multiple-tables.docx](/assembly/python-net/_sample_files/developer-guide/advanced-usage/loading-multiple-documenttable-objects-from-a-single-file-as-a-single-operation/multiple-tables.docx)
{{< /tab-text >}}
{{< /tab >}}
{{< tab "several-tables-report.pptx" >}}  
```text
Binary file (PPTX, 36 KB)
```
[Download full output](/assembly/python-net/_output_files/developer-guide/advanced-usage/loading-multiple-documenttable-objects-from-a-single-file-as-a-single-operation/loading_documenttableset_using_default_options/several-tables-report.pptx)
{{< /tab >}}
{{< /tabs >}}
