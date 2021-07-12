---
id: defining-relations-between-documenttable-instances-loaded-from-a-single-document
url: assembly/java/defining-relations-between-documenttable-instances-loaded-from-a-single-document
title: Defining Relations Between DocumentTable Instances Loaded from a Single Document
weight: 32
description: ""
keywords: 
productName: GroupDocs.Assembly for Java
hideChildren: False
---
{{< alert style="info" >}}The code uses some of the objects defined in [The Business Layer](https://docs.groupdocs.com/assembly/java/the-business-layer/).{{< /alert >}}

## Defining Relations Between Document Table Instances

API provides the ability to define relations between DocumentTable instances loaded from a single document. The following classes of the **GroupDocs.Assembly.Data** namespace have been added:

*   DocumentTableRelation
*   DocumentTableRelationCollection

Moreover, The **Relations** property of the **GroupDocs.Assembly.Data.DocumentTableSet** class has been added.

### Download

#### Data Source Document

*   [Related Tables Data.xlsx](https://github.com/groupdocs-assembly/GroupDocs.Assembly-for-Java/blob/master/Examples/GroupDocs.Assembly.Examples.Java/Data/Data%20Sources/Excel%20DataSource/Related%20Tables%20Data.xlsx?raw=true)

#### Template

*   [Using Document Table Relations.docx](https://github.com/groupdocs-assembly/GroupDocs.Assembly-for-Java/blob/master/Examples/GroupDocs.Assembly.Examples.Java/Data/Storage/Word%20Templates/Using%20Document%20Table%20Relations.docx?raw=true)

## Using Document Table Relations

{{< gist GroupDocsGists 4ae828a9377501da26d5db1c51b5cc83 >}}

## ColumnNameExtractingDocumentTableLoadHandler

{{< gist GroupDocsGists 110dd713ad2133a916048bfca273f644 >}}


