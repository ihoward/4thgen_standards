# 4GS Governance

This document describes how the Fourth Generation Standards framework is governed —
how contributions are submitted, how practices advance through their lifecycle, how
releases are approved, and how the community participates.

---

## Principles

1. **Openness** — All changes are proposed and discussed publicly via pull requests.
2. **Versioning** — Practices and taxonomy are versioned. Approved content is never
   silently modified.
3. **Reproducibility** — A numbered release pins a specific set of standard practices,
   ensuring compliance assessments are comparable across time.
4. **Separability** — Taxonomy relationships are stored separately from practice
   definitions. Practices can be reclassified without changing their criteria.
5. **Evidence orientation** — Practice criteria must describe observable, implementable
   characteristics — not intentions, aspirations, or stated values. When NEI (a 4GS
   standard) was ingested into the ACT-ID.io registry, its three evidence tiers
   (Inferred, Declared, Validated) mapped cleanly to structured criteria fields —
   while legacy taxonomy criteria arrived as unstructured paragraphs mixing thresholds,
   legal references, and metric descriptions into single text blobs. See the
   [proof of concept](README.md#proof-of-concept-nei-in-actidio) for details.

---

## Roles

### Maintainers

Maintainers are responsible for:

- Facilitating contribution discussion
- Advancing contributions through lifecycle stages
- Approving and publishing releases
- Maintaining documentation quality

Maintainers are appointed by atypical. Current maintainers: Ian Howard (atypical).

### Contributors

Any person may submit a contribution or comment on an open contribution. Contributions
are governed by [`CONTRIBUTING.md`](CONTRIBUTING.md) and the licences in [`LICENSE`](LICENSE).

---

## Contribution Lifecycle

### Submission

A contribution is submitted as a pull request containing a completed `FGC-xxxxx.md`
file in the `contributions/` directory.

Contributions may:

- Create a new practice concept and initial version
- Modify the criteria of an existing practice (creating a new version)
- Change taxonomy relationships (domain assignments)
- Propose a new taxonomy domain

### Review

Once submitted, a contribution enters the **Proposed** stage. Any community member
may comment. Maintainers may request clarification or rewrites.

### Candidate Stage

A maintainer may advance a contribution to **Candidate** when:

- The contribution is complete and well-specified
- No blocking objections remain unresolved
- At least one maintainer has reviewed and approved

### Standard Stage

A contribution advances to **Standard** when:

- The Candidate stage has been open for at least 14 days with no blocking objections
- A maintainer merges the pull request

---

## Identifier Assignment

Practice concept identifiers (FGP-xxxxxx) are deterministic: derived from the SHA-256
hash of the normalised practice name, base32-encoded, first 6 characters.

The normalised name is the lower-case, whitespace-normalised, punctuation-stripped
concept title. atypical assigns identifiers for approved contributions. Independently
generated IDs matching this algorithm are accepted; disputes are resolved by the
maintainer.

---

## Release Process

### Candidate Release

A candidate release (`FGR-<semver>C-FGC-<seed>`) may include Candidate practices.
It is used for evaluation purposes but not for formal compliance claims.

### Standard Release

A standard release (`FGR-<semver>`) must reference only Standard practices and a
Standard taxonomy version. Standard releases require approval from a maintainer and
a 7-day public review period with no blocking objections.

### Versioning Rules

| Change type | Version bump |
|-------------|-------------|
| New practices added | Minor (`1.0.0` → `1.1.0`) |
| Existing practice criteria revised (new version) | Minor |
| Practice retired | Major (`1.x.x` → `2.0.0`) |
| Taxonomy reorganisation (non-breaking) | Minor |

---

## Amendments to This Document

This governance document is itself subject to the contribution process. Proposed
amendments are submitted as pull requests and require maintainer approval.
