---
id: loading-of-template-documents-from-html-with-resources
url: assembly/java/loading-of-template-documents-from-html-with-resources
title: Loading of template documents from HTML with resources
weight: 1
description: ""
keywords: 
productName: GroupDocs.Assembly for Java
hideChildren: False
---
{{< alert style="info" >}}This feature is supported by version 19.5. or greater{{< /alert >}}{{< alert style="info" >}}The code uses some of the objects defined in [The Business Layer](https://docs.groupdocs.com/assembly/java/the-business-layer/).{{< /alert >}}

# Loading of template documents from HTML with resources

[GroupDocs.Assembly](https://apireference.groupdocs.com/java/assembly/com.groupdocs.assembly/package-summary) provides a great feature which is loading of HTML template documents referencing external resource files to be assembled and saved to non-HTML formats. 

Since version 19.5, when loading an HTML document from a file, its containing folder is used as a base URI to resolve external resource files' relative URIs to absolute ones by default as shown in the following example. The following code snippet shows the way of API usage:

{{< gist GroupDocsGists 381806c98068837063997a0a4a687529 >}}

The following code snippet shows the default folder used to resolve external resource files' relative URIs are overridden by an explicitly specified folder.

{{< gist GroupDocsGists 9cf9468c519b98d916b1c37f8be9dc9a >}}


