---
id: mcp-troubleshooting-faq
url: assembly/mcp/troubleshooting-faq
title: Troubleshooting & FAQ
weight: 5
description: "Solutions to the most common GroupDocs.Assembly MCP server issues — server not appearing in the client, startup failures, missing native dependencies, and first-launch timeouts."
keywords: MCP server not showing up in Claude Desktop, Claude can't see MCP tools, MCP server failed to start, dnx command not found, libgdiplus not found error, generate documents from template AI agent, mail merge MCP, fill Word template with JSON, document generation Claude
productName: GroupDocs.Assembly MCP Server
toc: True
---

Solutions to the most common GroupDocs.Assembly MCP server issues — server not appearing in the client, startup failures, missing native dependencies, and first-launch timeouts.

{{< alert style="info" >}}
**Platform-specific troubleshooting:** runtime problems depend on which build you run. For the `dnx` runner, native graphics libraries, and the Docker channel, see [Troubleshooting (.NET)]({{< ref "assembly/net/mcp/troubleshooting.md" >}}). The issues on this page apply to every platform.
{{< /alert >}}

## Why is my MCP server not showing up in Claude Desktop?

1. **Restart the client** — every client reads its MCP config only at startup.
2. Check the config file location for your OS ([per-client reference]({{< ref "assembly/net/mcp/install-in-ai-clients.md" >}})) and that the entry sits under the right root key (`mcpServers` for Claude Desktop/Cursor/Windsurf, `servers` for VS Code/VS 2022).
3. Validate the JSON — a trailing comma silently breaks the whole file. If you used the [installer](https://github.com/groupdocs/GroupDocs.Mcp.Installer), a timestamped `.bak` of your previous config sits next to the file for comparison.

## The first tool call is slow or fails once, then works

A **cold cache**: on the very first use the server's package or image is still downloading while the client is already waiting on the connection. Warming it once fixes it for good — the exact command depends on your build: [.NET]({{< ref "assembly/net/mcp/troubleshooting.md" >}}#the-first-tool-call-is-slow-or-fails-once-and-then-works).

## The server fails to start, or a runtime dependency is missing

These are properties of the build you run rather than of MCP, so the fixes live with the platform:

| Symptom | Where the fix is |
|---|---|
| `dnx: command not found` | [.NET troubleshooting]({{< ref "assembly/net/mcp/troubleshooting.md" >}}#dnx-command-not-found) — `dnx` ships inside the .NET 10 SDK |
| `DllNotFoundException: libgdiplus` on Linux/macOS | [.NET troubleshooting]({{< ref "assembly/net/mcp/troubleshooting.md" >}}#dllnotfoundexception-libgdiplus) — install the native graphics libraries, or use the Docker image |
| "docker daemon not reachable" | [.NET troubleshooting]({{< ref "assembly/net/mcp/troubleshooting.md" >}}#docker-daemon-not-reachable) — start Docker Desktop or `dockerd` |

## The agent says a file does not exist

Pass the template's and the data file's **names inside the storage folder** — `contract-template.docx`, `data/release-4.2.0.json` — not full paths from your machine. When a name is not found the tool answers with the files it can see, so the agent can correct itself; check that list against [`GROUPDOCS_MCP_STORAGE_PATH`]({{< ref "assembly/net/mcp/configuration.md" >}}).

## Why does my template come out unchanged?

Because its placeholders are not Assembly tags. `{{name}}`, `${name}` and `[[name]]` are other engines' syntax and stay in the document as text; Assembly reads `<<[name]>>`. [`get_template_fields`]({{< ref "assembly/mcp/tools-reference/get-template-fields.md" >}}) reports *"The template contains 2 '{{…}}' placeholder(s). GroupDocs.Assembly does not process that syntax and leaves it as text; write <<[name]>> instead."*

## Why does generation fail with "Can not get the value of member"?

The template reads a field the data does not have — names are case-sensitive. The error names the field and the fix, for example *"The template reads 'Email', which the data does not have."* Add the field, or pass `allowMissingMembers: true` to print nothing for it. Details: [inspect and fix a template]({{< ref "assembly/mcp/use-cases/inspect-and-fix-a-template.md" >}}).

## Why is my date one day early?

A date-only JSON string such as `"2026-11-12"` is read as a date and shifted by the machine's UTC offset. Write `"2026-11-12T00:00:00"` and format it in the template — `<<[contract.Date]:"d MMMM yyyy">>`. The Docker image runs in UTC and is not affected.

## Does the model write the document?

No. The model writes **data** — a JSON object — and the template decides the layout, the wording around the values, the tables and the charts. That is the point: the document looks the same every time, and a reviewer can check the data instead of re-reading prose.

## Can a template read files or URLs?

Yes — `<<image>>` and `<<doc>>` tags load whatever path or URL their expression returns. Treat templates as **trusted input**, like code, and run the server with one mounted folder — see [on-premise deployment]({{< ref "assembly/mcp/use-cases/on-premise-document-generation.md" >}}).

## Can I use my existing GroupDocs.Assembly templates?

Yes. Templates built for the GroupDocs.Assembly library work unchanged; the server feeds them JSON, XML, CSV or table data instead of .NET objects. Templates that reach .NET types or methods not available on plain data may need a small rewrite.

## Verifying an installation end-to-end

Ask your agent *"list your GroupDocs assembly tools and the license status"* — it should name `get_template_fields`, `assemble_document`, `assemble_per_record`, `get_document_info`, `get_supported_formats`, `get_license_status`. For a scripted check that performs the real MCP handshake and a live call through the engine, see [verifying a .NET installation]({{< ref "assembly/net/mcp/troubleshooting.md" >}}#verifying-an-installation-end-to-end).

## Still stuck?

Post your config (redact license paths) and the client name in the [Assembly forum](https://forum.groupdocs.com/c/assembly/15). Bugs: [GitHub issues](https://github.com/groupdocs-assembly/GroupDocs.Assembly.Mcp/issues).
