---
id: assembly-basic-usage-insert-hyperlinks-java
url: assembly/java/basic-usage-insert-hyperlinks
linktitle: Insert Hyperlinks Dynamically
title: Insert Hyperlinks Dynamically
weight: 21
description: "Create hyperlinks in documents with URLs and text dynamically set from data sources during assembly using GroupDocs.Assembly for Java."
keywords: insert hyperlinks, dynamic hyperlinks, link URLs, hyperlink text, clickable links, generate links, Java
productName: GroupDocs.Assembly for Java
hideChildren: False
---

## Overview

GroupDocs.Assembly for Java enables you to insert hyperlinks dynamically into documents using link tags. Hyperlinks can point to external URLs, bookmarks within the document, or specific cells/slides depending on the document type.

The main classes involved are:
- [DocumentAssembler](https://reference.groupdocs.com/assembly/java/com.groupdocs.assembly/documentassembler/) - assembles documents
- [DataSourceInfo](https://reference.groupdocs.com/assembly/java/com.groupdocs.assembly/datasourceinfo/) - wraps data sources

Here are the steps to insert hyperlinks dynamically:

* Create a template document with link tags
* Use the syntax `<<link [uri_expression][display_text_expression]>>`
* Provide URI and optional display text from your data source
* Assemble the document

{{< alert style="info" >}}
Link tags are replaced with clickable hyperlinks during document assembly. The URI expression is mandatory and must return a non-empty value, while display text is optional.
{{< /alert >}}

## Insert Hyperlink with URL and Text

Insert a hyperlink with both URL and display text:

```java
import com.groupdocs.assembly.*;

public class Website
{
    private String name;
    private String url;

    public Website(String name, String url)
    {
        this.name = name;
        this.url = url;
    }

    public String getName() { return name; }
    public String getUrl() { return url; }
}

public static void insertHyperlink() throws Exception
{
    Website website = new Website("Visit our website", "https://www.example.com");

    DocumentAssembler assembler = new DocumentAssembler();
    assembler.assembleDocument("HyperlinkTemplate.docx", "HyperlinkOutput.docx",
        new DataSourceInfo(website, "website"));

    System.out.println("Hyperlink inserted successfully.");
}
```

## Template Structure for Hyperlinks

In your template (HyperlinkTemplate.docx), use link tags:

```
Please <<link [website.getUrl()][website.getName()]>> for more information.
```

After assembly:

```
Please Visit our website for more information.
```

(The text "Visit our website" will be a clickable hyperlink.)

## Hyperlink with URL Only

If you omit the display text, the URL is used as the display text:

```java
import com.groupdocs.assembly.*;

public static void insertHyperlinkUrlOnly() throws Exception
{
    Website website = new Website(null, "https://www.example.com");

    DocumentAssembler assembler = new DocumentAssembler();
    assembler.assembleDocument("HyperlinkTemplate.docx", "HyperlinkOutput.docx",
        new DataSourceInfo(website, "website"));

    System.out.println("Hyperlink with URL only inserted successfully.");
}
```

Template:

```
Visit <<link [website.getUrl()]>> for more information.
```

## Insert Multiple Hyperlinks from Collection

Insert hyperlinks for each item in a collection:

```java
import com.groupdocs.assembly.*;

public static void insertHyperlinksFromCollection() throws Exception
{
    // Pass an array (or a POJO with a typed List<Website> getter) so that the engine
    // knows the item type; a raw java.util.List passed directly loses its element type
    Website[] websites = new Website[]
    {
        new Website("Home", "https://www.example.com"),
        new Website("About", "https://www.example.com/about"),
        new Website("Contact", "https://www.example.com/contact")
    };

    DocumentAssembler assembler = new DocumentAssembler();
    assembler.assembleDocument("HyperlinksTemplate.docx", "HyperlinksOutput.docx",
        new DataSourceInfo(websites, "websites"));

    System.out.println("Hyperlinks inserted from collection successfully.");
}
```

Template with foreach:

```
Links:
<<foreach [in websites]>>
- <<link [getUrl()][getName()]>>
<</foreach>>
```

## Hyperlink to Bookmark (Word Documents)

Link to bookmarks within the same document:

```java
import com.groupdocs.assembly.*;

public class Section
{
    private String title;
    private String bookmarkName;

    public Section(String title, String bookmarkName)
    {
        this.title = title;
        this.bookmarkName = bookmarkName;
    }

    public String getTitle() { return title; }
    public String getBookmarkName() { return bookmarkName; }
}

public static void insertBookmarkLink() throws Exception
{
    Section section = new Section("Go to Introduction", "Introduction");

    DocumentAssembler assembler = new DocumentAssembler();
    assembler.assembleDocument("BookmarkLinkTemplate.docx", "BookmarkLinkOutput.docx",
        new DataSourceInfo(section, "section"));

    System.out.println("Bookmark hyperlink inserted successfully.");
}
```

Template:

```
<<link [section.getBookmarkName()][section.getTitle()]>>
```

## Hyperlink to Cell (Spreadsheet Documents)

Link to cells in spreadsheet documents:

```java
import com.groupdocs.assembly.*;

public class CellLinkData
{
    private String cellReference;
    private String displayText;

    public CellLinkData(String cellReference, String displayText)
    {
        this.cellReference = cellReference;
        this.displayText = displayText;
    }

    public String getCellReference() { return cellReference; }
    public String getDisplayText() { return displayText; }
}

public static void insertCellLink() throws Exception
{
    CellLinkData data = new CellLinkData("A1", "Go to Home");

    DocumentAssembler assembler = new DocumentAssembler();
    assembler.assembleDocument("CellLinkTemplate.xlsx", "CellLinkOutput.xlsx",
        new DataSourceInfo(data, "data"));

    System.out.println("Cell hyperlink inserted successfully.");
}
```

Template:

```
<<link [data.getCellReference()][data.getDisplayText()]>>
```

The same link can also be declared with constant values: `<<link ["A1"]["Go to Home"]>>`.

## Hyperlink to Slide (Presentation Documents)

Link to slides in presentation documents:

```java
import com.groupdocs.assembly.*;

public class SlideLinkData
{
    private String slideNumber;
    private String displayText;

    public SlideLinkData(String slideNumber, String displayText)
    {
        this.slideNumber = slideNumber;
        this.displayText = displayText;
    }

    public String getSlideNumber() { return slideNumber; }
    public String getDisplayText() { return displayText; }
}

public static void insertSlideLink() throws Exception
{
    SlideLinkData data = new SlideLinkData("Slide1", "Go to First Slide");

    DocumentAssembler assembler = new DocumentAssembler();
    assembler.assembleDocument("SlideLinkTemplate.pptx", "SlideLinkOutput.pptx",
        new DataSourceInfo(data, "data"));

    System.out.println("Slide hyperlink inserted successfully.");
}
```

Template:

```
<<link [data.getSlideNumber()][data.getDisplayText()]>>
```

The same link can also be declared with constant values: `<<link ["Slide1"]["Go to First Slide"]>>`.

## Using URI Objects

You can use `java.net.URI` (or `java.net.URL`) objects directly:

```java
import com.groupdocs.assembly.*;
import java.net.URI;

public class WebsiteWithUri
{
    private URI url;
    private String name;

    public WebsiteWithUri(URI url, String name)
    {
        this.url = url;
        this.name = name;
    }

    public URI getUrl() { return url; }
    public String getName() { return name; }
}

public static void insertHyperlinkWithUri() throws Exception
{
    WebsiteWithUri website = new WebsiteWithUri(new URI("https://www.example.com"), "Visit our website");

    DocumentAssembler assembler = new DocumentAssembler();
    assembler.assembleDocument("HyperlinkTemplate.docx", "HyperlinkOutput.docx",
        new DataSourceInfo(website, "website"));

    System.out.println("Hyperlink with URI object inserted successfully.");
}
```

{{< alert style="warning" >}}
Link tags cannot be used within charts. For hyperlinks in charts, use alternative approaches or place links outside chart elements.
{{< /alert >}}

### Advanced Usage Topics

To learn more about bookmark creation, complex hyperlink scenarios, and advanced link formatting, please refer to the [advanced usage section]({{< ref "assembly/java/developer-guide/advanced-usage/_index.md" >}}).

## More resources

### GitHub Examples

You may easily run the code above and see the feature in action in our GitHub examples:

* [GroupDocs.Assembly for Java examples, plugins, and showcase](https://github.com/groupdocs-assembly/GroupDocs.Assembly-for-Java)
* [GroupDocs.Assembly for .NET examples, plugins, and showcase](https://github.com/groupdocs-assembly/GroupDocs.Assembly-for-.NET)
* [GroupDocs.Assembly for Python via .NET examples, plugins, and showcase](https://github.com/groupdocs-assembly/GroupDocs.Assembly-for-Python-via-.NET)

### Free Online Apps

Along with the full-featured Java library, we provide simple but powerful free online apps.

To assemble documents from templates and data sources, you can use the online apps from the **[GroupDocs.Assembly App Product Family](https://products.groupdocs.app/assembly/family)**.

