---
id: groupdocs-assembly-for-java-18-10-release-notes
url: assembly/java/groupdocs-assembly-for-java-18-10-release-notes
title: GroupDocs.Assembly for Java 18.10 Release Notes
weight: 2
description: ""
keywords: 
productName: GroupDocs.Assembly for Java
hideChildren: False
---
{{< alert style="info" >}}This page contains release notes for GroupDocs.Assembly for Java 18.10.{{< /alert >}}

## Major Features

Supported removal of paragraphs becoming empty after template syntax tags are removed or replaced with empty values for templates of Word Processing, Presentation, and Email file formats.

## Full List of Features Covering all Changes in this Release

| Key | Summary | Category |
| --- | --- | --- |
| ASSEMBLYNET-89  | Support removal of paragraphs becoming empty after template syntax tags are removed or replaced with empty values for Word Processing documents  | Feature  |
| ASSEMBLYNET-91  | Support removal of paragraphs becoming empty after template syntax tags are removed or replaced with empty values for Presentation documents  | Feature  |
| ASSEMBLYNET-92  | Support removal of paragraphs becoming empty after template syntax tags are removed or replaced with empty values for Email documents  | Feature  |

## Public API and Backward Incompatible Changes

{{< alert style="info" >}}This section lists public API changes that were introduced in GroupDocs.Assembly for Java 18.10. It includes not only new and obsoleted public methods, but also a description of any changes in the behaviour behind the scenes in GroupDocs.Assembly which may affect existing code. Any behaviour introduced that could be seen as a regression and modifies existing behaviour is especially important and is documented here.{{< /alert >}}

### Support removal of paragraphs becoming empty after template syntax tags are removed or replaced with empty values

The following new member was added to **DocumentAssemblyOptions**:

**Java**

```java
**
  * Specifies that the assembler should remove paragraphs becoming empty after template syntax tags are removed or replaced with empty values.
  * At the moment, this option is supported only for templates of Word Processing, Presentation, and Email file formats.
  */
public static final int REMOVE_EMPTY_PARAGRAPHS
```

When the new option is applied to **DocumentAssembler **options through **DocumentAssembler.setOptions()**, the engine additionally removes paragraphs becoming empty after template syntax tags are removed or replaced with empty values as shown in the following examples.

#### Example 1

Template document.

```java
Prefix
<<[""]>>
Suffix
```

Result document without the new option applied.

```java
Prefix
 
Suffix
```

Result document with the new option applied.

```java
Prefix
Suffix
```

#### Example 2

Template document.

```java
Prefix
<<if [false]>>
Text to be removed
<</if>>
Suffix
```

Result document without the new option applied.

```java
Prefix
 
Suffix
```

Result document with the new option applied.

```java
Prefix
Suffix
```

#### Example 3

{{< alert style="warning" >}}In this example, persons isassumed to be a data table having a field Name.{{< /alert >}}

  
Template document.

```java
Prefix
<<foreach [in persons]>>
<<[Name]>>
<</foreach>>
Suffix
```

Result document without the new option applied.

```java
Prefix
 
John Doe
 
Jane Doe
 
John Smith
 
Suffix
```

Result document with the new option applied.

```java
Prefix
John Doe
Jane Doe
John Smith
Suffix
```
