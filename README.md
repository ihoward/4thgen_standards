# Fourth Generation Standards (4GS)

**A specification framework for standards built the way open source software is built.**

---

## Overview

The Fourth Generation Standards (4GS) framework defines the practices that distinguish a
fourth generation standard from earlier generations. It is itself built as a fourth
generation standard: revision-controlled, structured, versioned, and governed through an
open contribution process.

This is the specification that answers the question: *what exactly must a standard do to
qualify as fourth generation?*

---

## The Four Generations

| Generation | Format | Properties |
|------------|--------|------------|
| 1st | Paper documents | Static, not searchable, geographic distribution only |
| 2nd | Electronic documents (PDF, HTML) | Distributable online, but unstructured |
| 3rd | Database-backed, offered as data | Queryable, but siloed, not interoperable, no provenance |
| **4th** | **Revision-controlled, relatable, metadata-rich, LLM-accessible** | Versionable, citable, machine-consumable, community-governed |

---

## Core Concepts

| Concept | Description |
|---|---|
| **Practice** | An observable, implementable characteristic of a fourth generation standard. |
| **Taxonomy** | A domain hierarchy that organises practices into meaningful groups. |
| **Contribution** | A formal change request that introduces or modifies practices or taxonomy. |
| **Release** | A versioned, stable snapshot of standard practices. |

---

## Identifier Formats

| Entity | Format | Example |
|---|---|---|
| Practice concept | `FGP-xxxxxx` | `FGP-4ukccp` |
| Practice version | `FGP-xxxxxx-vN` | `FGP-4ukccp-v1` |
| Taxonomy release | `FGT-<semver>` | `FGT-1.0.0` |
| Contribution | `FGC-xxxxx` | `FGC-00001` |
| Standard release | `FGR-<semver>` | `FGR-1.0.0` |

Identifiers are deterministic: the concept ID is derived from the SHA-256 hash of the
normalised practice name, base32-encoded, first 6 characters. Independent contributors
who describe the same practice arrive at the same identifier without coordination.

---

## Practice Lifecycle

```
Proposed  →  Candidate  →  Standard
```

- **Proposed**: Submitted via a contribution. Under active discussion.
- **Candidate**: Accepted for inclusion pending final review.
- **Standard**: Approved and included in a numbered release.

---

## Compliance Levels

A standard may claim fourth generation status at one of three levels:

| Level | Requirements |
|---|---|
| **Foundational** | Implements all practices in the Foundational release (FGR-1.0.0) |
| **Extended** | Foundational + all practices in the Extended release |
| **Full** | All Standard practices in the current release |

---

## Repository Structure

```
4thgen_standards/
├── README.md
├── LICENSE
├── CONTRIBUTING.md
├── GOVERNANCE.md
│
├── docs/
│   ├── framework.md          # Conceptual overview and design rationale
│   ├── methodology.md        # How practices are defined and validated
│   └── adoption_guide.md     # Step-by-step adoption pathway for standards organisations
│
├── practices/
│   ├── concepts/             # One YAML file per practice concept (FGP-xxxxxx.yaml)
│   └── versions/             # One YAML file per practice version (FGP-xxxxxx-vN.yaml)
│
├── taxonomy/
│   ├── nodes/                # FGT-<version>-nodes.csv — domain node table
│   └── edges/                # FGT-<version>-edges.csv — practice-domain relationships
│
├── contributions/
│   └── FGC-template.md       # Template for submitting a new contribution
│
├── releases/
│   └── FGR-template.yaml     # Template for a standard release manifest
│
└── tools/
    └── validate.py           # Repository integrity validation
```

---

## Current Releases

- [`FGR-1.0.0`](releases/FGR-1.0.0.yaml) — 12 practices across 5 domains (Foundational release)

---

## Reference Implementation

The [Neurodivergent Enablement Indicators (NEI)](https://atypical.business) framework is
the reference implementation: a fully operational standard built entirely using the
practices defined here.

- NEI repository: https://github.com/ihoward/neurodivergent-enablement-indicators
- Live demonstration: https://atypical.business

### Proof of Concept: NEI in ACT-ID.io

When the [ACT-ID.io](https://act-id.io) registry ingested NEI alongside 25 legacy
sustainable finance taxonomies, the operational difference was stark:

|                                   | NEI (4GS)              | Legacy (25 taxonomies)         |
|-----------------------------------|------------------------|--------------------------------|
| Ingestion code                    | ~100 lines             | ~1,400 lines                   |
| Extraction scripts                | 1                      | 4 (Excel, CSV, CBRT, PDF)      |
| Criteria records                  | 37 (structured)        | 4,553 (unstructured)           |
| Citations with bibliographic data | 97                     | 0                              |
| Information loss                  | None                   | Significant                    |
| Time to add to pipeline           | < 1 hour               | Weeks (cumulative)             |
| Machine-readable release manifest | Yes                    | No                             |

Each row traces directly to a 4GS practice: deterministic identifiers eliminated
deduplication heuristics, version-aware ingestion preserved historical criteria,
graph-native taxonomy enabled reclassification without identity changes, structured
evidence tiers made criteria actionable by role, and inline academic citations gave
end users verifiable provenance instead of circular legal references.

The full case study is available in
[`comparing older taxonomies to NEIs a 4GS standard.txt`](comparing%20older%20taxonomies%20to%20NEIs%20a%204GS%20standard.txt).

---

## Getting Started

- To **understand the framework**, read [`docs/framework.md`](docs/framework.md).
- To **adopt these practices**, read [`docs/adoption_guide.md`](docs/adoption_guide.md).
- To **propose a change**, read [`CONTRIBUTING.md`](CONTRIBUTING.md).
- To **evaluate a standard's generation level**, use the release manifest in [`releases/`](releases/).

---

## Licensing

| Component | Licence |
|---|---|
| Practice data, taxonomy CSVs, release manifests | CC0 1.0 Universal — public domain |
| Specification documents, governance, adoption guide | CC BY 4.0 — free use with attribution |
| Reference tooling | Apache 2.0 — open source |

The 4GS identifier namespace (FGP-, FGR-, FGT-, FGC-) is a trademark of atypical.
Identifier minting is a governed operation.

---

## Governance

See [`GOVERNANCE.md`](GOVERNANCE.md).

---

*Maintained by [atypical](https://atypical.business) — atypical.business*
