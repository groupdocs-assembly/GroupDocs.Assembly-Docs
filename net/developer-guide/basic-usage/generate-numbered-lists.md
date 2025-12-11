---
id: assembly-basic-usage-generate-numbered-lists
url: assembly/net/basic-usage-generate-numbered-lists
linktitle: Generate Numbered Lists
title: Generate Numbered Lists from Data Source
weight: 17
description: "Create numbered lists in documents by iterating over data collections and displaying items with numbers."
keywords: numbered lists, numbered items, foreach data band, list numbering, ordered lists, generate numbered
productName: GroupDocs.Assembly for .NET
hideChildren: False
---

## Overview

Numbered lists provide a sequential, ordered way to display collections of items in documents. GroupDocs.Assembly for .NET enables you to generate numbered lists by iterating over data collections using foreach data bands within numbered list structures.

The main classes involved are:
- [DocumentAssembler](https://reference.groupdocs.com/assembly/net/groupdocs.assembly/documentassembler/) - assembles documents
- [DataSourceInfo](https://reference.groupdocs.com/assembly/net/groupdocs.assembly/datasourceinfo/) - wraps data sources

Here are the steps to generate numbered lists:

* Create a numbered list in your template document
* Add a foreach data band within the list to iterate over your collection
* Reference collection item properties in list items
* Optionally use NumberOf() to display item numbers
* Close the foreach data band
* Assemble the document with your collection data

{{< alert style="info" >}}
The foreach data band automatically repeats numbered list items for each element in the collection, maintaining proper numbering sequence.
{{< /alert >}}

## Generate Numbered List from .NET Collection

Create a numbered list from a list of objects:

```csharp
using GroupDocs.Assembly;
using System.Collections.Generic;

public class Task
{
    public string Title { get; set; }
    public string Description { get; set; }
}

public static void GenerateNumberedList()
{
    // Create sample data
    List<Task> tasks = new List<Task>
    {
        new Task { Title = "Design", Description = "Create design mockups" },
        new Task { Title = "Develop", Description = "Implement features" },
        new Task { Title = "Test", Description = "Perform testing" }
    };
    
    // Assemble document
    DocumentAssembler assembler = new DocumentAssembler();
    assembler.AssembleDocument("NumberedListTemplate.docx", "NumberedListOutput.docx", 
        new DataSourceInfo(tasks, "tasks"));
    
    Console.WriteLine("Numbered list generated successfully.");
}
```

## Template Structure for Numbered Lists

In your template document (NumberedListTemplate.docx), create a numbered list:

```
Tasks to complete:

<<foreach [in tasks]>>
<<[Title]>> - <<[Description]>>
<</foreach>>
```

After assembly, you'll get:

```
Tasks to complete:

1. Design - Create design mockups
2. Develop - Implement features
3. Test - Perform testing
```

## Using NumberOf() Function

You can explicitly display item numbers using the NumberOf() function:

```csharp
using GroupDocs.Assembly;
using System.Collections.Generic;

public static void GenerateNumberedListWithNumber()
{
    List<string> items = new List<string> 
    { 
        "First item", 
        "Second item", 
        "Third item" 
    };
    
    DocumentAssembler assembler = new DocumentAssembler();
    assembler.AssembleDocument("NumberedListTemplate.docx", "NumberedListOutput.docx", 
        new DataSourceInfo(items, "items"));
    
    Console.WriteLine("Numbered list with explicit numbers generated successfully.");
}
```

Template with NumberOf():

```
Items:
<<foreach [in items]>>
<<[NumberOf()]>>. <<[items_Text]>>
<</foreach>>
```

## Generate Numbered List from DataTable

Generate numbered lists from ADO.NET DataTable:

```csharp
using GroupDocs.Assembly;
using System.Data;

public static void GenerateNumberedListFromDataTable()
{
    // Create DataTable
    DataTable tasksTable = new DataTable("Tasks");
    tasksTable.Columns.Add("Title", typeof(string));
    tasksTable.Columns.Add("Description", typeof(string));
    
    // Add rows
    tasksTable.Rows.Add("Design", "Create design mockups");
    tasksTable.Rows.Add("Develop", "Implement features");
    tasksTable.Rows.Add("Test", "Perform testing");
    
    DocumentAssembler assembler = new DocumentAssembler();
    assembler.AssembleDocument("NumberedListTemplate.docx", "NumberedListOutput.docx", 
        new DataSourceInfo(tasksTable, "tasks"));
    
    Console.WriteLine("Numbered list generated from DataTable successfully.");
}
```

## Numbered List in Spreadsheet

For spreadsheet templates, you can create numbered lists in cells:

```csharp
using GroupDocs.Assembly;
using System.Collections.Generic;

public static void GenerateNumberedListInSpreadsheet()
{
    List<Task> tasks = new List<Task>
    {
        new Task { Title = "Design", Description = "Create design mockups" },
        new Task { Title = "Develop", Description = "Implement features" }
    };
    
    DocumentAssembler assembler = new DocumentAssembler();
    assembler.AssembleDocument("NumberedListTemplate.xlsx", "NumberedListOutput.xlsx", 
        new DataSourceInfo(tasks, "tasks"));
    
    Console.WriteLine("Numbered list generated in spreadsheet successfully.");
}
```

Template for spreadsheet (in-cell):

```
"We provide support for the following products:<<foreach [in products]>>
<<[NumberOf()]>>. <<[ProductName]>><</foreach>>"
```

## Numbered List in Email

Generate numbered lists in email messages:

```csharp
using GroupDocs.Assembly;
using System.Collections.Generic;

public static void GenerateNumberedListInEmail()
{
    List<Task> tasks = new List<Task>
    {
        new Task { Title = "Design", Description = "Create design mockups" },
        new Task { Title = "Develop", Description = "Implement features" }
    };
    
    DocumentAssembler assembler = new DocumentAssembler();
    assembler.AssembleDocument("NumberedListTemplate.msg", "NumberedListOutput.msg", 
        new DataSourceInfo(tasks, "tasks"));
    
    Console.WriteLine("Numbered list generated in email successfully.");
}
```

{{< alert style="warning" >}}
In Word documents, ensure the numbered list formatting is applied in the template. The foreach data band will repeat the list item format and maintain proper numbering for each collection element.
{{< /alert >}}

### Advanced Usage Topics

To learn more about custom numbering formats, nested numbered lists, and advanced list formatting options, please refer to the [advanced usage section]({{< ref "assembly/net/developer-guide/advanced-usage/_index.md" >}}).

## More resources

### GitHub Examples

You may easily run the code above and see the feature in action in our GitHub examples:

* [GroupDocs.Assembly for .NET examples, plugins, and showcase](https://github.com/groupdocs-assembly/GroupDocs.Assembly-for-.NET)
* [GroupDocs.Assembly for Java examples, plugins, and showcase](https://github.com/groupdocs-assembly/GroupDocs.Assembly-for-Java)
* [GroupDocs.Assembly for Python via .NET examples, plugins, and showcase](https://github.com/groupdocs-assembly/GroupDocs.Assembly-for-Python-via-.NET)

### Free Online Apps

Along with the full-featured .NET library, we provide simple but powerful free online apps.

To assemble documents from templates and data sources, you can use the online apps from the **[GroupDocs.Assembly App Product Family](https://products.groupdocs.app/assembly/family)**.

