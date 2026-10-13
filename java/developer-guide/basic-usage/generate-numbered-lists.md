---
id: assembly-basic-usage-generate-numbered-lists-java
url: assembly/java/basic-usage-generate-numbered-lists
linktitle: Generate Numbered Lists
title: Generate Numbered Lists from Data Source
weight: 17
description: "Create numbered lists in documents by iterating over data collections and displaying items with numbers using GroupDocs.Assembly for Java."
keywords: numbered lists, numbered items, foreach data band, list numbering, ordered lists, generate numbered
productName: GroupDocs.Assembly for Java
hideChildren: False
---

## Overview

Numbered lists provide a sequential, ordered way to display collections of items in documents. GroupDocs.Assembly for Java enables you to generate numbered lists by iterating over data collections using foreach data bands within numbered list structures.

The main classes involved are:
- [DocumentAssembler](https://reference.groupdocs.com/assembly/java/com.groupdocs.assembly/documentassembler/) - assembles documents
- [DataSourceInfo](https://reference.groupdocs.com/assembly/java/com.groupdocs.assembly/datasourceinfo/) - wraps data sources

Here are the steps to generate numbered lists:

* Create a numbered list in your template document
* Add a foreach data band within the list to iterate over your collection
* Reference collection item members in list items
* Optionally use numberOf() to display item numbers
* Close the foreach data band
* Assemble the document with your collection data

{{< alert style="info" >}}
The foreach data band automatically repeats numbered list items for each element in the collection, maintaining proper numbering sequence.
{{< /alert >}}

## Generate Numbered List from Java Collection

Create a numbered list from a collection of objects:

```java
import com.groupdocs.assembly.*;

public class Task
{
    private final String title;
    private final String description;

    public Task(String title, String description)
    {
        this.title = title;
        this.description = description;
    }

    public String getTitle() { return title; }
    public String getDescription() { return description; }
}

public static void generateNumberedList() throws Exception
{
    // Create sample data
    Task[] tasks =
    {
        new Task("Design", "Create design mockups"),
        new Task("Develop", "Implement features"),
        new Task("Test", "Perform testing")
    };

    // Assemble document
    DocumentAssembler assembler = new DocumentAssembler();
    assembler.assembleDocument("NumberedListTemplate.docx", "NumberedListOutput.docx",
        new DataSourceInfo(tasks, "tasks"));

    System.out.println("Numbered list generated successfully.");
}
```

{{< alert style="info" >}}
Because of Java type erasure, the engine cannot determine the item type of a `java.util.List` passed directly as a data source, so calling item methods such as `getTitle()` fails. Pass an array (as shown above), or expose the list through a getter of a wrapper object (for example, `public List<Task> getTasks()`) and iterate over it in the template: `<<foreach [in data.getTasks()]>>`.
{{< /alert >}}

## Template Structure for Numbered Lists

In your template document (NumberedListTemplate.docx), create a numbered list:

```
Tasks to complete:

<<foreach [in tasks]>><<[getTitle()]>> - <<[getDescription()]>>
<</foreach>>
```

Put the opening `<<foreach>>` tag at the beginning of the numbered paragraph and the closing `<</foreach>>` tag at the beginning of the next paragraph. Members of Java objects are accessed through their getter methods. After assembly, you'll get:

```
Tasks to complete:

1. Design - Create design mockups
2. Develop - Implement features
3. Test - Perform testing
```

## Using numberOf() Function

You can explicitly display item numbers using the numberOf() function:

```java
import com.groupdocs.assembly.*;
import java.util.*;

public static void generateNumberedListWithNumber() throws Exception
{
    List<String> items = Arrays.asList(
        "First item",
        "Second item",
        "Third item"
    );

    DocumentAssembler assembler = new DocumentAssembler();
    assembler.assembleDocument("NumberOfTemplate.docx", "NumberedListOutput.docx",
        new DataSourceInfo(items, "items"));

    System.out.println("Numbered list with explicit numbers generated successfully.");
}
```

Template with numberOf() (NumberOfTemplate.docx):

```
Items:
<<foreach [item in items]>><<[item.numberOf()]>>. <<[item]>>
<</foreach>>
```

Here, the iteration variable `item` refers to the current string itself, and `item.numberOf()` returns its 1-based number within the data band.

## Generate Numbered List from DataTable

Generate numbered lists from a [DataTable](https://reference.groupdocs.com/assembly/java/com.groupdocs.assembly.system.data/datatable/):

```java
import com.groupdocs.assembly.*;
import com.groupdocs.assembly.system.data.*;

public static void generateNumberedListFromDataTable() throws Exception
{
    // Create DataTable
    DataTable tasksTable = new DataTable("Tasks");
    tasksTable.getColumns().add("Title", String.class);
    tasksTable.getColumns().add("Description", String.class);

    // Add rows
    tasksTable.getRows().add("Design", "Create design mockups");
    tasksTable.getRows().add("Develop", "Implement features");
    tasksTable.getRows().add("Test", "Perform testing");

    DocumentAssembler assembler = new DocumentAssembler();
    assembler.assembleDocument("DataTableNumberedListTemplate.docx", "NumberedListOutput.docx",
        new DataSourceInfo(tasksTable, "tasks"));

    System.out.println("Numbered list generated from DataTable successfully.");
}
```

DataTable columns are referenced by name rather than through getters, so the template (DataTableNumberedListTemplate.docx) looks as follows:

```
Tasks to complete:

<<foreach [in tasks]>><<[Title]>> - <<[Description]>>
<</foreach>>
```

## Numbered List in Spreadsheet

For spreadsheet templates, you can create numbered lists in cells:

```java
import com.groupdocs.assembly.*;

public static void generateNumberedListInSpreadsheet() throws Exception
{
    Task[] tasks =
    {
        new Task("Design", "Create design mockups"),
        new Task("Develop", "Implement features")
    };

    DocumentAssembler assembler = new DocumentAssembler();
    assembler.assembleDocument("NumberedListTemplate.xlsx", "NumberedListOutput.xlsx",
        new DataSourceInfo(tasks, "tasks"));

    System.out.println("Numbered list generated in spreadsheet successfully.");
}
```

Template for spreadsheet (in-cell):

```
"Tasks to complete:<<foreach [in tasks]>>
<<[numberOf()]>>. <<[getTitle()]>><</foreach>>"
```

## Numbered List in Email

Generate numbered lists in email messages:

```java
import com.groupdocs.assembly.*;

public static void generateNumberedListInEmail() throws Exception
{
    Task[] tasks =
    {
        new Task("Design", "Create design mockups"),
        new Task("Develop", "Implement features")
    };

    DocumentAssembler assembler = new DocumentAssembler();
    assembler.assembleDocument("NumberedListTemplate.msg", "NumberedListOutput.msg",
        new DataSourceInfo(tasks, "tasks"));

    System.out.println("Numbered list generated in email successfully.");
}
```

{{< alert style="warning" >}}
In Word documents, ensure the numbered list formatting is applied in the template. The foreach data band will repeat the list item format and maintain proper numbering for each collection element.
{{< /alert >}}

### Advanced Usage Topics

To learn more about custom numbering formats, nested numbered lists, and advanced list formatting options, please refer to the [advanced usage section]({{< ref "assembly/java/developer-guide/advanced-usage/_index.md" >}}).

## More resources

### GitHub Examples

You may easily run the code above and see the feature in action in our GitHub examples:

* [GroupDocs.Assembly for Java examples, plugins, and showcase](https://github.com/groupdocs-assembly/GroupDocs.Assembly-for-Java)
* [GroupDocs.Assembly for .NET examples, plugins, and showcase](https://github.com/groupdocs-assembly/GroupDocs.Assembly-for-.NET)
* [GroupDocs.Assembly for Python via .NET examples, plugins, and showcase](https://github.com/groupdocs-assembly/GroupDocs.Assembly-for-Python-via-.NET)

### Free Online Apps

Along with the full-featured Java library, we provide simple but powerful free online apps.

To assemble documents from templates and data sources, you can use the online apps from the **[GroupDocs.Assembly App Product Family](https://products.groupdocs.app/assembly/family)**.
