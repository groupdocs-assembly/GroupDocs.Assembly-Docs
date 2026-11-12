---
id: mcp-uc-generate-reports-from-repository-data
url: assembly/mcp/use-cases/generate-reports-from-repository-data
title: How to generate a PDF or Word report from JSON data in a repository with Claude Code
linkTitle: Reports from repo data
weight: 6
description: "Generate release notes, reports and certificates as PDF or Word from JSON files in a code repository with Claude Code over MCP, locally: templates are versioned with the code, outputs stay out of git."
keywords: Claude Code generate PDF report, release notes PDF from JSON, generate document from repository data, coding agent document generation, docs as code templates
productName: GroupDocs.Assembly MCP Server
toc: True
structuredData:
    showOrganization: True
    howTo:
        name: "How to generate a PDF or Word report from JSON data in a repository with Claude Code"
        description: "Generate release notes, reports and certificates as PDF or Word from JSON files in a code repository with Claude Code over MCP, locally: templates are versioned with the code, outputs stay out of git."
        steps:
        - name: "Install the server"
          text: "Run the GroupDocs.Assembly MCP server with Docker or dnx and register it in your AI client."
        - name: "Put the documents in the storage folder"
          text: "Point GROUPDOCS_MCP_STORAGE_PATH at the folder that holds the files the agent should use."
        - name: "Ask the agent"
          text: "Generate the release notes PDF for 4.2.0 from data/release-4.2.0.json, and a contribution certificate for everyone in data/contributors-2026.json."
---

Your repository already holds the data — a release manifest, a changelog, a contributors list. Run the GroupDocs.Assembly MCP server locally with the repository as its storage folder, and Claude Code (or any coding agent) turns that JSON into a formatted PDF or Word document from a template you version next to the code:

```bash
claude mcp add groupdocs-assembly \
  -e GROUPDOCS_MCP_STORAGE_PATH=$(pwd) -- dnx GroupDocs.Assembly.Mcp --yes
```

> Generate the release notes PDF for 4.2.0 from data/release-4.2.0.json, and a contribution certificate for everyone in data/contributors-2026.json.

{{< alert style="info" >}}
The commands and config snippets on this page are for the **.NET** build of the server — the only platform available today. Installation and client setup: [MCP server for .NET]({{< ref "assembly/net/mcp/_index.md" >}}). Other platforms will expose the same tools with their own launch command; everything else on this page applies unchanged.
{{< /alert >}}

## Prerequisites

* The .NET 10 SDK; the server registered for the project — [register in AI clients]({{< ref "assembly/net/mcp/install-in-ai-clients.md" >}}).
* Templates in the repository (`templates/release-notes.docx`, `templates/certificate.docx`) and JSON data (`data/*.json`).

## The repository

```text
./  (the repository = the storage folder)
  data/release-4.2.0.json        --+
  data/contributors-2026.json    --|--  the data is already in the repo
  templates/release-notes.docx   --|--  the layout is versioned with it
  templates/certificate.docx     --+
        |
  assemble_document    --> release-notes-4.2.0.pdf
  assemble_per_record  --> pnair.pdf  tvarga.pdf  mrossi.pdf
        (recordsPath "contributors", fileNameField "Handle")
```

## What the agent sees

Captured from server 26.11.0, with the repository as the storage folder (the evaluation note that opens each response is trimmed):

```text
-> get_template_fields {"template":{"filePath":
     "templates/release-notes.docx"}}
<- { "dataSourceNames": [ "release", "changes" ],
     "fields": [ "release.Product", "release.Version", "release.Date",
                 "changes[].Type", "changes[].Title", "changes[].PullRequest",
                 "changes[].Author" ] }

-> assemble_document {"template":{"filePath":
     "templates/release-notes.docx"},
     "data":{"filePath":"data/release-4.2.0.json"},"format":"pdf",
     "outputName":"release-notes-4.2.0.pdf"}
<- Assembled 'release-notes.docx' with 'release-4.2.0.json' (JSON object)
   as PDF
   Saved to: …/release-notes-4.2.0.pdf

-> assemble_per_record {"template":{"filePath":
     "templates/certificate.docx"},
     "data":{"filePath":"data/contributors-2026.json"},
     "recordsPath":"contributors","fileNameField":"Handle","format":"pdf"}
<- Assembled 3 of 3 document(s) from 'certificate.docx' with
   'contributors-2026.json', one per record (each record as 'contributor'),
   as PDF.
   Saved to:
   …/pnair.pdf
   …/tvarga.pdf
   …/mrossi.pdf
```

The release-notes template repeats a table row per change and ends with `<<[changes.Count()]>> changes from <<[changes.Select(c => c.Author).Distinct().Count()]>> contributors.` — the counting is done by the template, not by the model.

## Expected result

`release-notes-4.2.0.pdf` and one certificate per contributor, generated in the output folder. The JSON stays the source of truth; the next release is the same prompt with a new file.

## Keep outputs out of git

Generated files are written to the storage folder (or `GROUPDOCS_MCP_OUTPUT_PATH`). Point the output path at a build folder and ignore it:

```text
# .gitignore
out/
```

with `-e GROUPDOCS_MCP_OUTPUT_PATH=$(pwd)/out` on the `claude mcp add` line.

## Troubleshooting

| Symptom | Cause | Fix |
|---|---|---|
| The JSON's array is inside an object | per-record needs to know where | `recordsPath: "contributors"` |
| A date printed as `11/3/2026 12:00:00 AM` | no format in the template | `<<[release.Date]:"d MMMM yyyy">>` |
| A date one day early | a date-only string east of UTC | write `"2026-11-03T00:00:00"` in the JSON |

## FAQ

**Can this run in CI?** The server is an MCP server for agents; in CI, call the GroupDocs.Assembly library or run the agent. Locally, the agent is the build step.

**Are templates code?** Treat them so: image and document tags load the paths and URLs their expressions return. Review template changes like code changes.

**Can it read YAML or TOML?** No — JSON, XML, CSV and document tables. Ask the agent to convert first.

## Add to your CLAUDE.md or AGENTS.md

Agents follow project instructions about *when* to use a tool. Paste this into the instruction file your agent reads (`CLAUDE.md`, `AGENTS.md`, `.github/copilot-instructions.md`, `.cursorrules`):

```text
Release documents are generated, not written: use the groupdocs-assembly MCP
server with templates/*.docx and data/*.json. Output to out/ (gitignored).
Never edit the generated files; change the template or the data instead.
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
* [Inspect and fix a template]({{< ref "assembly/mcp/use-cases/inspect-and-fix-a-template.md" >}})
* [From notes or email to a document]({{< ref "assembly/mcp/use-cases/build-a-document-from-data-the-agent-extracted.md" >}})
* [On-premise deployment]({{< ref "assembly/mcp/use-cases/on-premise-document-generation.md" >}})
* [Tools reference]({{< ref "assembly/mcp/tools-reference/_index.md" >}}) · [Licensing]({{< ref "assembly/mcp/getting-started/licensing.md" >}}) · [Troubleshooting & FAQ]({{< ref "assembly/mcp/troubleshooting-faq.md" >}})
* Questions: [Assembly forum](https://forum.groupdocs.com/c/assembly/15)

## Read more

* [Your repo already has the data; let the agent make the PDF](https://blog.groupdocs.com/assembly/generate-pdf-report-from-repository-json-claude-code-mcp/) — the same scenario on the GroupDocs blog, with worked examples and the trade-offs.

