---
id: assembly-basic-usage-install-license-java
url: assembly/java/basic-usage-install-and-license
linktitle: Install and Apply License
title: Install GroupDocs.Assembly for Java and Apply License
weight: 1
description: "Learn how to install GroupDocs.Assembly via Maven or Gradle and apply a license to remove evaluation limitations in your Java applications."
keywords: install, Maven, Gradle, license, setup, configure, GroupDocs.Assembly, Java, apply license
productName: GroupDocs.Assembly for Java
hideChildren: False
---

## Overview

Before you can start generating documents with GroupDocs.Assembly for Java, you need to install the library and apply a license. This guide shows you how to add the package to your Maven or Gradle project and configure licensing to remove evaluation limitations.

The main classes involved are:
- [License](https://reference.groupdocs.com/assembly/java/com.groupdocs.assembly/license/) - for applying licenses
- [DocumentAssembler](https://reference.groupdocs.com/assembly/java/com.groupdocs.assembly/documentassembler/) - for assembling documents

Here are the steps to get started:

* Add the GroupDocs Artifact Repository and the GroupDocs.Assembly dependency to your Maven or Gradle build
* Apply a license from a file or stream using the `License.setLicense` method
* Verify that the license is applied correctly before using DocumentAssembler

{{< alert style="info" >}}
Calling `License.setLicense` multiple times is not harmful but wastes processor time. In desktop or console applications, call it once during startup (for example, at the beginning of the `main` method). In web applications, call it once during application initialization (for example, in the `contextInitialized` method of a `ServletContextListener`).
{{< /alert >}}

## Install via Maven

The easiest way to install GroupDocs.Assembly is to reference it in your Maven project. All GroupDocs packages are hosted at the [GroupDocs Artifact Repository](https://releases.groupdocs.com/java/repo/com/groupdocs/groupdocs-assembly/).

1. Add the GroupDocs Artifact Repository to your `pom.xml` file:

```xml
<repositories>
    <repository>
        <id>GroupDocs Artifact Repository</id>
        <name>GroupDocs Artifact Repository</name>
        <url>https://releases.groupdocs.com/java/repo/</url>
    </repository>
</repositories>
```

2. Add GroupDocs.Assembly as a dependency (use the latest available version):

```xml
<dependencies>
    <dependency>
        <groupId>com.groupdocs</groupId>
        <artifactId>groupdocs-assembly</artifactId>
        <version>26.10</version>
    </dependency>
</dependencies>
```

## Install via Gradle

Alternatively, you can add the repository and the dependency to your `build.gradle` file:

```groovy
repositories {
    maven { url 'https://releases.groupdocs.com/java/repo/' }
}

dependencies {
    implementation 'com.groupdocs:groupdocs-assembly:26.10'
}
```

## Apply License from File

After installation, apply your license file to remove evaluation limitations:

```java
import com.groupdocs.assembly.*;

public static void applyLicenseFromFile() throws Exception
{
    // Path to your license file
    String licensePath = "GroupDocs.Assembly.lic";

    // Apply the license
    License license = new License();
    license.setLicense(licensePath);

    System.out.println("License applied successfully from file.");
}
```

## Apply License from Stream

You can also load a license from a stream:

```java
import com.groupdocs.assembly.*;
import java.io.*;

public static void applyLicenseFromStream() throws Exception
{
    // Load license file into a stream
    try (InputStream stream = new FileInputStream("GroupDocs.Assembly.lic"))
    {
        License license = new License();
        license.setLicense(stream);

        System.out.println("License applied successfully from stream.");
    }
}
```

## Verify License Application

To verify that your license is applied correctly, call the `isLicensed` method of the `License` class. You can also check for evaluation watermarks in generated documents. If no watermarks appear, the license is active.

```java
import com.groupdocs.assembly.*;

public static void verifyLicense() throws Exception
{
    License license = new License();
    license.setLicense("GroupDocs.Assembly.lic");

    // Check whether the license has been applied
    System.out.println("License applied: " + license.isLicensed());

    // Try to assemble a simple document
    DocumentAssembler assembler = new DocumentAssembler();
    // If license is valid, no evaluation watermark will appear
    System.out.println("License verification: Check generated documents for watermarks.");
}
```

{{< alert style="warning" >}}
The license file contains a digital signature. Do not modify the license file, as even adding an extra line break will invalidate it.
{{< /alert >}}

### Advanced Usage Topics

To learn more about licensing options including metered licensing, please refer to the [advanced usage section]({{< ref "assembly/java/developer-guide/advanced-usage/_index.md" >}}).

## More resources

### GitHub Examples

You may easily run the code above and see the feature in action in our GitHub examples:

* [GroupDocs.Assembly for Java examples, plugins, and showcase](https://github.com/groupdocs-assembly/GroupDocs.Assembly-for-Java)
* [GroupDocs.Assembly for .NET examples, plugins, and showcase](https://github.com/groupdocs-assembly/GroupDocs.Assembly-for-.NET)
* [GroupDocs.Assembly for Python via .NET examples, plugins, and showcase](https://github.com/groupdocs-assembly/GroupDocs.Assembly-for-Python-via-.NET)

### Free Online Apps

Along with the full-featured Java library, we provide simple but powerful free online apps.

To assemble documents from templates and data sources, you can use the online apps from the **[GroupDocs.Assembly App Product Family](https://products.groupdocs.app/assembly/family)**.
