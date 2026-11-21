---
id: generate-word-report-from-template
url: assembly/net/generate-word-report-from-template
title: Generate a Word Document from a Template
linkTitle: Word document from a template
weight: 2
description: "Generate a Word document from a template in C#: fill a DOCX from a .NET object or a JSON file and save as DOCX or PDF, with no Microsoft Office on the server - mail merge without Word."
keywords: generate Word document from template C#, best library to generate Word documents from templates C#, DOCX template engine .NET, mail merge in C# without Microsoft Word, fill Word template with data C#, Word document from JSON C#, document generation API
productName: GroupDocs.Assembly for .NET
hideChildren: False
toc: True
---

The shortest complete path from data to a document: a template somebody edits in Word, a data
source of your choosing, and one call. No Microsoft Office on the server, no Open XML by hand, and
the layout stays with the people who own the report.

{{< alert style="info" >}}
A runnable implementation of this page is on GitHub:
[word-report-from-template-net](https://github.com/groupdocs-assembly/word-report-from-template-net).
{{< /alert >}}

## Step 1: a template

A tag is `<<[expression]>>`. The expression is evaluated against a data source that you name
yourself, and a format may follow the closing bracket:

```text
Order <<[order.Number]>> for <<[order.Customer]>>
Placed on <<[order.Placed]:"dd MMMM yyyy">>

<<foreach [line in order.Lines]>><<[line.Product]>> x<<[line.Quantity]>> - <<[line.Total]:"0.00">> EUR
<</foreach>>
Total: <<[order.Lines.Sum(l => l.Total)]:"0.00">> EUR
```

Three things are worth noticing. `foreach` repeats the text between its tags once per element. LINQ
is available inside the expressions — `Sum`, `Where`, `GroupBy`, `OrderBy` — so a total is part of
the template rather than of your code. And a format after the bracket, not inside it:
`<<[order.Placed]:"dd MMMM yyyy">>`.

The same tags work in a `.docx`, where they sit in the paragraphs, tables and headers of a document
your colleagues style in Word. See
[template syntax]({{< ref "/assembly/net/developer-guide/basic-usage/working-with-groupdocs.assembly-engine/template-syntax-part-1-of-2.md" >}})
for the full set.

## Step 2: an object

```csharp
Order order = new Order
{
    Number = 4117,
    Customer = "Quayside Bistro",
    Placed = new DateTime(2026, 11, 3),
    Lines = new List<OrderLine>
    {
        new OrderLine { Product = "Espresso beans, 1 kg", Quantity = 6, Price = 18.40m },
        new OrderLine { Product = "Oat milk, 1 l", Quantity = 24, Price = 1.95m }
    }
};

DocumentAssembler assembler = new DocumentAssembler();
assembler.AssembleDocument(
    Path.Combine(TemplatesPath, "order-confirmation.txt"),
    Path.Combine(OutputPath, "order-confirmation.txt"),
    new DataSourceInfo(order, "order"));
```

`"order"` is the name the template uses. Any public property of the object — and any computed
property, such as `Total => Quantity * Price` — is reachable from an expression.

{{< alert style="warning" >}}
A data source object must be of a visible type: a `public` class, not an anonymous type or a
`private` nested class. Anonymous types have no stable member names at runtime and are rejected.
{{< /alert >}}

## Step 3: a JSON file, and the same template

```csharp
assembler.AssembleDocument(
    Path.Combine(TemplatesPath, "Customer orders.docx"),
    Path.Combine(OutputPath, "customer-orders.docx"),
    new DataSourceInfo(new JsonDataSource(Path.Combine(DataSourcesPath, "Customers.json")), "customers"));
```

The template did not change when the data moved from objects to a file. Since 26.11 a template
written for typed objects works over JSON, XML and CSV as well: members of dates and numbers that
may be missing, Booleans usable as conditions and in predicates, `$id`/`$ref` references, and
grouping over nested objects.

Other data sources follow the same shape — see
[a database]({{< ref "/assembly/net/developer-guide/basic-usage/generate-from-database.md" >}}),
[XML]({{< ref "/assembly/net/developer-guide/basic-usage/generate-from-xml-datasource.md" >}}) and
[JSON]({{< ref "/assembly/net/developer-guide/basic-usage/generate-from-json-datasource.md" >}}).

## Step 4: another output format

```csharp
assembler.AssembleDocument(
    Path.Combine(TemplatesPath, "Customer orders.docx"),
    Path.Combine(OutputPath, "customer-orders.pdf"),
    new LoadSaveOptions(FileFormat.Pdf),
    new DataSourceInfo(new JsonDataSource(Path.Combine(DataSourcesPath, "Customers.json")), "customers"));
```

The output format is a load-save option, not a different API. DOCX, PDF, ODT, HTML, Markdown and
plain text come out of the same call; the list is on
[Supported document formats]({{< ref "/assembly/net/getting-started/supported-document-formats.md" >}}).

## Where this usually goes next

| You need | Read |
|---|---|
| The data has holes | [Templates for incomplete data]({{< ref "/assembly/net/use-cases/templates-for-incomplete-data.md" >}}) |
| A spreadsheet instead of a document | [Excel reports from a template]({{< ref "/assembly/net/use-cases/generate-excel-reports-from-template.md" >}}) |
| A deck | [Presentations from JSON]({{< ref "/assembly/net/use-cases/generate-presentations-from-json.md" >}}) |
| To serve this from a web application | [Reports in ASP.NET Core]({{< ref "/assembly/net/use-cases/generate-reports-in-aspnet-core.md" >}}) |
| To run it on Linux | [Docker and serverless]({{< ref "/assembly/net/use-cases/running-in-docker-and-serverless.md" >}}) |

## Is this mail merge?

It replaces it. Classic mail merge fills `MERGEFIELD` placeholders from one flat row of data: one
record, a fixed set of fields, no logic. A GroupDocs.Assembly template adds `<<foreach>>` for
repeating sections, `<<if>>` for conditions, expressions such as `Sum`, `GroupBy` and `OrderBy`,
and nested objects — so an invoice with a variable number of lines and a conditional block is a
single template rather than a template plus code.

## Frequently asked questions

**How do you generate a Word document from a template in C#?**
Put `<<[...]>>` tags in a `.docx` and call `DocumentAssembler.AssembleDocument` with the template,
an output path and a `DataSourceInfo` holding your data.

**Is Microsoft Word or Office needed on the server?**
No. GroupDocs.Assembly reads and writes the formats itself, on Windows and on Linux.

**Can the data be JSON instead of a .NET object?**
Yes. `JsonDataSource` takes a file, a stream or a string, and the template does not change.

**Can the same template produce a PDF?**
Yes — add `new LoadSaveOptions(FileFormat.Pdf)` to the call.

**Which template formats are supported?**
DOCX, DOC, DOCM, DOTX, RTF, ODT and plain text, plus spreadsheet, presentation and e-mail
templates with the same tag syntax.

## What to read next

*   [Install and apply a license]({{< ref "/assembly/net/developer-guide/basic-usage/install-and-apply-license.md" >}})
*   [Basic template syntax]({{< ref "/assembly/net/developer-guide/basic-usage/basic-template-syntax.md" >}})
*   Blog: [Generate Word documents from templates in C#](https://blog.groupdocs.com/assembly/generate-word-documents-from-templates-csharp/)
*   GitHub: [word-report-from-template-net](https://github.com/groupdocs-assembly/word-report-from-template-net)
