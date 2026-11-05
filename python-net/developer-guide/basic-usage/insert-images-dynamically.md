---
id: assembly-basic-usage-generate-images
url: assembly/python-net/basic-usage-generate-images
linktitle: Insert Images Dynamically
title: Insert Images Dynamically
weight: 20
description: "Insert images into documents from file paths, URLs, bytes and Base64 strings held in Python dicts during document assembly, using GroupDocs.Assembly for Python via .NET."
keywords: insert images, dynamic images, image from file, image from URL, image from bytes, Base64 image, image tag, generate images, Python
productName: GroupDocs.Assembly for Python via .NET
hideChildren: False
---

## Overview

GroupDocs.Assembly for Python via .NET allows you to insert images dynamically into documents using image tags. Images can be loaded from file paths, URLs, `bytes`, or Base64-encoded strings, making it easy to include dynamic images in your reports.

The main classes involved are:
- [DocumentAssembler](https://reference.groupdocs.com/assembly/python-net/groupdocs.assembly/documentassembler/) - assembles documents
- [DataSourceInfo](https://reference.groupdocs.com/assembly/python-net/groupdocs.assembly/datasourceinfo/) - wraps data sources

Here are the steps to insert images dynamically:

* Add a textbox to your template at the location where you want the image
* Set the textbox size and appearance to match desired image dimensions
* Insert an image tag `<<image [expression]>>` within the textbox
* Provide image data as a file path, a URL, `bytes` or a Base64 string
* Assemble the document

{{< alert style="info" >}}
Image tags are replaced with actual images during document assembly. The textbox acts as a placeholder and container for the image.
{{< /alert >}}

## Insert Image from File Path

Insert an image from a file path. A relative path is resolved against the current working directory:

{{< tabs "example1" >}}
{{< tab "Python" >}}
```python
from groupdocs.assembly import DataSourceInfo, DocumentAssembler

# Sample data with image path
customer = {
    "Name": "Quayside Bistro",
    "Photo": "quayside-bistro.png",
}

# Assemble document
assembler = DocumentAssembler()
assembler.assemble_document("customer-photo.docx", "customer-photo-report.docx",
                            DataSourceInfo(customer, "customer"))

print("Image inserted from file path successfully.")
```
{{< /tab >}}
{{< tab "customer-photo.docx" >}}
{{< tab-text >}}
The following sample file is used in this example: [customer-photo.docx](/assembly/python-net/_sample_files/developer-guide/basic-usage/insert-images-dynamically/customer-photo.docx)
{{< /tab-text >}}
{{< /tab >}}
{{< tab "quayside-bistro.png" >}}
{{< tab-text >}}
The following sample file is used in this example: [quayside-bistro.png](/assembly/python-net/_sample_files/developer-guide/basic-usage/insert-images-dynamically/quayside-bistro.png)
{{< /tab-text >}}
{{< /tab >}}
{{< tab "customer-photo-report.docx" >}}  
```text
Binary file (DOCX, 14 KB)
```
[Download full output](/assembly/python-net/_output_files/developer-guide/basic-usage/insert-images-dynamically/insert_image_from_file_path/customer-photo-report.docx)
{{< /tab >}}
{{< /tabs >}}

## Template Structure for Images

In your template (customer-photo.docx):

1. Insert a textbox where you want the image
2. Set the textbox size (width and height)
3. Add the image tag inside the textbox:

```text
Customer: <<[customer.Name]>>

[Textbox with image tag:]
<<image [customer.Photo]>>
```

## Insert Image from URL

Insert an image from a URL. The assembler downloads an `http:` or `https:` address while it builds the report. This example builds a `file:` URL for the sample picture, so it runs without a network:

{{< tabs "example2" >}}
{{< tab "Python" >}}
```python
from pathlib import Path

from groupdocs.assembly import DataSourceInfo, DocumentAssembler

customer = {
    "Name": "Quayside Bistro",
    # For example "https://harborlane.example/photos/quayside-bistro.png" on a reachable server
    "Photo": Path("quayside-bistro.png").resolve().as_uri(),
}

assembler = DocumentAssembler()
assembler.assemble_document("customer-photo.docx", "customer-photo-from-url.docx",
                            DataSourceInfo(customer, "customer"))

print("Image inserted from URL successfully.")
```
{{< /tab >}}
{{< tab "customer-photo.docx" >}}
{{< tab-text >}}
The following sample file is used in this example: [customer-photo.docx](/assembly/python-net/_sample_files/developer-guide/basic-usage/insert-images-dynamically/customer-photo.docx)
{{< /tab-text >}}
{{< /tab >}}
{{< tab "quayside-bistro.png" >}}
{{< tab-text >}}
The following sample file is used in this example: [quayside-bistro.png](/assembly/python-net/_sample_files/developer-guide/basic-usage/insert-images-dynamically/quayside-bistro.png)
{{< /tab-text >}}
{{< /tab >}}
{{< tab "customer-photo-from-url.docx" >}}  
```text
Binary file (DOCX, 14 KB)
```
[Download full output](/assembly/python-net/_output_files/developer-guide/basic-usage/insert-images-dynamically/insert_image_from_url/customer-photo-from-url.docx)
{{< /tab >}}
{{< /tabs >}}

The template is the same:

```text
Customer: <<[customer.Name]>>

[Textbox:]
<<image [customer.Photo]>>
```

A string that is neither a readable path nor a URL that answers, nor Base64 image data, fails the assembly: "Cannot load an image using the provided string value".

## Insert Image from Bytes

Insert an image from binary data. A Python `bytes` value reaches the template as a .NET byte array:

{{< tabs "example3" >}}
{{< tab "Python" >}}
```python
from groupdocs.assembly import DataSourceInfo, DocumentAssembler

# Load image into bytes
with open("quayside-bistro.png", "rb") as f:
    image_bytes = f.read()

customer = {
    "Name": "Quayside Bistro",
    "Photo": image_bytes,
}

assembler = DocumentAssembler()
assembler.assemble_document("customer-photo.docx", "customer-photo-from-bytes.docx",
                            DataSourceInfo(customer, "customer"))

print("Image inserted from bytes successfully.")
```
{{< /tab >}}
{{< tab "customer-photo.docx" >}}
{{< tab-text >}}
The following sample file is used in this example: [customer-photo.docx](/assembly/python-net/_sample_files/developer-guide/basic-usage/insert-images-dynamically/customer-photo.docx)
{{< /tab-text >}}
{{< /tab >}}
{{< tab "quayside-bistro.png" >}}
{{< tab-text >}}
The following sample file is used in this example: [quayside-bistro.png](/assembly/python-net/_sample_files/developer-guide/basic-usage/insert-images-dynamically/quayside-bistro.png)
{{< /tab-text >}}
{{< /tab >}}
{{< tab "customer-photo-from-bytes.docx" >}}  
```text
Binary file (DOCX, 14 KB)
```
[Download full output](/assembly/python-net/_output_files/developer-guide/basic-usage/insert-images-dynamically/insert_image_from_bytes/customer-photo-from-bytes.docx)
{{< /tab >}}
{{< /tabs >}}

Template:

```text
Customer: <<[customer.Name]>>

[Textbox:]
<<image [customer.Photo]>>
```

A `bytearray` works the same way, and so does the image encoded as a Base64 `str` (`base64.b64encode(image_bytes).decode("ascii")`).

## Insert Image from Stream

A data source dict cannot hold a stream: `DataSourceInfo` raises `TypeError` ("BytesIO cannot be part of a data source given as a dict") for an `io.BytesIO` or an open file. Pass the stream's bytes instead, with `getvalue()` for a `BytesIO` or `read()` for a file:

{{< tabs "example4" >}}
{{< tab "Python" >}}
```python
import io

from groupdocs.assembly import DataSourceInfo, DocumentAssembler

# A picture held in memory, for example one received over the network
with open("quayside-bistro.png", "rb") as f:
    image_stream = io.BytesIO(f.read())

customer = {
    "Name": "Quayside Bistro",
    "Photo": image_stream.getvalue(),
}

assembler = DocumentAssembler()
assembler.assemble_document("customer-photo.docx", "customer-photo-from-stream.docx",
                            DataSourceInfo(customer, "customer"))

print("Image inserted from stream successfully.")
```
{{< /tab >}}
{{< tab "customer-photo.docx" >}}
{{< tab-text >}}
The following sample file is used in this example: [customer-photo.docx](/assembly/python-net/_sample_files/developer-guide/basic-usage/insert-images-dynamically/customer-photo.docx)
{{< /tab-text >}}
{{< /tab >}}
{{< tab "quayside-bistro.png" >}}
{{< tab-text >}}
The following sample file is used in this example: [quayside-bistro.png](/assembly/python-net/_sample_files/developer-guide/basic-usage/insert-images-dynamically/quayside-bistro.png)
{{< /tab-text >}}
{{< /tab >}}
{{< tab "customer-photo-from-stream.docx" >}}  
```text
Binary file (DOCX, 14 KB)
```
[Download full output](/assembly/python-net/_output_files/developer-guide/basic-usage/insert-images-dynamically/insert_image_from_stream/customer-photo-from-stream.docx)
{{< /tab >}}
{{< /tabs >}}

## Image Sizing Options

Control how images are sized within textboxes:

{{< tabs "example5" >}}
{{< tab "Python" >}}
```python
from groupdocs.assembly import DataSourceInfo, DocumentAssembler

customer = {
    "Name": "Quayside Bistro",
    "Photo": "quayside-bistro.png",
}

assembler = DocumentAssembler()
assembler.assemble_document("image-sizing.docx", "image-sizing-report.docx",
                            DataSourceInfo(customer, "customer"))

print("Image inserted with sizing options.")
```
{{< /tab >}}
{{< tab "image-sizing.docx" >}}
{{< tab-text >}}
The following sample file is used in this example: [image-sizing.docx](/assembly/python-net/_sample_files/developer-guide/basic-usage/insert-images-dynamically/image-sizing.docx)
{{< /tab-text >}}
{{< /tab >}}
{{< tab "quayside-bistro.png" >}}
{{< tab-text >}}
The following sample file is used in this example: [quayside-bistro.png](/assembly/python-net/_sample_files/developer-guide/basic-usage/insert-images-dynamically/quayside-bistro.png)
{{< /tab-text >}}
{{< /tab >}}
{{< tab "image-sizing-report.docx" >}}  
```text
Binary file (DOCX, 14 KB)
```
[Download full output](/assembly/python-net/_output_files/developer-guide/basic-usage/insert-images-dynamically/image_sizing_options/image-sizing-report.docx)
{{< /tab >}}
{{< /tabs >}}

The template (image-sizing.docx) puts the square photo into six text boxes of the same 160x80 size, one per sizing option:

- `<<image [customer.Photo]>>` - Stretch to fill textbox (default)
- `<<image [customer.Photo] -keepRatio>>` - Keep the textbox size and the image's aspect ratio
- `<<image [customer.Photo] -fitHeight>>` - Keep the textbox width and change its height to the image's ratio
- `<<image [customer.Photo] -fitWidth>>` - Keep the textbox height and change its width to the image's ratio
- `<<image [customer.Photo] -fitSize>>` - Resize textbox to image size
- `<<image [customer.Photo] -fitSizeLim>>` - Resize textbox to image size, without making it larger

## Insert Multiple Images from Collection

Insert images for each item in a collection. Each customer of the Harbor Lane sample data names its photo in `Photo`:

{{< tabs "example6" >}}
{{< tab "Python" >}}
```python
import json

from groupdocs.assembly import DataSourceInfo, DocumentAssembler

with open("customers.json", encoding="utf-8") as f:
    customers = json.load(f)

assembler = DocumentAssembler()
assembler.assemble_document("customer-photos.docx", "customer-photos-report.docx",
                            DataSourceInfo(customers, "customers"))

print("Images inserted from collection successfully.")
```
{{< /tab >}}
{{< tab "customer-photos.docx" >}}
{{< tab-text >}}
The following sample file is used in this example: [customer-photos.docx](/assembly/python-net/_sample_files/developer-guide/basic-usage/insert-images-dynamically/customer-photos.docx)
{{< /tab-text >}}
{{< /tab >}}
{{< tab "customers.json" >}}
{{< tab-text >}}
The following sample file is used in this example: [customers.json](/assembly/python-net/_sample_files/developer-guide/basic-usage/insert-images-dynamically/customers.json)
{{< /tab-text >}}
{{< /tab >}}
{{< tab "quayside-bistro.png" >}}
{{< tab-text >}}
The following sample file is used in this example: [quayside-bistro.png](/assembly/python-net/_sample_files/developer-guide/basic-usage/insert-images-dynamically/quayside-bistro.png)
{{< /tab-text >}}
{{< /tab >}}
{{< tab "lantern-street-cafe.png" >}}
{{< tab-text >}}
The following sample file is used in this example: [lantern-street-cafe.png](/assembly/python-net/_sample_files/developer-guide/basic-usage/insert-images-dynamically/lantern-street-cafe.png)
{{< /tab-text >}}
{{< /tab >}}
{{< tab "saltmarsh-deli.png" >}}
{{< tab-text >}}
The following sample file is used in this example: [saltmarsh-deli.png](/assembly/python-net/_sample_files/developer-guide/basic-usage/insert-images-dynamically/saltmarsh-deli.png)
{{< /tab-text >}}
{{< /tab >}}
{{< tab "pier-nine-kitchen.png" >}}
{{< tab-text >}}
The following sample file is used in this example: [pier-nine-kitchen.png](/assembly/python-net/_sample_files/developer-guide/basic-usage/insert-images-dynamically/pier-nine-kitchen.png)
{{< /tab-text >}}
{{< /tab >}}
{{< tab "customer-photos-report.docx" >}}  
```text
Binary file (DOCX, 26 KB)
```
[Download full output](/assembly/python-net/_output_files/developer-guide/basic-usage/insert-images-dynamically/insert_multiple_images_from_collection/customer-photos-report.docx)
{{< /tab >}}
{{< /tabs >}}

Template with foreach:

```text
<<foreach [in customers]>>Customer: <<[CustomerName]>>
[Textbox:]
<<image [Photo]>>

<</foreach>>
```

{{< alert style="warning" >}}
An image given as a path or a `file:` URL is read when the document is assembled, so the file must exist then. Image data given as `bytes` is copied into the data source when `DataSourceInfo` is created.
{{< /alert >}}

### Advanced Usage Topics

To learn more about image formatting, Base64-encoded images, image optimization, and advanced image handling, please refer to the [advanced usage section]({{< ref "assembly/python-net/developer-guide/advanced-usage/_index.md" >}}).

## More resources

### GitHub Examples

You may easily run the code above and see the feature in action in our GitHub examples:

* [GroupDocs.Assembly for .NET examples, plugins, and showcase](https://github.com/groupdocs-assembly/GroupDocs.Assembly-for-.NET)
* [GroupDocs.Assembly for Java examples, plugins, and showcase](https://github.com/groupdocs-assembly/GroupDocs.Assembly-for-Java)
* [GroupDocs.Assembly for Python via .NET examples, plugins, and showcase](https://github.com/groupdocs-assembly/GroupDocs.Assembly-for-Python-via-.NET)

### Free Online Apps

Along with the full-featured library, we provide simple but powerful free online apps.

To assemble documents from templates and data sources, you can use the online apps from the **[GroupDocs.Assembly App Product Family](https://products.groupdocs.app/assembly/family)**.
