---
id: assembly-basic-usage-generate-images-java
url: assembly/java/basic-usage-generate-images
linktitle: Insert Images Dynamically
title: Insert Images Dynamically
weight: 20
description: "Insert images into documents from file paths, URLs, or binary data sources during document assembly using GroupDocs.Assembly for Java."
keywords: insert images, dynamic images, image from file, image from URL, image from stream, generate images, Java
productName: GroupDocs.Assembly for Java
hideChildren: False
---

## Overview

GroupDocs.Assembly for Java allows you to insert images dynamically into documents using image tags. Images can be loaded from file paths, URLs, streams, byte arrays, `BufferedImage` objects, or Base64-encoded strings, making it easy to include dynamic images in your reports.

The main classes involved are:
- [DocumentAssembler](https://reference.groupdocs.com/assembly/java/com.groupdocs.assembly/documentassembler/) - assembles documents
- [DataSourceInfo](https://reference.groupdocs.com/assembly/java/com.groupdocs.assembly/datasourceinfo/) - wraps data sources

Here are the steps to insert images dynamically:

* Add a textbox to your template at the location where you want the image
* Set the textbox size and appearance to match desired image dimensions
* Insert an image tag `<<image [expression]>>` within the textbox
* Provide image data from file path, URL, stream, or byte array
* Assemble the document

{{< alert style="info" >}}
Image tags are replaced with actual images during document assembly. The textbox acts as a placeholder and container for the image.
{{< /alert >}}

{{< alert style="info" >}}
The expression of an image tag must return a value of one of the following types: `byte[]` (image data), `java.io.InputStream` (a stream to read image data from), `java.awt.image.BufferedImage`, or `String` (a file path, a URI such as `https://...` or `file:/...`, or Base64-encoded image bytes). The type is checked by the declared return type of the getter, so declare getters with one of these types rather than `Object`.
{{< /alert >}}

## Insert Image from File Path

Insert an image from a file path:

```java
import com.groupdocs.assembly.*;

public class Product
{
    private String name;
    private String imagePath;

    public Product(String name, String imagePath)
    {
        this.name = name;
        this.imagePath = imagePath;
    }

    public String getName() { return name; }
    public String getImagePath() { return imagePath; }
}

public static void insertImageFromFilePath() throws Exception
{
    // Sample data with image path
    Product product = new Product("Laptop", "C:\\Images\\laptop.jpg");

    // Assemble document
    DocumentAssembler assembler = new DocumentAssembler();
    assembler.assembleDocument("ImageTemplate.docx", "ImageOutput.docx",
        new DataSourceInfo(product, "product"));

    System.out.println("Image inserted from file path successfully.");
}
```

## Template Structure for Images

In your template (ImageTemplate.docx):

1. Insert a textbox where you want the image
2. Set the textbox size (width and height)
3. Add the image tag inside the textbox:

```
Product: <<[product.getName()]>>

[Textbox with image tag:]
<<image [product.getImagePath()]>>
```

## Insert Image from URL

Insert an image from a URL:

```java
import com.groupdocs.assembly.*;

public class OnlineProduct
{
    private String name;
    private String imageUrl;

    public OnlineProduct(String name, String imageUrl)
    {
        this.name = name;
        this.imageUrl = imageUrl;
    }

    public String getName() { return name; }
    public String getImageUrl() { return imageUrl; }
}

public static void insertImageFromUrl() throws Exception
{
    OnlineProduct product = new OnlineProduct("Laptop", "https://example.com/images/laptop.jpg");

    DocumentAssembler assembler = new DocumentAssembler();
    assembler.assembleDocument("ImageTemplate.docx", "ImageOutput.docx",
        new DataSourceInfo(product, "product"));

    System.out.println("Image inserted from URL successfully.");
}
```

Template:

```
Product: <<[product.getName()]>>

[Textbox:]
<<image [product.getImageUrl()]>>
```

## Insert Image from Byte Array

Insert an image from binary data:

```java
import com.groupdocs.assembly.*;
import java.nio.file.Files;
import java.nio.file.Paths;

public class ProductWithImageData
{
    private String name;
    private byte[] imageData;

    public ProductWithImageData(String name, byte[] imageData)
    {
        this.name = name;
        this.imageData = imageData;
    }

    public String getName() { return name; }
    public byte[] getImageData() { return imageData; }
}

public static void insertImageFromByteArray() throws Exception
{
    // Load image into byte array
    byte[] imageBytes = Files.readAllBytes(Paths.get("C:\\Images\\laptop.jpg"));

    ProductWithImageData product = new ProductWithImageData("Laptop", imageBytes);

    DocumentAssembler assembler = new DocumentAssembler();
    assembler.assembleDocument("ImageTemplate.docx", "ImageOutput.docx",
        new DataSourceInfo(product, "product"));

    System.out.println("Image inserted from byte array successfully.");
}
```

Template:

```
Product: <<[product.getName()]>>

[Textbox:]
<<image [product.getImageData()]>>
```

## Insert Image from Stream

Insert an image from a stream:

```java
import com.groupdocs.assembly.*;
import java.io.FileInputStream;
import java.io.InputStream;

public class ProductWithImageStream
{
    private String name;
    private InputStream imageStream;

    public ProductWithImageStream(String name, InputStream imageStream)
    {
        this.name = name;
        this.imageStream = imageStream;
    }

    public String getName() { return name; }
    public InputStream getImageStream() { return imageStream; }
}

public static void insertImageFromStream() throws Exception
{
    try (InputStream imageStream = new FileInputStream("C:\\Images\\laptop.jpg"))
    {
        ProductWithImageStream product = new ProductWithImageStream("Laptop", imageStream);

        DocumentAssembler assembler = new DocumentAssembler();
        assembler.assembleDocument("ImageTemplate.docx", "ImageOutput.docx",
            new DataSourceInfo(product, "product"));

        System.out.println("Image inserted from stream successfully.");
    }
}
```

## Image Sizing Options

Control how images are sized within textboxes:

```java
import com.groupdocs.assembly.*;

public static void insertImageWithSizing() throws Exception
{
    Product product = new Product("Laptop", "C:\\Images\\laptop.jpg");

    DocumentAssembler assembler = new DocumentAssembler();
    assembler.assembleDocument("ImageTemplate.docx", "ImageOutput.docx",
        new DataSourceInfo(product, "product"));

    System.out.println("Image inserted with sizing options.");
}
```

Template sizing options:

- `<<image [product.getImagePath()]>>` - Stretch to fill textbox (default)
- `<<image [product.getImagePath()] -keepRatio>>` - Keep aspect ratio within textbox
- `<<image [product.getImagePath()] -fitHeight>>` - Fit to textbox height
- `<<image [product.getImagePath()] -fitWidth>>` - Fit to textbox width
- `<<image [product.getImagePath()] -fitSize>>` - Resize textbox to image size
- `<<image [product.getImagePath()] -fitSizeLim>>` - Resize textbox up to image size

## Insert Multiple Images from Collection

Insert images for each item in a collection:

```java
import com.groupdocs.assembly.*;

public static void insertImagesFromCollection() throws Exception
{
    // Pass an array (or a POJO with a typed List<Product> getter) so that the engine
    // knows the item type; a raw java.util.List passed directly loses its element type
    Product[] products = new Product[]
    {
        new Product("Laptop", "C:\\Images\\laptop.jpg"),
        new Product("Mouse", "C:\\Images\\mouse.jpg")
    };

    DocumentAssembler assembler = new DocumentAssembler();
    assembler.assembleDocument("ImagesTemplate.docx", "ImagesOutput.docx",
        new DataSourceInfo(products, "products"));

    System.out.println("Images inserted from collection successfully.");
}
```

Template with foreach:

```
<<foreach [in products]>>
Product: <<[getName()]>>

[Textbox:]
<<image [getImagePath()]>>

<</foreach>>
```

{{< alert style="warning" >}}
If an image expression returns a stream, the assembler reads the image data from it but does not close it. Close the stream yourself after the document is assembled, for example with a try-with-resources statement as shown above.
{{< /alert >}}

### Advanced Usage Topics

To learn more about image formatting, Base64-encoded images, image optimization, and advanced image handling, please refer to the [advanced usage section]({{< ref "assembly/java/developer-guide/advanced-usage/_index.md" >}}).

## More resources

### GitHub Examples

You may easily run the code above and see the feature in action in our GitHub examples:

* [GroupDocs.Assembly for Java examples, plugins, and showcase](https://github.com/groupdocs-assembly/GroupDocs.Assembly-for-Java)
* [GroupDocs.Assembly for .NET examples, plugins, and showcase](https://github.com/groupdocs-assembly/GroupDocs.Assembly-for-.NET)
* [GroupDocs.Assembly for Python via .NET examples, plugins, and showcase](https://github.com/groupdocs-assembly/GroupDocs.Assembly-for-Python-via-.NET)

### Free Online Apps

Along with the full-featured Java library, we provide simple but powerful free online apps.

To assemble documents from templates and data sources, you can use the online apps from the **[GroupDocs.Assembly App Product Family](https://products.groupdocs.app/assembly/family)**.

