---
id: use-of-in-line-syntax-error-messages-into-templates
url: assembly/java/use-of-in-line-syntax-error-messages-into-templates
title: Use of In-line Syntax Error Messages into Templates
weight: 38
description: ""
keywords: 
productName: GroupDocs.Assembly for Java
hideChildren: False
---
{{< alert style="info" >}}This feature is supported by version 19.3 or greater.{{< /alert >}}{{< alert style="info" >}}The code uses some of the objects defined in [The Business Layer](https://docs.groupdocs.com/assembly/java/the-business-layer/).{{< /alert >}}{{< alert style="info" >}}This version provide the ability to display inline template syntax errors in generated, Word Processing, Presentation, Spreadsheets, Emails and Plain Text documents .{{< /alert >}}

## Use of In-line Syntax Error Messages

By default, Document Assembler throws an exception when encounters a template syntax error. Such an exception provides information on a reason of the error and specifies a tag or expression part where the error is encountered. In most cases, this information is enough to find a place in a template causing the error and fix it.

However, when dealing with complex templates containing a large number of tags, it becomes harder to find an exact place in a template causing an error. To make things easier, the engine supports the *DocumentAssemblyOptions.INLINE\_ERROR\_MESSAGES* option that enables in-lining of a syntax error message into a template document at an exact position where the error occurs during run-time.

{{< alert style="warning" >}}A template syntax error message is written using a bold font to make it more apparent.{{< /alert >}}

Consider the following template.

```java
<<var [name]>>
```

By default, such a template causes the engine to throw an exception while building a report. However, when *DocumentAssemblyOptions.INLINE\_ERROR\_MESSAGES* is applied, no exception is thrown and the report looks as follows then.

```java
<<var [name] Error! An assignment operator is expected. >>
```

{{< alert style="warning" >}}Only messages describing errors in template syntax can be in-lined, messages describing errors encountered during expression's evaluation cannot be appeared.{{< /alert >}}

When DocumentAssemblyOptions.INLINE\_ERROR\_MESSAGES is applied, a Boolean value returned by a  DocumentAssembler.assembleDocument overload indicates whether building of a report was finished successfully or was interrupted because of a template syntax error. This enables you to process reports which building succeeded or failed differently as shown in the following code snippet.

{{< gist GroupDocsGists 5de10b3f197d01029e4370d87304ba82 >}}

{{< alert style="warning" >}}In this article the Word Processing document template file has been used. Therefore, the process for the other file formats is same.{{< /alert >}}  

## Download Demo File

Please download the sample demo document files:

*   [Inline error demo.docx](https://github.com/groupdocs-assembly/GroupDocs.Assembly-for-.NET/blob/master/Examples/Data/Source/Word%20Templates/Inline%20Error%20Demo.docx?raw=true)
