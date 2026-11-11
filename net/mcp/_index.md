---
id: mcp-net
url: assembly/net/mcp
title: MCP server for .NET
linkTitle: MCP Server
weight: 7
description: "Install and configure the GroupDocs.Assembly MCP server for .NET — one-click install links for VS Code and Cursor, per-OS setup for Windows, Linux, and macOS, and the full environment-variable reference."
keywords: GroupDocs.Assembly MCP .NET, install MCP server dnx, MCP server Docker image, MCP server configuration, Model Context Protocol .NET
productName: GroupDocs.Assembly MCP Server for .NET
hideChildren: True
toc: True
---

Everything needed to **install and run** the GroupDocs.Assembly MCP server on the .NET platform. What the server *does* — its tools, use cases, and licensing model — is platform-independent and lives in the [MCP server section]({{< ref "assembly/mcp/_index.md" >}}).

| The .NET build at a glance | |
|---|---|
| Package | [`GroupDocs.Assembly.Mcp`](https://www.nuget.org/packages/GroupDocs.Assembly.Mcp) (current **26.11.0**) |
| One-command run | `dnx GroupDocs.Assembly.Mcp --yes` |
| Container images | `ghcr.io/groupdocs-assembly/assembly-net-mcp` · `groupdocs/assembly-net-mcp` |
| Prerequisites | [.NET 10 SDK](https://dotnet.microsoft.com/download/dotnet/10.0) for the NuGet channel, or Docker |
| Source | [GroupDocs.Assembly.Mcp on GitHub](https://github.com/groupdocs-assembly/GroupDocs.Assembly.Mcp) |
| Release notes | [changelog](https://github.com/groupdocs-assembly/GroupDocs.Assembly.Mcp/tree/main/changelog) · [GitHub releases](https://github.com/groupdocs-assembly/GroupDocs.Assembly.Mcp/releases) |

## Start here

1. **Install** for your operating system — [Windows]({{< ref "assembly/net/mcp/windows-installation.md" >}}) · [Linux]({{< ref "assembly/net/mcp/linux-installation.md" >}}) · [macOS]({{< ref "assembly/net/mcp/macos-installation.md" >}})
2. **Register it in your AI client** — [one-click links and per-client configs]({{< ref "assembly/net/mcp/install-in-ai-clients.md" >}})
3. **Point it at your documents** — [configuration]({{< ref "assembly/net/mcp/configuration.md" >}})
4. **License it** — evaluation, a license file, or metered keys: [Licensing]({{< ref "assembly/mcp/getting-started/licensing.md" >}})

## In this section

* [Install on Windows]({{< ref "assembly/net/mcp/windows-installation.md" >}})
* [Install on Linux]({{< ref "assembly/net/mcp/linux-installation.md" >}})
* [Install on macOS]({{< ref "assembly/net/mcp/macos-installation.md" >}})
* [Register in AI clients]({{< ref "assembly/net/mcp/install-in-ai-clients.md" >}}) — VS Code, Cursor, Claude, Visual Studio, Windsurf, Cline, Codex, Rider
* [Configuration]({{< ref "assembly/net/mcp/configuration.md" >}}) — storage, output, license, metered keys
* [System requirements]({{< ref "assembly/net/mcp/system-requirements.md" >}})
* [Troubleshooting (.NET)]({{< ref "assembly/net/mcp/troubleshooting.md" >}}) — `dnx`, native libraries, Docker daemon

## Platform-independent reference

* [Tools reference]({{< ref "assembly/mcp/tools-reference/_index.md" >}}) — `get_template_fields`, `assemble_document`, `assemble_per_record`, `get_document_info`, `get_supported_formats`, `get_license_status`
* [Use cases]({{< ref "assembly/mcp/use-cases/_index.md" >}}) · [Supported formats]({{< ref "assembly/mcp/supported-formats.md" >}}) · [Troubleshooting & FAQ]({{< ref "assembly/mcp/troubleshooting-faq.md" >}})
