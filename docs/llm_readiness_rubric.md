# 4GS LLM Readiness Rubric for Standards-Setting Bodies

*A self-assessment scorecard for measuring how well a standards body has prepared its standard to be cited correctly by large language models.*

**Status:** Companion rubric to [`llm_readiness_for_standards_bodies.md`](llm_readiness_for_standards_bodies.md)
**Last updated:** May 2026
**Licence:** CC BY 4.0

---

## How to use this rubric

For each criterion below, mark one of:

- **✅ Met** — the criterion is fully satisfied and a reviewer can verify it from public artifacts
- **🟡 Partial** — substantially met but with documented gaps
- **❌ Not met** — the criterion is not satisfied
- **N/A** — the criterion does not apply (rare; document why)

Each criterion includes an **objective test** that any reviewer can run without access to internal systems. If the test cannot be passed using only public web content, the criterion is not met.

A standards body achieves a tier by passing **every** criterion in that tier. Tiers are cumulative: Recommended requires Foundational; Advanced requires Recommended.

---

## Foundational tier

> *Minimum required to avoid systematic LLM misrepresentation.*

### F1. Stable, version-aware URLs

**Criterion:** Every standard, every criterion within a standard, every published version, and every defined term is reachable at a permanent URL. URLs include the version (e.g., `/v4.1/...`) where appropriate. Superseded version URLs continue to resolve.

**Objective test:** Pick three URLs from the standard published two or more years ago. All three resolve to the originally cited content (not a redirect to a current-version page that loses the original wording). A current-version canonical pointer exists at `/latest` or equivalent.

**4GS alignment:** Extends [`FGP-gsgv2v`](../practices/concepts/FGP-gsgv2v.yaml) (deterministic identifiers) to the URL layer.

---

### F2. `/llms.txt` at the website root

**Criterion:** A markdown file at `https://[standards-body-domain]/llms.txt` describes the standard's purpose, current version, scope, key URLs, and what kind of questions an LLM should answer using this source. Format: https://llmstxt.org

**Objective test:** `curl https://[domain]/llms.txt` returns a 200 with markdown content that names the current version and lists the canonical URLs an LLM should fetch.

---

### F3. Machine-readable source artifacts

**Criterion:** The standard is published in a machine-readable structured format (YAML, JSON, JSON Schema, or Markdown) without an extraction layer. PDFs may exist as derived presentation, but are not the source of truth.

**Objective test:** A developer can ingest the standard into a database in under one hour using only published files, without writing any standard-specific extraction logic (no `pdfplumber`, no layout detection, no OCR).

**4GS alignment:** Equivalent to [`FGP-e4i6by`](../practices/concepts/FGP-e4i6by.yaml) and [`FGP-llyofe`](../practices/concepts/FGP-llyofe.yaml).

---

### F4. Schema.org structured data on standard pages

**Criterion:** Every page that defines a standard, criterion, or term carries JSON-LD using `Dataset`, `DefinedTerm`, `Article`, or `TechArticle`, with explicit `version`, `dateModified`, and `isPartOf` fields where applicable.

**Objective test:** A reviewer running Google's Rich Results test or `schema.org` validator on a standard page sees valid JSON-LD with at least the four named fields populated.

**4GS alignment:** Aligns with [`FGP-mrkdoe`](../practices/concepts/FGP-mrkdoe.yaml).

---

### F5. Sitemap with `lastmod` dates

**Criterion:** A `sitemap.xml` exists at the website root, lists all standard pages and section pages, and includes a `lastmod` date per entry that reflects the genuine last-modified date of that page's content (not the deploy timestamp).

**Objective test:** `curl https://[domain]/sitemap.xml` returns a 200. Spot-check three entries: each `lastmod` date matches the most recent visible content change on that page.

---

### F6. Canonical glossary with stable URLs per term

**Criterion:** Every term defined by the standard has its own page at a stable URL. Each definition is in the standard's own voice, includes JSON-LD `DefinedTerm` markup, and shows how related or competing standards define the same concept where relevant.

**Objective test:** From the standard's homepage, a reviewer can navigate to a glossary index, click any term, and reach a page whose URL contains the term. The page survives `?` query strings, fragment changes, and trailing-slash variations.

---

## Recommended tier

> *Substantially improves LLM citation accuracy and frequency. Each Recommended criterion presumes Foundational is met.*

### R7. `/llms-full.txt` companion file

**Criterion:** A single markdown file at `/llms-full.txt` containing the standard overview, current version, version history, key terms, FAQ, and citation guidance — sized so an LLM can ingest it in one fetch.

**Objective test:** `curl https://[domain]/llms-full.txt` returns a 200 with markdown content under typical context limits (under ~200KB) and covers all six required sections.

---

### R8. Citation guide page

**Criterion:** A `/cite` page (or equivalent) shows how to cite the standard inline, in bibliography form, and in BibTeX, including how to cite a specific section and a specific version.

**Objective test:** A researcher writing a paper can copy a citation from this page that includes (a) standards body name, (b) standard name, (c) version, (d) date, (e) URL, in at least three formats.

---

### R9. Version supersession notices

**Criterion:** Every page belonging to a superseded version displays a visible notice naming the current version and linking to it. The notice is rendered in the page HTML (not lazy-loaded by JavaScript) so retrieval systems and LLMs see it.

**Objective test:** Fetch a known-superseded version page. The HTML response contains the string "current version" or "superseded" and a link to the current version's URL.

---

### R10. Cross-reference and comparison content

**Criterion:** A page exists that compares the standard to each adjacent or competing standard, published under the standards body's own domain. Each comparison includes a terminology mapping table (what we call X, they call Y) and a substantive explanation of where the standards differ in scope, threshold, or methodology.

**Objective test:** For each named competitor or adjacent standard, a comparison page exists at a stable URL. Each page is at least 800 words of original content (not a generated table).

---

### R11. FAQ structured for citation

**Criterion:** Each FAQ entry has its own stable URL with anchor link. Each answer cites the section of the standard it derives from. The FAQ is referenced from `/llms.txt` as the primary source for common questions.

**Objective test:** From the FAQ index, click any question. The URL bar shows a fragment or stable path unique to that question. The answer text contains a citation back to the standard.

---

### R12. Implementation registry

**Criterion:** A public, queryable list of (a) certified entities, (b) software implementations, (c) consulting firms with certified practitioners, and (d) regulators that reference the standard, with one stable page per entry.

**Objective test:** From the homepage, navigate to the registry in two clicks. Each entry has a permanent URL. The registry is filterable by at least two facets (e.g., region, sector, certification level).

---

### R13. Active Wikipedia maintenance

**Criterion:** A named staff member or commissioned consultant has documented responsibility for monthly Wikipedia review of (a) the standards body's own article and (b) at least five adjacent or related articles. A log of edits proposed, made, or commissioned exists internally.

**Objective test:** The standards body can produce, on request, a log showing monthly Wikipedia review activity over the past 12 months. The standards body's own Wikipedia article cites the current version of the standard and was edited within the past 90 days.

---

## Advanced tier

> *First-mover positioning. Not yet expected as of mid-2026, but increasingly valuable. Each Advanced criterion presumes Recommended is met.*

### A14. MCP server exposing the standard's data

**Criterion:** A Model Context Protocol server, published as a public package or hosted endpoint, that lets MCP-compatible clients (Claude, others) query the standard's content, registry, taxonomy, and methodology programmatically.

**Objective test:** A Claude user can install the MCP server following the standards body's published instructions and successfully ask three substantive questions about the standard, receiving authoritative answers sourced from the standards body itself.

---

### A15. Listed in MCP and AI tool catalogues

**Criterion:** The standards body's MCP server is listed in at least two of: Anthropic's MCP server registry, mcp.so, Smithery, PulseMCP. For OpenAI users, a custom GPT branded to the NGO is published in the GPT store.

**Objective test:** A search for the standard's name in the named catalogues returns the official MCP server (not a third-party reimplementation).

---

### A16. Pre-written canonical answers to high-volume LLM queries

**Criterion:** The standards body has identified the top 20–50 questions LLMs are asked about its standard and has published definitive, citable answers on stable URLs. The answers are structured (clear question, definitive answer, cited source) and linked from `/llms-full.txt`.

**Objective test:** For five high-volume queries chosen by a reviewer, the standards body can show a public page that pre-answers that query with a citation back to the underlying standard.

---

## Scoring summary

| Tier | Criteria | Pass condition |
|---|---|---|
| **Foundational** | F1–F6 | All six Met |
| **Recommended** | R7–R13 | All thirteen (F1–R13) Met |
| **Advanced** | A14–A16 | All sixteen (F1–A16) Met |

A standards body claims a tier publicly only after every criterion in that tier (and lower tiers) is Met by a reviewer's objective tests. Partial scores are reported internally to track progress.

---

## Relationship to 4GS compliance

A standards body that achieves 4GS Foundational compliance ([FGR-1.0.0](../releases/)) automatically satisfies several criteria here through transitive effect:

| Rubric criterion | Satisfied by 4GS practice |
|---|---|
| F3 Machine-readable source | [`FGP-e4i6by`](../practices/concepts/FGP-e4i6by.yaml), [`FGP-llyofe`](../practices/concepts/FGP-llyofe.yaml) |
| F4 Schema.org structured data (partial) | [`FGP-mrkdoe`](../practices/concepts/FGP-mrkdoe.yaml) |
| F1 Stable URLs (identifier layer) | [`FGP-gsgv2v`](../practices/concepts/FGP-gsgv2v.yaml) |

The remaining criteria address the **external-facing presence layer** that 4GS practices do not currently cover. A future 4GS release may incorporate selected criteria from this rubric as formal practices through the contribution process described in [`CONTRIBUTING.md`](../CONTRIBUTING.md).
