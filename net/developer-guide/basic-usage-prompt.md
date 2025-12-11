You are an expert in SDK technical documentation, information architecture, SEO, and developer onboarding for .NET libraries.  
Your task is to:

1. Design a **new, extended “Basic Usage” documentation structure** for **GroupDocs.Assembly for .NET**.  
2. **Generate one Markdown article file per Basic Usage topic**, using the provided topic template.  
3. Optimize each article for **best documentation practice and SEO** (developer-focused, task-based, keyword-aware).

The documentation is authored in **Markdown (HUGO content)**.

***

## Input documentation and references

Use these as primary inputs for understanding product capabilities, API surface, and existing content:

- GroupDocs.Assembly for .NET docs root:  
  https://docs.groupdocs.com/assembly/net/[3]
- Basic Usage (current):  
  https://docs.groupdocs.com/assembly/net/basic-usage/[4]
- Introducing GroupDocs.Assembly for .NET:  
  https://docs.groupdocs.com/assembly/net/introducing-groupdocs-assembly-for-net/[5]
- GroupDocs.Assembly for .NET examples (GitHub):  
  https://github.com/groupdocs-assembly/GroupDocs.Assembly-for-.NET[6]
- GroupDocs.Assembly for Java (for inspiration of structure and topic coverage only):  
  https://docs.groupdocs.com/assembly/java/[7]
- GroupDocs.Signature for .NET Basic Usage (target style & granularity):  
  https://docs.groupdocs.com/signature/net/basic-usage/[8]
- API reference root for cross-linking:  
  https://reference.groupdocs.com/assembly/net/[1]

You must follow the **style and approach** of the earlier `docs-promts.md` analysis prompt, but adapt it entirely to the **“Basic Usage topics + per-topic files”** perspective.[9]

***

## Overall goal

Create a **complete, fine‑grained Basic Usage section** for GroupDocs.Assembly for .NET that:

1. Covers all **core operations and simple scenarios** a typical developer needs in the first 1–3 days.[4][5]
2. Exposes **all important capabilities as small, focused topics**, each in its own Basic Usage Markdown file (one topic = one file).[6][8]
3. Uses **task-based, SEO‑friendly titles and headings** (e.g., “Generate DOCX from JSON data in C#”).  
4. Demonstrates **data sources, template syntax, and output formats** with concise, runnable C# examples (no copied text, all wording must be original).[5][4][6]
5. Clearly separates **Basic Usage** (simple, single‑feature flows) from Advanced Usage (complex templates, custom engines, performance tuning).

***

## Your role

Act as:

- Information architect for developer documentation.  
- .NET SDK technical writer experienced in templating/reporting APIs.  
- SEO-oriented content designer for developer audiences.

You must:

- Infer all **fundamental and frequently used operations** from existing docs, examples, and product description.[4][5][6]
- Mirror the **per-operation, per-type topic model** seen in GroupDocs.Signature Basic Usage for GroupDocs.Assembly concepts.[8]
- Use **task-based “how to” naming** and integrate keywords such as `assemble`, `generate`, `compose`, `create`, `build`, `collect` naturally in titles, descriptions, and body.

***

## Constraints and style principles

- Audience: C#/.NET developers with basic understanding of streams, file paths, and classes.  
- Do **not** copy any sentences from the existing docs; always paraphrase in your own words.  
- Basic Usage = one main scenario, simple template, simple data source, common output formats, minimal configuration.[5][4]
- Each topic must be **small, self‑contained, and runnable** in under ~10–20 minutes.  
- Write in clear, direct language; avoid marketing fluff.  
- Follow **good SEO practice**:
  - Use **descriptive H1/H2 headings** that include keywords like “C#”, “.NET”, “assemble document”, “generate report”, “compose template”.  
  - Naturally repeat main keywords 2–4 times in the article (title, first paragraph, one subheading, body).  
  - Use synonyms to avoid keyword stuffing (assemble, generate, compose, build, create).  
  - Make code examples copy‑paste‑ready and properly fenced.  

***

## Task 1 – Design the Basic Usage topic list

Design a **hierarchical Basic Usage structure** (table of contents) that will map to **one Markdown file per topic**.

At minimum, include sections and topics for:

1. **Getting started basics**  
   - Install via NuGet and apply license.  
   - First “generate a simple document from in-memory object” scenario.[10][11]

2. **Working with templates**  
   - Load templates from file path and stream.  
   - Supported template formats and basic notes (DOCX, XLSX, PPTX, etc.).[6][5]
   - Minimal template syntax usage (fields, simple expressions).  

3. **Data sources – Basic scenarios**  
   For each data source type, define a **separate Basic Usage topic** (and therefore a separate file) with:  
   - Short conceptual explanation.  
   - Simple flow: data source → template → output document.

   Required data source topics (each one = its own topic/file):[5][6]
   - Generate document from **custom .NET objects**.  
   - Generate document from **XML data source**.  
   - Generate document from **JSON data source**.  
   - Generate document from **database (ADO.NET / ORM)**.  
   - Generate document from **OData**.  
   - Generate document using **external documents / Word tables / spreadsheets** as a data source.[6]

   In titles and copy, use synonyms like `generate`, `compose`, `create`, not only `assemble`.

4. **Core output operations**  
   - Generate and save output in the **same format as template**.  
   - Generate and save output in **another format** (e.g. DOCX → PDF, DOCX → HTML).[5][6]
   - Work with **streams vs file paths**.

5. **Basic content generation patterns**  
   Separate topics (one topic = one file) for each frequent pattern:  
   - Generate **tables** from a collection.  
   - Generate **bullet lists** from a data source.  
   - Generate **numbered lists** from a data source.  
   - Generate **master–detail (parent–child) reports** (e.g., order with order items).  
   - Generate **charts** from data.  
   - Generate **images** dynamically (file path, URL, binary data).  
   - Insert **hyperlinks** dynamically.[12][6]

6. **Formatting and simple calculations**  
   - Apply **numeric, date/time, and text formatting** in templates.[12][6]
   - Add **conditional content** (if/else).  
   - Use **simple aggregates** (sum, count, average).  
   - Use **basic formulas** in spreadsheet templates.[6]

7. **Barcodes and special elements**  
   - Generate **barcodes** in documents.  
   - Generate **QR codes** (if supported) and/or describe how barcode-like elements are handled.  
   - Use Word template features like **NEXT‑like behavior** for repeating documents.[12][6]

8. **Email and message generation basics**  
   - Generate **email messages** (subject, body, recipients) from data.  
   - Attach files and configure basic message properties.[12][6]

9. **Error handling and diagnostics (basic)**  
   - Handle common template/data errors.  
   - Log and inspect generation results.

10. **Performance-friendly basic patterns**  
   - Basic advice for moderately large data (streaming, simple batching).

**Deliverable for Task 1**:  
A Markdown bullet list (with nested bullets) of all Basic Usage topics, where each leaf node represents **one future Markdown file**. Add a **1–2 sentence description** of the goal of each topic.

***

## Task 2 – Per-topic metadata and file mapping

For **each topic** from Task 1, define the metadata needed to fill the front-matter of `basic-usage-template.md` and to guide content generation.

For every topic, specify:

- **File id** – a unique id string (e.g., `assembly-basic-usage-json-datasource`).  
- **File URL segment** – slug part to replace `{REPLACE-WITH-TOPICS-URL}` (e.g., `basic-usage-json-data-source`).  
- **Title** – SEO-friendly, task-based (e.g., “Generate DOCX report from JSON data in C#”).  
- **Weight** – integer value to order topics from simplest to more complex.  
- **Description** – short, keyword-rich description (~20–30 words, original text).  
- **Keywords** – at least 4–6 relevant keywords and phrases including variations on `assemble`, `generate`, `compose`, `build`, plus data source / format / C# terms.  
- **Parent section** – e.g., “Data sources basics”, “Content patterns basics”.

**Deliverable for Task 2**:  
A Markdown table with columns:

- Topic id  
- File URL segment  
- Title  
- Parent section  
- Weight  
- Description  
- Keywords  

***

## Task 3 – Per-topic content planning (for template)

For **each topic**, define how the `basic-usage-template.md` should be filled.

Use the attached template file structure (front matter + Overview + examples + alerts + more resources).[1]

For each topic, specify:

- **Overview content plan**:
  - 2–3 sentences that explain what the topic does, which scenarios it supports, and which main classes/namespaces are involved.  
  - Links to relevant API reference pages (e.g., `DocumentAssembler`, `DataSourceInfo`, etc.) using the reference root.[1]
- **Step list**:
  - 4–7 bullet points describing the steps a developer must take (e.g., “Create data source object”, “Load template file”, “Call DocumentAssembler.AssembleDocument”, “Save result to stream”).  
- **Code examples**:
  - Number of code snippets and their focus (e.g., “main example with file paths”, “variant using streams”, “variant showing another output format”).  
  - Make sure examples are short, focused, and runnable, but you do **not** need to provide full final code in this planning step.  
- **Alerts / info boxes**:
  - Important notes to highlight via `{{< alert style="info" >}}...{{< /alert >}}`, such as disposal of streams, template limitations, or best practices.  
- **Links to advanced usage**:
  - One bullet directing to the relevant advanced usage section or developer guide when a user needs more complex scenarios.  
- **GitHub / online apps**:
  - Which example repositories or apps should be linked in “More resources” section (e.g., .NET, Java, Python via .NET examples, or online apps).[1]

**Deliverable for Task 3**:  
Extend the Markdown table from Task 2 (or provide a second table) adding columns:

- Primary scenario (1–2 sentences)  
- Pre-requisites  
- Examples required (short description)  
- Key API types to reference  
- Notes for alerts / gotchas  

***

## Task 4 – Topic priority for implementation

Not all topics will be implemented at once. For each topic:

- Assign **Priority**:
  - **P1** – must-have for initial Basic Usage release.  
  - **P2** – should-have, adds value but not critical for day-one.  
  - **P3** – nice-to-have, can be added later.  
- Base the priority on:
  - Frequency and importance of scenario in real projects.  
  - Onboarding impact (how quickly it helps users get results).  
  - Coverage of major data sources and formats.[5][6]

**Deliverable for Task 4**:  
Add a **Priority (P1/P2/P3)** column to the per-topic table.

***

## Task 5 – Generate final Markdown files per topic

Using the **basic-usage-template.md** as a structural pattern, **generate the full Markdown content for selected topics**.

1. Start with all **P1 topics**.  
2. For each P1 topic, produce a complete Markdown file that:
   - Replaces front-matter placeholders:
     - `id`  
     - `url`  
     - `title`  
     - `weight`  
     - `description`  
     - `keywords`  
   - Fills **Overview** with topic-specific explanation and SEO keywords.  
   - Lists the **step-by-step procedure** using bullet points.  
   - Provides **at least one C# example** (` ```csharp ` fenced) implementing the core scenario in a concise way (no duplicated text from existing docs).  
   - Optionally adds a **second example** when it significantly improves clarity (e.g., stream vs file path).  
   - Uses **alert blocks** for important notes (disposal of streams, template restrictions, etc.).  
   - Ends with:
     - “Advanced Usage” link (HUGO `ref` to corresponding folder).  
     - “More resources” section with GitHub examples and online app links as in the template, adjusted to Assembly.[attached_file:21]  

3. Output each topic’s Markdown file **as a separate section** in your response, clearly separated by a heading, so it can be copied into an individual `.md` file later.

**Deliverable for Task 5**:  
- Completed Markdown content for all P1 topics, each ready to be saved as a separate `.md` file based on `basic-usage-template.md`.

---

## Final output structure for this prompt

When you run this prompt, produce:

1. **Section A – Basic Usage topic list (TOC)** – from Task 1.  
2. **Section B – Per-topic metadata and planning tables** – from Tasks 2–4.  
3. **Section C – Ready-to-use Markdown files for all P1 topics** – from Task 5, one after another, using the template structure.

The result must be detailed enough that a documentation writer can:

- Directly create the folder and file structure for Basic Usage.  
- Paste each generated Markdown file content into Hugo.  
- Confidently extend the same pattern for P2/P3 topics later.

[1](https://ppl-ai-file-upload.s3.amazonaws.com/web/direct-files/attachments/116161834/e0192354-615e-467a-9f27-a83cf91121fa/basic-usage-template.md)
[2](https://ppl-ai-file-upload.s3.amazonaws.com/web/direct-files/attachments/116161834/bce3560e-a181-4fd9-875a-44c6988e2fcf/basic-usage-prompts.md)
[3](https://www.componentsource.com/product/groupdocs-assembly-for-net)
[4](https://github.com/groupdocs-assembly/GroupDocs.Assembly-for-.NET)
[5](https://www.nuget.org/packages/GroupDocs.Assembly/3.3.0)
[6](https://docs.groupdocs.com/assembly/net/introducing-groupdocs-assembly-for-net/)
[7](https://docs.groupdocs.com/assembly/net/working-with-json-data-sources/)
[8](https://docs.groupdocs.com/assembly/net/barcode-image-generation-in-word-processing-document/)
[9](https://docs.groupdocs.com/assembly/net/basic-usage/)
[10](https://products.groupdocs.com/assembly/net/barcode/pdf/)
[11](https://marketplace.visualstudio.com/items?itemName=GroupDocs.GroupDocsAssembly)
[12](https://docs.groupdocs.com/assembly/net/product-overview/)