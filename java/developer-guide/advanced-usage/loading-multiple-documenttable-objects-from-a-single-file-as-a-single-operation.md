---
id: loading-multiple-documenttable-objects-from-a-single-file-as-a-single-operation
url: assembly/java/loading-multiple-documenttable-objects-from-a-single-file-as-a-single-operation
title: Loading Multiple DocumentTable Objects from a Single File as a Single Operation
weight: 31
description: ""
keywords: 
productName: GroupDocs.Assembly for Java
hideChildren: False
---
{{< alert style="info" >}}The code uses some of the objects defined in [The Business Layer](https://docs.groupdocs.com/assembly/java/the-business-layer/).{{< /alert >}}

## Loading Multiple DocumentTable Objects

API provides the ability to load multiple DocumentTable objects from a single file as a single operation. Following classes and interfaces of the **GroupDocs.Assembly.Data** namespace have been added:

*   DocumentTableSet
*   DocumentTableCollection
*   IDocumentTableLoadHandler
*   DocumentTableLoadArgs.

Moreover, following properties of the **GroupDocs.Assembly.Data.DocumentTable** class have been added:

*   Name
*   IndexInDocument

### Download

#### Data Source Document

*   [Multiple Tables Data.docx](https://github.com/groupdocs-assembly/GroupDocs.Assembly-for-Java/blob/master/Examples/GroupDocs.Assembly.Examples.Java/Data/Data%20Sources/Word%20DataSource/Multiple%20Tables%20Data.docx?raw=true)

#### Template

*   [Using Document Table Set as Data Source.pptx](https://github.com/groupdocs-assembly/GroupDocs.Assembly-for-Java/blob/master/Examples/GroupDocs.Assembly.Examples.Java/Data/Storage/Presentation%20Templates/Using%20Document%20Table%20Set%20as%20Data%20Source.pptx?raw=true)

## Loading DocumentTableSet using Default Options

{{< gist GroupDocsGists a9f1b1ea045eff6e7004b46256c9e26c >}}

## Loading DocumentTableSet using Custom Options

{{< gist GroupDocsGists 3b0816c688566c74b9ca36b5de92b129 >}}

## Using DocumentTableSet as Data Source

{{< gist GroupDocsGists 707671eb240c923a431ba23be6869c84 >}}

## CustomDocumentTableLoadHandler

{{< gist GroupDocsGists 5d1dc2b3d63082d2e07439a8ce58ba59 >}}

## ColumnNameExtractingDocumentTableLoadHandler

{{< gist GroupDocsGists edfa4d2ffc4b2aff4da49dc86dc08e63 >}}


