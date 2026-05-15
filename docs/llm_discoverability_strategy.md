# LLM Discoverability Strategy for a Standards-Setting NGO

*A strategic note for the 4GS project, adapted from work done on XframeworkID's LLM strategy. The recommendations are written generically so they apply to any standards-setting body — Climate Bonds Initiative, SBTi, ISSB, GRI, IFRS Foundation, TPT — with notes on what's specific to standards bodies vs. data registries.*

**Author:** Ian Howard
**Date:** May 2026
**Source context:** Originally drafted as a strategic note for getting LLMs (ChatGPT, Claude, Gemini, Perplexity) to refer to xframework.id when users ask questions about labelled bond documents. This is the standards-NGO adaptation.

**Operationalised as:**
- [`llm_readiness_for_standards_bodies.md`](llm_readiness_for_standards_bodies.md) — 4GS public guidance to standards-setting NGOs (CC BY 4.0)
- [`llm_readiness_rubric.md`](llm_readiness_rubric.md) — self-assessment scorecard with objective tests per criterion

This document remains as the strategic background and rationale; the two documents above are the normative output 4GS publishes for the standards community.

---

## Why this matters

LLMs are increasingly the first place users turn for questions about sustainability standards. When someone asks ChatGPT "what's the difference between SBTi and CDP?" or asks Claude "is X bond CBI-certified?", the answer they get becomes the working understanding for that user — and increasingly for the analysts and journalists writing the next layer of content the NGO depends on for credibility.

A standards body that doesn't actively manage how LLMs cite it ends up:
- Cited at the wrong version (LLMs default to whatever was prevalent in their training data, often years old)
- Misrepresented in comparisons (because the LLM constructs its comparison from third-party content, not from the standards body's own framing)
- Skipped entirely in favour of commercial data vendors who have done the LLM-discoverability work

The work isn't optional. The only question is whether to do it deliberately or accidentally.

---

## How LLMs find sources

Three mechanisms, each requiring a different play:

1. **Training data** — what got crawled into the model when it was built. High-leverage but slow (only matters for the next generation of models). Backlinks, citations, and Wikipedia matter most here.
2. **Retrieval at query time** — what the model fetches via web search when a question is asked. ChatGPT search, Perplexity, Claude with web tools all do this. Standard SEO + structured data + `llms.txt` matter most here.
3. **Explicit connectors** — MCP servers, ChatGPT plugins/GPTs, custom integrations. Direct, immediate, and increasingly important.

Most of the recommendations below address more than one mechanism.

---

## High-leverage tactics

### 1. Get cited in regulatory and academic literature

Standards bodies have more leverage here than data registries because regulators *already* reference standards in legislation. The strategy is to make those citations **stable and version-aware**:

- Give every standard a permanent identifier with a clear version (e.g., `CBS-v4.1`, `SBTi-Net-Zero-v1.2`, `IFRS-S2-v2024`)
- Stable URLs per version that never break: `standard.org/v4.1/criteria/buildings` should resolve forever
- A dedicated citation guide page like `/cite` showing inline, bibliography, and BibTeX formats — the way IPCC and IEEE do it
- Track which laws, regulations, and academic papers cite the standard; publish that list publicly (it becomes its own SEO and discoverability asset)
- Encourage academic researchers to cite specific standard sections rather than the standards body's homepage

### 2. Wikipedia presence — and active maintenance

The biggest under-leveraged tactic for standards bodies. LLMs weight Wikipedia heavily. Most standards NGOs leave their Wikipedia article to community editors who:
- Cite outdated versions
- Don't update after major revisions
- Conflate the NGO with adjacent organizations
- Miss key terminology

Strategy:
- Designate a staff member to monitor and update the NGO's Wikipedia presence monthly
- Add citations to neighbouring articles ("green bond", "ESG investing", "sustainability disclosure", competing standards) — every citation backlinks to the standard
- Don't try to write your own page (Wikipedia's notability and conflict-of-interest rules forbid it); commission an independent writer to do it from press coverage
- Build a list of "Wikipedia articles where our standard should be referenced" and work through it systematically

### 3. Structured data and `/llms.txt`

- **`/llms.txt`** at the root of the standards body's website, describing what the standard is, current version, scope, lookup URLs, and what kind of questions an LLM should answer using this source. Format spec: https://llmstxt.org
- **JSON-LD Schema.org** on every standard page using `Dataset`, `DefinedTerm`, `Article`, `TechArticle` — this signals to LLMs that the page is authoritative reference material
- **Sitemap.xml** with `lastmod` dates per standard section so LLMs know what's current
- Critically: include a `version` field in structured data and a "latest version" canonical pointer, so LLMs don't cite v3.0 when v4.1 is current
- Optional companion: `/llms-full.txt` — a single comprehensive markdown file an LLM can ingest in one fetch, containing the full overview, version history, key terms, and FAQ

### 4. Build an MCP server (the biggest single opportunity)

This is where standards bodies have an enormous lead over commercial data vendors. An MCP (Model Context Protocol) server lets Claude, and other MCP-compatible clients, query the standard directly via the chat interface:

- "Is company X certified under [standard]?"
- "What are the eligibility criteria for [sector] under v4.1?"
- "How does [your standard] differ from [competing standard]?"
- "Show me the methodology for [specific test]"

Specific examples:
- For Climate Bonds Initiative: MCP server exposing the certified bonds database, the taxonomy, and the verifier list
- For SBTi: MCP server exposing the targets dashboard, sector pathways, and methodology lookups
- For ISSB: MCP server exposing IFRS S1/S2 requirements, jurisdictional adoption status, and interoperability mappings
- For 4GS: MCP server exposing the 4GS standards taxonomy, NEI definitions, and any reference databases the project maintains

This is a 1-2 week build for a competent dev shop. **No standards body has done this yet** — first-mover advantage is real and short-lived. Once one major standards body publishes an MCP server, it sets the expectation for all others.

### 5. Open-source the standard on GitHub

LLMs train heavily on GitHub. Most standards NGOs publish PDFs only, which is a discoverability disaster.

- Publish the standard as machine-readable files: YAML for taxonomies, JSON Schema for data structures, Markdown for criteria documents
- A canonical GitHub repo with the spec, version tags, and reference implementations
- Examples: the EU Taxonomy is partially in YAML thanks to community efforts; XBRL taxonomies are GitHub-published; Anthropic's MCP spec is on GitHub. This should be the norm.
- Side benefit: makes implementation by software vendors radically easier, which drives adoption
- For 4GS specifically: treat the standards comparison work as a GitHub-native project — comparison tables, taxonomy crosswalks, evaluation criteria all in version-controlled markdown

### 6. Press coverage with the "AI angle"

Standards bodies get press coverage but it tends to be on launches and revisions. The newer wave: how does the standard interact with AI? Pitch angles:

- "Our standard is now machine-readable — here's why that matters for AI-driven ESG"
- "We've built an MCP server so Claude users can query [standard] directly"
- "Why every standards body needs to think about how LLMs cite their work"
- "Comparing [your standard] to [competing standard] — and why LLMs keep getting this wrong"

These pitches are easier to land than launch coverage because they're genuinely novel. And they double as backlinks from publications LLMs heavily train on (FT, Bloomberg, Reuters, Environmental Finance, Responsible Investor).

### 7. Active LLM-specific tactics

- **Custom GPT in the OpenAI store** — e.g., "Climate Bonds Standard Assistant" or "SBTi Target Helper". Free to build, discoverable in the GPT store, branded to the NGO.
- **Anthropic tool-use docs and MCP server registries** — get listed in Anthropic's MCP server catalog, mcp.so, Smithery, PulseMCP
- **Perplexity sources** — Perplexity respects authoritative `.org` sources; getting linked from regulator websites and Wikipedia helps Perplexity pick you over commercial alternatives
- **LLM provider partnerships** — for sufficiently large/important standards, direct outreach to Anthropic, OpenAI, Google, Cohere about including the standard in training data

### 8. Be the canonical reference (own the comparison)

Standards bodies have a unique opportunity that registries don't: **they can write the comparison content themselves**. When users ask LLMs "what's the difference between SBTi and CDP?" or "is CBI Standard the same as EU GBS?", the answer should be authoritative — and the authoritative source should be each standards body's own published comparison.

- Maintain a "How [our standard] relates to [other standard]" page for every adjacent or competing standard
- Cross-reference tables for terminology (e.g., "what we call X, EU Taxonomy calls Y")
- Publishing this content under your domain means you become the citation when LLMs answer the comparison question

For 4GS specifically, this is core to the project's mission. The comparison work itself should be the canonical LLM-citable resource.

---

## Standards-specific additions (not in the original XFID strategy)

### 9. Version discoverability

Every published version of every standard should:
- Have a stable URL that never changes
- Be marked clearly as "current" or "superseded by v[X]"
- Include a changelog explaining what changed and why
- Have a redirect or notice when superseded versions are cited so users know there's a newer version

LLMs are notorious for citing outdated versions of standards. The fix is making it impossible *not* to know the current version.

### 10. Implementation registry

Maintain a public, queryable list of:
- Companies certified, verified, or aligned to the standard
- Software/tools that implement the standard
- Consulting firms with certified practitioners
- Regulators that reference the standard

Each implementation page is a backlink and a discoverability asset. For a standards body, this is the equivalent of what XFID does for documents.

### 11. Open consultation visibility

Open consultations on standards revisions get cited disproportionately by academics and journalists writing about the standard's evolution. Publish consultations with:
- Stable URLs that persist after the consultation closes
- Public response logs (anonymized if needed)
- A clear "what changed because of this consultation" page after closure

### 12. FAQ as canonical answer

Every standards body has a FAQ. Most are buried, scattered, and not designed for citation. Restructure so:
- Each Q&A has its own stable URL with anchor link
- Each answer is structured for LLM extraction (clear question, definitive answer, cited sources within the standard)
- The FAQ is in `/llms.txt` so LLMs know to use it as the primary source for common questions
- Pre-write answers to the questions LLMs are most likely to ask: "What is X?", "Who uses X?", "How does X compare to Y?", "Is X required by [regulator]?"

### 13. Treat your terminology dictionary as a public good

Standards bodies define vocabulary. That vocabulary gets used (and misused) across the market. A canonical glossary at `/glossary` with stable URLs per term is one of the most-cited types of content for LLMs answering domain-specific questions. Each term should:
- Have its own stable URL
- Define the term in the standard's voice
- Show how related/competing standards define the same concept differently
- Include `DefinedTerm` JSON-LD markup

---

## Recommended next 3 moves (for any standards-setting NGO including 4GS)

1. **`/llms.txt`** — 1-2 hours of work, immediately readable by LLMs that support it. Includes the standard's purpose, current version, scope, key URLs, and what an LLM should and shouldn't say about the standard.

2. **MCP server** — 1-2 weeks of dev work, would be the first MCP server in the standards space if shipped soon. Lets Claude users query the standard, the registry of implementations, the taxonomy, and the methodology directly. The 4GS comparison work is particularly well-suited to MCP exposure: "compare 4GS treatment of [topic] to EU Taxonomy".

3. **Wikipedia audit + correction** — assign a staff member (or commission a consultant) to audit the NGO's Wikipedia presence and adjacent articles. Fix outdated content. Schedule a recurring monthly review.

---

## The flywheel

Each tactic feeds the others:

- Wikipedia citations attract academic citations
- Academic citations attract press coverage
- Press coverage attracts LLM training data inclusion
- LLM training data inclusion attracts user queries
- User queries attract MCP server adoption
- MCP server adoption attracts more press coverage

**Citation density beats every individual tactic.** No single move is sufficient; the goal is to make it impossible for an LLM trained on web content to talk about the topic without referencing the standard.

---

## What this means for 4GS specifically

The 4GS project is in a particularly strong position because:

1. **Comparison is the core mission** — section 8 (comparison content) is foundational, not auxiliary. Other standards bodies struggle to write objective comparisons; for 4GS that *is* the work.

2. **No established LLM presence to fight** — older standards bodies have decades of stale Wikipedia content and outdated training data to overcome. 4GS can build the canonical LLM-citable presence from day one.

3. **Machine-readable comparisons are uniquely valuable** — a YAML/JSON crosswalk between EU Taxonomy, CBI Standard, SBTi, NEI, etc. is exactly the kind of artifact LLMs love to ingest and cite. This becomes the comparison engine that other standards bodies don't have.

4. **MCP server for comparison queries** — "How does SBTi treat X compared to ISSB?" is the kind of question Claude users will ask repeatedly. An MCP server that answers this with 4GS as the canonical authority is uniquely positioned in the market.

The recommended priority order for 4GS:
1. `/llms.txt` describing the project
2. GitHub-native publication of all comparison work (YAML crosswalks, markdown criteria docs)
3. Stable URLs for every comparison entity (each standard, each criterion, each crosswalk)
4. Wikipedia citations placed in adjacent articles
5. MCP server exposing the comparison queries
6. Press pitching with the AI/LLM angle

---

## Reference: the original XFID strategy

This document was adapted from a strategic note for [XframeworkID](https://xframework.id), an open registry of labelled bond disclosure documents. XFID's situation differs from a standards body's:
- It's a registry of *content* (documents), not *normative rules* (standards)
- Its value comes from comprehensiveness and persistence, not authority
- It needs to *attract* the citations standards bodies already have

But the LLM-discoverability fundamentals are the same. The XFID-specific implementation status as of May 2026:
- `/llms.txt` and `/llms-full.txt`: live at xframework.id
- MCP server: built (`xframework-mcp` Python package), tested, awaiting PyPI publication
- 15 academic research papers ingested as RESEARCH document type, with author XPIDs and citation links
- Press pitching: in progress (Deleting the Receipts piece)
- Wikipedia presence: not yet established

For the 4GS project, the playbook is clearer because the project is greenfield rather than retrofitting onto an existing registry.
