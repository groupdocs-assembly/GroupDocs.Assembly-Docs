---
id: groupdocs-assembly-for-java-20-4-release-notes
url: assembly/java/groupdocs-assembly-for-java-20-4-release-notes
title: GroupDocs.Assembly for Java 20.4 Release Notes
weight: 90
description: ""
keywords: 
productName: GroupDocs.Assembly for Java
hideChildren: False
---
### Major Features

Provided an option to fit an image within textbox bounds while maintaining ratio.

## Full List of Features Covering all Changes in this Release

| Key | Summary | Category |
| --- | --- | --- |
| ASSEMBLYNET-149  | Provide an option to fit an image within textbox bounds while maintaining ratio for Word Processing documents  | Feature  |
| ASSEMBLYNET-150  | Provide an option to fit an image within textbox bounds while maintaining ratio for emails with RTF bodies  | Feature  |
| ASSEMBLYNET-151  | Provide an option to fit an image within textbox bounds while maintaining ratio for Spreadsheet documents  | Feature  |
| ASSEMBLYNET-152  | Provide an option to fit an image within textbox bounds while maintaining ratio for Presentation documents  | Feature  |

## Public API and Backward Incompatible Changes 

### Provided an option to fit an image within textbox bounds while maintaining ratio

To keep the size of the textbox and stretch the image within bounds of the textbox preserving the ratio of the image, use the *keepRatio* switch as follows.

```java
<<image [image_expression] -keepRatio>>

```
