---
id: development-environment-installation-and-configuration
url: assembly/java/installation
title: Development Environment Installation and Configuration
weight: 6
description: ""
keywords: 
productName: GroupDocs.Assembly for Java
hideChildren: False
---
## Development Environment

### Operating Systems

**GroupDocs.Assembly for Java** can be executed on any Operating System with Java JDK installed.

*   Windows Desktops and Servers
*   Linux
*   Mac OS

### Supported Runtime

**GroupDocs.Assembly for Java** supports Java run-time version 7 (1.7) and above.

### Development Environments

*   NetBeans
*   IntelliJ IDEA
*   Eclipse

## Installation from GroupDocs Artifactory using Maven

GroupDocs hosts all Java APIs on [GroupDocs Artifactory](https://repository.groupdocs.com/webapp/#/artifacts/browse/tree/General/repo). You can easily use [GroupDocs.Assembly for Java](https://artifact.groupdocs.com/webapp/#/artifacts/browse/tree/General/repo/com/groupdocs/groupdocs-assembly) API directly into your Maven projects with simple configurations.

### Specify GroupDocs Repository Configuration

First, you need to specify GroupDocs repository configuration/location in your Maven `pom.xml` as follows:
```
<repositories>
	<repository>
		<id>GroupDocsJavaAPI</id>
		<name>GroupDocs Java API</name>
		<url>http://repository.groupdocs.com/repo/</url>
	</repository>
</repositories>
```

### Define GroupDocs.Assembly for Java API Dependency

Then define GroupDocs.Assembly for Java API dependency in your `pom.xml` as follows:
```
<dependencies>
    <dependency>
        <groupId>com.groupdocs</groupId>
        <artifactId>groupdocs-assembly</artifactId>
        <version>20.3</version> 
    </dependency>
</dependencies>
```

After performing above-mentioned steps, GroupDocs.Assembly for Java dependency will finally be added to your Maven project.
