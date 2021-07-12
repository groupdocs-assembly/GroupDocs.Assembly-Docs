---
id: saving-to-html-with-external-resource-files
url: assembly/java/saving-to-html-with-external-resource-files
title: Saving to HTML with External Resource Files
weight: 2
description: ""
keywords: 
productName: GroupDocs.Assembly for Java
hideChildren: False
---
{{< alert style="info" >}}This feature is supported by version 19.5. or greater{{< /alert >}}{{< alert style="info" >}}The code uses some of the objects defined in [The Business Layer](https://docs.groupdocs.com/assembly/java/the-business-layer/).{{< /alert >}}

# Saving to HTML with External Resource Files

Since version 19.5, The [GroupDocs.Assembly](https://apireference.groupdocs.com/java/assembly/com.groupdocs.assembly/package-summary) provides a great feature which is saving of external resource files while an assembled document loaded from a non-HTML format is being saved to HTML.

From now on, when saving an assembled document to an HTML file, by default, external resource files are stored to a folder having the same name as the HTML file without extension plus the "\_files" suffix. This folder is located in the same folder as the HTML file. The following example illustrates the scenario. The following code snippet shows the way of API usage:

{{< gist GroupDocsGists 367999066c740ee88e491398f29a2765 >}}

In the following example, the default folder used to store HTML resource files is overridden by an explicitly specified folder.

{{< gist GroupDocsGists 50bbba0f46352df7fc4e6a9f556e31f3 >}}


