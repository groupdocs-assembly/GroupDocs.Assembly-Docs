---
id: {REPLACE-WITH-UNIQUE-ID}
url: assmbely/net/{REPLACE-WITH-TOPICS-URL}
title: {REPLACE-WITH-TITLE}
weight: {REPLACE-SEQUENCE-FROM-most-simple-topics-to-complicated}
description: "{REPLACE-WITH-UNIQUE-ID}"
keywords: {replace with keywords here according to the article use words assemble, generate, compose, collect and sinomymous}
productName: GroupDocs.Assembly for .NET 
toc: True
---
## Overview

{Put here short overview about this topics usag - use this article specific keywords}
{Explaine which classes should be used with name and link to the reference like
See objects in reference
https://reference.groupdocs.com/assembly/net/

Here are the steps how to XXXX:
* Instantiate the required [Assmbler](https://reference.groupdocs.com/assembly/net/groupdocs.assembly/datasourceinfo/) object with the settings you want to generate the preview
* Instantiate the [DataSource](https://reference.groupdocs.com/assembly/net/groupdocs.assembly/datasourceinfo/) object with:
* delegate for Assembly stream creation (see event handler [CreateAssemblyStream](https://reference.groupdocs.com/Assembly/net/groupdocs.Assembly.options/createAssemblystream));
* unique Assembly identifier.
and so on
}

Use special block to highlight some important points for example

{{< alert style="info" >}}
Stream that were created by [CreateAssemblyStream](https://reference.groupdocs.com/Assembly/net/groupdocs.Assembly.options/createAssemblystream) delegate will be disposed automatically once after generation of preview image. If you need to implement custom image preview stream disposing you have to pass additional argument [ReleaseAssemblyStream](https://reference.groupdocs.com/Assembly/net/groupdocs.Assembly.options/releaseAssemblystream) to clean up resources.  
{{< /alert >}}

* Call the static method [GenerateAssemblyPreview](https://reference.groupdocs.com/Assembly/net/groupdocs.Assembly/Assembly/generateAssemblypreview) method of [Assembly](https://reference.groupdocs.com/Assembly/net/groupdocs.Assembly/Assembly) and pass [PreviewAssemblyOptions](https://reference.groupdocs.com/Assembly/net/groupdocs.Assembly.options/previewAssemblyoptions) to it.

## {Repalce with topic}

This example demonstrates how to ..............

```csharp
public static void XXXX()
{
    
}

```

##  Adaptive rendering for QR Code Assembly previews

{{< alert style="info" >}}
If the specified width and height are not appropriate for generating a readable QR Code preview, the system will automatically use default size values. These defaults are chosen as the nearest optimal dimensions to ensure the QR Code remains clear and scannable. 
{{< /alert >}}

This example demonstrates how to generate a preview image for a QR Code Assembly using GroupDocs.Assembly. You’ll see how to configure the QR Code’s appearance, including size, color, and text alignment, and how to generate and save the preview image stream.

```csharp
public static void XXXX()
{
    
}

```

##  Adaptive rendering for Barcode Assembly previews

{{< alert style="info" >}}
When the width and height provided for the Barcode preview are not suitable, the preview generation will fall back to default size values. These defaults are selected to produce a barcode image that is readable and properly rendered.
{{< /alert >}}

This section shows how to create a preview for a Barcode Assembly. The example covers setting barcode properties such as type, size, and color, as well as generating the preview image with a custom stream handler.

```csharp
public static void GetPreview()
{
    // Initialize QR Code signing options
    BarcodeSignOptions signOptions = new BarcodeSignOptions("GROUP DOCS", BarcodeTypes.MaxiCode)
    {
        Width = 400,                          // Width of the Barcode code
        Height = 400,                         // Height of the Barcode code
        ForeColor = Color.Red,                // Color of the Barcode code
        CodeTextAlignment = CodeTextAlignment.Below, // Text alignment relative to the Barcode code
        Text = "GROUP DOCS"                   // Text displayed below the Barcode code
    };

    // Configure preview generation options for the QR code Assembly
    PreviewAssemblyOptions previewOptions = new PreviewAssemblyOptions(
        qrSignOptions,
        CreateAssemblyStream,   // Delegate to create the stream
        ReleaseAssemblyStream   // Delegate to release the stream
    )
    {
        AssemblyId = Guid.NewGuid().ToString(),  // Unique identifier for the preview
        PreviewFormat = PreviewAssemblyOptions.PreviewFormats.PNG  // Output format of preview
    };

    // Generate the Assembly preview image
    Assembly.GenerateAssemblyPreview(previewOptions);
}

private static Stream CreateAssemblyStream(PreviewAssemblyOptions previewOptions)
{
    string imageFilePath = 
        $"Assembly-{previewOptions.AssemblyId}-" +
        $"{previewOptions.SignOptions.GetType().Name}.jpg";

    return new FileStream(imageFilePath, FileMode.Create);
}

private static void ReleaseAssemblyStream(PreviewAssemblyOptions previewOptions, 
    Stream AssemblyStream)
{
    AssemblyStream.Dispose();
    Console.WriteLine(
        $"Assembly {previewOptions.AssemblyId}-" +
        $"{previewOptions.SignOptions.GetType().Name} is ready for preview"
    );
}
```

## Rotate Barcode and QR Code previews

This example demonstrates how to apply rotation to Barcode and QR Code Assembly previews. Rotation can help fit Assemblys into specific layout requirements or create visual effects.

```csharp
public static void GetPreview()
{
    // Initialize Barcode signing options
    BarcodeSignOptions barcodeSignOptions = new BarcodeSignOptions("GROUP DOCS", BarcodeTypes.MaxiCode)
    {
        Width = 400,                               // Width of the barcode
        Height = 400,                              // Height of the barcode
        ForeColor = Color.Red,                     // Foreground color of the barcode
        CodeTextAlignment = CodeTextAlignment.Below,  // Position of the text relative to the barcode
        Text = "GROUP DOCS",                       // Text displayed with the barcode
        RotationAngle = 45                         // Rotate the barcode by 45 degrees
    };

    // Configure preview generation options for the QR code Assembly
    PreviewAssemblyOptions previewOptions = new PreviewAssemblyOptions(
        qrSignOptions,
        CreateAssemblyStream,   // Delegate to create the stream
        ReleaseAssemblyStream   // Delegate to release the stream
    )
    {
        AssemblyId = Guid.NewGuid().ToString(),  // Unique identifier for the preview
        PreviewFormat = PreviewAssemblyOptions.PreviewFormats.PNG  // Output format of preview
    };

    // Generate the Assembly preview image
    Assembly.GenerateAssemblyPreview(previewOptions);
}

private static Stream CreateAssemblyStream(PreviewAssemblyOptions previewOptions)
{
    string imageFilePath = 
        $"Assembly-{previewOptions.AssemblyId}-" +
        $"{previewOptions.SignOptions.GetType().Name}.jpg";

    return new FileStream(imageFilePath, FileMode.Create);
}

private static void ReleaseAssemblyStream(PreviewAssemblyOptions previewOptions, 
    Stream AssemblyStream)
{
    AssemblyStream.Dispose();
    Console.WriteLine(
        $"Assembly {previewOptions.AssemblyId}-" +
        $"{previewOptions.SignOptions.GetType().Name} is ready for preview"
    );
}
```

## Transparency for Barcode/QR previews

This snippet shows how to set the transparency level of Barcode or QR Code previews, allowing you to customize the Assembly's visual blending with the underlying document.

```csharp
public static void GetPreview()
{
    // Initialize barcode signing options with Codabar type
    BarcodeSignOptions barcodeSignOptions = new BarcodeSignOptions("GROUP DOCS", BarcodeTypes.Codabar)
    {
        Width = 400,                               // Width of the barcode preview
        Height = 400,                              // Height of the barcode preview
        ForeColor = Color.Red,                     // Foreground color of the barcode bars
        CodeTextAlignment = CodeTextAlignment.Below,  // Position text below the barcode
        Text = "GROUP DOCS",                       // Text displayed with the barcode
        Transparency = 0.5                         // Set barcode background transparency (50%)
    };

    // Configure preview generation options for the QR code Assembly
    PreviewAssemblyOptions previewOptions = new PreviewAssemblyOptions(
        qrSignOptions,
        CreateAssemblyStream,   // Delegate to create the stream
        ReleaseAssemblyStream   // Delegate to release the stream
    )
    {
        AssemblyId = Guid.NewGuid().ToString(),  // Unique identifier for the preview
        PreviewFormat = PreviewAssemblyOptions.PreviewFormats.PNG  // Output format of preview
    };

    // Generate the Assembly preview image
    Assembly.GenerateAssemblyPreview(previewOptions);
}

private static Stream CreateAssemblyStream(PreviewAssemblyOptions previewOptions)
{
    string imageFilePath = 
        $"Assembly-{previewOptions.AssemblyId}-" +
        $"{previewOptions.SignOptions.GetType().Name}.jpg";

    return new FileStream(imageFilePath, FileMode.Create);
}

private static void ReleaseAssemblyStream(PreviewAssemblyOptions previewOptions, 
    Stream AssemblyStream)
{
    AssemblyStream.Dispose();
    Console.WriteLine(
        $"Assembly {previewOptions.AssemblyId}-" +
        $"{previewOptions.SignOptions.GetType().Name} is ready for preview"
    );
}
```

### Advanced Usage Topics

To learn more about document eSign features, please refer to the [advanced usage section]({{< ref "assembly/net/developer-guide/advanced-usage/_index.md" >}}).

## More resources

### GitHub Examples

You may easily run the code above and see the feature in action in our GitHub examples:

* [GroupDocs.Assembly for .NET examples, plugins, and showcase](https://github.com/groupdocs-assembly/GroupDocs.Assembly-for-.NET)
* [GroupDocs.Assembly for Java examples, plugins, and showcase](https://github.com/groupdocs-assembly/GroupDocs.Assembly-for-Java)
* [GroupDocs.Assembly for Python via .NET examples, plugins, and showcase](https://github.com/groupdocs-assembly/GroupDocs.Assembly-for-Python-via-.NET)

### Free Online Apps

Along with the full-featured .NET library, we provide simple but powerful free online apps.

To sign PDF, Word, Excel, PowerPoint, and other documents you can use the online apps from the **[GroupDocs.Assembly App Product Family](https://products.groupdocs.app/assembly/family)**.
