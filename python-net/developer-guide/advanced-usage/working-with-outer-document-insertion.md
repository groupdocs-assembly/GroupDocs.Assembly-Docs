---
id: working-with-outer-document-insertion
url: assembly/python-net/working-with-outer-document-insertion
title: Working with Outer Document Insertion
weight: 28
description: "Working with Outer Document Insertion with GroupDocs.Assembly for Python via .NET: the template, the Python data and the code."
keywords: working with outer document insertion, GroupDocs.Assembly, Python, report generation
productName: GroupDocs.Assembly for Python via .NET
hideChildren: False
---
{{< alert style="info" >}}The example reads the shop data described in [The Business Layer]({{< ref "assembly/python-net/developer-guide/basic-usage/working-with-a-business-case/the-business-layer.md" >}}).{{< /alert >}}

## Inserting Documents Dynamically

You can insert contents of outer documents to your reports dynamically using doc tags. A doc tag denotes a placeholder within a template for a document to be inserted during run-time.

```text
<<doc [document_expression]>>
```

{{< alert style="warning" >}}A doc tag can be used almost anywhere in a template document except text-boxes and charts. Spreadsheet and presentation templates cannot hold one: for an XLSX or PPTX template the engine raises "Tag 'doc' is not well-formed".{{< /alert >}}

An expression declared within a doc tag is used by the engine to load a document to be inserted during run-time. The expression must return a value of one of the following types:

*   A byte array containing document data
*   A Stream instance able to read document data
*   An instance of the Document class
*   A string containing a document URI

{{< alert style="warning" >}}If an expression declared within a doc tag returns a stream object, then the stream is closed by the engine as soon as a corresponding document is loaded.{{< /alert >}}

By default, a document being inserted is not checked against template syntax and is not populated with data. However, you can enable this by using a build switch as follows.

```text
<<doc [document_expression] -build>>
```

When a build switch is used, the engine treats a document being inserted as a template that can access the following data available at the scope of a corresponding doc tag:

*   Data sources
*   Variables
*   A contextual object (see "[Using Contextual Object Member Access](https://docs.aspose.com/display/wordsnet/Template+Syntax#nowhere)" for more information)
*   Known external types (see "[Setting up Known External Types](https://docs.aspose.com/display/wordsnet/Template+Syntax#nowhere)"for more information)

{{< alert style="success" >}}For detailed technical information about syntax, expressions and report generation by the engine, please visit: [Working with GroupDocs.Assembly Engine]({{< ref "assembly/python-net/developer-guide/basic-usage/working-with-groupdocs.assembly-engine/_index.md" >}}){{< /alert >}}

### Working with Outer Document Insertion 

#### Download Templates

Get designed and outer templates from here.

*   [inserting-document.odt](/assembly/python-net/_sample_files/developer-guide/advanced-usage/working-with-outer-document-insertion/inserting-document.odt)
*   [nested-external-document.docx](/assembly/python-net/_sample_files/developer-guide/advanced-usage/working-with-outer-document-insertion/nested-external-document.docx)
*   [nested-external-document.msg](/assembly/python-net/_sample_files/developer-guide/advanced-usage/working-with-outer-document-insertion/nested-external-document.msg)

#### The Code

{{< tabs "example1" >}}
{{< tab "Python" >}}
```python
import json

from groupdocs.assembly import DataSourceInfo, DocumentAssembler

with open("customer.json", encoding="utf-8") as f:
    customer = json.load(f)

assembler = DocumentAssembler()
assembler.assemble_document("inserting-document.odt", "inserting-document-report.odt", [
    DataSourceInfo(customer, "customer"),
    DataSourceInfo("outer-document.docx", "document_expression"),
])
```
{{< /tab >}}
{{< tab "inserting-document.odt" >}}
{{< tab-text >}}
The following sample file is used in this example: [inserting-document.odt](/assembly/python-net/_sample_files/developer-guide/advanced-usage/working-with-outer-document-insertion/inserting-document.odt)
{{< /tab-text >}}
{{< /tab >}}
{{< tab "customer.json" >}}
{{< tab-text >}}
The following sample file is used in this example: [customer.json](/assembly/python-net/_sample_files/developer-guide/advanced-usage/working-with-outer-document-insertion/customer.json)
{{< /tab-text >}}
{{< /tab >}}
{{< tab "outer-document.docx" >}}
{{< tab-text >}}
The following sample file is used in this example: [outer-document.docx](/assembly/python-net/_sample_files/developer-guide/advanced-usage/working-with-outer-document-insertion/outer-document.docx)
{{< /tab-text >}}
{{< /tab >}}
{{< tab "pictures" >}}
{{< tab-text >}}
The following sample files are used in this example: [quayside-bistro.png](/assembly/python-net/_sample_files/developer-guide/advanced-usage/working-with-outer-document-insertion/quayside-bistro.png), [lantern-street-cafe.png](/assembly/python-net/_sample_files/developer-guide/advanced-usage/working-with-outer-document-insertion/lantern-street-cafe.png), [saltmarsh-deli.png](/assembly/python-net/_sample_files/developer-guide/advanced-usage/working-with-outer-document-insertion/saltmarsh-deli.png), [pier-nine-kitchen.png](/assembly/python-net/_sample_files/developer-guide/advanced-usage/working-with-outer-document-insertion/pier-nine-kitchen.png)
{{< /tab-text >}}
{{< /tab >}}
{{< tab "inserting-document-report.odt" >}}  
```text
Binary file (ODT, 11 KB)
```
[Download full output](/assembly/python-net/_output_files/developer-guide/advanced-usage/working-with-outer-document-insertion/the_code/inserting-document-report.odt)
{{< /tab >}}
{{< /tabs >}}

### Outer Document Insertion in Word Processing Formats

#### Download Templates

Get designed and outer templates from here.

#### The Code

{{< tabs "example2" >}}
{{< tab "Python" >}}
```python
import json

from groupdocs.assembly import DataSourceInfo, DocumentAssembler

with open("customer.json", encoding="utf-8") as f:
    customer = json.load(f)

assembler = DocumentAssembler()
assembler.assemble_document("nested-external-document.docx", "nested-external-document-report.docx", DataSourceInfo(customer, "customer"))
```
{{< /tab >}}
{{< tab "nested-external-document.docx" >}}
{{< tab-text >}}
The following sample file is used in this example: [nested-external-document.docx](/assembly/python-net/_sample_files/developer-guide/advanced-usage/working-with-outer-document-insertion/nested-external-document.docx)
{{< /tab-text >}}
{{< /tab >}}
{{< tab "customer.json" >}}
{{< tab-text >}}
The following sample file is used in this example: [customer.json](/assembly/python-net/_sample_files/developer-guide/advanced-usage/working-with-outer-document-insertion/customer.json)
{{< /tab-text >}}
{{< /tab >}}
{{< tab "outer-document.docx" >}}
{{< tab-text >}}
The following sample file is used in this example: [outer-document.docx](/assembly/python-net/_sample_files/developer-guide/advanced-usage/working-with-outer-document-insertion/outer-document.docx)
{{< /tab-text >}}
{{< /tab >}}
{{< tab "pictures" >}}
{{< tab-text >}}
The following sample files are used in this example: [quayside-bistro.png](/assembly/python-net/_sample_files/developer-guide/advanced-usage/working-with-outer-document-insertion/quayside-bistro.png), [lantern-street-cafe.png](/assembly/python-net/_sample_files/developer-guide/advanced-usage/working-with-outer-document-insertion/lantern-street-cafe.png), [saltmarsh-deli.png](/assembly/python-net/_sample_files/developer-guide/advanced-usage/working-with-outer-document-insertion/saltmarsh-deli.png), [pier-nine-kitchen.png](/assembly/python-net/_sample_files/developer-guide/advanced-usage/working-with-outer-document-insertion/pier-nine-kitchen.png)
{{< /tab-text >}}
{{< /tab >}}
{{< tab "nested-external-document-report.docx" >}}  
```text
Binary file (DOCX, 16 KB)
```
[Download full output](/assembly/python-net/_output_files/developer-guide/advanced-usage/working-with-outer-document-insertion/the_code_2/nested-external-document-report.docx)
{{< /tab >}}
{{< /tabs >}}

### Outer Document Insertion in Email Formats

#### Download Templates

Get designed and outer templates from here.

#### The Code

{{< tabs "example3" >}}
{{< tab "Python" >}}
```python
import json
from datetime import datetime

from groupdocs.assembly import DataSourceInfo, DocumentAssembler

def parse_dates(item):
    # JSON has no dates: turn the order dates into datetime objects for the template
    for key in ("OrderDate", "ShippingDate"):
        if key in item:
            item[key] = datetime.strptime(item[key], "%Y-%m-%dT%H:%M:%S")
    return item

with open("customer.json", encoding="utf-8") as f:
    customer = json.load(f, object_hook=parse_dates)

assembler = DocumentAssembler()
assembler.assemble_document("nested-external-document.msg", "nested-external-document-report.msg", [
    DataSourceInfo(customer, "customer"),
    DataSourceInfo("Harbor Lane Provisions <orders@harborlane.example>", "sender"),
    DataSourceInfo(["Quayside Bistro <orders@quaysidebistro.example>", "jonas.weber@harborlane.example"], "recipients"),
    DataSourceInfo("amara.osei@harborlane.example", "cc"),
    DataSourceInfo("Nested external document", "subject"),
])
```
{{< /tab >}}
{{< tab "nested-external-document.msg" >}}
{{< tab-text >}}
The following sample file is used in this example: [nested-external-document.msg](/assembly/python-net/_sample_files/developer-guide/advanced-usage/working-with-outer-document-insertion/nested-external-document.msg)
{{< /tab-text >}}
{{< /tab >}}
{{< tab "customer.json" >}}
{{< tab-text >}}
The following sample file is used in this example: [customer.json](/assembly/python-net/_sample_files/developer-guide/advanced-usage/working-with-outer-document-insertion/customer.json)
{{< /tab-text >}}
{{< /tab >}}
{{< tab "outer-document.docx" >}}
{{< tab-text >}}
The following sample file is used in this example: [outer-document.docx](/assembly/python-net/_sample_files/developer-guide/advanced-usage/working-with-outer-document-insertion/outer-document.docx)
{{< /tab-text >}}
{{< /tab >}}
{{< tab "pictures" >}}
{{< tab-text >}}
The following sample files are used in this example: [quayside-bistro.png](/assembly/python-net/_sample_files/developer-guide/advanced-usage/working-with-outer-document-insertion/quayside-bistro.png), [lantern-street-cafe.png](/assembly/python-net/_sample_files/developer-guide/advanced-usage/working-with-outer-document-insertion/lantern-street-cafe.png), [saltmarsh-deli.png](/assembly/python-net/_sample_files/developer-guide/advanced-usage/working-with-outer-document-insertion/saltmarsh-deli.png), [pier-nine-kitchen.png](/assembly/python-net/_sample_files/developer-guide/advanced-usage/working-with-outer-document-insertion/pier-nine-kitchen.png)
{{< /tab-text >}}
{{< /tab >}}
{{< tab "nested-external-document-report.msg" >}}  
```text
Binary file (MSG, 36 KB)
```
[Download full output](/assembly/python-net/_output_files/developer-guide/advanced-usage/working-with-outer-document-insertion/the_code_3/nested-external-document-report.msg)
{{< /tab >}}
{{< /tabs >}}
