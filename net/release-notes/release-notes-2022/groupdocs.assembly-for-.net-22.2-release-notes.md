---
id: groupdocs-assembly-for-net-22-2-release-notes
url: assembly/net/groupdocs-assembly-for-net-22-2-release-notes
title: GroupDocs.Assembly for .NET 22.2 Release Notes
weight: 100
description: "GroupDocs.Assembly for .NET 22.2 Release Notes – the latest updates and fixes."
keywords: 
productName: GroupDocs.Assembly for .NET
hideChildren: False
---
## Major Features

Improved error reporting and working with arrays, and supported several exact date-time parse formats while loading JSON.

## Full List of Features Covering all Changes in this Release

| Key             | Summary                                                      | Category |
| :-------------- | :----------------------------------------------------------- | :------- |
| ASSEMBLYNET-205 | Add feature to support array type identifiers in template syntax | Feature  |
| ASSEMBLYNET-206 | Support several exact date-time parse formats while loading JSON | Feature  |
| ASSEMBLYNET-217 | Add context to exceptions thrown while evaluating expressions | Feature  |
| ASSEMBLYNET-207 | DocumentAssembler.AssembleDocument throws System.InvalidCastException for Word Processing documents | Bug      |
| ASSEMBLYNET-208 | DocumentAssembler.AssembleDocument throws System.InvalidCastException for emails with HTML and RTF bodies | Bug      |
| ASSEMBLYNET-209 | DocumentAssembler.AssembleDocument throws an exception for Spreadsheet and Presentation documents | Bug      |

## Public API and Backward Incompatible Changes

{{< alert style="info" >}}This section lists public API changes that were introduced in GroupDocs.Assembly for .NET 22.2. It includes not only new and obsoleted public methods, but also a description of any changes in the behavior behind the scenes in GroupDocs.Assembly which may affect existing code. Any behavior introduced that could be seen as a regression and modifies existing behavior is especially important and is documented here.{{< /alert >}}

### Supported several exact date-time parse formats while loading JSON

A detailed description of this feature can be found in the ["Accessing JSON Data"](https://docs.groupdocs.com/assembly/net/groupdocs-assembly-engine-apis/#accessing-json-data) section.

