# Contributing to Fourth Generation Standards

Thank you for contributing. This document explains how to propose new practices,
modify existing ones, or change taxonomy.

---

## What you can propose

- **New practice** — a characteristic that should be required of a fourth generation
  standard, which is not yet in the specification
- **Practice revision** — updated criteria for an existing practice (creates a new version)
- **Taxonomy change** — a new domain, or reclassification of existing practices
- **Documentation improvement** — corrections or additions to `docs/`

---

## How to submit a contribution

1. Fork this repository.

2. Copy [`contributions/FGC-template.md`](contributions/FGC-template.md) to
   `contributions/FGC-<next-number>.md`. Use the next sequential number.

3. Fill in all required fields in the template.

4. If proposing a new practice, create the practice concept and version files
   (see below).

5. Open a pull request. The title should be: `[FGC-XXXXX] Brief description`.

---

## Practice concept file format

`practices/concepts/FGP-xxxxxx.yaml`:

```yaml
id: FGP-xxxxxx
normalized_name: "lower case whitespace normalised name without punctuation"

title: Human-readable title

description: |
  What this practice means and why it matters for fourth generation standards.
```

## Practice version file format

`practices/versions/FGP-xxxxxx-v1.yaml`:

```yaml
id: FGP-xxxxxx-v1
concept_id: FGP-xxxxxx

compliance_level: foundational  # foundational | extended | full

criteria:
  required: |
    What a standard must demonstrably implement to meet this practice.
    Observable and verifiable, not aspirational.

  recommended: |
    Additional implementation details that strengthen compliance but are
    not required for the minimum bar.

rationale: |
  Why this practice is necessary for fourth generation status. What problem
  it solves that earlier generation approaches do not.

citations:
  supporting:
    - >
      Author, A. (Year). Title. Journal/Source.
      https://doi.org/...
  dissenting: []
```

Structured citations matter: when NEI was ingested into the ACT-ID.io registry, its
inline DOI-linked references produced 97 distinct, verifiable citations across 37
indicators. Legacy taxonomies yielded zero bibliographic citations — only generic
document-level references like "EU Taxonomy Regulation." See the
[proof of concept](README.md#proof-of-concept-nei-in-actidio).

---

## Identifier generation

Practice concept IDs are deterministic. To generate the ID for a new practice:

```python
import hashlib, base64

def make_id(normalized_name):
    h = hashlib.sha256(normalized_name.encode()).digest()
    b32 = base64.b32encode(h).decode().lower().rstrip('=')
    return f'FGP-{b32[:6]}'
```

The `normalized_name` is the lower-case, whitespace-normalised (single spaces),
punctuation-stripped version of the concept title.

---

## Review timeline

- Maintainers will acknowledge contributions within 7 days.
- Candidate status: reached when complete, uncontested, and reviewed.
- Standard status: reached 14 days after Candidate with no blocking objections.

---

## Code of conduct

Contributions should be substantive, evidence-grounded, and constructive.
Disputes are resolved by maintainers. Personal criticism is not welcome.
