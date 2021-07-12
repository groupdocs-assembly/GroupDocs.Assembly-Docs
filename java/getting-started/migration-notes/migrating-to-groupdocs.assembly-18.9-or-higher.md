---
id: migrating-to-groupdocs-assembly-18-9-or-higher
url: assembly/java/migrating-to-groupdocs-assembly-18-9-or-higher
title: Migrating to GroupDocs.Assembly 18.9 or Higher
weight: 1
description: ""
keywords: 
productName: GroupDocs.Assembly for Java
hideChildren: False
---
{{< alert style="info" >}}This document describes the changes to the GroupDocs.Assembly API from version 18.7 to 18.9 or greater that may be of interest to module/application developers. It includes not only new and updated public methods, added & removed classes etc., but also a description of any changes in the behaviour behind the scenes in GroupDocs.Assembly.{{< /alert >}}

### Breaking changes

Removed members of DocumentAssembler were replaced with new ones. Removed members were not marked as obsolete (deprecated) before removal as usual, because this would complicate migration to new members of DocumentAssembler in Java. Thus, we have introduced a breaking change and customers need to migrate their code from removed members of DocumentAssembler to newly added ones when upgrading to the new version of GroupDocs.Assembly.

Since version 18.9, the Metered licensing security has been improved. Metered licensing is now applicable only in Java runtime version *8u101* or above. Please use other types of licensing if you are using v18.9 or greater in Java 7.

### Newly added types

**Java**

```java
/**
  * Provides information on a single data source object to be used to assemble a document from a template.
  */
public class DataSourceInfo
```

**Java**

```java
/**
  * A utility class providing constants. Specifies the format of a file.
  */
public final class FileFormat
```

**Java**

```java
/**
  * Specifies additional options for loading and saving of a document to be assembled.
  */
public class LoadSaveOptions
```

### New members of DocumentAssembler

**Java**

```java
/**
  * Loads a template document from the specified source path, populates the template document with data from the specified single or multiple sources, and stores the result document to the target path using default {@link com.groupdocs.assembly.LoadSaveOptions}.
  * 
  * @param sourcePath The path to a template document to be populated with data.
  * @param targetPath The path to a result document.
  * @param dataSourceInfos Provides information on data source objects to be used.
  */
public void assembleDocument(String sourcePath, String targetPath, DataSourceInfo... dataSourceInfos) throws Exception
```

**Java**

```java
/**
  * Loads a template document from the specified source path, populates the template document with data from the specified single or multiple sources, and stores the result document to the target path using the given {@link com.groupdocs.assembly.LoadSaveOptions}.
  * 
  * @param sourcePath The path to a template document to be populated with data.
  * @param targetPath The path to a result document.
  * @param loadSaveOptions Specifies additional options for document loading and saving.
  * @param dataSourceInfos Provides information on data source objects to be used.
  */
public void assembleDocument(String sourcePath, String targetPath, LoadSaveOptions loadSaveOptions, DataSourceInfo... dataSourceInfos) throws Exception
```

**Java**

```java
/**
  * Loads a template document from the specified source stream, populates the template document with data from the specified single or multiple sources, and stores the result document to the target stream using default {@link com.groupdocs.assembly.LoadSaveOptions}.
  * 
  * @param sourceStream The stream to read a template document from.
  * @param targetStream The stream to write a result document.
  * @param dataSourceInfos Provides information on data source objects to be used.
  */
public void assembleDocument(InputStream sourceStream, OutputStream targetStream, DataSourceInfo... dataSourceInfos) throws Exception
```

**Java**

```java
/**
  * Loads a template document from the specified source stream, populates the template document with data from the specified single or multiple sources, and stores the result document to the target stream using the given {@link com.groupdocs.assembly.LoadSaveOptions}.
  * 
  * @param sourceStream The stream to read a template document from.
  * @param targetStream The stream to write a result document.
  * @param loadSaveOptions Specifies additional options for document loading and saving.
  * @param dataSourceInfos Provides information on data source objects to be used.
  */
public void assembleDocument(InputStream sourceStream, OutputStream targetStream, LoadSaveOptions loadSaveOptions, DataSourceInfo... dataSourceInfos) throws Exception
```

### Removed members of DocumentAssembler

**Java**

```java
public void assembleDocument(String sourcePath, String targetPath, Object dataSource)
public void assembleDocument(String sourcePath, String targetPath, Object dataSource, String dataSourceName)
public void assembleDocument(String sourcePath, String targetPath, Object[] dataSources, String[] dataSourceNames)
public void assembleDocument(InputStream sourceStream, OutputStream targetStream, Object dataSource)
public void assembleDocument(InputStream sourceStream, OutputStream targetStream, Object dataSource, String dataSourceName)
public void assembleDocument(InputStream sourceStream, OutputStream targetStream, Object[] dataSources, String[] dataSourceNames)
```

### Breaking changes

Removed members of DocumentAssembler were replaced with new ones. Removed members were not marked as obsolete (deprecated) before removal as usual, because this would complicate migration to new members of DocumentAssembler in Java. Thus, we have introduced a breaking change and customers need to migrate their code from removed members of DocumentAssembler to newly added ones when upgrading to the new version of GroupDocs.Assembly.

### Migrating code from removed members of DocumentAssembler to newly added ones

The following table shows how to migrate code from removed members of DocumentAssembler to newly added ones.

| Old Code                                                     | New Code                                                     |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| `assembler.assembleDocument(sourcePath, targetPath, dataSource);` | `assembler.assembleDocument(sourcePath, targetPath, new DataSourceInfo(dataSource));` |
| `assembler.assembleDocument(sourcePath, targetPath, dataSource, dataSourceName);` | `assembler.assembleDocument(sourcePath, targetPath, new DataSourceInfo(dataSource, dataSourceName));` |
| `Object[] dataSources = new Object[] { dataSource1, dataSource2 };<br/>String[] dataSourceNames = new String[] { dataSourceName1, dataSourceName2 };<br/> <br/>assembler.assembleDocument(sourcePath, targetPath, dataSources, dataSourceNames);<br/>` | `assembler.assembleDocument(sourcePath, targetPath, new DataSourceInfo(dataSource1, dataSourceName1), new DataSourceInfo(dataSource2, dataSourceName2));` |
| `assembler.assembleDocument(sourceStream, targetStream, dataSource);` | `assembler.assembleDocument(sourceStream, targetStream, new DataSourceInfo(dataSource));` |
| `assembler.assembleDocument(sourceStream, targetStream, dataSource, dataSourceName);` | `assembler.assembleDocument(sourceStream, targetStream, new DataSourceInfo(dataSource, dataSourceName));` |
| `Object[] dataSources = new Object[] { dataSource1, dataSource2 };<br/>String[] dataSourceNames = new String[] { dataSourceName1, dataSourceName2 };<br/> <br/>assembler.assembleDocument(sourceStream, targetStream, dataSources, dataSourceNames);` | `assembler.assembleDocument(sourceStream, targetStream, new DataSourceInfo(dataSource1, dataSourceName1), new DataSourceInfo(dataSource2, dataSourceName2));` |

