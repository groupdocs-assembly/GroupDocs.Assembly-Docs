---
id: groupdocs-assembly-for-java-20-8-release-notes
url: assembly/java/groupdocs-assembly-for-java-20-8-release-notes
title: GroupDocs.Assembly for Java 20.8 Release Notes
weight: 70
description: ""
keywords: 
productName: GroupDocs.Assembly for Java
hideChildren: False
---
### Major Features

GroupDocs.Assembly for Java 20.8 comes up with several improvements in dynamic barcode insertion.

## Full List of Features Covering all Changes in this Release

| Key | Summary | Category |
| --- | --- | --- |
| ASSEMBLYNET-48 | Support dynamic generation of GS1-128 AI 8102 Coupon Extended barcodes | Feature |
| ASSEMBLYNET-49 | Support dynamic generation of UPCA & GS1 Databar Coupon barcodes | Feature |
| ASSEMBLYNET-159 | Improve barcode scaling | Feature |
| ASSEMBLYJAVA-19 | Barcode text is truncated upon some circumstances | Bug |
| ASSEMBLYJAVA-20 | Anti-aliasing does not work expectedly for barcode text | Bug |

## Public API and Backward Incompatible Changes 

{{< alert style="info" >}}This section lists public API changes that were introduced in GroupDocs.Assembly for Java 20.8. It includes not only new and obsoleted public methods, but also a description of any changes in the behavior behind the scenes in GroupDocs.Assembly which may affect existing code. Any behavior introduced that could be seen as a regression and modifies existing behavior is especially important and is documented here.{{< /alert >}}

### Supported dynamic generation of GS1-128 AI 8102 Coupon Extended and UPCA & GS1 Databar Coupon barcodes

From now, the following identifiers can be used to generate GS1-128 AI 8102 Coupon Extended and UPCA & GS1 Databar Coupon barcodes:

| Identifier | Description |
| --- | --- |
| code128GS1UPCA | GS1-128 AI 8102 Coupon Extended barcode |
| databarGS1UPCA | UPCA & GS1 Databar Coupon barcode |

For more information on dynamic insertion of barcodes, see [Barcodes Syntax and Properties](https://docs.groupdocs.com/assembly/java/barcodes-syntax-and-properties/).

### Improved barcode scaling

Starting from this version, barcode scaling is supported for the most of barcode types. For more information on scaling of barcodes, see [Scaling Barcode Symbols](https://docs.groupdocs.com/assembly/java/barcodes-syntax-and-properties/#scaling-barcode-symbols).
