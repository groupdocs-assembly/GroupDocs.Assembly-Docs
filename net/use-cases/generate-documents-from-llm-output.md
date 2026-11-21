---
id: generate-documents-from-llm-output
url: assembly/net/generate-documents-from-llm-output
title: Generate Documents from Model Output
linkTitle: Documents from model output
weight: 1
description: "Turn the JSON a language model returns into a branded Word or PDF document: a JSON Schema as the contract between the model and the template, and control over the external resources the data may reference."
keywords: LLM document generation, structured output to Word, JSON Schema template, AI report generation C#, model output to PDF, document automation
productName: GroupDocs.Assembly for .NET
hideChildren: False
toc: True
---

A language model reads a contract, an e-mail thread or a scanned invoice well, and writes a
finished business document badly: it has no access to your fonts, your logo, your numbering or the
wording legal approved. Splitting the work solves both halves. The model returns **data**, and a
template turns that data into the document.

GroupDocs.Assembly is the second half. It never sees the model: it sees a JSON file and a template,
which is what makes the arrangement portable across models, SDKs and local runtimes.

{{< alert style="info" >}}
A runnable implementation of this page is on GitHub:
[llm-json-to-branded-documents-net](https://github.com/groupdocs-assembly/llm-json-to-branded-documents-net).
{{< /alert >}}

## The contract: a JSON Schema on both sides

Model output is incomplete in ways real data usually is not: an array that happens to be empty, an
object that is `null`, a field the source document never mentioned. Describe the data with a
[JSON Schema]({{< ref "/assembly/net/developer-guide/advanced-usage/working-with-simple-data-sources/working-with-json-data-sources.md" >}})
and hand the same schema to both sides — to the model as the shape of the answer, and to the
assembler as the shape of the data.

{{< alert style="info" >}}Schema support for `JsonDataSource` is available since version 26.11.{{< /alert >}}

```csharp
JsonDataSource dataSource = new JsonDataSource(
    Path.Combine(DataSourcesPath, "Customer.json"),
    Path.Combine(DataSourcesPath, "Customer.schema.json"));

DocumentAssembler assembler = new DocumentAssembler();
assembler.AssembleDocument(
    Path.Combine(TemplatesPath, "Json schema.docx"),
    Path.Combine(OutputPath, "statement.docx"),
    new DataSourceInfo(dataSource, "customer"));
```

With this data:

```json
{
  "Name": "Quayside Bistro",
  "Account": "00042",
  "Cards": [],
  "Loyalty": null
}
```

the document renders as *Customer: Quayside Bistro*, *Account number: 00042*, *No payment card on
file* and an empty loyalty line.

Without the schema the same template and the same data fail, for two reasons that both come from
the engine having to learn the shape of the data from the data itself:

*   an **empty array** has no element type, so `<<[customer.Cards.First().Type]>>` cannot be
    resolved even though the branch around it is never rendered;
*   `"00042"` **looks like a number**, so it reaches the document as `42`.

The schema settles both before the first value is read. Members it declares may be used by the
template even when the data has them empty, null or missing, and their types come from the schema.

## Writing the prompt around the schema

Nothing in the prompt needs to describe the document. It describes the data:

```text
Return only a JSON object that satisfies the JSON Schema below. No prose, no markdown fences.

1. Use exactly the property names of the schema. The template reads those names.
2. Keep the declared types. A value the schema calls a string stays a string, even when it
   looks like a number: an account number 00042 must not become 42.
3. When the source does not mention something, leave it out, or use null, or an empty array -
   whichever the schema allows. Do not invent a value.
4. Do not add properties the schema does not declare.
```

Rule 3 is the one that pays for itself. A model told to "be safe" will invent a plausible value,
and an invented loyalty level is worse than a blank line.

## Model output is untrusted data

A model can return a string that looks like an image reference, because the document it read
contained one. Since 26.11 a URI that comes from **data** is not fetched by default, while a URI the
**template** carries is — so the branding your designer put in the template keeps working, and a
value derived from somebody else's document does not make your server issue requests.

```csharp
// The image URI comes from data, so it is skipped by default and the image is left empty.
const string photoUri = "https://images.example.com/photos/no-photo.jpg";

DocumentAssembler assembler = new DocumentAssembler();
assembler.AssembleDocument(
    Path.Combine(TemplatesPath, "Inserting image.docx"),
    Path.Combine(OutputPath, "skipped.docx"),
    new DataSourceInfo(photoUri, "expression"));

// Allow a trusted host and see every decision.
LoadSaveOptions options = new LoadSaveOptions();
options.WhitelistedResources.Add("images.example.com");
options.ExternalResourceHandler = new LocalImageHandler(Path.Combine(ImagesPath, "no-photo.jpg"));

assembler.AssembleDocument(
    Path.Combine(TemplatesPath, "Inserting image.docx"),
    Path.Combine(OutputPath, "provided.docx"),
    options,
    new DataSourceInfo(photoUri, "expression"));
```

The handler sees every reference and may supply the bytes itself, so the assembly step can run with
no outbound network at all:

```csharp
public class LocalImageHandler : ExternalResourceHandler
{
    private readonly string mImagePath;

    public LocalImageHandler(string imagePath)
    {
        mImagePath = imagePath;
    }

    public override void OnLoading(ExternalResourceLoadingArgs args)
    {
        Console.WriteLine($"{args.Origin} resource {args.Uri}: {(args.Skipped ? "skipped" : "allowed")}");

        // Provide the content instead of requesting it.
        if (!args.Skipped && args.Uri.StartsWith("https://images.example.com/", StringComparison.OrdinalIgnoreCase))
            args.Data = File.ReadAllBytes(mImagePath);
    }
}
```

The full picture is on
[Controlling External Resources]({{< ref "/assembly/net/developer-guide/advanced-usage/loading-and-saving-with-external-resource-files/controlling-external-resources.md" >}}).

## One template, objects and JSON alike

A template written for typed objects runs unchanged over the same data as JSON, XML or CSV. Since
26.11 that includes the parts that used to differ: members of dates and numbers that may be missing
in a file, Booleans used as conditions and in predicates, `$id`/`$ref` references written by
Json.NET with preserved references, and grouping over nested objects that compare by value.

```csharp
assembler.AssembleDocument(
    Path.Combine(TemplatesPath, "Customer orders.docx"),
    Path.Combine(OutputPath, "orders.docx"),
    new DataSourceInfo(new JsonDataSource(Path.Combine(DataSourcesPath, "Customers.json")), "customers"));
```

This matters here because model output arrives as a file, while the template was usually written
against the classes of the system that already prints the document.

## Checklist for production

*   **Validate before you assemble.** The schema protects the template; it does not make the data
    true. Business rules — a total that matches the lines, a date in range — are still yours.
*   **Keep the model out of the document path.** Store the JSON it returned. A document you cannot
    reproduce from stored data is a document you cannot explain later.
*   **Decide what a missing member means.** See
    [Templates for incomplete data]({{< ref "/assembly/net/use-cases/templates-for-incomplete-data.md" >}}).
*   **Leave the external-resource default alone** unless a reviewer agreed otherwise, and whitelist
    hosts rather than switching the check off.

## What to read next

*   [Templates for incomplete data]({{< ref "/assembly/net/use-cases/templates-for-incomplete-data.md" >}}) — the schema and the two assembly options, in detail
*   [Working with JSON data sources]({{< ref "/assembly/net/developer-guide/advanced-usage/working-with-simple-data-sources/working-with-json-data-sources.md" >}}) — load options, types and references
*   [Controlling external resources]({{< ref "/assembly/net/developer-guide/advanced-usage/loading-and-saving-with-external-resource-files/controlling-external-resources.md" >}}) — the whole policy surface
*   Blog: [From model output to a branded document](https://blog.groupdocs.com/assembly/llm-json-to-branded-documents-csharp/)
*   GitHub: [llm-json-to-branded-documents-net](https://github.com/groupdocs-assembly/llm-json-to-branded-documents-net)
