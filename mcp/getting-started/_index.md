---
id: mcp-getting-started
url: assembly/mcp/getting-started
title: Quick start
weight: 1
description: "Install and register the GroupDocs.Assembly MCP server in Claude Desktop, VS Code, Cursor, or any MCP client in three commands using the guided installer — then verify the setup automatically."
keywords: how to install MCP server, set up document MCP server, add MCP server to Claude Desktop, MCP server quick start
productName: GroupDocs.Assembly MCP Server
hideChildren: True
toc: True
---

{{< alert style="info" >}}
These steps install the **.NET** build of the server — the only platform available today. Java, Python, and Node.js builds are planned; each will get its own install section under its platform. Platform-independent material (tools, use cases, licensing) lives here and applies to all of them.
{{< /alert >}}

Install and register the GroupDocs.Assembly MCP server in Claude Desktop, VS Code, Cursor, or any MCP client in three commands with the guided [installer](https://github.com/groupdocs/GroupDocs.Mcp.Installer) — then verify the setup automatically:

```powershell
git clone https://github.com/groupdocs/GroupDocs.Mcp.Installer.git
cd GroupDocs.Mcp.Installer

# wizard: products, channel, clients, folders, license
./install-groupdocs-mcp.ps1 -Interactive
# preview - prints everything, changes nothing
./install-groupdocs-mcp.ps1 -DryRun
# apply + warm caches + verify the setup in one go
./install-groupdocs-mcp.ps1 -Verify
```

Then **restart your AI client** (Claude Desktop, VS Code, Cursor, …) so it picks up the new server.

## Your first prompt

Put a template with `<<[...]>>` tags (say `contract-template.docx`) into the storage folder you chose, then ask your agent:

> What data does contract-template.docx need? Fill it for Contoso Pharma with the three services below and save it as a PDF

The agent calls `get_template_fields`, fills the JSON skeleton it gets back from your text, and calls `assemble_document` with `dataJson` and `format: pdf`. The PDF lands in your storage folder as `contract-template_assembled.pdf`; the template is untouched and nothing is uploaded.

## Where to go next

* **Fresh machine?** Follow your OS page — it includes the prerequisite bootstrap:
  [Windows]({{< ref "assembly/net/mcp/windows-installation.md" >}}) · [Linux]({{< ref "assembly/net/mcp/linux-installation.md" >}}) · [macOS]({{< ref "assembly/net/mcp/macos-installation.md" >}})
* **Manual or single-client install** (exact JSON per client): [Register in AI clients]({{< ref "assembly/net/mcp/install-in-ai-clients.md" >}})
* **Docker-only shop:** run `./install-groupdocs-mcp.ps1 -EmitCompose -Clients @()` to generate a `docker-compose.yml` instead of client registration — see [Configuration]({{< ref "assembly/net/mcp/configuration.md" >}}).
* **Licensing:** the server works in evaluation mode out of the box; your existing GroupDocs.Assembly license applies — [Licensing]({{< ref "assembly/mcp/getting-started/licensing.md" >}}).
