---
id: assembly-basic-usage-insert-hyperlinks
url: assembly/net/basic-usage-insert-hyperlinks
title: Insert Hyperlinks Dynamically in C#
weight: 21
description: "Create hyperlinks in documents with URLs and text dynamically set from data sources during assembly."
keywords: insert hyperlinks, dynamic hyperlinks, link URLs, hyperlink text, clickable links, generate links
productName: GroupDocs.Assembly for .NET
toc: True
---

## Overview

GroupDocs.Assembly for .NET enables you to insert hyperlinks dynamically into documents using link tags. Hyperlinks can point to external URLs, bookmarks within the document, or specific cells/slides depending on the document type.

The main classes involved are:
- [DocumentAssembler](https://reference.groupdocs.com/assembly/net/groupdocs.assembly/documentassembler/) - assembles documents
- [DataSourceInfo](https://reference.groupdocs.com/assembly/net/groupdocs.assembly/datasourceinfo/) - wraps data sources

Here are the steps to insert hyperlinks dynamically:

* Create a template document with link tags
* Use the syntax `<<link [uri_expression][display_text_expression]>>`
* Provide URI and optional display text from your data source
* Assemble the document

{{< alert style="info" >}}
Link tags are replaced with clickable hyperlinks during document assembly. The URI expression is mandatory, while display text is optional.
{{< /alert >}}

## Insert Hyperlink with URL and Text

Insert a hyperlink with both URL and display text:

```csharp
using GroupDocs.Assembly;

public class Website
{
    public string Name { get; set; }
    public string Url { get; set; }
}

public static void InsertHyperlink()
{
    var website = new Website
    {
        Name = "Visit our website",
        Url = "https://www.example.com"
    };
    
    DocumentAssembler assembler = new DocumentAssembler();
    assembler.AssembleDocument("HyperlinkTemplate.docx", "HyperlinkOutput.docx", 
        new DataSourceInfo(website, "website"));
    
    Console.WriteLine("Hyperlink inserted successfully.");
}
```

## Template Structure for Hyperlinks

In your template (HyperlinkTemplate.docx), use link tags:

```
Please <<link [website.Url][website.Name]>> for more information.
```

After assembly:

```
Please Visit our website for more information.
```

(The text "Visit our website" will be a clickable hyperlink.)

## Hyperlink with URL Only

If you omit the display text, the URL is used as the display text:

```csharp
using GroupDocs.Assembly;

public static void InsertHyperlinkUrlOnly()
{
    var website = new Website
    {
        Url = "https://www.example.com"
    };
    
    DocumentAssembler assembler = new DocumentAssembler();
    assembler.AssembleDocument("HyperlinkTemplate.docx", "HyperlinkOutput.docx", 
        new DataSourceInfo(website, "website"));
    
    Console.WriteLine("Hyperlink with URL only inserted successfully.");
}
```

Template:

```
Visit <<link [website.Url]>> for more information.
```

## Insert Multiple Hyperlinks from Collection

Insert hyperlinks for each item in a collection:

```csharp
using GroupDocs.Assembly;
using System.Collections.Generic;

public static void InsertHyperlinksFromCollection()
{
    List<Website> websites = new List<Website>
    {
        new Website { Name = "Home", Url = "https://www.example.com" },
        new Website { Name = "About", Url = "https://www.example.com/about" },
        new Website { Name = "Contact", Url = "https://www.example.com/contact" }
    };
    
    DocumentAssembler assembler = new DocumentAssembler();
    assembler.AssembleDocument("HyperlinksTemplate.docx", "HyperlinksOutput.docx", 
        new DataSourceInfo(websites, "websites"));
    
    Console.WriteLine("Hyperlinks inserted from collection successfully.");
}
```

Template with foreach:

```
Links:
<<foreach [in websites]>>
- <<link [Url][Name]>>
<</foreach>>
```

## Hyperlink to Bookmark (Word Documents)

Link to bookmarks within the same document:

```csharp
using GroupDocs.Assembly;

public class Section
{
    public string Title { get; set; }
    public string BookmarkName { get; set; }
}

public static void InsertBookmarkLink()
{
    var section = new Section
    {
        Title = "Go to Introduction",
        BookmarkName = "Introduction"
    };
    
    DocumentAssembler assembler = new DocumentAssembler();
    assembler.AssembleDocument("BookmarkLinkTemplate.docx", "BookmarkLinkOutput.docx", 
        new DataSourceInfo(section, "section"));
    
    Console.WriteLine("Bookmark hyperlink inserted successfully.");
}
```

Template:

```
<<link [section.BookmarkName][section.Title]>>
```

## Hyperlink to Cell (Spreadsheet Documents)

Link to cells in spreadsheet documents:

```csharp
using GroupDocs.Assembly;

public static void InsertCellLink()
{
    var data = new { CellReference = "A1", DisplayText = "Go to Home" };
    
    DocumentAssembler assembler = new DocumentAssembler();
    assembler.AssembleDocument("CellLinkTemplate.xlsx", "CellLinkOutput.xlsx", 
        new DataSourceInfo(data, "data"));
    
    Console.WriteLine("Cell hyperlink inserted successfully.");
}
```

Template:

```
<<link ["A1"]["Go to Home"]>>
```

## Hyperlink to Slide (Presentation Documents)

Link to slides in presentation documents:

```csharp
using GroupDocs.Assembly;

public static void InsertSlideLink()
{
    var data = new { SlideNumber = "Slide1", DisplayText = "Go to First Slide" };
    
    DocumentAssembler assembler = new DocumentAssembler();
    assembler.AssembleDocument("SlideLinkTemplate.pptx", "SlideLinkOutput.pptx", 
        new DataSourceInfo(data, "data"));
    
    Console.WriteLine("Slide hyperlink inserted successfully.");
}
```

Template:

```
<<link ["Slide1"]["Go to First Slide"]>>
```

## Using Uri Objects

You can use Uri objects directly:

```csharp
using GroupDocs.Assembly;
using System;

public class Website
{
    public Uri Url { get; set; }
    public string Name { get; set; }
}

public static void InsertHyperlinkWithUri()
{
    var website = new Website
    {
        Url = new Uri("https://www.example.com"),
        Name = "Visit our website"
    };
    
    DocumentAssembler assembler = new DocumentAssembler();
    assembler.AssembleDocument("HyperlinkTemplate.docx", "HyperlinkOutput.docx", 
        new DataSourceInfo(website, "website"));
    
    Console.WriteLine("Hyperlink with Uri object inserted successfully.");
}
```

{{< alert style="warning" >}}
Link tags cannot be used within charts. For hyperlinks in charts, use alternative approaches or place links outside chart elements.
{{< /alert >}}

### Advanced Usage Topics

To learn more about bookmark creation, complex hyperlink scenarios, and advanced link formatting, please refer to the [advanced usage section]({{< ref "assembly/net/developer-guide/advanced-usage/_index.md" >}}).

## More resources

### GitHub Examples

You may easily run the code above and see the feature in action in our GitHub examples:

* [GroupDocs.Assembly for .NET examples, plugins, and showcase](https://github.com/groupdocs-assembly/GroupDocs.Assembly-for-.NET)
* [GroupDocs.Assembly for Java examples, plugins, and showcase](https://github.com/groupdocs-assembly/GroupDocs.Assembly-for-Java)
* [GroupDocs.Assembly for Python via .NET examples, plugins, and showcase](https://github.com/groupdocs-assembly/GroupDocs.Assembly-for-Python-via-.NET)

### Free Online Apps

Along with the full-featured .NET library, we provide simple but powerful free online apps.

To assemble documents from templates and data sources, you can use the online apps from the **[GroupDocs.Assembly App Product Family](https://products.groupdocs.app/assembly/family)**.

