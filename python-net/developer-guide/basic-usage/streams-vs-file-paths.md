---
id: assembly-basic-usage-streams-vs-files
url: assembly/python-net/basic-usage-streams-vs-files
linktitle: Work with Streams vs File Paths
title: Work with Streams vs File Paths
weight: 14
description: "Learn when and how to use io.BytesIO and binary file streams versus file paths for template loading and document saving in Python."
keywords: streams, file paths, io.BytesIO, binary file, stream handling, efficient processing, memory efficient, Python, web application
productName: GroupDocs.Assembly for Python via .NET
hideChildren: False
---

## Overview

GroupDocs.Assembly for Python via .NET supports both file paths and streams for template loading and document saving. Understanding when to use each approach helps you build efficient, scalable applications. File paths are simpler for local file system operations, while streams are essential for memory-based processing, remote templates, and web applications.

The main class involved is:
- [DocumentAssembler](https://reference.groupdocs.com/assembly/python-net/groupdocs.assembly/documentassembler/) - its [assemble_document](https://reference.groupdocs.com/assembly/python-net/groupdocs.assembly/documentassembler/assemble_document/) method takes two paths or two streams

Here are the considerations for choosing between streams and file paths:

* Use file paths for simple local file system operations
* Use streams for memory-based processing, remote templates, or web applications
* Open a file as a binary stream when one side is a file and the other is in memory
* Always close the streams you open, preferably with a `with` block

{{< alert style="info" >}}
`assemble_document` takes the template and the report as two paths or as two streams, optionally with [LoadSaveOptions](https://reference.groupdocs.com/assembly/python-net/groupdocs.assembly/loadsaveoptions/) before the data sources. A stream is a binary file object: `open(path, "rb")` or `io.BytesIO`. Streams can also be passed by keyword: `source_stream=`, `target_stream=` and then `data_source_infos=`.
{{< /alert >}}

## When to Use File Paths

File paths are ideal for:
- Simple local file system operations
- Templates stored on disk
- Output documents saved to disk
- Scripts and desktop applications with direct file access

{{< tabs "example1" >}}
{{< tab "Python" >}}
```python
from decimal import Decimal

from groupdocs.assembly import DataSourceInfo, DocumentAssembler

# Simple file path approach
template_path = "delivery-invoice.docx"
output_path = "delivery-invoice-report.docx"

data = {"CustomerName": "Quayside Bistro", "Amount": Decimal("552.00")}

assembler = DocumentAssembler()
assembler.assemble_document(template_path, output_path, DataSourceInfo(data, "invoice"))

print("Document assembled using file paths.")
```
{{< /tab >}}
{{< tab "delivery-invoice.docx" >}}
{{< tab-text >}}
The following sample file is used in this example: [delivery-invoice.docx](/assembly/python-net/_sample_files/developer-guide/basic-usage/streams-vs-file-paths/delivery-invoice.docx)
{{< /tab-text >}}
{{< /tab >}}
{{< tab "delivery-invoice-report.docx" >}}  
```text
Binary file (DOCX, 7 KB)
```
[Download full output](/assembly/python-net/_output_files/developer-guide/basic-usage/streams-vs-file-paths/when_to_use_file_paths/delivery-invoice-report.docx)
{{< /tab >}}
{{< /tabs >}}

## When to Use Streams

Streams are essential for:
- Memory-based processing (no disk I/O)
- Templates loaded from databases or remote sources
- Web applications serving documents directly
- Processing templates in memory for performance

{{< tabs "example2" >}}
{{< tab "Python" >}}
```python
import io
from datetime import datetime

from groupdocs.assembly import DataSourceInfo, DocumentAssembler

# Load template into memory
with open("stock-report.docx", "rb") as f:
    template_bytes = f.read()

with io.BytesIO(template_bytes) as template_stream, io.BytesIO() as output_stream:
    data = {"Title": "Quarterly stock report", "Date": datetime(2015, 3, 31)}

    assembler = DocumentAssembler()
    assembler.assemble_document(template_stream, output_stream, DataSourceInfo(data, "report"))

    # Use output stream (e.g., send via HTTP, save to database)
    output_bytes = output_stream.getvalue()

with open("stock-report-report.docx", "wb") as f:
    f.write(output_bytes)

print("Document assembled using streams.")
```
{{< /tab >}}
{{< tab "stock-report.docx" >}}
{{< tab-text >}}
The following sample file is used in this example: [stock-report.docx](/assembly/python-net/_sample_files/developer-guide/basic-usage/streams-vs-file-paths/stock-report.docx)
{{< /tab-text >}}
{{< /tab >}}
{{< tab "stock-report-report.docx" >}}  
```text
Binary file (DOCX, 7 KB)
```
[Download full output](/assembly/python-net/_output_files/developer-guide/basic-usage/streams-vs-file-paths/when_to_use_streams/stock-report-report.docx)
{{< /tab >}}
{{< /tabs >}}

## Mixed Approach: File Input, Stream Output

`assemble_document` has no form that takes a path for one side and a stream for the other. To load the template from a file and keep the report in memory, open the file as a stream:

{{< tabs "example3" >}}
{{< tab "Python" >}}
```python
import io

from groupdocs.assembly import DataSourceInfo, DocumentAssembler

# Template from a file, output to a memory stream
with open("stock-item.docx", "rb") as template_stream, io.BytesIO() as output_stream:
    data = {"Name": "Smoked sea salt", "Value": 100}

    assembler = DocumentAssembler()
    assembler.assemble_document(template_stream, output_stream, DataSourceInfo(data, "item"))

    # Use output stream (e.g., send via HTTP response)
    output_bytes = output_stream.getvalue()

print("Document assembled, output size: {0} bytes".format(len(output_bytes)))
```
{{< /tab >}}
{{< tab "stock-item.docx" >}}
{{< tab-text >}}
The following sample file is used in this example: [stock-item.docx](/assembly/python-net/_sample_files/developer-guide/basic-usage/streams-vs-file-paths/stock-item.docx)
{{< /tab-text >}}
{{< /tab >}}
{{< tab "mixed-approach-file-input-stream-output.txt" >}}  
```text
Document assembled, output size: 7529 bytes
```
[Download full output](/assembly/python-net/_output_files/developer-guide/basic-usage/streams-vs-file-paths/mixed_approach_file_input_stream_output/mixed-approach-file-input-stream-output.txt)
{{< /tab >}}
{{< /tabs >}}

## Mixed Approach: Stream Input, File Output

To load the template from memory and save the report to a file, pass the file, opened for writing in binary mode, as the output stream:

{{< tabs "example4" >}}
{{< tab "Python" >}}
```python
import io
from datetime import datetime

from groupdocs.assembly import DataSourceInfo, DocumentAssembler

# Template from a memory stream
with open("stock-report.docx", "rb") as f:
    template_bytes = f.read()

data = {"Title": "Monthly stock report", "Date": datetime(2015, 4, 30)}

# Report to a file opened for writing
with io.BytesIO(template_bytes) as template_stream, open("stock-report-from-stream.docx", "wb") as output_stream:
    assembler = DocumentAssembler()
    assembler.assemble_document(template_stream, output_stream, DataSourceInfo(data, "report"))

print("Document assembled from stream to file.")
```
{{< /tab >}}
{{< tab "stock-report.docx" >}}
{{< tab-text >}}
The following sample file is used in this example: [stock-report.docx](/assembly/python-net/_sample_files/developer-guide/basic-usage/streams-vs-file-paths/stock-report.docx)
{{< /tab-text >}}
{{< /tab >}}
{{< tab "stock-report-from-stream.docx" >}}  
```text
Binary file (DOCX, 7 KB)
```
[Download full output](/assembly/python-net/_output_files/developer-guide/basic-usage/streams-vs-file-paths/mixed_approach_stream_input_file_output/stock-report-from-stream.docx)
{{< /tab >}}
{{< /tabs >}}

## Web Application Example

In web applications, streams are typically preferred: the template comes as bytes and the response body is bytes. This function fits a Flask, Django or FastAPI view:

{{< tabs "example5" >}}
{{< tab "Python" >}}
```python
import io

from groupdocs.assembly import DataSourceInfo, DocumentAssembler


def generate_document_for_web(template_bytes, data):
    with io.BytesIO(template_bytes) as template_stream, io.BytesIO() as output_stream:
        assembler = DocumentAssembler()
        assembler.assemble_document(template_stream, output_stream, DataSourceInfo(data, "data"))
        return output_stream.getvalue()


with open("web-order.docx", "rb") as f:
    template_bytes = f.read()

order = {"CustomerName": "Pier Nine Kitchen", "ProductName": "Smoked sea salt", "Quantity": 50}
document_bytes = generate_document_for_web(template_bytes, order)

with open("web-order-report.docx", "wb") as f:
    f.write(document_bytes)
```
{{< /tab >}}
{{< tab "web-order.docx" >}}
{{< tab-text >}}
The following sample file is used in this example: [web-order.docx](/assembly/python-net/_sample_files/developer-guide/basic-usage/streams-vs-file-paths/web-order.docx)
{{< /tab-text >}}
{{< /tab >}}
{{< tab "web-order-report.docx" >}}  
```text
Binary file (DOCX, 7 KB)
```
[Download full output](/assembly/python-net/_output_files/developer-guide/basic-usage/streams-vs-file-paths/web_application_example/web-order-report.docx)
{{< /tab >}}
{{< /tabs >}}

## Loading Template from Remote Source

Streams enable loading templates from URLs or remote sources. To keep the example runnable, it opens the template's own `file:` URL; an `https://` address works the same way:

{{< tabs "example6" >}}
{{< tab "Python" >}}
```python
import io
import pathlib
from urllib.request import urlopen

from groupdocs.assembly import DataSourceInfo, DocumentAssembler


def load_template_from_url(url, data):
    # Download template
    response = urlopen(url)
    try:
        template_bytes = response.read()
    finally:
        response.close()

    with io.BytesIO(template_bytes) as template_stream, io.BytesIO() as output_stream:
        assembler = DocumentAssembler()
        assembler.assemble_document(template_stream, output_stream, DataSourceInfo(data, "data"))
        return output_stream.getvalue()


template_url = pathlib.Path("web-order.docx").resolve().as_uri()
order = {"CustomerName": "Saltmarsh Deli", "ProductName": "Smoked gouda", "Quantity": 30}

with open("web-order-from-url.docx", "wb") as f:
    f.write(load_template_from_url(template_url, order))
```
{{< /tab >}}
{{< tab "web-order.docx" >}}
{{< tab-text >}}
The following sample file is used in this example: [web-order.docx](/assembly/python-net/_sample_files/developer-guide/basic-usage/streams-vs-file-paths/web-order.docx)
{{< /tab-text >}}
{{< /tab >}}
{{< tab "web-order-from-url.docx" >}}  
```text
Binary file (DOCX, 7 KB)
```
[Download full output](/assembly/python-net/_output_files/developer-guide/basic-usage/streams-vs-file-paths/loading_template_from_remote_source/web-order-from-url.docx)
{{< /tab >}}
{{< /tabs >}}

## Stream Disposal Best Practices

Always close the streams you open. A `with` block closes them even when the assembly raises:

{{< tabs "example7" >}}
{{< tab "Python" >}}
```python
import io

from groupdocs.assembly import DataSourceInfo, DocumentAssembler

# Good: the with block closes both streams
with open("stock-item.docx", "rb") as template_stream, io.BytesIO() as output_stream:
    data = {"Name": "Chestnut honey", "Value": 190}

    assembler = DocumentAssembler()
    assembler.assemble_document(template_stream, output_stream, DataSourceInfo(data, "item"))

    with open("stock-item-report.docx", "wb") as f:
        f.write(output_stream.getvalue())
# Streams are closed here

print("Streams properly disposed.")
```
{{< /tab >}}
{{< tab "stock-item.docx" >}}
{{< tab-text >}}
The following sample file is used in this example: [stock-item.docx](/assembly/python-net/_sample_files/developer-guide/basic-usage/streams-vs-file-paths/stock-item.docx)
{{< /tab-text >}}
{{< /tab >}}
{{< tab "stock-item-report.docx" >}}  
```text
Binary file (DOCX, 7 KB)
```
[Download full output](/assembly/python-net/_output_files/developer-guide/basic-usage/streams-vs-file-paths/stream_disposal_best_practices/stock-item-report.docx)
{{< /tab >}}
{{< /tabs >}}

{{< alert style="warning" >}}
DocumentAssembler closes neither the template stream nor the output stream: both are still open when `assemble_document` returns, and the output `io.BytesIO` is positioned at 0 with the whole document in `getvalue()`. Closing them is up to your code.
{{< /alert >}}

## Performance Considerations

- **File Paths**: Simpler; the engine reads and writes the files itself
- **Streams**: More flexible; nothing touches the disk unless you write it
- **Memory Streams (`io.BytesIO`)**: Best for small to medium documents, since the whole document is held in memory
- **File Streams (`open(path, "rb")`)**: Read a template from disk without loading it into a `bytes` object first

### Advanced Usage Topics

To learn more about advanced stream handling and performance optimization, please refer to the [advanced usage section]({{< ref "assembly/python-net/developer-guide/advanced-usage/_index.md" >}}).

## More resources

### GitHub Examples

You may easily run the code above and see the feature in action in our GitHub examples:

* [GroupDocs.Assembly for .NET examples, plugins, and showcase](https://github.com/groupdocs-assembly/GroupDocs.Assembly-for-.NET)
* [GroupDocs.Assembly for Java examples, plugins, and showcase](https://github.com/groupdocs-assembly/GroupDocs.Assembly-for-Java)
* [GroupDocs.Assembly for Python via .NET examples, plugins, and showcase](https://github.com/groupdocs-assembly/GroupDocs.Assembly-for-Python-via-.NET)

### Free Online Apps

Along with the full-featured library, we provide simple but powerful free online apps.

To assemble documents from templates and data sources, you can use the online apps from the **[GroupDocs.Assembly App Product Family](https://products.groupdocs.app/assembly/family)**.
