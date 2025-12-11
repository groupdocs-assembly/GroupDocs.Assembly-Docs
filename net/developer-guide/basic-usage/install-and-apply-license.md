---
id: assembly-basic-usage-install-license
url: assembly/net/basic-usage-install-and-license
linktitle: Install and Apply License
title: Install GroupDocs.Assembly for .NET and Apply License
weight: 1
description: "Learn how to install GroupDocs.Assembly via NuGet and apply a license to remove evaluation limitations in your .NET applications."
keywords: install, NuGet, license, setup, configure, GroupDocs.Assembly, .NET, C#, apply license
productName: GroupDocs.Assembly for .NET
hideChildren: False
---

## Overview

Before you can start generating documents with GroupDocs.Assembly for .NET, you need to install the library and apply a license. This guide shows you how to install the package via NuGet and configure licensing to remove evaluation limitations.

The main classes involved are:
- [License](https://reference.groupdocs.com/assembly/net/groupdocs.assembly/license/) - for applying licenses
- [DocumentAssembler](https://reference.groupdocs.com/assembly/net/groupdocs.assembly/documentassembler/) - for assembling documents

Here are the steps to get started:

* Install GroupDocs.Assembly package via NuGet Package Manager or Package Manager Console
* Apply a license from a file or stream using the `License.SetLicense` method
* Verify that the license is applied correctly before using DocumentAssembler

{{< alert style="info" >}}
Calling `License.SetLicense` multiple times is not harmful but wastes processor time. In Windows Forms or console applications, call it once during startup. In ASP.NET applications, call it in `Application_Start` method in Global.asax.cs.
{{< /alert >}}

## Install via NuGet Package Manager

The easiest way to install GroupDocs.Assembly is through NuGet Package Manager in Visual Studio.

1. Right-click your project in Solution Explorer
2. Select "Manage NuGet Packages"
3. Search for "GroupDocs.Assembly"
4. Click "Install" to install the latest version

## Install via Package Manager Console

Alternatively, you can install the package using Package Manager Console:

```csharp
// Run this command in Package Manager Console:
// Install-Package GroupDocs.Assembly
```

## Apply License from File

After installation, apply your license file to remove evaluation limitations:

```csharp
using GroupDocs.Assembly;

public static void ApplyLicenseFromFile()
{
    // Path to your license file
    string licensePath = "GroupDocs.Assembly.lic";
    
    // Apply the license
    License license = new License();
    license.SetLicense(licensePath);
    
    Console.WriteLine("License applied successfully from file.");
}
```

## Apply License from Stream

You can also load a license from a stream:

```csharp
using GroupDocs.Assembly;
using System.IO;

public static void ApplyLicenseFromStream()
{
    // Load license file into a stream
    using (FileStream stream = new FileStream("GroupDocs.Assembly.lic", FileMode.Open))
    {
        License license = new License();
        license.SetLicense(stream);
        
        Console.WriteLine("License applied successfully from stream.");
    }
}
```

## Verify License Application

To verify that your license is applied correctly, you can check for evaluation watermarks in generated documents. If no watermarks appear, the license is active.

```csharp
using GroupDocs.Assembly;

public static void VerifyLicense()
{
    License license = new License();
    license.SetLicense("GroupDocs.Assembly.lic");
    
    // Try to assemble a simple document
    DocumentAssembler assembler = new DocumentAssembler();
    // If license is valid, no evaluation watermark will appear
    Console.WriteLine("License verification: Check generated documents for watermarks.");
}
```

{{< alert style="warning" >}}
The license file contains a digital signature. Do not modify the license file, as even adding an extra line break will invalidate it.
{{< /alert >}}

### Advanced Usage Topics

To learn more about licensing options including metered licensing, please refer to the [advanced usage section]({{< ref "assembly/net/developer-guide/advanced-usage/_index.md" >}}).

## More resources

### GitHub Examples

You may easily run the code above and see the feature in action in our GitHub examples:

* [GroupDocs.Assembly for .NET examples, plugins, and showcase](https://github.com/groupdocs-assembly/GroupDocs.Assembly-for-.NET)
* [GroupDocs.Assembly for Java examples, plugins, and showcase](https://github.com/groupdocs-assembly/GroupDocs.Assembly-for-Java)
* [GroupDocs.Assembly for Python via .NET examples, plugins, and showcase](https://github.com/groupdocs-assembly/GroupDocs.Assembly-for-Python-via-.NET)

### Free Online Apps

Along with the full-featured .NET library, we provide simple but powerful free online apps.

To assemble documents from templates and data sources, you can use the online apps from the **[GroupDocs.Assembly App Product Family](https://products.groupdocs.app/assembly/family)**.

