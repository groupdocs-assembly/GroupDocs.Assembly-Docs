---
id: removing-empty-paragraphs
url: assembly/java/removing-empty-paragraphs
title: Removing Empty Paragraphs
weight: 37
description: ""
keywords: 
productName: GroupDocs.Assembly for Java
hideChildren: False
---
{{< alert style="info" >}}This feature is supported by version 18.10. or greater.{{< /alert >}}{{< alert style="info" >}}The code uses some of the objects defined in [The Business Layer](https://docs.groupdocs.com/assembly/java/the-business-layer/).{{< /alert >}}

GroupDocs.Assembly for Java API supports the removal of paragraphs becoming empty after template syntax tags are removed or replaced with empty values. A new member **REMOVE\_EMPTY\_PARAGRAPHS **is added to **DocumentAssemblyOptions**. When this new option is applied to **DocumentAssembler** options through **DocumentAssembler.setOptions()**, the engine additionally removes empty paragraphs.

## Removing Empty Paragraphs in Word Processing Document 

### The Code

{{< gist GroupDocsGists 5c3a2b1ce4879f7c1d139023f5ca370c >}}

### Download

*   [Empty Paragraph.docx](https://github.com/groupdocs-assembly/GroupDocs.Assembly-for-Java/blob/master/Examples/GroupDocs.Assembly.Examples.Java/Data/Storage/Word%20Templates/Empty%20Paragraph.docx)

## Removing Empty Paragraphs in Presentation Document 

### The Code

{{< gist GroupDocsGists 8a60018c3b127c1652d70fb6ff623be5 >}}

### Download

*   [Empty Paragraph.pptx](https://github.com/groupdocs-assembly/GroupDocs.Assembly-for-Java/blob/master/Examples/GroupDocs.Assembly.Examples.Java/Data/Storage/Presentation%20Templates/Empty%20Paragraph.pptx)

## Removing Empty Paragraphs in Email Document 

### The Code

{{< gist GroupDocsGists a1361185b1472dcea8c0cb015ab89e0c >}}

### Download

*   [Empty Paragraph.msg](https://github.com/groupdocs-assembly/GroupDocs.Assembly-for-Java/blob/master/Examples/GroupDocs.Assembly.Examples.Java/Data/Storage/Email%20Templates/Empty%20Paragraph.msg)
