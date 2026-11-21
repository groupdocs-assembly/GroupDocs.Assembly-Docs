---
id: controlling-external-resources
url: assembly/net/controlling-external-resources
title: Controlling External Resources
weight: 3
description: "Control loading of network resources referenced by templates and data: skip, allow, whitelist or provide them with LoadSaveOptions of GroupDocs.Assembly for .NET."
keywords: external resources, SkipExternalResources, TrustTemplateResources, WhitelistedResources, ExternalResourceHandler, ExternalResourceOrigin, image URI, security
productName: GroupDocs.Assembly for .NET
hideChildren: False
---
{{< alert style="info" >}}This feature is supported by version 26.11 or greater.{{< /alert >}}

{{< alert style="warning" >}}Since version 26.11, external resources whose references come from data are **not loaded by default**: for example, `<<image [item.PhotoUrl]>>` where `PhotoUrl` is an `http` or `https` URI gives an empty image. Add the hosts to `LoadSaveOptions.WhitelistedResources`, or set `LoadSaveOptions.SkipExternalResources` to `false` to keep the previous behavior. Resources referenced by the template itself are loaded as before.{{< /alert >}}

An `<<image>>` or `<<doc>>` tag can evaluate to a URI taken from data. When a server assembles documents from data supplied by others, such a URI could make the server request internal addresses. Template documents can reference network resources too: an image of an HTML template, a linked image or an `INCLUDEPICTURE` field of a Word document, an external link of a workbook.

GroupDocs.Assembly tells where each reference to an external resource comes from (`ExternalResourceOrigin`):

*   **Template**: the template document references the resource itself, including a literal URI of a tag such as `<<image ["https://example.com/logo.png"]>>`;
*   **Data**: the reference comes from data, such as a URI a tag expression evaluates to, or a resource of a document inserted by `<<doc>>` from data.

By default, resources referenced by the template are loaded, and resources whose references come from data are skipped.

## Options

Four [LoadSaveOptions](https://reference.groupdocs.com/assembly/net/groupdocs.assembly/loadsaveoptions/) properties control loading of external resources:

| Property | Default | Description |
| --- | --- | --- |
| `SkipExternalResources` | `true` | External resources are not loaded. |
| `TrustTemplateResources` | `true` | Resources referenced by the template are loaded even when skipping is on. Set it to `false` when templates come from untrusted sources. |
| `WhitelistedResources` | empty | Host names (a host and its subdomains) or absolute URI prefixes allowed even when skipping is on. |
| `ExternalResourceHandler` | `null` | Called for every external resource before it is requested, with its `Uri`, `Origin` and pre-set `Skipped` decision, to allow it, skip it, or provide its content. |

External resources are resources reaching the network: `http`, `https` and `ftp` URIs, UNC paths (`\\host\share`) and `file` URIs with a remote host. **Local file paths are not affected**, so templates and `<<image>>` tags using local files keep working.

A skipped image of a document is replaced with a transparent image; a skipped `<<image>>` or `<<doc>>` value is treated as an empty value.

## Allowing, Skipping and Providing Resources

In the example, the template inserts an image with `<<image [expression]>>`, and the image URI comes from data. With default options, the image is skipped. With the host added to `WhitelistedResources`, the image is allowed, and a handler derived from `ExternalResourceHandler` reports every decision and provides the content from a local file instead of requesting it.

```csharp
using System;
using System.IO;
using GroupDocs.Assembly;

const string photoUri = "https://images.example.com/photos/no-photo.jpg";
DocumentAssembler assembler = new DocumentAssembler();

// Default options: the URI comes from data, so the image is skipped and left empty.
assembler.AssembleDocument("Inserting image.docx", "Skipped.docx", new DataSourceInfo(photoUri, "expression"));

// Allow a trusted host and see every decision. The handler can also provide the content itself.
LoadSaveOptions options = new LoadSaveOptions();
options.WhitelistedResources.Add("images.example.com");
options.ExternalResourceHandler = new LocalImageHandler("no-photo.jpg");

assembler.AssembleDocument("Inserting image.docx", "Provided.docx", options, new DataSourceInfo(photoUri, "expression"));

public class LocalImageHandler : ExternalResourceHandler
{
    private readonly string mImagePath;

    public LocalImageHandler(string imagePath) { mImagePath = imagePath; }

    public override void OnLoading(ExternalResourceLoadingArgs args)
    {
        Console.WriteLine($"{args.Origin} resource {args.Uri}: {(args.Skipped ? "skipped" : "allowed")}");

        // Provide the content instead of requesting it.
        if (!args.Skipped && args.Uri.StartsWith("https://images.example.com/", StringComparison.OrdinalIgnoreCase))
            args.Data = File.ReadAllBytes(mImagePath);
    }
}
```

Output:

```
Data resource https://images.example.com/photos/no-photo.jpg: allowed
```

In the handler, set `args.Skipped` to `true` to skip a resource or to `false` to allow it, and set `args.Data` to provide the content of the resource yourself.

Example: [ControlExternalResources.cs](https://github.com/groupdocs-assembly/GroupDocs.Assembly-for-.NET/blob/master/Examples/GroupDocs.Assembly.Examples.CSharp/AdvancedUsage/ControlExternalResources.cs).

## Restoring the Previous Behavior

To load all external resources as versions before 26.11 did, turn skipping off:

```csharp
LoadSaveOptions options = new LoadSaveOptions();
options.SkipExternalResources = false;

DocumentAssembler assembler = new DocumentAssembler();
assembler.AssembleDocument("Inserting image.docx", "output.docx", options, new DataSourceInfo(photoUri, "expression"));
```

## Templates from Untrusted Sources

When templates also come from untrusted sources, do not trust their resources either. Only whitelisted resources are then loaded:

```csharp
LoadSaveOptions options = new LoadSaveOptions();
options.TrustTemplateResources = false;
options.WhitelistedResources.Add("https://cdn.example.com/assets/");

DocumentAssembler assembler = new DocumentAssembler();
assembler.AssembleDocument("Untrusted template.docx", "output.docx", options, new DataSourceInfo(photoUri, "expression"));
```

A scenario where the data comes from outside and the policy earns its keep: [Generate Word documents from LLM output]({{< ref "/assembly/net/use-cases/generate-documents-from-llm-output.md" >}}).
