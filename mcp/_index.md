---
id: mcp
url: assembly/mcp
title: GroupDocs.Assembly MCP Server
weight: 6
description: "GroupDocs.Assembly MCP server lets AI agents like Claude, Cursor, and Copilot generate documents from templates and data — contracts, letters, reports with tables and charts — in Word, Excel, PowerPoint, PDF and email, locally on your machine."
keywords: document generation MCP server, generate documents from templates AI agent, mail merge MCP, fill Word template with JSON, Claude generate PDF from template locally
productName: GroupDocs.Assembly MCP Server
hideChildren: True
toc: True
---

**GroupDocs.Assembly MCP server** lets AI agents like Claude, Cursor, and Copilot **generate documents from templates and data** — a contract from a JSON object, a letter per customer, a report with tables and charts from a CSV — in Word, Excel, PowerPoint, PDF and email, **locally on your machine**. The agent supplies the data; the template controls the document. 

Run it with one command. The Docker image is self-contained — the runtime and every native dependency the engine needs are inside it:

```bash
docker run --rm -i -v $(pwd)/documents:/data \
  ghcr.io/groupdocs-assembly/assembly-net-mcp:latest
```

With the .NET 10 SDK installed, the same server also runs without Docker:

```bash
dnx GroupDocs.Assembly.Mcp --yes
```

Both are the **.NET** build of the server and run on Windows, Linux, and macOS. Other platforms will each get their own launcher — see [Install for your platform](#install-for-your-platform).

Or use the [guided installer]({{< ref "assembly/mcp/getting-started/_index.md" >}}) to register the server in your AI client, verify the setup, and configure shared folders in one pass.

Then ask your agent, in plain language:

> What data does contract-template.docx need? Fill it for Contoso Pharma with the three services below and save it as a PDF.

## What you can do

Six tools (full details in the [tools reference]({{< ref "assembly/mcp/tools-reference/_index.md" >}})):

| The user asks… | The agent calls | It gets back |
|---|---|---|
| "What does this template need?" | [`get_template_fields`]({{< ref "assembly/mcp/tools-reference/get-template-fields.md" >}}) | tags, data names, a JSON skeleton to fill |
| "Make the contract / invoice / report" | [`assemble_document`]({{< ref "assembly/mcp/tools-reference/assemble-document.md" >}}) | the generated document, in the template's format or PDF, HTML, Markdown… |
| "One letter per customer" | [`assemble_per_record`]({{< ref "assembly/mcp/tools-reference/assemble-per-record.md" >}}) | one file per record, named by a field; failed records listed |
| "What's in this data file?" | [`get_document_info`]({{< ref "assembly/mcp/tools-reference/get-document-info.md" >}}) | family, tags, JSON shape, spreadsheet tables and columns |
| "Can it save an Excel template as PDF?" | [`get_supported_formats`]({{< ref "assembly/mcp/tools-reference/get-supported-formats.md" >}}) | template, save and data formats |
| "Why does it say Evaluation Only?" | [`get_license_status`]({{< ref "assembly/mcp/tools-reference/get-license-status.md" >}}) | the licensing mode |

## Ask the template, fill the data, render

The pattern behind every scenario — captured from the server:

```text
user              agent                        Assembly MCP server
 |  "Make the contract for this order: Contoso Pharma, 12 months ..."  |
 |---------------->|                                                   |
 |                 |-- get_template_fields ------------------------->|
 |                 |   {"template":{"filePath":                        |
 |                 |     "contract-template.docx"}}                    |
 |                 |<- {"dataSourceNames":["contract","customer",      |
 |                 |    "items"], "dataSkeleton":{"customer":{"Name":  |
 |                 |    ""...}, "items":[{"Title":"","Quantity":0}]}} -|
 |                 |   the agent fills the skeleton from the order     |
 |                 |-- assemble_document --------------------------->|
 |                 |   {"template":{...},"dataJson":"{...}",           |
 |                 |    "format":"pdf"}                                |
 |                 |<- "Assembled 'contract-template.docx' with inline |
 |                 |    JSON (JSON object) as PDF" --------------------|
 |<- "Contract SA-2026-118 is ready: 3 services, total 75500 EUR."     |
   the model writes the data; layout, tables and wording come from the template
```

The model never composes the document. It reads the template's **data contract** — the skeleton from `get_template_fields` — and fills it; the engine renders tables, totals, conditional paragraphs, charts, images and barcodes exactly as the template defines them. The same data gives the same document every time, and a reviewer checks a JSON object instead of re-reading prose.

## How data reaches the template

```text
data you give            what the template sees               how to name it
-----------------------  -----------------------------------  ----------------
JSON object              its keys: contract, customer, items  nothing to do
JSON array / XML / CSV   one collection                       worked out from
spreadsheet / Word table   (columns are the members)            the template, or
                                                                dataSourceName
"2026-11-12T00:00:00"    a date - format it in the template   :"d MMMM yyyy"
{{name}} in a template   left as text - not Assembly syntax   use <<[name]>>
```

JSON (inline or a file), XML, CSV and the tables of Excel, Word and PowerPoint documents all work. Details and the template language in one table: [tools reference]({{< ref "assembly/mcp/tools-reference/_index.md" >}}#how-the-tools-address-templates-and-data).

## Scenarios

* [Generate documents with AI agents]({{< ref "assembly/mcp/use-cases/generate-documents-with-ai-agents.md" >}}) — start here: template → skeleton → document.
* [One document per record (mail merge)]({{< ref "assembly/mcp/use-cases/one-document-per-record-mail-merge.md" >}}) — a letter per customer, named after the customer.
* [Reports with tables and charts from data files]({{< ref "assembly/mcp/use-cases/reports-with-tables-and-charts-from-data-files.md" >}}) — a spreadsheet or CSV in, a report out.
* [Inspect and fix a template]({{< ref "assembly/mcp/use-cases/inspect-and-fix-a-template.md" >}}) — what it needs, and why it failed.
* [Build a document from data the agent extracted]({{< ref "assembly/mcp/use-cases/build-a-document-from-data-the-agent-extracted.md" >}}) — from an email or notes to a finished contract.
* [Generate reports from repository data]({{< ref "assembly/mcp/use-cases/generate-reports-from-repository-data.md" >}}) — release notes and certificates with Claude Code.
* [On-premise architecture]({{< ref "assembly/mcp/use-cases/on-premise-document-generation.md" >}}) — what stays local, and what a template can reach.

## Install for your platform

Installation, prerequisites, and client configuration are platform-specific; the tools and licensing model are the same everywhere.

| Platform | Status | Install and setup |
|---|---|---|
| .NET | **Available** | [MCP server for .NET]({{< ref "assembly/net/mcp/_index.md" >}}) |
| Java | Planned | [Tell us you need it](https://forum.groupdocs.com/c/assembly/15) |
| Python | Planned | [Tell us you need it](https://forum.groupdocs.com/c/assembly/15) |
| Node.js | Planned | [Tell us you need it](https://forum.groupdocs.com/c/assembly/15) |

## Supported AI clients

| Client | How it connects |
|---|---|
| Claude Desktop | `claude_desktop_config.json` |
| Claude Code | `claude mcp add` CLI |
| VS Code / GitHub Copilot | user-level or workspace `mcp.json` |
| Visual Studio 2022 (17.14+) | `.mcp.json` in the solution root |
| Cursor | `~/.cursor/mcp.json` |
| Windsurf | `~/.codeium/windsurf/mcp_config.json` |
| Cline | Cline MCP settings |
| Codex CLI | `codex mcp add` CLI |
| JetBrains Rider | manual registration (Settings → AI Assistant → MCP) |

Exact config blocks for every client: [Register in AI clients]({{< ref "assembly/net/mcp/install-in-ai-clients.md" >}}).

## Delivery channels

| | NuGet (`dnx`) | Docker |
|---|---|---|
| Prerequisites | .NET 10 SDK (+ `libgdiplus` on Linux/macOS for presentation templates and charts) | Docker only |
| Native dependencies | installed by you (or the setup script) | bundled in the image |
| Package | `GroupDocs.Assembly.Mcp` on NuGet | `ghcr.io/groupdocs-assembly/assembly-net-mcp` · `groupdocs/assembly-net-mcp` |
| Time zone | the machine's — see the date note in the [tools reference]({{< ref "assembly/mcp/tools-reference/_index.md" >}}#how-the-tools-address-templates-and-data) | UTC |

## How it works

The server uses MCP's **local stdio transport**: your AI client starts the server as a child process and talks to it over standard input/output. No inbound ports, no external endpoints, no telemetry — the data path is *agent → local server → local filesystem*. Templates and data are read from your storage folder; generated documents are written next to them. Details: [On-premise architecture]({{< ref "assembly/mcp/use-cases/on-premise-document-generation.md" >}}).

## Resources

* [Quick start]({{< ref "assembly/mcp/getting-started/_index.md" >}}) · [Use cases]({{< ref "assembly/mcp/use-cases/_index.md" >}}) · [Supported formats]({{< ref "assembly/mcp/supported-formats.md" >}}) · [Troubleshooting & FAQ]({{< ref "assembly/mcp/troubleshooting-faq.md" >}})
* GitHub: [server source](https://github.com/groupdocs-assembly/GroupDocs.Assembly.Mcp) · [installer](https://github.com/groupdocs/GroupDocs.Mcp.Installer) · [integration tests](https://github.com/groupdocs-assembly/GroupDocs.Assembly.Mcp.Tests)
* [NuGet package](https://www.nuget.org/packages/GroupDocs.Assembly.Mcp) · [Docker image](https://github.com/orgs/groupdocs-assembly/packages/container/package/assembly-net-mcp) · [MCP Registry](https://registry.modelcontextprotocol.io/v0/servers?search=io.github.groupdocs-assembly/groupdocs-assembly-mcp)
* The library behind it: [GroupDocs.Assembly for .NET]({{< ref "assembly/net/_index.md" >}}) and its [template syntax]({{< ref "assembly/net/developer-guide/basic-usage/working-with-groupdocs.assembly-engine/template-syntax-part-1-of-2.md" >}})
* Questions: [Assembly forum](https://forum.groupdocs.com/c/assembly/15)
