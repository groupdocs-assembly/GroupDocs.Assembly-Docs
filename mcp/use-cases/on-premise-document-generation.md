---
id: mcp-uc-on-premise-document-generation
url: assembly/mcp/use-cases/on-premise-document-generation
title: "Running GroupDocs MCP servers on-premise: architecture and security model"
linkTitle: On-premise deployment
weight: 7
description: "Run document generation for AI agents fully on-premise with the GroupDocs.Assembly MCP server: local stdio, no inbound ports, no telemetry, templates as trusted input."
keywords: on-premise MCP server, self-hosted document generation, MCP security model, air-gapped template engine, local document generation AI
productName: GroupDocs.Assembly MCP Server
toc: True
structuredData:
    showOrganization: True
    howTo:
        name: "Running GroupDocs MCP servers on-premise: architecture and security model"
        description: "Run document generation for AI agents fully on-premise with the GroupDocs.Assembly MCP server: local stdio, no inbound ports, no telemetry, templates as trusted input."
        steps:
        - name: "Run the pinned image inside the perimeter"
          text: "Start the GroupDocs.Assembly MCP server from its versioned Docker image as a child process of the AI client."
        - name: "Mount only the folders the agent may reach"
          text: "Map the document folder read-write and the license folder read-only."
        - name: "Choose the license mode"
          text: "Use a license file for fully offline operation; metered licensing needs outbound egress for usage reports."
---

Run document generation for AI agents **fully on-premise**: the GroupDocs.Assembly MCP server uses local stdio transport with **no inbound ports and no telemetry**, and reads templates and data from folders you choose, locally. It reaches the network only for metered licensing and for URLs a template asks for — both of which you can switch off. This page is the one to send your security reviewer.

{{< alert style="info" >}}
The commands and config snippets on this page are for the **.NET** build of the server — the only platform available today. Installation and client setup: [MCP server for .NET]({{< ref "assembly/net/mcp/_index.md" >}}). Other platforms will expose the same tools with their own launch command; everything else on this page applies unchanged.
{{< /alert >}}

## The architecture in one picture

```text
+--------------+          +--------------------+         +------------------+
|  AI client   |  stdio   | MCP server process | reads / | local filesystem |
| (Claude, VS  | <----->  | (GroupDocs engine) | <-----> | storage / output |
| Code, agent) | JSON-RPC |   child process    |  writes |     folders      |
+--------------+          +--------------------+         +------------------+
```

* **Transport:** the AI client *starts the server as a child process* and communicates over standard input/output. The server never listens on a network socket.
* **Data path:** agent → local server → local filesystem. Templates and data files are read from the storage folder; generated documents are written there (or to `GROUPDOCS_MCP_OUTPUT_PATH`).
* **Network use:** getting the server — ghcr.io/docker.io once per image, while `dnx` without a pinned version (`GroupDocs.Assembly.Mcp@<version>`) checks nuget.org for the latest release **every time it starts the server**; at runtime only if metered licensing is enabled — or if a **template** asks for a URL (below).
* **Telemetry:** none. The engine runs in-process.

## Templates are trusted input

A template is closer to code than to a document. `<<image [expr]>>` and `<<doc [expr]>>` tags load **whatever path or URL their expression returns** — from the data, or written into the template. A template from an untrusted source could read a file the server can reach, or make a request to an internal address.

* **Run with one mounted folder.** In Docker the container sees `/data` and nothing else; that is the boundary.
* **Review templates like code** — they live in a repository, changes go through review.
* **Data is printed, not executed.** JSON, XML and CSV values cannot run code — but when a template's image or document tag takes its path from the data, the data chooses what is loaded. Keep such tags pointing at fixed folders.

## A tighter deployment

```bash
docker run --rm -i --user "$(id -u):$(id -g)" \
  -v /srv/templates:/data \
  -v /srv/licenses:/license:ro \
  -e GROUPDOCS_MCP_STORAGE_PATH=/data \
  -e GROUPDOCS_LICENSE_PATH=/license/GroupDocs.Assembly.lic \
  --network none \
  ghcr.io/groupdocs-assembly/assembly-net-mcp:26.11.0
```

* Pin the tag (`:26.11.0`, not `:latest`).
* `--network none` makes URL-loading tags fail instead of fetching — and rules out metered licensing, so use a license file.
* License read-only; the image runs in UTC (dates in data are not shifted).
* `--user` is for Linux: the image runs as a non-root user (uid 1654), and the generated documents must be written into a folder you own. In a JSON client config write the numbers (`"--user", "1000:1000"`, from `id -u` and `id -g`) — clients run no shell.

## The part that still travels

The **data** usually starts in the conversation: the agent extracts it from your message, or reads it from a file and passes it as `dataJson`. With a cloud-hosted model, those values have reached your model provider; the generated document has not. To keep values off the conversation entirely, pass a data **file** (`data: { "filePath": "orders.json" }`) — the agent then handles only names.

## License management

* **License file** — read from local disk by the local process. Fully offline; the right answer for air-gapped deployments.
* **Metered (pay-per-use)** — reports *usage* to GroupDocs servers, so it needs outbound egress. Document content is never part of that report.

Both: [Licensing]({{< ref "assembly/mcp/getting-started/licensing.md" >}}).

## What this fits — honestly

**A good fit:** contracts, letters, certificates and reports generated from approved templates, inside a network that does not allow uploads; generation steps for coding agents in a repository.

**Not what this is:** a shared service or a sandbox for untrusted templates. One stdio server, one client, one machine; templates are trusted.

## FAQ

**Does any document content leave the machine?** Not from the server, unless a template's tag names a URL. Values the agent writes into `dataJson` are in the conversation with your model provider.

**Does it need internet at runtime?** No — unless metered licensing is on, or a template loads a URL. Unpinned `dnx` also checks nuget.org at each start: pin the version and keep the package cached.

**Can I run it air-gapped?** Yes: pre-pull the image or pre-cache the package, use a license file, pin the version, `--network none`.

**What ports does it open?** None. stdio only.

**How do I prove that?** The [verification script]({{< ref "assembly/net/mcp/troubleshooting.md" >}}#verifying-an-installation-end-to-end) performs a real handshake and a real engine call so you can watch exactly what happens.

## Read more

* [3 architectures for AI document processing, and the one that keeps files inside your network](https://blog.groupdocs.com/total/on-premise-ai-document-processing-mcp/) — the same scenario on the GroupDocs blog, with worked examples and the trade-offs.

