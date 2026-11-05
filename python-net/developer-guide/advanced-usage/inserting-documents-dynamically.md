---
id: inserting-documents-dynamically
url: assembly/python-net/inserting-documents-dynamically
title: Inserting Documents Dynamically
weight: 43
description: "Inserting Documents Dynamically with GroupDocs.Assembly for Python via .NET: the template, the Python data and the code."
keywords: inserting documents dynamically, GroupDocs.Assembly, Python, report generation
productName: GroupDocs.Assembly for Python via .NET
hideChildren: False
---
{{< alert style="info" >}}The example reads the shop data described in [The Business Layer]({{< ref "assembly/python-net/developer-guide/basic-usage/working-with-a-business-case/the-business-layer.md" >}}).{{< /alert >}}

{{< alert style="warning" >}}Dynamic insertion of documents from Base64-encoded bytes is available for file formats where dynamic document insertion is available for Word Processing documents and emails with HTML and RTF bodies only.{{< /alert >}}

You can insert contents of outer documents to your reports dynamically using `doc` tags. A `doc` tag denotes a placeholder within a template for a document to be inserted during runtime.

Syntax of a `doc` tag is defined as follows:

```text
<<doc [document_expression]>>
```

And simply call the assembler method to generate report like following code snippets:

{{< tabs "example1" >}}
{{< tab "Python" >}}
```python
import json

from groupdocs.assembly import DataSourceInfo, DocumentAssembler

with open("customer.json", encoding="utf-8") as f:
    customer = json.load(f)

assembler = DocumentAssembler()
assembler.assemble_document("inserting-document.docx", "inserting-document-report.docx", [
    DataSourceInfo(customer, "customer"),
    DataSourceInfo("outer-document.docx", "document_expression"),
])
```
{{< /tab >}}
{{< tab "inserting-document.docx" >}}
{{< tab-text >}}
The following sample file is used in this example: [inserting-document.docx](/assembly/python-net/_sample_files/developer-guide/advanced-usage/inserting-documents-dynamically/inserting-document.docx)
{{< /tab-text >}}
{{< /tab >}}
{{< tab "customer.json" >}}
{{< tab-text >}}
The following sample file is used in this example: [customer.json](/assembly/python-net/_sample_files/developer-guide/advanced-usage/inserting-documents-dynamically/customer.json)
{{< /tab-text >}}
{{< /tab >}}
{{< tab "outer-document.docx" >}}
{{< tab-text >}}
The following sample file is used in this example: [outer-document.docx](/assembly/python-net/_sample_files/developer-guide/advanced-usage/inserting-documents-dynamically/outer-document.docx)
{{< /tab-text >}}
{{< /tab >}}
{{< tab "pictures" >}}
{{< tab-text >}}
The following sample files are used in this example: [quayside-bistro.png](/assembly/python-net/_sample_files/developer-guide/advanced-usage/inserting-documents-dynamically/quayside-bistro.png), [lantern-street-cafe.png](/assembly/python-net/_sample_files/developer-guide/advanced-usage/inserting-documents-dynamically/lantern-street-cafe.png), [saltmarsh-deli.png](/assembly/python-net/_sample_files/developer-guide/advanced-usage/inserting-documents-dynamically/saltmarsh-deli.png), [pier-nine-kitchen.png](/assembly/python-net/_sample_files/developer-guide/advanced-usage/inserting-documents-dynamically/pier-nine-kitchen.png)
{{< /tab-text >}}
{{< /tab >}}
{{< tab "inserting-document-report.docx" >}}  
```text
Binary file (DOCX, 17 KB)
```
[Download full output](/assembly/python-net/_output_files/developer-guide/advanced-usage/inserting-documents-dynamically/inserting_documents_dynamically/inserting-document-report.docx)
{{< /tab >}}
{{< /tabs >}}

{{< alert style="warning" >}}A `doc` tag can be used almost anywhere in a template document except textboxes and charts.{{< /alert >}}

An expression declared within a `doc` tag is used by the assembler to load a document to be inserted during runtime. The expression must return a value of one of the following types:

*   A byte array containing document data
*   A [Stream](http://msdn.microsoft.com/en-us/library/system.io.stream(v=vs.110).aspx) instance able to read document data
*   An instance of the Document class
*   A string containing a document URI, path, or Base64-encoded document data

While building a report, an expression declared within a `doc` tag is evaluated and its result is used to load a document which content replaces the `doc` tag then.

{{< alert style="warning" >}}If an expression declared within a `doc` tag returns a stream object, then the stream is closed by the assembler as soon as a corresponding document is loaded.{{< /alert >}}

By default, while inserting content of an outer document, the engine applies corresponding styles of a template document. This makes content of a result document look more consistent. However, you can keep source formatting for content being inserted by using a `sourceStyles` switch as shown in the following snippet:

```text
<<doc [document_expression] -sourceStyles>>
```

By default, a document being inserted is not checked against template syntax and is not populated with data. However, you can enable this by using a `build` switch as follows:

```text
<<doc [document_expression] -build>>
```

When a `build` switch is used, the assembler treats a document being inserted as a template that can access the following data available at the scope of a corresponding `doc` tag:

*   Data sources
*   Variables
*   A contextual object (see [“Using Contextual Object Member Access”]({{< ref "assembly/python-net/developer-guide/basic-usage/working-with-groupdocs.assembly-engine/template-syntax-part-1-of-2.md#using-contextual-object-member-access" >}}) for more information)
*   Known external types (see [“Setting up Known External Types”]({{< ref "assembly/python-net/developer-guide/basic-usage/working-with-groupdocs.assembly-engine/groupdocs.assembly-engine-apis.md#setting-up-known-external-types" >}}) for more information)
