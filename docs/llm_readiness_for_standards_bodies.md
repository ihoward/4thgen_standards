# 4GS Recommendations: LLM Readiness for Standards-Setting Bodies

*A 4GS guidance document for any standards-setting NGO — Climate Bonds Initiative, SBTi, ISSB, GRI, IFRS Foundation, TPT, GRESB, and others — on what their standard must do to be correctly cited and consulted by large language models.*

**Status:** Guidance (CC BY 4.0)
**Last updated:** May 2026
**Companion document:** [`llm_readiness_rubric.md`](llm_readiness_rubric.md) — self-assessment scorecard
**Background note:** [`llm_discoverability_strategy.md`](llm_discoverability_strategy.md) — strategic rationale, tactics, and worked examples

---

## Why 4GS issues this guidance

LLMs (ChatGPT, Claude, Gemini, Perplexity, and their successors) are now the first place practitioners, journalists, regulators, and researchers turn for questions about sustainability and disclosure standards. The answers those models give become the working understanding of the field — and the input to the next wave of derivative content the standards body depends on.

A standards body that doesn't actively manage how LLMs cite it is routinely:

- Cited at the wrong version (LLMs default to whatever was prevalent in their training data, often years stale)
- Misrepresented in comparisons (the LLM constructs its comparison from third-party content, not the standards body's own framing)
- Skipped entirely in favour of commercial data vendors who have done the LLM-readiness work

4GS treats LLM readiness as a first-class property of a fourth generation standard. A standard that meets all engineering practices in 4GS but cannot be reliably cited by an LLM has not finished the job. The five practices in the LLM Accessibility group ([`FGP-y7u3jx`](../practices/concepts/FGP-y7u3jx.yaml), [`FGP-a5svie`](../practices/concepts/FGP-a5svie.yaml), [`FGP-am3s6q`](../practices/concepts/FGP-am3s6q.yaml), [`FGP-awmbvg`](../practices/concepts/FGP-awmbvg.yaml), [`FGP-ynq64v`](../practices/concepts/FGP-ynq64v.yaml)) formalise that requirement.

---

## The relationship between 4GS practices and LLM readiness

A substantial portion of foundational LLM readiness is **already a consequence of 4GS compliance**. NGOs that have adopted 4GS practices have, often without realising it, eliminated most of the failure modes that cause LLMs to misrepresent standards.

| 4GS practice | What it gives you for LLMs |
|---|---|
| [`FGP-4ukccp`](../practices/concepts/FGP-4ukccp.yaml) Version control all artifacts | GitHub-native publication; LLMs train heavily on GitHub |
| [`FGP-llyofe`](../practices/concepts/FGP-llyofe.yaml) Practices stored as structured data | Machine-readable source — no PDF extraction layer between standard and LLM |
| [`FGP-e4i6by`](../practices/concepts/FGP-e4i6by.yaml) Natively machine-readable without extraction | Same — eliminates the `pdfplumber` failure mode |
| [`FGP-mrkdoe`](../practices/concepts/FGP-mrkdoe.yaml) Linked data export (JSON-LD) | Schema.org markup that signals "authoritative reference" to LLMs |
| [`FGP-gsgv2v`](../practices/concepts/FGP-gsgv2v.yaml) Stable, deterministic identifiers | Citable atoms — every concept has a name an LLM can quote |
| [`FGP-mqf6ip`](../practices/concepts/FGP-mqf6ip.yaml) Concept identity separated from version | Lets an LLM cite the concept and the version separately, correctly |
| [`FGP-np4qch`](../practices/concepts/FGP-np4qch.yaml) Semantic versioning with explicit change rules | Lets an LLM say *which* version it is talking about |
| [`FGP-67pjjx`](../practices/concepts/FGP-67pjjx.yaml) Attributable and permanently recorded changes | Provenance LLMs can cite back to |
| [`FGP-uatad2`](../practices/concepts/FGP-uatad2.yaml) Documentation auto-generated from source | Eliminates documentation drift, the source of LLM misrepresentation |

Five of the recommendations below — R1 (/llms.txt), R2 (stable URLs), R3 (version supersession), R7 (companion document), and R14 (MCP server) — are now also formal 4GS practices in the LLM Accessibility group (see [`FGC-00001`](../contributions/FGC-00001.md)). The remaining recommendations address the broader external-facing layer that 4GS practices do not yet cover: citation graphs, Wikipedia, registries, and pre-written canonical answers.

---

## The thirteen recommendations

The recommendations are tiered to match 4GS's compliance levels.

- **Foundational** — the minimum required to avoid systematic LLM misrepresentation
- **Recommended** — substantially improves LLM citation accuracy and frequency
- **Advanced** — first-mover positioning; not yet expected, but increasingly valuable

The full self-assessment criteria are in [`llm_readiness_rubric.md`](llm_readiness_rubric.md).

### Foundational

**R1. Stable, version-aware URLs.**
Every standard, every criterion within a standard, every published version, and every defined term has a permanent URL. Superseded versions resolve forever. Current-version URLs use a `/latest` or canonical pointer. URLs include the version (e.g., `/v4.1/criteria/buildings`) so an LLM citing the URL is implicitly citing the version.

**R2. `/llms.txt` at the website root.**
A short markdown file at `/llms.txt` describing the standard's purpose, current version, scope, key URLs, and what kind of questions an LLM should answer using this source. Specification: https://llmstxt.org

**R3. Machine-readable source artifacts.**
Standards are published as YAML, JSON, JSON Schema, and Markdown — not as PDFs that require extraction. (4GS practice [`FGP-e4i6by`](../practices/concepts/FGP-e4i6by.yaml).) PDFs may exist as a derived presentation form, but they are not the source of truth.

**R4. Schema.org structured data on every standard page.**
JSON-LD using `Dataset`, `DefinedTerm`, `Article`, or `TechArticle` types, with explicit `version`, `dateModified`, and `isPartOf` fields. (Aligns with 4GS practice [`FGP-mrkdoe`](../practices/concepts/FGP-mrkdoe.yaml).)

**R5. Sitemap with `lastmod` dates per standard section.**
Lets retrieval systems and LLMs determine what is current without crawling everything.

**R6. Canonical glossary with stable URLs per term.**
The standards body's vocabulary is one of the most-cited types of content for LLMs answering domain-specific questions. Each defined term gets its own URL, its own JSON-LD `DefinedTerm` markup, and a clear definition in the standard's own voice.

### Recommended

**R7. `/llms-full.txt` companion file.**
A single comprehensive markdown file an LLM can ingest in one fetch. Contains the standard overview, current version, version history, key terms, FAQ, and citation guidance.

**R8. Citation guide (`/cite` page).**
Inline, bibliography, and BibTeX formats for citing the standard, individual sections, and individual versions — the way IPCC and IEEE do it.

**R9. Version supersession notices.**
Pages for superseded versions display a clear notice: "This is version X. The current version is [Y]." This is the single highest-leverage fix for the most common LLM error: citing the wrong version.

**R10. Cross-reference / comparison content with adjacent standards.**
A "How [our standard] relates to [other standard]" page for every adjacent or competing standard. Cross-reference tables for terminology. Publishing this content under your domain means *you* become the citation when LLMs answer comparison questions, rather than a third-party blog of varying accuracy.

**R11. FAQ structured for citation.**
Each Q&A has its own stable URL with anchor link. Each answer is structured for LLM extraction (clear question, definitive answer, cited source within the standard). The FAQ is referenced from `/llms.txt`.

**R12. Implementation registry.**
A public, queryable list of certified entities, software implementations, consulting firms with certified practitioners, and regulators that reference the standard. Each implementation page is a backlink and an LLM-discoverability asset.

**R13. Active Wikipedia maintenance.**
Designate a staff member (or commission a consultant) to monitor and correct the NGO's Wikipedia presence and adjacent articles monthly. Outdated Wikipedia content is the single largest contributor to LLM misrepresentation of long-established standards. Do not write the page yourself (Wikipedia's conflict-of-interest rules forbid it); commission an independent writer.

### Advanced

**R14. MCP server exposing the standard's data.**
A Model Context Protocol server that lets Claude and other MCP-compatible clients query the standard, the registry of implementations, the taxonomy, and the methodology directly via the chat interface. As of mid-2026 no major standards body has shipped one; first-mover advantage is real and short-lived.

**R15. Listed in MCP and AI tool catalogues.**
Anthropic's MCP server registry, mcp.so, Smithery, PulseMCP. For OpenAI: a custom GPT in the GPT store, branded to the NGO.

**R16. Pre-written canonical answers to high-volume LLM queries.**
The standards body identifies the questions LLMs are most often asked about its standard ("What is X?", "Is company Y certified?", "How does X compare to Z?", "Is X required by [regulator]?") and publishes definitive, citable answers on stable URLs. The FAQ becomes the canonical source LLMs surface.

---

## How to apply this guidance

For a standards body that is already 4GS-compliant or working toward compliance:

1. **Read the rubric.** Score the standard against [`llm_readiness_rubric.md`](llm_readiness_rubric.md).
2. **Address the foundational tier first.** R1–R6 are mostly inexpensive (days to weeks of work) and yield the largest reduction in LLM misrepresentation.
3. **Schedule the recommended tier.** R7–R13 are typically 1–3 months of staff time spread over a year.
4. **Treat the advanced tier as positioning.** R14–R16 are competitive moves; doing them in 2026 still places a standards body ahead of all peers.

For a standards body that has not yet adopted 4GS: addressing the foundational tier inevitably leads back to the underlying 4GS practices (machine-readable artifacts, version control, deterministic identifiers). Implementing 4GS first is the more efficient sequence.

---

## What 4GS itself does

4GS is committed to meeting all foundational and recommended criteria as it matures, and to demonstrating the advanced tier (MCP server, comparison-query interface) as a reference implementation that other standards bodies can adopt or fork. Progress is tracked in the [4GS repository](../README.md).

---

## Licence and use

This guidance is published under CC BY 4.0. Standards-setting bodies are free to adopt, adapt, and republish it as part of their own digital strategy, with attribution. The companion rubric ([`llm_readiness_rubric.md`](llm_readiness_rubric.md)) is published on the same terms.

A standards body that adopts these recommendations may state that its standard is **"LLM-ready (4GS guidance)"** in marketing and stakeholder communications, citing the level of compliance achieved (Foundational, Recommended, or Advanced).
