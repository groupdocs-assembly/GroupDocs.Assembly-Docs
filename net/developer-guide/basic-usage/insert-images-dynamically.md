---
id: assembly-basic-usage-generate-images
url: assembly/net/basic-usage-generate-images
title: Insert Images Dynamically in C#
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
    
    DocumentAssembler assembler = new DocumentAssembler();
    assembler.AssembleDocument("ImageTemplate.docx", "ImageOutput.docx", 
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

