---
id: merging-table-cells-dynamically
url: assembly/java/merging-table-cells-dynamically
title: Merging Table Cells Dynamically
weight: 6
description: ""
keywords: 
productName: GroupDocs.Assembly for Java
hideChildren: False
---
{{< alert style="info" >}}This feature is supported by version 19.1 or greater{{< /alert >}}{{< alert style="info" >}}The code uses some of the objects defined in [The Business Layer](https://docs.groupdocs.com/assembly/java/the-business-layer/).{{< /alert >}}

# Merging Table Cells Dynamically

Using GroupDocs.Assembly for Java, you can merge table cells with equal textual contents within your reports dynamically using **cellMerge** tags. Syntax of a **cellMerge** tag is defined as follows:

`<<cellMerge -horz>>`

{{< alert style="warning" >}}A horz switch is optional. If the switch is present, it denotes a cell merging operation in a horizontal direction. If the switch is missing, it means that a cell merging operation is to be performed in a vertical direction (the default).{{< /alert >}}

For two or more successive table cells to be merged dynamically in either direction by the engine, the following requirements must be met:

*   Each of the cells must contain a **cellMerge** tag denoting a cell merging operation in the same direction.
*   Each of the cells must not be already merged in another direction.
*   The cells must have equal textual contents (ignoring leading and trailing whitespaces).

Consider the following template:

<table style="background-color: white; background-image: initial; border-collapse: collapse; border-top-color: initial; border-top-style: none; border-top-width: initial; border-right-color: initial; border-right-style: none; border-right-width: initial; border-bottom-color: initial; border-bottom-style: none; border-bottom-width: initial; border-left-color: initial; border-left-style: none; border-left-width: initial;"><tbody><tr><td style="width: 89.625px; border-top-color: windowtext; border-top-style: solid; border-top-width: 1pt; border-right-color: windowtext; border-right-style: solid; border-right-width: 1pt; border-bottom-color: windowtext; border-bottom-style: solid; border-bottom-width: 1pt; border-left-color: windowtext; border-left-style: solid; border-left-width: 1pt; padding-top: 0in; padding-right: 5.4pt; padding-bottom: 0in; padding-left: 5.4pt;"><p style="margin-bottom: 0.0001pt; line-height: normal;"><strong><span style="font-family: &quot;Courier New&quot;; color: rgb(127, 127, 127);">...</span></strong></p></td><td style="width: 368.625px; border-top-color: windowtext; border-top-style: solid; border-top-width: 1pt; border-right-color: windowtext; border-right-style: solid; border-right-width: 1pt; border-bottom-color: windowtext; border-bottom-style: solid; border-bottom-width: 1pt; border-image-source: initial; border-image-slice: initial; border-image-width: initial; border-image-outset: initial; border-image-repeat: initial; border-left-color: initial; border-left-style: none; border-left-width: initial; padding-top: 0in; padding-right: 5.4pt; padding-bottom: 0in; padding-left: 5.4pt;"><p style="margin-bottom: 0.0001pt; line-height: normal;"><strong><span style="font-family: &quot;Courier New&quot;; color: rgb(127, 127, 127);">...</span></strong></p></td><td style="width: 98.625px; border-top-color: windowtext; border-top-style: solid; border-top-width: 1pt; border-right-color: windowtext; border-right-style: solid; border-right-width: 1pt; border-bottom-color: windowtext; border-bottom-style: solid; border-bottom-width: 1pt; border-image-source: initial; border-image-slice: initial; border-image-width: initial; border-image-outset: initial; border-image-repeat: initial; border-left-color: initial; border-left-style: none; border-left-width: initial; padding-top: 0in; padding-right: 5.4pt; padding-bottom: 0in; padding-left: 5.4pt;"><p style="margin-bottom: 0.0001pt; line-height: normal;"><strong><span style="font-family: &quot;Courier New&quot;; color: rgb(127, 127, 127);">...</span></strong></p></td></tr><tr><td style="width: 89.625px; border-right-color: windowtext; border-right-style: solid; border-right-width: 1pt; border-bottom-color: windowtext; border-bottom-style: solid; border-bottom-width: 1pt; border-left-color: windowtext; border-left-style: solid; border-left-width: 1pt; border-image-source: initial; border-image-slice: initial; border-image-width: initial; border-image-outset: initial; border-image-repeat: initial; border-top-color: initial; border-top-style: none; border-top-width: initial; padding-top: 0in; padding-right: 5.4pt; padding-bottom: 0in; padding-left: 5.4pt;"><p style="margin-bottom: 0.0001pt; line-height: normal;"><strong><span style="font-family: &quot;Courier New&quot;; color: rgb(127, 127, 127);">...</span></strong></p></td><td style="width: 368.625px; border-top-color: initial; border-top-style: none; border-top-width: initial; border-left-color: initial; border-left-style: none; border-left-width: initial; border-bottom-color: windowtext; border-bottom-style: solid; border-bottom-width: 1pt; border-right-color: windowtext; border-right-style: solid; border-right-width: 1pt; padding-top: 0in; padding-right: 5.4pt; padding-bottom: 0in; padding-left: 5.4pt;"><p style="margin-bottom: 0.0001pt; line-height: normal;"><strong><span style="font-family: &quot;Courier New&quot;; color: rgb(127, 127, 127);">&lt;&lt;cellMerge&gt;&gt;&lt;&lt;[</span><span style="font-family: &quot;Courier New&quot;; color: rgb(127, 127, 127);"><span style="font-family: Consolas;">Variable1</span></span></strong><strong><span style="font-family: &quot;Courier New&quot;; color: rgb(127, 127, 127);">]&gt;&gt;</span></strong></p></td><td style="width: 98.625px; border-top-color: initial; border-top-style: none; border-top-width: initial; border-left-color: initial; border-left-style: none; border-left-width: initial; border-bottom-color: windowtext; border-bottom-style: solid; border-bottom-width: 1pt; border-right-color: windowtext; border-right-style: solid; border-right-width: 1pt; padding-top: 0in; padding-right: 5.4pt; padding-bottom: 0in; padding-left: 5.4pt;"><p style="margin-bottom: 0.0001pt; line-height: normal;"><strong><span style="font-family: &quot;Courier New&quot;; color: rgb(127, 127, 127);">...</span></strong></p></td></tr><tr><td style="width: 89.625px; border-right-color: windowtext; border-right-style: solid; border-right-width: 1pt; border-bottom-color: windowtext; border-bottom-style: solid; border-bottom-width: 1pt; border-left-color: windowtext; border-left-style: solid; border-left-width: 1pt; border-image-source: initial; border-image-slice: initial; border-image-width: initial; border-image-outset: initial; border-image-repeat: initial; border-top-color: initial; border-top-style: none; border-top-width: initial; padding-top: 0in; padding-right: 5.4pt; padding-bottom: 0in; padding-left: 5.4pt;"><p style="margin-bottom: 0.0001pt; line-height: normal;"><strong><span style="font-family: &quot;Courier New&quot;; color: rgb(127, 127, 127);">...</span></strong></p></td><td style="width: 368.625px; border-top-color: initial; border-top-style: none; border-top-width: initial; border-left-color: initial; border-left-style: none; border-left-width: initial; border-bottom-color: windowtext; border-bottom-style: solid; border-bottom-width: 1pt; border-right-color: windowtext; border-right-style: solid; border-right-width: 1pt; padding-top: 0in; padding-right: 5.4pt; padding-bottom: 0in; padding-left: 5.4pt;"><p style="margin-bottom: 0.0001pt; line-height: normal;"><strong><span style="font-family: &quot;Courier New&quot;; color: rgb(127, 127, 127);">&lt;&lt;cellMerge&gt;&gt;&lt;&lt;[</span><span style="font-family: &quot;Courier New&quot;; color: rgb(127, 127, 127);"><span style="font-family: Consolas;">Variable2</span></span></strong><strong><span style="font-family: &quot;Courier New&quot;; color: rgb(127, 127, 127);">]&gt;&gt;</span></strong></p></td><td style="width: 98.625px; border-top-color: initial; border-top-style: none; border-top-width: initial; border-left-color: initial; border-left-style: none; border-left-width: initial; border-bottom-color: windowtext; border-bottom-style: solid; border-bottom-width: 1pt; border-right-color: windowtext; border-right-style: solid; border-right-width: 1pt; padding-top: 0in; padding-right: 5.4pt; padding-bottom: 0in; padding-left: 5.4pt;"><p style="margin-bottom: 0.0001pt; line-height: normal;"><strong><span style="font-family: &quot;Courier New&quot;; color: rgb(127, 127, 127);">...</span></strong></p></td></tr><tr><td style="width: 89.625px; border-right-color: windowtext; border-right-style: solid; border-right-width: 1pt; border-bottom-color: windowtext; border-bottom-style: solid; border-bottom-width: 1pt; border-left-color: windowtext; border-left-style: solid; border-left-width: 1pt; border-image-source: initial; border-image-slice: initial; border-image-width: initial; border-image-outset: initial; border-image-repeat: initial; border-top-color: initial; border-top-style: none; border-top-width: initial; padding-top: 0in; padding-right: 5.4pt; padding-bottom: 0in; padding-left: 5.4pt;"><p style="margin-bottom: 0.0001pt; line-height: normal;"><strong><span style="font-family: &quot;Courier New&quot;; color: rgb(127, 127, 127);">...</span></strong></p></td><td style="width: 368.625px; border-top-color: initial; border-top-style: none; border-top-width: initial; border-left-color: initial; border-left-style: none; border-left-width: initial; border-bottom-color: windowtext; border-bottom-style: solid; border-bottom-width: 1pt; border-right-color: windowtext; border-right-style: solid; border-right-width: 1pt; padding-top: 0in; padding-right: 5.4pt; padding-bottom: 0in; padding-left: 5.4pt;"><p style="margin-bottom: 0.0001pt; line-height: normal;"><strong><span style="font-family: &quot;Courier New&quot;; color: rgb(127, 127, 127);">...</span></strong></p></td><td style="width: 98.625px; border-top-color: initial; border-top-style: none; border-top-width: initial; border-left-color: initial; border-left-style: none; border-left-width: initial; border-bottom-color: windowtext; border-bottom-style: solid; border-bottom-width: 1pt; border-right-color: windowtext; border-right-style: solid; border-right-width: 1pt; padding-top: 0in; padding-right: 5.4pt; padding-bottom: 0in; padding-left: 5.4pt;"><p style="margin-bottom: 0.0001pt; line-height: normal;"><strong><span style="font-family: &quot;Courier New&quot;; color: rgb(127, 127, 127);">...</span></strong></p></td></tr></tbody></table>
{{< alert style="warning" >}}The cellMerge tag works only if Variable1 and Variable2 have the same values.{{< /alert >}}

### Merging Table Cells Dynamically in Word Processing Document 

#### The Code

{{< gist GroupDocsGists a599c02fb2d040474cac0f63a6196d72 >}}

#### Download

*   [Merging Cells Dynamically.docx](https://github.com/groupdocs-assembly/GroupDocs.Assembly-for-Java/blob/master/Examples/GroupDocs.Assembly.Examples.Java/Data/Storage/Word%20Templates/Merging%20Cells%20Dynamically.docx)

### Merging Table Cells Dynamically in Presentation Document 

#### The Code

{{< gist GroupDocsGists a77fa5b41c336a97dc35833c75504aa4 >}}



#### Download

*   [Merging Cells Dynamically.pptx](https://github.com/groupdocs-assembly/GroupDocs.Assembly-for-Java/blob/master/Examples/GroupDocs.Assembly.Examples.Java/Data/Storage/Presentation%20Templates/Merging%20Cells%20Dynamically.pptx)

### Merging Table Cells Dynamically in Spreadsheet Document 

#### The Code

{{< gist GroupDocsGists cdca8717022763fe59c22e23b2fd0785 >}}



#### Download

*   [Merging Cells Dynamically.xlsx](https://github.com/groupdocs-assembly/GroupDocs.Assembly-for-Java/blob/master/Examples/GroupDocs.Assembly.Examples.Java/Data/Storage/Spreadsheet%20Templates/Merging%20Cells%20Dynamically.xlsx)

### Merging Table Cells Dynamically in Email Document 

#### The Code

{{< gist GroupDocsGists 2e4861574c4af4fbf40fa41dec7d4b5a >}}



#### Download

*   [Merging Cells Dynamically.msg](https://github.com/groupdocs-assembly/GroupDocs.Assembly-for-Java/blob/master/Examples/GroupDocs.Assembly.Examples.Java/Data/Storage/Email%20Templates/Merging%20Cells%20Dynamically.msg)
