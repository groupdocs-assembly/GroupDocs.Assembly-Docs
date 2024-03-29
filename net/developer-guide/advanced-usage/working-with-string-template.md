---
id: working-with-string-template
url: assembly/net/working-with-string-template
title: Working with String Template
weight: 37
description: ""
keywords: 
productName: GroupDocs.Assembly for .NET
hideChildren: False
---
GroupDocs.Assembly API allows you to use a string as input and output template, instead of document. This feature improves programmability while working with strings instead of documents, the resultant output string can be used as per the application needs. Follow these steps to using a string as input and output template:

*   Initialize [DocumentAssembler](https://reference.groupdocs.com/net/assembly/groupdocs.assembly/documentassembler)
*   Define **sourceString @"<<\[yourValue\]>>"**
*   Convert sourceString to **sourceBytes** using **Encoding.UTF8.GetBytes(sourceString)**
*   Get**targetBytes** using [DocumentAssembler.AssembleDocument()](https://reference.groupdocs.com/net/assembly/groupdocs.assembly/documentassembler/methods/assembledocument/index)
*   Get **targetString** using **Encoding.UTF8.GetString(targetBytes)**
