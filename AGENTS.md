# GroupDocs.Assembly Docs - AGENTS.md

> Instructions for AI agents working with **GroupDocs.Assembly** documentation in this repository.

GroupDocs.Assembly is an on-premise SDK for document automation and report generation: it fills templates in Microsoft Office, OpenDocument, email, HTML, Markdown and text formats, documents with tags such as `<<[customer.Name]>>`, with data from objects, JSON, XML, CSV and document tables, and saves the reports in the template's format or another one, such as PDF.

**Supported formats (canon):** the per-platform tables below. Format lists differ between platforms, so do not quote one platform's list or count for another.

## Platforms in this docs tree

| Platform slug | Docs hub | Formats table |
|---|---|---|
| `net` | [net/_index.md](net/_index.md) | [net/getting-started/supported-document-formats.md](net/getting-started/supported-document-formats.md) |
| `java` | [java/_index.md](java/_index.md) | [java/getting-started/supported-document-formats.md](java/getting-started/supported-document-formats.md) |
| `nodejs-java` | [nodejs-java/_index.md](nodejs-java/_index.md) | [nodejs-java/getting-started/supported-document-formats.md](nodejs-java/getting-started/supported-document-formats.md) |
| `python-net` | [python-net/_index.md](python-net/_index.md) | [python-net/getting-started/supported-document-formats.md](python-net/getting-started/supported-document-formats.md) |

## .NET target frameworks (canon)

When documenting .NET install/runtime requirements, quote [net/getting-started/system-requirements.md](net/getting-started/system-requirements.md) and do not invent other TFMs. Since 26.6 the GroupDocs.Assembly NuGet package is a metapackage over builds for .NET Framework (4.0 Client Profile, 4.6.2), .NET Standard 2.0, .NET 6, .NET 8 and .NET 10.

The Python package (`groupdocs-assembly-net`) embeds its own .NET runtime, so Python readers install no .NET at all. Its requirements are on the python-net system requirements page.

## Product lines (do not confuse)

| Line | Where to send readers |
|---|---|
| **On-premise SDK** (this docs tree) | Platform hubs above; examples repos; NuGet / Maven / PyPI / npm packages |
| **GroupDocs Cloud** | Separate Cloud product docs/packages - do not mix install snippets |
| **Docs MCP** | Link only: [https://docs.groupdocs.com/mcp](https://docs.groupdocs.com/mcp) - do not edit MCP repos from this surface |

## Editing conventions

- The public URL of a page comes from its `url:` front matter, not from its file path. Keep `url:` unchanged when you move or rename a file.
- `{{< ref "..." >}}` resolves content paths: after moving a file, update every `ref` that points to it.
- Redirects are Hugo `aliases:` front matter on the destination page.
- Menu titles (`title:`, `linkTitle:`) are plain text: no emoji.
- Template text on a page (`<<foreach [o in orders]>>...`) is the same on every platform; only the code around it differs.
- Code examples on a page have runnable counterparts in the platform's examples repository; keep the two in sync.
- python-net: `_sample_files/` comes from GroupDocs.Assembly-SampleFiles (`sync.ps1`) and `_output_files/` from docs-to-code-examples (`generate_outputs.py`); do not edit either by hand.
