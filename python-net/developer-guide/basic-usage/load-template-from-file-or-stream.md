---
id: assembly-basic-usage-load-template
url: assembly/python-net/basic-usage-load-template
linktitle: Load Template Documents
title: Load Template Documents from File or Stream
weight: 3
description: "Learn how to load template documents from file paths, binary files and io.BytesIO streams for document assembly in Python."
keywords: load template, file path, stream, io.BytesIO, binary file, template document, DOCX, XLSX, PPTX, Python
productName: GroupDocs.Assembly for Python via .NET
hideChildren: False
---

## Overview

GroupDocs.Assembly for Python via .NET supports loading template documents from both file paths and streams. This flexibility allows you to work with templates stored on disk, in memory, or retrieved from remote sources.

The main class involved is:
- [DocumentAssembler](https://reference.groupdocs.com/assembly/python-net/groupdocs.assembly/documentassembler/) - its [assemble_document](https://reference.groupdocs.com/assembly/python-net/groupdocs.assembly/documentassembler/assemble_document/) method takes either two file paths or two streams

Here are the steps to load and use templates:

* Load a template from a file path by passing the path as a string
* Load a template from a stream by passing a binary file object or an `io.BytesIO`
* Choose the appropriate form based on your use case (file system vs memory/remote)
* Save the assembled document to a file path or to a stream accordingly

{{< alert style="info" >}}
`assemble_document` takes the template and the report either both as paths or both as streams. A stream is any binary file object: a file opened with `open(path, "rb")` or an `io.BytesIO`. The assembler leaves the streams you pass open, so manage their lifetime yourself, preferably with a `with` block.
{{< /alert >}}

## Load Template from File Path

The simplest way to load a template is from a file path:

{{< tabs "example1" >}}
{{< tab "Python" >}}
```python
from groupdocs.assembly import DataSourceInfo, DocumentAssembler

# Template and output file paths
template_path = "invoice-summary.docx"
output_path = "invoice-summary-report.docx"

# Sample data
invoice_data = {"CustomerName": "Quayside Bistro", "Amount": 552.00}

# Assemble document from file path
assembler = DocumentAssembler()
assembler.assemble_document(template_path, output_path, DataSourceInfo(invoice_data, "invoice"))

print("Document assembled successfully.")
```
{{< /tab >}}
{{< tab "invoice-summary.docx" >}}
{{< tab-text >}}
The following sample file is used in this example: [invoice-summary.docx](/assembly/python-net/_sample_files/developer-guide/basic-usage/load-template-from-file-or-stream/invoice-summary.docx)
{{< /tab-text >}}
{{< /tab >}}
{{< tab "invoice-summary-report.docx" >}}  
```text
Binary file (DOCX, 7 KB)
```
[Download full output](/assembly/python-net/_output_files/developer-guide/basic-usage/load-template-from-file-or-stream/load_template_from_file_path/invoice-summary-report.docx)
{{< /tab >}}
{{< /tabs >}}

## Load Template from Stream

When working with templates in memory or from remote sources, use streams:

{{< tabs "example2" >}}
{{< tab "Python" >}}
```python
import io
from datetime import datetime

from groupdocs.assembly import DataSourceInfo, DocumentAssembler

# Load template into a memory stream
with open("report-cover.docx", "rb") as f:
    template_bytes = f.read()

data = {"Title": "Quarterly stock report", "Date": datetime(2015, 3, 31)}

# The report goes to a file opened for writing in binary mode
with io.BytesIO(template_bytes) as template_stream, open("report-cover-report.docx", "wb") as output_stream:
    assembler = DocumentAssembler()
    assembler.assemble_document(template_stream, output_stream, DataSourceInfo(data, "report"))

print("Document assembled from stream successfully.")
```
{{< /tab >}}
{{< tab "report-cover.docx" >}}
{{< tab-text >}}
The following sample file is used in this example: [report-cover.docx](/assembly/python-net/_sample_files/developer-guide/basic-usage/load-template-from-file-or-stream/report-cover.docx)
{{< /tab-text >}}
{{< /tab >}}
{{< tab "report-cover-report.docx" >}}  
```text
Binary file (DOCX, 7 KB)
```
[Download full output](/assembly/python-net/_output_files/developer-guide/basic-usage/load-template-from-file-or-stream/load_template_from_stream/report-cover-report.docx)
{{< /tab >}}
{{< /tabs >}}

## Load Template from Remote Source

You can load templates from URLs or other remote sources: read the response's bytes into an `io.BytesIO`. To keep the example runnable, it opens the template's own `file:` URL; pass your `https://` address the same way:

{{< tabs "example3" >}}
{{< tab "Python" >}}
```python
import io
import pathlib
from urllib.request import urlopen

from groupdocs.assembly import DataSourceInfo, DocumentAssembler

# Any URL urllib can open: https://... on your server, here the template's file: URL
template_url = pathlib.Path("company-letter.docx").resolve().as_uri()

# Download template from the URL
response = urlopen(template_url)
try:
    template_bytes = response.read()
finally:
    response.close()

with io.BytesIO(template_bytes) as template_stream, io.BytesIO() as output_stream:
    data = {"Company": "Harbor Lane Provisions", "Year": 2015}

    assembler = DocumentAssembler()
    assembler.assemble_document(template_stream, output_stream, DataSourceInfo(data, "company"))

    with open("company-letter-report.docx", "wb") as f:
        f.write(output_stream.getvalue())

print("Document assembled from remote template.")
```
{{< /tab >}}
{{< tab "company-letter.docx" >}}
{{< tab-text >}}
The following sample file is used in this example: [company-letter.docx](/assembly/python-net/_sample_files/developer-guide/basic-usage/load-template-from-file-or-stream/company-letter.docx)
{{< /tab-text >}}
{{< /tab >}}
{{< tab "company-letter-report.docx" >}}  
```text
Binary file (DOCX, 7 KB)
```
[Download full output](/assembly/python-net/_output_files/developer-guide/basic-usage/load-template-from-file-or-stream/load_template_from_remote_source/company-letter-report.docx)
{{< /tab >}}
{{< /tabs >}}

## Mixed File and Stream Usage

To read the template from disk and keep the report in memory, open the template file as a binary stream:

{{< tabs "example4" >}}
{{< tab "Python" >}}
```python
import io

from groupdocs.assembly import DataSourceInfo, DocumentAssembler

# Template from a file, opened as a stream
with open("item-label.docx", "rb") as template_stream, io.BytesIO() as output_stream:
    data = {"Name": "Smoked sea salt", "Value": 100}

    assembler = DocumentAssembler()
    assembler.assemble_document(template_stream, output_stream, DataSourceInfo(data, "item"))

    # Use the output stream (e.g., send via HTTP, save to database)
    output_bytes = output_stream.getvalue()

with open("item-label-report.docx", "wb") as f:
    f.write(output_bytes)

print("Document assembled with mixed file/stream usage.")
```
{{< /tab >}}
{{< tab "item-label.docx" >}}
{{< tab-text >}}
The following sample file is used in this example: [item-label.docx](/assembly/python-net/_sample_files/developer-guide/basic-usage/load-template-from-file-or-stream/item-label.docx)
{{< /tab-text >}}
{{< /tab >}}
{{< tab "item-label-report.docx" >}}  
```text
Binary file (DOCX, 7 KB)
```
[Download full output](/assembly/python-net/_output_files/developer-guide/basic-usage/load-template-from-file-or-stream/mixed_file_and_stream_usage/item-label-report.docx)
{{< /tab >}}
{{< /tabs >}}

{{< alert style="warning" >}}
`assemble_document` has no form that takes a path for one side and a stream for the other: `assemble_document("item-label.docx", io.BytesIO(), ...)` raises `TypeError` ("no overload matched"). Open the file as a stream instead, as above. After the call, the output `BytesIO` is positioned at 0, and `getvalue()` returns the whole document.
{{< /alert >}}

### Advanced Usage Topics

To learn more about working with different template formats, custom document loading, and advanced stream handling, please refer to the [advanced usage section]({{< ref "assembly/python-net/developer-guide/advanced-usage/_index.md" >}}).

## More resources

### GitHub Examples

You may easily run the code above and see the feature in action in our GitHub examples:

* [GroupDocs.Assembly for .NET examples, plugins, and showcase](https://github.com/groupdocs-assembly/GroupDocs.Assembly-for-.NET)
* [GroupDocs.Assembly for Java examples, plugins, and showcase](https://github.com/groupdocs-assembly/GroupDocs.Assembly-for-Java)
* [GroupDocs.Assembly for Python via .NET examples, plugins, and showcase](https://github.com/groupdocs-assembly/GroupDocs.Assembly-for-Python-via-.NET)

### Free Online Apps

Along with the full-featured library, we provide simple but powerful free online apps.

To assemble documents from templates and data sources, you can use the online apps from the **[GroupDocs.Assembly App Product Family](https://products.groupdocs.app/assembly/family)**.
