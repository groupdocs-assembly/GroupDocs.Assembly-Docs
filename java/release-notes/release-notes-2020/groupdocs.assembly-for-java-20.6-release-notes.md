---
id: groupdocs-assembly-for-java-20-6-release-notes
url: assembly/java/groupdocs-assembly-for-java-20-6-release-notes
title: GroupDocs.Assembly for Java 20.6 Release Notes
weight: 80
description: ""
keywords: 
productName: GroupDocs.Assembly for Java
hideChildren: False
---
### Major Features

Supported working with POT and OTP Presentation document formats and working with ordered lists for Markdown.

## Full List of Features Covering all Changes in this Release

| Key | Summary | Category |
| --- | --- | --- |
| ASSEMBLYNET-143 | Support ordered lists for Markdown | Feature |
| ASSEMBLYNET-154 | Support working with POT and OTP Presentation document formats | Feature |
| ASSEMBLYNET-158 | InvalidOperationException is thrown on accessing an empty JSON array | Bug |

## Public API and Backward Incompatible Changes 

### Supported ordered lists for Markdown

From now on, ordered lists (see chapter 5.3 of [Markdown specification](https://spec.commonmark.org/0.28/)) are supported when saving assembled Markdown documents to Word Processing formats and saving assembled Word Processing documents and emails to Markdown.

### Supported working with POT and OTP Presentation document formats

Support for loading of template POT and OTP Presentation documents and saving of assembled Presentation documents to POT and OTP formats.

#### Loading of a POT (or OTP) template for Presentation document assembly:

```java
DocumentAssembler assembler = new DocumentAssembler();
assembler.assembleDocument("template.pot", "result.pptx", ...); // For OTP, it might be "template.otp".
```

#### Saving an assembled Presentation document to the POT (or OTP) format using file extension:

```java
DocumentAssembler assembler = new DocumentAssembler();
assembler.assembleDocument("template.pptx", "result.pot", ...); // For OTP, it might be "result.otp".
```

#### Saving an assembled Presentation document to the POT (or OTP) format using explicit specifying:

```java
InputStream sourceStream = ...;
OutputStream targetStream = ...;
 
DocumentAssembler assembler = new DocumentAssembler();
assembler.assembleDocument(sourceStream, targetStream, new LoadSaveOptions(FileFormat.POT), ...); // For OTP, FileFormat.OTP should be used.
```
