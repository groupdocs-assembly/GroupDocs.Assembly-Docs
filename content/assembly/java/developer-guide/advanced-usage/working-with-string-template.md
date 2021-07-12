---
id: working-with-string-template
url: assembly/java/working-with-string-template
title: Working with String Template
weight: 35
description: ""
keywords: 
productName: GroupDocs.Assembly for Java
hideChildren: False
---
GroupDocs.Assembly API allows you to use a string as input and output template, instead of document. This feature improves programmability while working with strings instead of documents, the resultant output string can be used as per the application needs. Follow these steps to using a string as input and output template:

*   Initialize **DocumentAssembler**
*   Define **sourceString "<<\[yourValue\]>>"**
*   Convert sourceString to **sourceBytes** using **ByteArrayInputStream(sourceBytes)**
*   Get **targetBytes** using **DocumentAssembler.assembleDocument()**
*   Get** targetString **using **new String(targetBytes, StandardCharsets.UTF\_8)**

{{< gist GroupDocsGists 6af297f6037c73ea88d0947c4dcec6b7 >}}
