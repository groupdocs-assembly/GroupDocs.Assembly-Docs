---
id: mcp-use-cases
url: assembly/mcp/use-cases
title: Use cases
weight: 3
description: "Step-by-step scenarios for generating documents with AI agents over MCP: contracts from a template, mail merge, reports with tables and charts, fixing templates, documents from agent-extracted data, and reports from repository data."
keywords: MCP document generation use cases, generate documents with AI examples, mail merge Claude, report from CSV AI agent, template automation scenarios
productName: GroupDocs.Assembly MCP Server
hideChildren: True
toc: False
---

Step-by-step scenarios for generating documents from templates with AI agents over MCP — each page answers one real question completely, with the setup, the calls the agent makes, the results it gets back (captured from the server), and the exact prompt:

* [How to generate documents from templates with AI agents using MCP]({{< ref "assembly/mcp/use-cases/generate-documents-with-ai-agents.md" >}}) — start here: ask the template what it needs, fill the skeleton, render — and the template syntax that matters.
* [How to generate one document per record (mail merge) with an AI agent]({{< ref "assembly/mcp/use-cases/one-document-per-record-mail-merge.md" >}}) — a letter per customer, a certificate per attendee: files named by a field, failed records listed.
* [How to build a report with tables and charts from a CSV or spreadsheet with an AI agent]({{< ref "assembly/mcp/use-cases/reports-with-tables-and-charts-from-data-files.md" >}}) — a spreadsheet or CSV in, a Word, PDF or PowerPoint report out — tables, totals and charts from the template.
* [How to find out what a template needs and why it failed]({{< ref "assembly/mcp/use-cases/inspect-and-fix-a-template.md" >}}) — the JSON skeleton, the {{name}} trap, unclosed blocks, missing fields, inline errors and binary templates.
* [How to turn notes or an email into a finished document with an AI agent]({{< ref "assembly/mcp/use-cases/build-a-document-from-data-the-agent-extracted.md" >}}) — the agent extracts the facts, the template makes the document — and a missing field stops the run.
* [How to generate a PDF or Word report from JSON data in a repository with Claude Code]({{< ref "assembly/mcp/use-cases/generate-reports-from-repository-data.md" >}}) — release notes and certificates from data/*.json and versioned templates — with Claude Code or any coding agent.
* [Running GroupDocs MCP servers on-premise: architecture and security model]({{< ref "assembly/mcp/use-cases/on-premise-document-generation.md" >}}) — architecture and security model — what stays local, and what a template can reach.

New to the server? [Quick start]({{< ref "assembly/mcp/getting-started/_index.md" >}}) first.
