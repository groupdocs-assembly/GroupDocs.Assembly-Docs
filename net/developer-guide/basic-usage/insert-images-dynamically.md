---
id: assembly-basic-usage-generate-images
url: assembly/net/basic-usage-generate-images
linktitle: Insert Images Dynamically
title: Insert Images Dynamically
weight: 20
description: "Insert images into documents from file paths, URLs, or binary data sources during document assembly."
keywords: insert images, dynamic images, image from file, image from URL, image from stream, generate images
productName: GroupDocs.Assembly for .NET
hideChildren: False
---

## Overview

GroupDocs.Assembly for .NET allows you to insert images dynamically into documents using image tags. Images can be loaded from file paths, URLs, streams, byte arrays, or Base64-encoded strings, making it easy to include dynamic images in your reports.

The main classes involved are:
- [DocumentAssembler](https://reference.groupdocs.com/assembly/net/groupdocs.assembly/documentassembler/) - assembles documents
- [DataSourceInfo](https://reference.groupdocs.com/assembly/net/groupdocs.assembly/datasourceinfo/) - wraps data sources

Here are the steps to insert images dynamically:

* Add a textbox to your template at the location where you want the image
* Set the textbox size and appearance to match desired image dimensions
* Insert an image tag `<<image [expression]>>` within the textbox
* Provide image data from file path, URL, stream, or byte array
* Assemble the document

{{< alert style="info" >}}
Image tags are replaced with actual images during document assembly. The textbox acts as a placeholder and container for the image.
{{< /alert >}}

## Insert Image from File Path

Insert an image from a file path:

```csharp
using GroupDocs.Assembly;

public class Product
{
    public string Name { get; set; }
    public string ImagePath { get; set; }
}

public static void InsertImageFromFilePath()
{
    // Sample data with image path
    var product = new Product
    {
        Name = "Laptop",
        ImagePath = @"C:\Images\laptop.jpg"
    };
    
    // Assemble document
    DocumentAssembler assembler = new DocumentAssembler();
    assembler.AssembleDocument("ImageTemplate.docx", "ImageOutput.docx", 
        new DataSourceInfo(product, "product"));
    
    Console.WriteLine("Image inserted from file path successfully.");
}
```

## Template Structure for Images

In your template (ImageTemplate.docx):

1. Insert a textbox where you want the image
2. Set the textbox size (width and height)
3. Add the image tag inside the textbox:

```
Product: <<[product.Name]>>

[Textbox with image tag:]
<<image [product.ImagePath]>>
```

## Insert Image from URL

Insert an image from a URL:

{{< alert style="warning" >}}
Since version 26.11, external resources whose references come from data, such as an `http` or `https` URI returned by an image expression, are skipped by default and give an empty image. Allow the hosts you trust with `LoadSaveOptions.WhitelistedResources`, as shown below, or set `LoadSaveOptions.SkipExternalResources` to `false`. See [Controlling External Resources]({{< ref "assembly/net/developer-guide/advanced-usage/loading-and-saving-with-external-resource-files/controlling-external-resources.md" >}}).
{{< /alert >}}

```csharp
using GroupDocs.Assembly;

public class Product
{
    public string Name { get; set; }
    public string ImageUrl { get; set; }
}

public static void InsertImageFromUrl()
{
    var product = new Product
    {
        Name = "Laptop",
        ImageUrl = "https://example.com/images/laptop.jpg"
    };
    
    // The URL comes from data, so its host must be allowed
    LoadSaveOptions options = new LoadSaveOptions();
    options.WhitelistedResources.Add("example.com");

    DocumentAssembler assembler = new DocumentAssembler();
    assembler.AssembleDocument("ImageTemplate.docx", "ImageOutput.docx", options,
        new DataSourceInfo(product, "product"));
    
    Console.WriteLine("Image inserted from URL successfully.");
}
```

Template:

```
Product: <<[product.Name]>>

[Textbox:]
<<image [product.ImageUrl]>>
```

## Insert Image from a Relative Path

A relative file path returned by an image expression, such as `"../Images/no-photo.jpg"`, is resolved against the folder of the template first, by analogy with linked resources of Microsoft Office documents. If no file exists there, the current directory of the application is used. A template loaded from a stream has no folder: set it with `LoadSaveOptions.ResourceLoadBaseUri`.

In the example, templates are in `C:\Reports\Templates`, images are in `C:\Reports\Images`, and the template inserts `<<image [expression]>>`:

```csharp
using GroupDocs.Assembly;
using System.IO;

public static void InsertImageFromRelativePath()
{
    const string relativePath = "../Images/no-photo.jpg";
    DocumentAssembler assembler = new DocumentAssembler();

    // A template loaded from a file: the path is resolved against the folder of the template.
    assembler.AssembleDocument(@"C:\Reports\Templates\Inserting image.docx", "output.docx",
        new DataSourceInfo(relativePath, "expression"));

    // A template loaded from a stream has no folder: set it with ResourceLoadBaseUri.
    LoadSaveOptions options = new LoadSaveOptions();
    options.ResourceLoadBaseUri = @"C:\Reports\Templates";

    using (FileStream template = File.OpenRead(@"C:\Reports\Templates\Inserting image.docx"))
    using (FileStream report = File.Create("output-from-stream.docx"))
    {
        assembler.AssembleDocument(template, report, options, new DataSourceInfo(relativePath, "expression"));
    }
}
```

Relative paths are resolved this way since version 26.11. Example: [InsertImageFromRelativePath.cs](https://github.com/groupdocs-assembly/GroupDocs.Assembly-for-.NET/blob/master/Examples/GroupDocs.Assembly.Examples.CSharp/AdvancedUsage/InsertImageFromRelativePath.cs).

## Insert Image from Byte Array

Insert an image from binary data:

```csharp
using GroupDocs.Assembly;
using System.IO;

public class Product
{
    public string Name { get; set; }
    public byte[] ImageData { get; set; }
}

public static void InsertImageFromByteArray()
{
    // Load image into byte array
    byte[] imageBytes = File.ReadAllBytes(@"C:\Images\laptop.jpg");
    
    var product = new Product
    {
        Name = "Laptop",
        ImageData = imageBytes
    };
    
    DocumentAssembler assembler = new DocumentAssembler();
    assembler.AssembleDocument("ImageTemplate.docx", "ImageOutput.docx", 
        new DataSourceInfo(product, "product"));
    
    Console.WriteLine("Image inserted from byte array successfully.");
}
```

Template:

```
Product: <<[product.Name]>>

[Textbox:]
<<image [product.ImageData]>>
```

## Insert Image from Stream

Insert an image from a stream:

```csharp
using GroupDocs.Assembly;
using System.IO;

public class Product
{
    public string Name { get; set; }
    public Stream ImageStream { get; set; }
}

public static void InsertImageFromStream()
{
    using (FileStream imageStream = new FileStream(@"C:\Images\laptop.jpg", FileMode.Open))
    {
        var product = new Product
        {
            Name = "Laptop",
            ImageStream = imageStream
        };
        
        DocumentAssembler assembler = new DocumentAssembler();
        assembler.AssembleDocument("ImageTemplate.docx", "ImageOutput.docx", 
            new DataSourceInfo(product, "product"));
        
        Console.WriteLine("Image inserted from stream successfully.");
    }
}
```

## Image Sizing Options

Control how images are sized within textboxes:

```csharp
using GroupDocs.Assembly;

public static void InsertImageWithSizing()
{
    var product = new Product
    {
        Name = "Laptop",
        ImagePath = @"C:\Images\laptop.jpg"
    };
    
    DocumentAssembler assembler = new DocumentAssembler();
    assembler.AssembleDocument("ImageTemplate.docx", "ImageOutput.docx", 
        new DataSourceInfo(product, "product"));
    
    Console.WriteLine("Image inserted with sizing options.");
}
```

Template sizing options:

- `<<image [product.ImagePath]>>` - Stretch to fill textbox (default)
- `<<image [product.ImagePath] -keepRatio>>` - Keep aspect ratio within textbox
- `<<image [product.ImagePath] -fitHeight>>` - Fit to textbox height
- `<<image [product.ImagePath] -fitWidth>>` - Fit to textbox width
- `<<image [product.ImagePath] -fitSize>>` - Resize textbox to image size
- `<<image [product.ImagePath] -fitSizeLim>>` - Resize textbox up to image size

## Insert Multiple Images from Collection

Insert images for each item in a collection:

```csharp
using GroupDocs.Assembly;
using System.Collections.Generic;

public static void InsertImagesFromCollection()
{
    List<Product> products = new List<Product>
    {
        new Product { Name = "Laptop", ImagePath = @"C:\Images\laptop.jpg" },
        new Product { Name = "Mouse", ImagePath = @"C:\Images\mouse.jpg" }
    };
    
    DocumentAssembler assembler = new DocumentAssembler();
    assembler.AssembleDocument("ImagesTemplate.docx", "ImagesOutput.docx", 
        new DataSourceInfo(products, "products"));
    
    Console.WriteLine("Images inserted from collection successfully.");
}
```

Template with foreach:

```
<<foreach [in products]>>
Product: <<[Name]>>

[Textbox:]
<<image [ImagePath]>>

<</foreach>>
```

## Insert Images into Table Cells of Presentations

In a presentation template, a table cell is an image container as well: the image becomes the picture fill of the cell, including cells of rows repeated by `<<foreach>>`. A template table listing products with their pictures looks like this:

| Name | Photo |
| --- | --- |
| `<<foreach [p in products]>><<[p.Name]>>` | `<<image [p.Photo] -fitHeight>><</foreach>>` |

```csharp
using GroupDocs.Assembly;

public class Product
{
    public string Name { get; set; }
    public string Photo { get; set; }
}

public static void InsertImagesIntoTableCells()
{
    Product[] products =
    {
        new Product { Name = "Logo", Photo = "Images/Logo.jpg" },
        new Product { Name = "No photo", Photo = "Images/no-photo.jpg" },
    };

    new DocumentAssembler().AssembleDocument("Image in table cell.pptx", "output.pptx",
        new DataSourceInfo(products, "products"));
}
```

With `-fitHeight`, the row grows to show the image with its aspect ratio. The other fit switches keep the aspect ratio of the image within the cell, because the width of a cell is the width of its whole column. Tags in shapes of group shapes, including nested groups, are processed like tags in other shapes. Table cells and group shapes of presentations are supported since version 26.11. Example: [InsertImageIntoTableCell.cs](https://github.com/groupdocs-assembly/GroupDocs.Assembly-for-.NET/blob/master/Examples/GroupDocs.Assembly.Examples.CSharp/AdvancedUsage/InsertImageIntoTableCell.cs).

{{< alert style="warning" >}}
If an image expression returns a stream, the stream is automatically closed by the assembler after the image is loaded. Do not dispose the stream manually.
{{< /alert >}}

### Advanced Usage Topics

To learn more about image formatting, Base64-encoded images, image optimization, and advanced image handling, please refer to the [advanced usage section]({{< ref "assembly/net/developer-guide/advanced-usage/_index.md" >}}).

## More resources

### GitHub Examples

You may easily run the code above and see the feature in action in our GitHub examples:

* [GroupDocs.Assembly for .NET examples, plugins, and showcase](https://github.com/groupdocs-assembly/GroupDocs.Assembly-for-.NET)
* [GroupDocs.Assembly for Java examples, plugins, and showcase](https://github.com/groupdocs-assembly/GroupDocs.Assembly-for-Java)
* [GroupDocs.Assembly for Python via .NET examples, plugins, and showcase](https://github.com/groupdocs-assembly/GroupDocs.Assembly-for-Python-via-.NET)

### Free Online Apps

Along with the full-featured .NET library, we provide simple but powerful free online apps.

To assemble documents from templates and data sources, you can use the online apps from the **[GroupDocs.Assembly App Product Family](https://products.groupdocs.app/assembly/family)**.

