---
id: groupdocs-assembly-for-java-20-11-release-notes
url: assembly/java/groupdocs-assembly-for-java-20-11-release-notes
title: GroupDocs.Assembly for Java 20.11 Release Notes
weight: 50
description: ""
keywords: 
productName: GroupDocs.Assembly for Java
hideChildren: False
---
## Major Features

GroupDocs.Assembly for Java 20.11 comes up with several improvements and bug fixes in working with charts, Markdown, JSON data sources, and other areas.

## Full List of Features Covering all Changes in this Release

| Key             | Summary                                                      | Category |
| :-------------- | :----------------------------------------------------------- | :------- |
| ASSEMBLYNET-172 | Support inline links for Markdown                            | Feature  |
| ASSEMBLYNET-173 | Support inline images for Markdown                           | Feature  |
| ASSEMBLYNET-165 | Nullable int is not recognized for JsonDataSource            | Bug      |
| ASSEMBLYNET-166 | Chart legend entries removed in a template appear in a result Word Processing document | Bug      |
| ASSEMBLYNET-167 | Tag "removeif" throws NullReferenceException for a Word Processing document | Bug      |
| ASSEMBLYNET-168 | JsonDataSource cannot access a property having the same name as its containing object | Bug      |
| ASSEMBLYNET-169 | Tag "cellMerge" with empty cells throws ArgumentOutOfRangeException for a Word Processing document | Bug      |
| ASSEMBLYNET-170 | Tag "backColor" adds unwanted carriage return for a Word Processing document | Bug      |
| ASSEMBLYNET-171 | JsonDataSource throws DuplicateNameException                 | Bug      |

## Public API and Backward Incompatible Changes 

{{< alert style="info" >}}This section lists public API changes that were introduced in GroupDocs.Assembly for Java 20.11. It includes not only new and obsoleted public methods, but also a description of any changes in the behavior behind the scenes in GroupDocs.Assembly which may affect existing code. Any behavior introduced that could be seen as a regression and modifies existing behavior is especially important and is documented here.{{< /alert >}}

### Supported Inline Links and Inline Images for Markdown

From now on, inline links and inline images (see [Inline Link](https://spec.commonmark.org/0.29/#inline-link)) are supported when saving assembled Markdown documents to Word Processing formats and saving assembled Word Processing documents and emails to Markdown.