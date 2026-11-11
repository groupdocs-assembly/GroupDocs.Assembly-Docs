---
id: mcp-uc-inspect-and-fix-a-template
url: assembly/mcp/use-cases/inspect-and-fix-a-template
title: How to find out what a template needs and why it failed
linkTitle: Inspect and fix templates
weight: 4
description: "Find out what data a document template needs and why generation failed, with an AI agent over MCP, locally: tags and a JSON skeleton without a run, then the engine's errors in plain words."
keywords: what fields does a template need, why did my template fail, template syntax error AI, debug Word template mail merge, get_template_fields
productName: GroupDocs.Assembly MCP Server
toc: True
structuredData:
    showOrganization: True
    howTo:
        name: "How to find out what a template needs and why it failed"
        description: "Find out what data a document template needs and why generation failed, with an AI agent over MCP, locally: tags and a JSON skeleton without a run, then the engine's errors in plain words."
        steps:
        - name: "Install the server"
          text: "Run the GroupDocs.Assembly MCP server with Docker or dnx and register it in your AI client."
        - name: "Put the documents in the storage folder"
          text: "Point GROUPDOCS_MCP_STORAGE_PATH at the folder that holds the files the agent should use."
        - name: "Ask the agent"
          text: "What does order-lines.docx need, and why won't it generate?"
---

Run the GroupDocs.Assembly MCP server locally and your agent can tell you what a template needs before anything is generated, and explain in plain words why it failed afterwards — a placeholder in the wrong syntax, an unclosed block, a missing field:

```bash
dnx GroupDocs.Assembly.Mcp --yes
```

> What does order-lines.docx need, and why won't it generate?

{{< alert style="info" >}}
The commands and config snippets on this page are for the **.NET** build of the server — the only platform available today. Installation and client setup: [MCP server for .NET]({{< ref "assembly/net/mcp/_index.md" >}}). Other platforms will expose the same tools with their own launch command; everything else on this page applies unchanged.
{{< /alert >}}

## Prerequisites

* The server registered in your AI client — [quick start]({{< ref "assembly/mcp/getting-started/_index.md" >}}).

## Two kinds of checking

```text
get_template_fields  -- static: reads the tags, generates nothing
   |   tags, dataSourceNames, fields, dataSkeleton, notes
   |   notes flag: {{...}} placeholders, unreadable binary templates
   v
assemble_document    -- the engine: finds what static reading cannot
   |   unclosed <<foreach>> ...... "Unexpected end of template"
   |   field missing in data ..... "The template reads 'Email', ..."
   |   empty list + arithmetic ... "Can not apply operator '*' ..."
   v
assemble_document {"inlineErrors":true}
       writes "Error! ..." into the output next to each bad tag
```

## What the agent sees

Captured from server 26.11.0 (the evaluation note that opens each response is trimmed).

**A template in another engine's syntax** (`Dear {{name}}, your order {{order_id}} has shipped.`):

```text
-> get_template_fields {"template":{"filePath":"shipping-notice.docx"}}
<- { "tagCount": 0, "notes": [
     "No <<…>> tags were found: this document is not a GroupDocs.Assembly
      template, or its tags are in a part the server does not read (text
      boxes in charts, embedded objects).",
     "The template contains 2 '{{…}}' placeholder(s). GroupDocs.Assembly
      does not process that syntax and leaves it as text; write <<[name]>>
      instead." ] }
```

**An unclosed block** — `get_template_fields` lists the tags (it reads them statically); the engine finds the problem:

```text
-> assemble_document {"template":{"filePath":"order-lines.docx"},
     "dataJson":"{\"lines\":[{\"Title\":\"Cable\",\"Quantity\":2}]}"}
<- Document assembly failed for 'order-lines.docx': ... Unexpected end of
   template. A block tag is not closed: every <<foreach>> needs <</foreach>>
   and every <<if>> needs <</if>>.
```

**Errors written into the output** — `inlineErrors: true` generates anyway and marks each bad tag (here the upstream sample with `<< var [name]>>`):

```text
-> assemble_document {"template":{"filePath":"inline-error.docx"},
     "dataJson":"{\"name\":\"x\"}","inlineErrors":true}
<- Assembled 'inline-error.docx' with inline JSON (JSON object as 'product')
   as DOCX. The template has errors: each one is written into the output
   next to its tag, starting with 'Error!'
```

The document then reads `<< var [name] Error! An assignment operator is expected. >>`.

**A binary template:**

```text
-> get_template_fields {"template":{"filePath":"contracts-table.msg"}}
<- { "readable": false, "notes": [ "Tags cannot be read from a .msg template
     without generating it. Save the template as DOCX, XLSX, PPTX or EML to
     inspect it, or generate it with assemble_document and inlineErrors=true
     to see which fields fail." ] }
```

**Markdown is a template too** — `product-readme.md` reported `"dataSourceNames": [ "product", "description" ]` and generated a DOCX.

## Expected result

Before a run: the list of data the template needs, and any syntax the engine will ignore. After a failed run: the reason in one sentence and the fix.

## Troubleshooting

| Symptom | Cause | Fix |
|---|---|---|
| *"Unexpected end of template. A block tag is not closed"* | a `<<foreach>>` or `<<if>>` without its closing tag | add `<</foreach>>` / `<</if>>` |
| *"Can not apply operator '*' to operands of type 'System.Object' and 'System.Object'"* | arithmetic over an **empty** list — it carries no types, even with `allowMissingMembers` | pass at least one item, or wrap the block in `<<if [items.Any()]>>` |
| `"readable": false` | a binary template (MSG, DOC, XLS, PPT) | save it as DOCX/XLSX/PPTX/EML to inspect; pass `dataSourceName` with array, CSV or table data |

## FAQ

**Is the skeleton exact?** It is inferred from the tags; the server says so in `notes`. Values computed through `Select` or `GroupBy` projections are not followed.

**Why do tags in a chart not show up?** Static reading skips some parts (text boxes in charts, embedded objects); the note says so. The engine still processes chart tags — see [reports with charts]({{< ref "assembly/mcp/use-cases/reports-with-tables-and-charts-from-data-files.md" >}}).

**Where is the syntax documented?** In the library: [template syntax, part 1]({{< ref "assembly/net/developer-guide/basic-usage/working-with-groupdocs.assembly-engine/template-syntax-part-1-of-2.md" >}}) and [part 2]({{< ref "assembly/net/developer-guide/basic-usage/working-with-groupdocs.assembly-engine/template-syntax-part-2-of-2.md" >}}), and [inline error messages]({{< ref "assembly/net/developer-guide/advanced-usage/use-of-in-line-syntax-error-messages-into-templates.md" >}}).

## Add to your CLAUDE.md or AGENTS.md

Agents follow project instructions about *when* to use a tool. Paste this into the instruction file your agent reads (`CLAUDE.md`, `AGENTS.md`, `.github/copilot-instructions.md`, `.cursorrules`):

```text
Before filling a template, call get_template_fields and read its notes. If
assemble_document fails, quote the server's message, fix the data or tell me
the template line to change; use inlineErrors=true only for debugging copies.
```

## Honest limits

* **Evaluation mode:** every generated document starts with an *Evaluation Only* line, workbooks gain a worksheet, and e-mail templates lose their HTML body. [Licensing]({{< ref "assembly/mcp/getting-started/licensing.md" >}}).
* **`<<[name]>>`, not `{{name}}`:** other engines' placeholders stay in the output as text.
* **Templates are trusted input:** image and document tags load the paths and URLs their expressions return.
* **Dates:** write them as `"2026-11-12T00:00:00"` and format them in the template; a date-only string can shift by a day on machines east of UTC.

## Related

* [Generate documents with AI agents]({{< ref "assembly/mcp/use-cases/generate-documents-with-ai-agents.md" >}})
* [One document per record (mail merge)]({{< ref "assembly/mcp/use-cases/one-document-per-record-mail-merge.md" >}})
* [Reports with tables and charts]({{< ref "assembly/mcp/use-cases/reports-with-tables-and-charts-from-data-files.md" >}})
* [From notes or email to a document]({{< ref "assembly/mcp/use-cases/build-a-document-from-data-the-agent-extracted.md" >}})
* [Reports from repository data]({{< ref "assembly/mcp/use-cases/generate-reports-from-repository-data.md" >}})
* [On-premise deployment]({{< ref "assembly/mcp/use-cases/on-premise-document-generation.md" >}})
* [Tools reference]({{< ref "assembly/mcp/tools-reference/_index.md" >}}) · [Licensing]({{< ref "assembly/mcp/getting-started/licensing.md" >}}) · [Troubleshooting & FAQ]({{< ref "assembly/mcp/troubleshooting-faq.md" >}})
* Questions: [Assembly forum](https://forum.groupdocs.com/c/assembly/15)

## Read more

* [What does this template need? Ask it.](https://blog.groupdocs.com/assembly/ask-the-template-what-it-needs-get-template-fields-mcp/) — the same scenario on the GroupDocs blog, with worked examples and the trade-offs.

