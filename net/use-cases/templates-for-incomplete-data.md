---
id: templates-for-incomplete-data
url: assembly/net/templates-for-incomplete-data
title: Templates for Incomplete Data
linkTitle: Templates for incomplete data
weight: 3
description: "Keep a report assembling when the data has holes: a JSON Schema as the contract, AllowMissingMembers for sparse data and InlineErrorMessages for templates you do not own."
keywords: JSON Schema template, AllowMissingMembers, InlineErrorMessages, null safe template, missing member, document assembly options
productName: GroupDocs.Assembly for .NET
hideChildren: False
toc: True
---

Data has holes: a customer with no payment card yet, a loyalty record that is `null`, a field an
upstream system quietly stopped sending. A report that fills in perfectly during development and
fails on the third customer of the night batch is the usual way this is discovered.

Three mechanisms decide what happens instead. Pick by what a hole *means* in your case.

{{< alert style="info" >}}
A runnable implementation of this page is on GitHub:
[data-safe-templates-net](https://github.com/groupdocs-assembly/data-safe-templates-net).
{{< /alert >}}

## The data this page uses

```json
{
  "Name": "Quayside Bistro",
  "Account": "00042",
  "Cards": [],
  "Loyalty": null
}
```

Valid JSON, and a correct template over it still does not assemble.

## 1. A JSON Schema: the shape is known in advance

{{< alert style="info" >}}Schema support for `JsonDataSource` is available since version 26.11.{{< /alert >}}

Without a schema the engine learns the shape of the data from the data itself, which fails in two
ways:

*   an **empty array** gives it no element type, so `<<[customer.Cards.First().Type]>>` cannot be
    resolved — even though the branch around that tag is never rendered;
*   `"00042"` **looks like a number**, so it is loaded as `42` and the document shows the wrong
    account.

Passing the schema settles both before the first value is read:

```csharp
JsonDataSource dataSource = new JsonDataSource(
    Path.Combine(DataSourcesPath, "Customer.json"),
    Path.Combine(DataSourcesPath, "Customer.schema.json"));

DocumentAssembler assembler = new DocumentAssembler();
assembler.AssembleDocument(
    Path.Combine(TemplatesPath, "Json schema.docx"),
    Path.Combine(OutputPath, "with-schema.docx"),
    new DataSourceInfo(dataSource, "customer"));
```

Members the schema declares may be used by the template even when the data has them empty, null or
missing, and their types come from the schema:

```json
{
  "$schema": "https://json-schema.org/draft/2020-12/schema",
  "type": "object",
  "properties": {
    "Name":    { "type": "string" },
    "Account": { "type": "string" },
    "Cards":   { "type": "array",
                 "items": { "type": "object",
                            "properties": { "Type": { "type": "string" }, "Last4": { "type": "string" } } } },
    "Loyalty": { "type": ["object", "null"],
                 "properties": { "Level": { "type": "string" } } }
  }
}
```

Use this when the data comes from a system whose contract you know — an API, an export, the output
of a model you prompted with the same schema. Details are on
[Working with JSON data sources]({{< ref "/assembly/net/developer-guide/advanced-usage/working-with-simple-data-sources/working-with-json-data-sources.md" >}}).

## 2. `AllowMissingMembers`: the data is genuinely sparse

A member the data does not have at all. By default that is an error:

```text
An error has been encountered at the end of expression 'customer.Fax]>'.
Can not get the value of member 'Fax' on type 'System.Data.DataRow'.
```

With the option it renders as an empty value and the document is produced:

```csharp
DocumentAssembler assembler = new DocumentAssembler
{
    Options = DocumentAssemblyOptions.AllowMissingMembers
};

assembler.AssembleDocument(template, output, new DataSourceInfo(data, "customer"));
```

Use it when a blank really is the right output. Leave it off when a missing member means somebody
changed the data and nobody noticed — that is the case where you want the batch to stop.

## 3. `InlineErrorMessages`: the template is not yours

For templates edited by people outside your team. The error is written into the report where the
tag was, and `AssembleDocument` returns `false`:

```csharp
DocumentAssembler assembler = new DocumentAssembler
{
    Options = DocumentAssemblyOptions.InlineErrorMessages
};

bool success = assembler.AssembleDocument(template, output, new DataSourceInfo(data, "customer"));
```

A nightly batch of two thousand documents finishes, and the three that are wrong carry the reason
in their own text, next to the tag that caused it. Check the return value and route those three to
whoever owns the template — see
[Error handling]({{< ref "/assembly/net/developer-guide/basic-usage/error-handling.md" >}}).

## Choosing

| Situation | Use |
|---|---|
| The shape is known in advance; values may be empty, null or missing | a JSON Schema |
| The data is genuinely sparse and a blank is correct | `AllowMissingMembers` |
| Templates are edited outside your team | `InlineErrorMessages`, and check the return value |
| A missing member means something upstream broke | the default: let it throw |

The options combine. A schema plus `InlineErrorMessages` is a reasonable default for a service that
assembles documents from data it does not own.

## What to read next

*   [Generate documents from model output]({{< ref "/assembly/net/use-cases/generate-documents-from-llm-output.md" >}}) — where incomplete data comes from most often
*   [Error handling]({{< ref "/assembly/net/developer-guide/basic-usage/error-handling.md" >}}) — the options in the reference
*   Blog: [Templates that survive incomplete data](https://blog.groupdocs.com/assembly/templates-that-survive-incomplete-data-csharp/)
*   GitHub: [data-safe-templates-net](https://github.com/groupdocs-assembly/data-safe-templates-net)
