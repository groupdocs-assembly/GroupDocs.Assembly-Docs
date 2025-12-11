# Complete Basic Usage Documentation Structure

This document provides the complete structure, metadata tables, and implementation guide for all Basic Usage topics for GroupDocs.Assembly for .NET.

## Section A – Complete Topic List (TOC)

See the comprehensive topic list in `basic-usage-structure-and-content.md` for the full hierarchical structure.

## Section B – Complete Metadata Table

The complete metadata table with all topics (P1, P2, P3) is provided in `basic-usage-structure-and-content.md`.

## Section C – Implementation Status

### P1 Topics - Implementation Status

| Topic ID | File Name | Status | Notes |
|----------|-----------|--------|-------|
| assembly-basic-usage-install-license | `install-and-apply-license.md` | ✅ Complete | Ready to use |
| assembly-basic-usage-first-document | `generate-first-document.md` | ✅ Complete | Ready to use |
| assembly-basic-usage-load-template | `load-template-from-file-or-stream.md` | ✅ Complete | Ready to use |
| assembly-basic-usage-template-syntax-basics | `basic-template-syntax.md` | ✅ Complete | Ready to use |
| assembly-basic-usage-custom-objects | `generate-from-custom-objects.md` | ✅ Complete | Ready to use |
| assembly-basic-usage-xml-datasource | `generate-from-xml-datasource.md` | ✅ Complete | Ready to use |
| assembly-basic-usage-json-datasource | `generate-from-json-datasource.md` | ✅ Complete | Ready to use |
| assembly-basic-usage-database-datasource | `generate-from-database.md` | ✅ Complete | Ready to use |
| assembly-basic-usage-same-format-output | `same-format-output.md` | ✅ Complete | Ready to use |
| assembly-basic-usage-different-format-output | `different-format-output.md` | ✅ Complete | Ready to use |
| assembly-basic-usage-streams-vs-files | `streams-vs-file-paths.md` | ✅ Complete | Ready to use |
| assembly-basic-usage-generate-tables | `generate-tables-from-collection.md` | ✅ Complete | Ready to use |
| assembly-basic-usage-generate-bullet-lists | `generate-bullet-lists.md` | ✅ Complete | Ready to use |
| assembly-basic-usage-generate-numbered-lists | `generate-numbered-lists.md` | ✅ Complete | Ready to use |
| assembly-basic-usage-master-detail | `generate-master-detail-reports.md` | ✅ Complete | Ready to use |
| assembly-basic-usage-generate-images | `insert-images-dynamically.md` | ✅ Complete | Ready to use |
| assembly-basic-usage-insert-hyperlinks | `insert-hyperlinks-dynamically.md` | ✅ Complete | Ready to use |
| assembly-basic-usage-formatting | `apply-formatting.md` | ✅ Complete | Ready to use |
| assembly-basic-usage-conditional-content | `conditional-content.md` | ✅ Complete | Ready to use |
| assembly-basic-usage-aggregates | `use-aggregates.md` | ✅ Complete | Ready to use |
| assembly-basic-usage-generate-emails | `generate-email-messages.md` | ✅ Complete | Ready to use |
| assembly-basic-usage-error-handling | `error-handling.md` | ✅ Complete | Ready to use |

## Pattern for Creating Remaining Topics

All remaining P1 topics should follow this pattern:

1. **Front Matter**: Use the exact format from the metadata table
2. **Overview Section**: 
   - Explain what the topic does
   - List main classes with API reference links
   - Provide step-by-step bullet list
3. **Code Examples**: 
   - At least one complete, runnable C# example
   - Optional second example showing variations
   - Use proper code fencing with `csharp` language
4. **Alerts**: Use `{{< alert >}}` blocks for important notes
5. **Advanced Usage Link**: Reference to advanced usage section
6. **More Resources**: GitHub examples and online apps links

## Quick Reference: Template Structure

```markdown
---
id: {topic-id}
url: assembly/net/{url-segment}
title: {Title}
weight: {weight}
description: "{Description}"
keywords: {keywords}
productName: GroupDocs.Assembly for .NET
toc: True
---

## Overview

{2-3 sentences explaining the topic}

The main classes involved are:
- [ClassName](https://reference.groupdocs.com/assembly/net/...) - description

Here are the steps to {action}:

* Step 1
* Step 2
* Step 3

{{< alert style="info" >}}
Important note here
{{< /alert >}}

## {Main Section Title}

{Description of the example}

```csharp
{Complete, runnable C# code}
```

## {Optional Second Example}

{Description}

```csharp
{Code}
```

{{< alert style="warning" >}}
Warning or important note
{{< /alert >}}

### Advanced Usage Topics

To learn more about {related topics}, please refer to the [advanced usage section]({{< ref "assembly/net/developer-guide/advanced-usage/_index.md" >}}).

## More resources

### GitHub Examples

You may easily run the code above and see the feature in action in our GitHub examples:

* [GroupDocs.Assembly for .NET examples, plugins, and showcase](https://github.com/groupdocs-assembly/GroupDocs.Assembly-for-.NET)
* [GroupDocs.Assembly for Java examples, plugins, and showcase](https://github.com/groupdocs-assembly/GroupDocs.Assembly-for-Java)
* [GroupDocs.Assembly for Python via .NET examples, plugins, and showcase](https://github.com/groupdocs-assembly/GroupDocs.Assembly-for-Python-via-.NET)

### Free Online Apps

Along with the full-featured .NET library, we provide simple but powerful free online apps.

To assemble documents from templates and data sources, you can use the online apps from the **[GroupDocs.Assembly App Product Family](https://products.groupdocs.app/assembly/family)**.
```

## Next Steps

1. Review the completed files to understand the pattern
2. Use the metadata table in `basic-usage-structure-and-content.md` for topic details
3. Create remaining P1 topic files following the established pattern
4. Test each file for proper Hugo rendering
5. Create P2 and P3 topics after P1 topics are complete

