---
id: hello-world
url: assembly/python-net/hello-world
title: Hello, World!
second_title: Basic Example of Using GroupDocs.Assembly for Python via .NET
linkTitle: Hello World
weight: 2
keywords: "hello world, example, get started, template, report, docx"
description: Quickly get started with GroupDocs.Assembly for Python via .NET by creating and running a simple example that fills a Word template with data from a Python dict.
productName: GroupDocs.Assembly for Python via .NET
hideChildren: False
toc: True
---

## Introduction
A "Hello, World!" example is often the first step when exploring GroupDocs.Assembly for Python via .NET. It serves as a simple test to confirm that your development environment is correctly set up and that the library is functioning as expected.

## Overview
GroupDocs.Assembly for Python via .NET builds reports from templates. A template is an ordinary document, here a Word document, with tags such as `<<[customer.Name]>>` where the data goes. The data can be Python dicts and lists, JSON, XML or CSV files, or the tables of other documents, and the report can be saved in any of the [supported formats]({{< ref "assembly/python-net/getting-started/supported-document-formats.md" >}}).

## How to build a report from a template
The following steps demonstrate how to fill a template with data using GroupDocs.Assembly for Python via .NET:

1. Import the `DocumentAssembler` and `DataSourceInfo` classes from `groupdocs.assembly`.
2. Put the data in a Python dict. Its keys are the names the template's tags read.
3. Wrap the dict in a `DataSourceInfo` with the name the template uses for it, `customer`.
4. Call `assemble_document()` with the template, the report to write and the data.

The template, `hello-world.docx`, holds:

```text
Hello, <<[customer.Name]>>!
Your order of <<[customer.Product]>> is on its way.

Harbor Lane Provisions, 18 Quayside Road, Port Ellery
```

## Complete example
The example below fills the template with the data of one customer and saves the report as `hello-world-report.docx`:

{{< tabs "code-example-hello-world" >}}
{{< tab "hello_world.py" >}}
```python
from groupdocs.assembly import DataSourceInfo, DocumentAssembler

def hello_world():
    # The data: a dict whose keys the template's tags read
    customer = {"Name": "Quayside Bistro", "Product": "Harbor Blend whole bean coffee"}

    # Fill the template's tags and save the report
    assembler = DocumentAssembler()
    assembler.assemble_document("hello-world.docx", "hello-world-report.docx", DataSourceInfo(customer, "customer"))
    print("The report is saved to hello-world-report.docx")

if __name__ == "__main__":
    hello_world()
```
{{< /tab >}}
{{< tab "hello-world.docx" >}}
{{< tab-text >}}
The following sample file is used in this example: [hello-world.docx](/assembly/python-net/_sample_files/getting-started/hello-world/hello-world.docx)
{{< /tab-text >}}
{{< /tab >}}
{{< tab "hello-world-report.docx" >}}  
```text
Binary file (DOCX, 7 KB)
```
[Download full output](/assembly/python-net/_output_files/getting-started/hello-world/hello_world/hello-world-report.docx)
{{< /tab >}}
{{< /tabs >}}

The report reads "Hello, Quayside Bistro!" and "Your order of Harbor Blend whole bean coffee is on its way.": each tag is replaced with the value of its key, and the rest of the document, its text and formatting, stays as it is.

The output format follows the report's extension: name it `hello-world-report.pdf` and the same template gives a PDF. To fill tables, lists and charts from lists of dicts, see the [Quick Start Guide]({{< ref "assembly/python-net/getting-started/quick-start-guide.md" >}}) and the [Developer Guide]({{< ref "assembly/python-net/developer-guide/_index.md" >}}).

## Additional resources
This demo references the GroupDocs.Assembly for Python via .NET [code samples](https://github.com/groupdocs-assembly/GroupDocs.Assembly-for-Python-via-.NET/).
