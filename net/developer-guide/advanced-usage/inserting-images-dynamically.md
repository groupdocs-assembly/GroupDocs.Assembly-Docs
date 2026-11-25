---
id: inserting-images-dynamically
url: assembly/net/inserting-images-dynamically
title: Inserting Images Dynamically
weight: 44
description: "Insert images into a report at run time with the image tag in GroupDocs.Assembly for .NET: textbox placeholders, image expressions and the C# call that assembles it."
keywords: 
productName: GroupDocs.Assembly for .NET
hideChildren: False
---
{{< alert style="info" >}}This feature is supported by version 20.3 or greater.{{< /alert >}}{{< alert style="info" >}}The code uses some of the objects defined in [The Business Layer](https://docs.groupdocs.com/assembly/net/the-business-layer/).{{< /alert >}}

You can insert images to your reports dynamically using image tags. To declare a dynamically inserted image within your template, do the following steps:

1.  Add a textbox to your template at the place where you want an image to be inserted.
2.  Set common image attributes such as frame, size, and others for the textbox, making the textbox look like a blank inserted image.
3.  Specify an image tag within the textbox using the following syntax.

```csharp
<<image [image_expression]>>
```

And simply call the assembler method to generate report like following code snippets:

{{< gist GroupDocsGists b06d6c5655c84fc772c6411d66016943 InsertImageDynamicallyInWord_20.3.cs >}}

The expression declared within an image tag is used by the assembler to build an image to be inserted. The expression must return a value of one of the following types:

*   A byte array containing an image data
*   A [Stream](http://msdn.microsoft.com/en-us/library/system.io.stream(v=vs.110).aspx) instance able to read an image data
*   An [Image](http://msdn.microsoft.com/en-us/library/system.drawing.image(v=vs.110).aspx) object
*   A string containing an image URI, path, or Base64-encoded image data

A relative path is resolved against the folder of the template first, and then against the current directory of the application. For a template loaded from a stream, set the folder with `LoadSaveOptions.ResourceLoadBaseUri`. See [Insert Image from a Relative Path]({{< ref "assembly/net/developer-guide/basic-usage/insert-images-dynamically.md#insert-image-from-a-relative-path" >}}).

{{< alert style="warning" >}}Since version 26.11, an image URI reaching the network (`http`, `https`, `ftp`, a UNC path) that comes from data is skipped by default, and the image is left empty. Allow trusted hosts with `LoadSaveOptions.WhitelistedResources`, or set `LoadSaveOptions.SkipExternalResources` to `false`. See [Controlling External Resources]({{< ref "assembly/net/developer-guide/advanced-usage/loading-and-saving-with-external-resource-files/controlling-external-resources.md" >}}).{{< /alert >}}

In a presentation template, an image tag can also be placed in a table cell: the image becomes the picture fill of the cell, including cells of rows repeated by `<<foreach>>`. Tags in shapes of group shapes, including nested groups, are processed like tags in other shapes. See [Insert Images into Table Cells of Presentations]({{< ref "assembly/net/developer-guide/basic-usage/insert-images-dynamically.md#insert-images-into-table-cells-of-presentations" >}}).

While building a report, the following procedure is applied to an image tag:

1.  The expression declared within the tag is evaluated and its result is used to form an image.
2.  The corresponding textbox is filled with this image.
3.  The tag is removed from the textbox.

{{< alert style="warning" >}}If the expression declared within an image tag returns a stream object, then it is closed by the assembler as soon as the corresponding image is built. {{< /alert >}}

By default, the assembler stretches an image filling a textbox to the size of the textbox. However, you can change this behavior in the following ways:

*   To keep the size of the textbox and stretch the image within bounds of the textbox preserving the ratio of the image, use the *keepRatio* switch as follows:
  
    ```csharp
    <<image [image_expression] -keepRatio>>
    ```
    
*   To keep the width of the textbox and change its height preserving the ratio of the image, use the fitHeight switch as follows.
  
    ```csharp
    <<image [image_expression] -fitHeight>>
    ```
    
*   To keep the height of the textbox and change its width preserving the ratio of the image, use the fitWidth switch as follows.
  
    ```csharp
    <<image [image_expression] -fitWidth>>
    ```
    
*   To change the size of the textbox according to the size of the image, use the fitSize switch as follows.
  
    ```csharp
    <<image [image_expression] -fitSize>>
    ```
    
*   To change the size of the textbox according to the size of the image without increasing the size of the textbox, use the fitSizeLim switch as follows.
  
    ```csharp
    <<image [image_expression] -fitSizeLim>>
    ```
    
    {{< alert style="warning" >}}If the size of the image is greater than the size of the textbox, then the fitSizeLim switch acts like fitHeight or fitWidth. Otherwise, the fitSizeLim switch acts like fitSize.{{< /alert >}}
    

{{< alert style="warning" >}}Dynamic insertion of images from Base64-encoded bytes is available for file formats where dynamic image insertion is available for almost all supported file formats.{{< /alert >}}

An image in every row of a table, including a presentation table: [Generate PowerPoint presentations from JSON]({{< ref "/assembly/net/use-cases/generate-presentations-from-json.md" >}}).
