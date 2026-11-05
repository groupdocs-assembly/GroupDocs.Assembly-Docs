---
id: working-with-string-template
url: assembly/python-net/working-with-string-template
title: Working with String Template
weight: 37
description: "Working with String Template with GroupDocs.Assembly for Python via .NET: the template, the Python data and the code."
keywords: working with string template, GroupDocs.Assembly, Python, report generation
productName: GroupDocs.Assembly for Python via .NET
hideChildren: False
---
GroupDocs.Assembly API allows you to use a string as input and output template, instead of document. This feature improves programmability while working with strings instead of documents, the resultant output string can be used as per the application needs. Follow these steps to using a string as input and output template:

*   Initialize [DocumentAssembler](https://reference.groupdocs.com/assembly/python-net/groupdocs.assembly/documentassembler/)
*   Define **sourceString @"<<\[yourValue\]>>"**
*   Convert sourceString to **sourceBytes** using **Encoding.UTF8.GetBytes(sourceString)**
*   Get**targetBytes** using [DocumentAssembler.assemble_document()](https://reference.groupdocs.com/assembly/python-net/groupdocs.assembly/documentassembler/assemble_document/)
*   Get **targetString** using **Encoding.UTF8.GetString(targetBytes)**
