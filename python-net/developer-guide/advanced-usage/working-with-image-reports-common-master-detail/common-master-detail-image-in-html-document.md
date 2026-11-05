---
id: common-master-detail-image-in-html-document
url: assembly/python-net/common-master-detail-image-in-html-document
title: Common Master-Detail Image in HTML Document
weight: 4
description: "Common Master-Detail Image in HTML Document with GroupDocs.Assembly for Python via .NET: customers' photos embedded as Base64 data, their names and products, from Python data."
keywords: common master-detail image in html document, base64 image, GroupDocs.Assembly, Python, report generation
productName: GroupDocs.Assembly for Python via .NET
hideChildren: False
---
{{< alert style="info" >}}In this article, we will use GroupDocs.Assembly to generate a Common Master-Detail report in HTML Document format.{{< /alert >}}{{< alert style="info" >}}The examples read the shop data described in [The Business Layer]({{< ref "assembly/python-net/developer-guide/basic-usage/working-with-a-business-case/the-business-layer.md" >}}).{{< /alert >}}

## Common Master-Detail Image in HTML Document

### Reporting Requirement

As a report developer, you are required to represent the information of the customers and products with the following key requirements:

*   Report must show customers' picture and name.
*   It must associate the customers with their products.
*   Report must be generated in the HTML Document.

### Adding Syntax to be evaluated by GroupDocs.Assembly Engine

An HTML report cannot hold a picture file, so the template embeds each customer's photo in an `img` element as Base64-encoded data. The template is an HTML file whose tags are written with the angle brackets escaped, `&lt;&lt;` and `&gt;&gt;`, so that the HTML stays valid:

```text
<html>
<body>
&lt;&lt;foreach [in customers]&gt;&gt;
<img height="100" width="100" src="data:image/png;base64,&lt;&lt;[PhotoBase64]&gt;&gt;"/>
<h2>&lt;&lt;[CustomerName]&gt;&gt;</h2>
<p><b>Products: &lt;&lt;foreach [in Order]&gt;&gt;&lt;&lt;[IndexOf() != 0 ? ", " : ""]&gt;&gt;&lt;&lt;[Product.ProductName]&gt;&gt;&lt;&lt;/foreach&gt;&gt;</b></p>
&lt;&lt;/foreach&gt;&gt;
</body>
</html>
```

The .NET template computes the Base64 text in the template, with a C# helper class registered as a known type (`FileUtil.GetBytesAsBase64(Photo)`). In Python, the code computes it while loading the data and gives each customer a `PhotoBase64` member, so the template only outputs it.

{{< alert style="success" >}}For detailed technical information about syntax, expressions and report generation by the engine, please visit: [Working with GroupDocs.Assembly Engine]({{< ref "assembly/python-net/developer-guide/basic-usage/working-with-groupdocs.assembly-engine/_index.md" >}}).{{< /alert >}}

### Download Common Master-Detail Template

Please download the sample Common master-detail document we created in this article:

*   [common-master-detail-photos.html](/assembly/python-net/_sample_files/developer-guide/advanced-usage/working-with-image-reports-common-master-detail/common-master-detail-image-in-html-document/common-master-detail-photos.html)

### Generating The Report

Each customer's `Photo` is the file name of its picture. The code reads each picture and stores its Base64 text in the customer's dict.

{{< tabs "example1" >}}
{{< tab "Python" >}}
```python
import base64
import json

from groupdocs.assembly import DataSourceInfo, DocumentAssembler

with open("customers.json", encoding="utf-8") as f:
    customers = json.load(f)

# An HTML report embeds each photo as Base64 text
for customer in customers:
    with open(customer["Photo"], "rb") as photo:
        customer["PhotoBase64"] = base64.b64encode(photo.read()).decode("ascii")

assembler = DocumentAssembler()
assembler.assemble_document("common-master-detail-photos.html", "common-master-detail-photos-report.html", DataSourceInfo(customers, "customers"))
```
{{< /tab >}}
{{< tab "common-master-detail-photos.html" >}}
{{< tab-text >}}
The following sample file is used in this example: [common-master-detail-photos.html](/assembly/python-net/_sample_files/developer-guide/advanced-usage/working-with-image-reports-common-master-detail/common-master-detail-image-in-html-document/common-master-detail-photos.html)
{{< /tab-text >}}
{{< /tab >}}
{{< tab "customers.json" >}}
{{< tab-text >}}
The following sample file is used in this example: [customers.json](/assembly/python-net/_sample_files/developer-guide/advanced-usage/working-with-image-reports-common-master-detail/common-master-detail-image-in-html-document/customers.json)
{{< /tab-text >}}
{{< /tab >}}
{{< tab "quayside-bistro.png" >}}
{{< tab-text >}}
The following sample file is used in this example: [quayside-bistro.png](/assembly/python-net/_sample_files/developer-guide/advanced-usage/working-with-image-reports-common-master-detail/common-master-detail-image-in-html-document/quayside-bistro.png)
{{< /tab-text >}}
{{< /tab >}}
{{< tab "lantern-street-cafe.png" >}}
{{< tab-text >}}
The following sample file is used in this example: [lantern-street-cafe.png](/assembly/python-net/_sample_files/developer-guide/advanced-usage/working-with-image-reports-common-master-detail/common-master-detail-image-in-html-document/lantern-street-cafe.png)
{{< /tab-text >}}
{{< /tab >}}
{{< tab "saltmarsh-deli.png" >}}
{{< tab-text >}}
The following sample file is used in this example: [saltmarsh-deli.png](/assembly/python-net/_sample_files/developer-guide/advanced-usage/working-with-image-reports-common-master-detail/common-master-detail-image-in-html-document/saltmarsh-deli.png)
{{< /tab-text >}}
{{< /tab >}}
{{< tab "pier-nine-kitchen.png" >}}
{{< tab-text >}}
The following sample file is used in this example: [pier-nine-kitchen.png](/assembly/python-net/_sample_files/developer-guide/advanced-usage/working-with-image-reports-common-master-detail/common-master-detail-image-in-html-document/pier-nine-kitchen.png)
{{< /tab-text >}}
{{< /tab >}}
{{< tab "common-master-detail-photos-report.html" >}}  
```text
<html>
<body>

<img height="100" width="100" src="data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAAPAAAADwCAYAAAA+VemSAAAABHNCSVQICAgIfAhkiAAAE+pJREFUeJzt3X1QVOe9B/AvcQWCLMgiL4LKimwElKIhopC4Go3lRquGjpqkNzHR29ibjnfCH53ea9JkMm1Tm0w719ybmdyajk0ybROTToz16g1NogZTfCuaiCiKIkoEBVyQXXCBVe8fZhN8QdjnPLtnn3O+n38ycTzP+cnwPc85z3nO80R0XfJeBREp6Q69CyAicQwwkcIYYCKFMcBECmOAiRTGABMpjAEmUhgDTKQwBphIYQwwkcIYYCKFMcBECmOAiRTGABMpjAEmUphFawNaPyaOuMWfNbS34e+njuNsZztc3R64urvg6u7ChW4PvL6+6/7ud+/K03T+vx2v1nQ8z2+s80dbhiMxJha
[TRUNCATED]
```
[Download full output](/assembly/python-net/_output_files/developer-guide/advanced-usage/working-with-image-reports-common-master-detail/common-master-detail-image-in-html-document/generating_the_report/common-master-detail-photos-report.html)
{{< /tab >}}
{{< /tabs >}}

### Encoding the Photos in the Template

The template can also do the encoding, as the .NET one does. Pass each photo as `bytes`, which reaches the template as a byte array, and make the engine aware of the .NET `System.Convert` class, whose `ToBase64String` method encodes it. Only the expression in the `img` element differs from the template above:

```text
<img height="100" width="100" src="data:image/png;base64,&lt;&lt;[Convert.ToBase64String(PhotoBytes)]&gt;&gt;"/>
```

Without the conversion, a byte array is written as its type name, `System.Byte[]`.

{{< tabs "example2" >}}
{{< tab "Python" >}}
```python
import json

from groupdocs.assembly import DataSourceInfo, DocumentAssembler

with open("customers.json", encoding="utf-8") as f:
    customers = json.load(f)

# Each photo goes to the template as bytes
for customer in customers:
    with open(customer["Photo"], "rb") as photo:
        customer["PhotoBytes"] = photo.read()

assembler = DocumentAssembler()
# The template calls Convert.ToBase64String
assembler.known_types.add("System.Convert")
assembler.assemble_document("common-master-detail-photo-bytes.html", "common-master-detail-photo-bytes-report.html", DataSourceInfo(customers, "customers"))
```
{{< /tab >}}
{{< tab "common-master-detail-photo-bytes.html" >}}
{{< tab-text >}}
The following sample file is used in this example: [common-master-detail-photo-bytes.html](/assembly/python-net/_sample_files/developer-guide/advanced-usage/working-with-image-reports-common-master-detail/common-master-detail-image-in-html-document/common-master-detail-photo-bytes.html)
{{< /tab-text >}}
{{< /tab >}}
{{< tab "customers.json" >}}
{{< tab-text >}}
The following sample file is used in this example: [customers.json](/assembly/python-net/_sample_files/developer-guide/advanced-usage/working-with-image-reports-common-master-detail/common-master-detail-image-in-html-document/customers.json)
{{< /tab-text >}}
{{< /tab >}}
{{< tab "quayside-bistro.png" >}}
{{< tab-text >}}
The following sample file is used in this example: [quayside-bistro.png](/assembly/python-net/_sample_files/developer-guide/advanced-usage/working-with-image-reports-common-master-detail/common-master-detail-image-in-html-document/quayside-bistro.png)
{{< /tab-text >}}
{{< /tab >}}
{{< tab "lantern-street-cafe.png" >}}
{{< tab-text >}}
The following sample file is used in this example: [lantern-street-cafe.png](/assembly/python-net/_sample_files/developer-guide/advanced-usage/working-with-image-reports-common-master-detail/common-master-detail-image-in-html-document/lantern-street-cafe.png)
{{< /tab-text >}}
{{< /tab >}}
{{< tab "saltmarsh-deli.png" >}}
{{< tab-text >}}
The following sample file is used in this example: [saltmarsh-deli.png](/assembly/python-net/_sample_files/developer-guide/advanced-usage/working-with-image-reports-common-master-detail/common-master-detail-image-in-html-document/saltmarsh-deli.png)
{{< /tab-text >}}
{{< /tab >}}
{{< tab "pier-nine-kitchen.png" >}}
{{< tab-text >}}
The following sample file is used in this example: [pier-nine-kitchen.png](/assembly/python-net/_sample_files/developer-guide/advanced-usage/working-with-image-reports-common-master-detail/common-master-detail-image-in-html-document/pier-nine-kitchen.png)
{{< /tab-text >}}
{{< /tab >}}
{{< tab "common-master-detail-photo-bytes-report.html" >}}  
```text
<html>
<body>

<img height="100" width="100" src="data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAAPAAAADwCAYAAAA+VemSAAAABHNCSVQICAgIfAhkiAAAE+pJREFUeJzt3X1QVOe9B/AvcQWCLMgiL4LKimwElKIhopC4Go3lRquGjpqkNzHR29ibjnfCH53ea9JkMm1Tm0w719ybmdyajk0ybROTToz16g1NogZTfCuaiCiKIkoEBVyQXXCBVe8fZhN8QdjnPLtnn3O+n38ycTzP+cnwPc85z3nO80R0XfJeBREp6Q69CyAicQwwkcIYYCKFMcBECmOAiRTGABMpjAEmUhgDTKQwBphIYQwwkcIYYCKFMcBECmOAiRTGABMpjAEmUphFawNaPyaOuMWfNbS34e+njuNsZztc3R64urvg6u7ChW4PvL6+6/7ud+/K03T+vx2v1nQ8z2+s80dbhiMxJha
[TRUNCATED]
```
[Download full output](/assembly/python-net/_output_files/developer-guide/advanced-usage/working-with-image-reports-common-master-detail/common-master-detail-image-in-html-document/encoding_the_photos_in_the_template/common-master-detail-photo-bytes-report.html)
{{< /tab >}}
{{< /tabs >}}
