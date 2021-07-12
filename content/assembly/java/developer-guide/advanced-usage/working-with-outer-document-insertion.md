---
id: working-with-outer-document-insertion
url: assembly/java/working-with-outer-document-insertion
title: Working with Outer Document Insertion
weight: 27
description: ""
keywords: 
productName: GroupDocs.Assembly for Java
hideChildren: False
---
{{< alert style="info" >}}The code uses some of the objects defined in [The Business Layer](https://docs.groupdocs.com/assembly/java/the-business-layer/).{{< /alert >}}

## Inserting Documents Dynamically

You can insert contents of outer documents into your reports dynamically using doc tags. A doc tag denotes a placeholder within a template for a document to be inserted during run-time.

```java
<<doc [document_expression]>>
```

{{< alert style="warning" >}}A doc tag can be used almost anywhere in a template document except text-boxes and charts.{{< /alert >}}

An expression declared within a doc tag is used by the engine to load a document to be inserted during run-time. The expression must return a value of one of the following types:

*   A byte array containing document data
*   A Stream instance able to read document data
*   An instance of the Document class
*   A string containing a document URI

{{< alert style="warning" >}}If an expression declared within a doc tag returns a stream object, then the stream is closed by the engine as soon as a corresponding document is loaded.{{< /alert >}}

By default, a document being inserted is not checked against template syntax and is not populated with data. However, you can enable this by using a build switch as follows.

```java
<<doc [document_expression] -build>>
```

When a build switch is used, the engine treats a document being inserted as a template that can access the following data available at the scope of a corresponding doc tag:

*   Data sources
*   Variables
*   A contextual object (see "[Using Contextual Object Member Access](https://docs.aspose.com/display/wordsnet/Template+Syntax#nowhere)" for more information)
*   Known external types (see "[Setting up Known External Types](https://docs.aspose.com/display/wordsnet/Template+Syntax#nowhere)" for more information)

{{< alert style="success" >}}For detailed technical information about syntax, expressions and report generation by the engine, please visit: [Working with GroupDocs.Assembly Engine](https://docs.groupdocs.com/assembly/java/working-with-groupdocs-assembly-engine/){{< /alert >}}

## Working with Outer Document Insertion 

### Download Templates

Get designed and outer templates from here.

*   [OuterDocInsertion.odt](https://github.com/groupdocs-assembly/GroupDocs.Assembly-for-Java/blob/master/Examples/GroupDocs.Assembly.Examples.Java/Data/Storage/Word%20Templates/OuterDocInsertion.docx?raw=true)
*   [OuterDoc.docx](https://github.com/aliahmedgroupdocs/GroupDocs.Assembly-for-Java/blob/master/Examples/GroupDocs.Assembly.Examples.Java/Data/OuterDocument/OuterDoc.docx)

### The Code

{{< gist GroupDocsGists 34b13865c8dda8793d034ad699e0215a >}}

## Outer Document Insertion in Word Processing Formats

{{< alert style="info" >}}This feature is supported by version 18.12 or greater.{{< /alert >}}

### Download Templates

Get designed and outer templates from here.

*   [NestedExternalDocument.docx](https://github.com/groupdocs-assembly/GroupDocs.Assembly-for-Java/blob/master/Examples/GroupDocs.Assembly.Examples.Java/Data/Storage/Word%20Templates/Nested%20External%20Document.docx)
*   [OuterDocument.docx](https://github.com/groupdocs-assembly/GroupDocs.Assembly-for-Java/blob/master/Examples/GroupDocs.Assembly.Examples.Java/Data/OuterDocument/NestedOuterDocument.docx)

### The Code

{{< gist GroupDocsGists b15426f07e0bea783e56b9c7282af55a >}}

## Outer Document Insertion in Email Formats

{{< alert style="info" >}}This feature is supported by version 18.12 or greater.{{< /alert >}}

### Download Templates

Get designed and outer templates from here.

*   [NestedExternalDocument.msg](https://github.com/groupdocs-assembly/GroupDocs.Assembly-for-Java/blob/master/Examples/GroupDocs.Assembly.Examples.Java/Data/Storage/Email%20Templates/Nested%20External%20Document.msg)
*   [OuterDocument.docx](https://github.com/groupdocs-assembly/GroupDocs.Assembly-for-Java/blob/master/Examples/GroupDocs.Assembly.Examples.Java/Data/OuterDocument/NestedOuterDocument.docx)

### The Code

{{< gist GroupDocsGists 7340a6f3264cb45bc688a3c1618255d1 >}}


