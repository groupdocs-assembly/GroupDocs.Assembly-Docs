---
id: installation
url: assembly/java/installation
title: Installation
weight: 4
description: "This topic describes how to install GroupDocs.Assembly for Python."
keywords: installation, maven
productName: GroupDocs.Assembly for Java
hideChildren: False
toc: True
---
## Install using Maven

All GroupDocs packages are hosted at [GroupDocs Artifact Repository](https://releases.groupdocs.com/java/repo/com/groupdocs/groupdocs-assembly/). You can download packages or reference GroupDocs.Assembly for Java API directly in your Maven project using following steps. 

### Add GroupDocs Artifact Repository

Add GroupDocs Artifact Repository to your `pom.xml` file:

{{< tabs "pom-repository">}}
{{< tab "pom.xml" >}}
```xml
<repositories>
    <repository>
        <id>GroupDocs Artifact Repository</id>
        <name>GroupDocs Artifact Repository</name>
        <url>https://releases.groupdocs.com/java/repo/</url>
    </repository>
</repositories>
```
{{< /tab >}}
{{< /tabs >}}

### Add GroupDocs.Assembly as a dependency

Define GroupDocs.Assembly for Java API dependency in your `pom.xml`:

{{< tabs "pom-dependency">}}
{{< tab "pom.xml" >}}
```xml
<dependencies>
    <dependency>
        <groupId>com.groupdocs</groupId>
        <artifactId>groupdocs-assembly</artifactId>
        <version>24.4</version> 
    </dependency>
</dependencies>
```
{{< /tab >}}
{{< /tabs >}}

```
