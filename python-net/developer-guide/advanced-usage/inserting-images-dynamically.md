---
id: inserting-images-dynamically
url: assembly/python-net/inserting-images-dynamically
title: Inserting Images Dynamically
weight: 44
description: "Inserting Images Dynamically with GroupDocs.Assembly for Python via .NET: the template, the Python data and the code."
keywords: inserting images dynamically, GroupDocs.Assembly, Python, report generation
productName: GroupDocs.Assembly for Python via .NET
hideChildren: False
---
{{< alert style="info" >}}The example reads the shop data described in [The Business Layer]({{< ref "assembly/python-net/developer-guide/basic-usage/working-with-a-business-case/the-business-layer.md" >}}).{{< /alert >}}

You can insert images to your reports dynamically using image tags. To declare a dynamically inserted image within your template, do the following steps:

1.  Add a textbox to your template at the place where you want an image to be inserted.
2.  Set common image attributes such as frame, size, and others for the textbox, making the textbox look like a blank inserted image.
3.  Specify an image tag within the textbox using the following syntax.

```text
<<image [image_expression]>>
```

And simply call the assembler method to generate report like following code snippets:

{{< tabs "example1" >}}
{{< tab "Python" >}}
```python
from groupdocs.assembly import DataSourceInfo, DocumentAssembler

assembler = DocumentAssembler()
assembler.assemble_document("inserting-image.docx", "inserting-image-report.docx", DataSourceInfo("logo.png", "expression"))
```
{{< /tab >}}
{{< tab "inserting-image.docx" >}}
{{< tab-text >}}
The following sample file is used in this example: [inserting-image.docx](/assembly/python-net/_sample_files/developer-guide/advanced-usage/inserting-images-dynamically/inserting-image.docx)
{{< /tab-text >}}
{{< /tab >}}
{{< tab "logo.png" >}}
{{< tab-text >}}
The following sample file is used in this example: [logo.png](/assembly/python-net/_sample_files/developer-guide/advanced-usage/inserting-images-dynamically/logo.png)
{{< /tab-text >}}
{{< /tab >}}
{{< tab "inserting-image-report.docx" >}}  
```text
Binary file (DOCX, 16 KB)
```
[Download full output](/assembly/python-net/_output_files/developer-guide/advanced-usage/inserting-images-dynamically/inserting_images_dynamically/inserting-image-report.docx)
{{< /tab >}}
{{< /tabs >}}

The expression declared within an image tag is used by the assembler to build an image to be inserted. The expression must return a value of one of the following types:

*   A byte array containing an image data
*   A [Stream](http://msdn.microsoft.com/en-us/library/system.io.stream(v=vs.110).aspx) instance able to read an image data
*   An [Image](http://msdn.microsoft.com/en-us/library/system.drawing.image(v=vs.110).aspx) object
*   A string containing an image URI, path, or Base64-encoded image data

While building a report, the following procedure is applied to an image tag:

1.  The expression declared within the tag is evaluated and its result is used to form an image.
2.  The corresponding textbox is filled with this image.
3.  The tag is removed from the textbox.

{{< alert style="warning" >}}If the expression declared within an image tag returns a stream object, then it is closed by the assembler as soon as the corresponding image is built. {{< /alert >}}

By default, the assembler stretches an image filling a textbox to the size of the textbox. However, you can change this behavior in the following ways:

*   To keep the size of the textbox and stretch the image within bounds of the textbox preserving the ratio of the image, use the *keepRatio* switch as follows:
  
    ```text
    <<image [image_expression] -keepRatio>>
    ```
    
*   To keep the width of the textbox and change its height preserving the ratio of the image, use the fitHeight switch as follows.
  
    ```text
    <<image [image_expression] -fitHeight>>
    ```
    
*   To keep the height of the textbox and change its width preserving the ratio of the image, use the fitWidth switch as follows.
  
    ```text
    <<image [image_expression] -fitWidth>>
    ```
    
*   To change the size of the textbox according to the size of the image, use the fitSize switch as follows.
  
    ```text
    <<image [image_expression] -fitSize>>
    ```
    
*   To change the size of the textbox according to the size of the image without increasing the size of the textbox, use the fitSizeLim switch as follows.
  
    ```text
    <<image [image_expression] -fitSizeLim>>
    ```
    
    {{< alert style="warning" >}}If the size of the image is greater than the size of the textbox, then the fitSizeLim switch acts like fitHeight or fitWidth. Otherwise, the fitSizeLim switch acts like fitSize.{{< /alert >}}
    

{{< alert style="warning" >}}Dynamic insertion of images from Base64-encoded bytes is available for file formats where dynamic image insertion is available for almost all supported file formats.{{< /alert >}}
