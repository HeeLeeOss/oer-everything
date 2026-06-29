# PLAN — oer-everything

> Status: Draft · Version: 0.1.0 · Last updated: 2026-06-28 · Owner: TBD (maintainer) · Lane: donated

> **Positioning.** oer-everything is not another content repository, and it is not a competitor to
> the subject libraries it serves. It is the **connective tissue** — the standards spine, the shared
> metadata model, the license gate, and the quality bar — that turns scattered, openly-licensed
> educational resources across math, science, reading, and computer science into **one navigable,
> standards-aligned K-12 library a teacher can actually find their way around.** The moat is not the
> content (others author that); it is the *coordination*: a single, verifiable map from "the standard
> I have to teach this week" to "a free, vetted, openly-licensed resource that teaches it."

## Executive summary

A teacher in an under-resourced classroom does not lack open educational resources (OER) in the
abstract — there are millions of them. They lack a way to *find the right one*: aligned to the exact
standard they must teach, at the right grade band, genuinely free to use and adapt, accurate, and
accessible. The open-education landscape is fragmented across hundreds of repositories with
incompatible metadata, unverified or mislabeled licenses, dead links, and no consistent mapping to
the curriculum standards teachers are actually accountable to. The result is a paradox of plenty:
abundant open content, persistently low usable findability.

**oer-everything is the umbrella layer that fixes findability, not the content beneath it.** It
delivers (1) a shared, standards-aligned **metadata model** for K-12 learning resources
(schema.org/`LearningResource` + LRMI); (2) a machine-readable **standards registry** with stable
identifiers (CASE / ASN GUIDs) for the frameworks teachers are held to (Common Core Math & ELA, NGSS,
CSTA K-12 CS, with a path to state frameworks); (3) a **crosswalk** binding each cataloged resource to
the standards it teaches; (4) a **license + provenance gate** that admits only verifiably open
content; (5) a **quality rubric** with educator review; and (6) a **privacy-first static discovery
site** where a teacher browses by grade → subject → standard and lands on a usable, free resource.

The project **coordinates** sibling Elyos OER projects rather than duplicating them. The live
`oer-math` project is the first content source ingested end-to-end; later phases onboard
`oer-science-labs`, `open-coding-curriculum`, and reading/decodable libraries through one published
**coordination protocol**. oer-everything owns the spine (schema, standards, crosswalk, gate,
discovery); each subject library owns its content.

**The deliverable is the map and the metadata, not re-authored content.** We catalog, align, verify,
and surface; we do not re-host or re-write what a subject library already maintains. Risk tier is
**low**, with two non-negotiable gates that carry the real risk: a **license/provenance gate** (only
open/PD/CC content, every license verified, no "best-guessing") and a **child-safety/privacy stance**
(zero collection of student or teacher personal data — enforced by a no-backend, no-accounts,
no-tracking architecture, which sidesteps COPPA/FERPA exposure by design rather than by policy).

## Problem & beneficiaries

**Who is helped (the beneficiary).** The primary beneficiary is the **K-12 teacher in a
resource-constrained setting** — under-funded districts, rural schools, charter and community schools,
homeschool co-ops, refugee/displacement education programs, and after-school/tutoring nonprofits —
who must teach to specific standards and cannot afford commercial curricula. Secondary beneficiaries:
**students** (better, freely-available materials), **curriculum coordinators** (a standards-coverage
view), and the **OER authors/subject libraries** themselves (increased, attributed reuse of work they
already produced, surfaced through a standards lens they could not build alone).

**The verified need.** The *general* need is well established: standards-alignment and discoverability
are repeatedly cited as the top barriers to OER adoption, ahead of content availability. We treat
that macro-need as real. We are explicit, however, that the **per-classroom, per-partner delivery need
is TO BE SECURED**: no specific teacher, school, district, or teacher-serving nonprofit has yet
committed to adopt and use this library. Until a named beneficiary confirms adoption, individual tasks
carry `verifiedNeed: false`. This honesty is load-bearing: Elyos's bar is **delivered, not merged** —
a catalog nobody teaches from is not a good deed, however well-built.

**Partner / requestor.** TO BE SECURED. Candidate channels: teacher-serving nonprofits and OER
intermediaries (e.g., open-curriculum nonprofits, library/education foundations), individual district
curriculum offices, homeschool and refugee-education networks, and the maintainers of sibling OER
projects. M0 includes explicit outreach; no partner is assumed.

**Coordination, not competition.** A distinct part of the problem is *internal* to Elyos: the roadmap
already contains many sibling education projects (`oer-math` live; `oer-science-labs`,
`open-coding-curriculum`, `decodable-readers`, `teacher-lesson-plans`, `quiz-bank-open`,
`curriculum-standards-map`, and more, selected/candidate). Without an umbrella they will produce
incompatible metadata and duplicated standards work. oer-everything exists partly to **prevent that
fragmentation** by giving them one schema, one standards registry, and one discovery surface.

## Goals and non-goals

**Goals**
- Publish a shared, standards-aligned **metadata model** (schema.org/`LearningResource` + LRMI) that
  every Elyos OER subject library and external contributor can target.
- Stand up a machine-readable **standards registry** with stable GUIDs (CASE/ASN) for the core K-12
  frameworks teachers are accountable to, and a **crosswalk** from resources to standards.
- Make **license + provenance verification a non-skippable, auditable gate**: only openly-licensed
  (PD / CC0 / CC-BY / CC-BY-SA where compatible) resources enter the library; everything else is
  flagged and excluded.
- Deliver a **privacy-first static discovery surface** where a teacher finds a usable, free resource
  for a given grade + standard — with **zero collection of student or teacher data**.
- Raise the floor on quality via an **OER quality + grade-appropriateness rubric** plus educator
  review, and on access via **WCAG 2.2 AA** conformance as a gate (not an aspiration).
- **Coordinate** sibling subject libraries through one published contribution protocol; ingest
  `oer-math` first, then science/CS/reading libraries.

**Non-goals (what oer-everything will NOT do — constraints as identity)**
- **It will not re-author or re-host content a subject library owns.** The umbrella indexes, aligns,
  verifies, and links; it does not duplicate the authoring shops beneath it. (If a resource needs
  authoring, that is a task for `oer-math`/`oer-science-labs`/etc., not here.)
- **It will not catalog non-open content.** No "all rights reserved," no unclear license, no
  free-as-in-beer-but-not-adaptable resources. Open/PD/CC only, every license verified.
- **It will not collect any student or teacher personal data** — no accounts, no logins, no
  analytics that identify users, no cookies beyond strictly-necessary, no third-party trackers. This
  is architectural (static site, no backend), not merely a policy promise.
- **It will not reproduce full standards text where the framework's license forbids it.** It uses
  standards **identifiers/codes and structure** (facts) and links to the official text; it reproduces
  full descriptive text only for frameworks whose license permits it (see compliance).
- **It will not rank, grade, score, profile, or surveil teachers or students.**
- **It will not become a paywalled, ad-supported, or login-gated platform**, and will not build
  proprietary/closed integrations.
- **It will not provide medical, legal, or safety advice**, and will not take partisan positions on
  contested curricular topics (it presents evidence-based, standards-aligned content and labels
  sensitive science topics as such — see compliance).
- **It will not auto-publish or auto-ingest**; a human reviews and accepts every resource through the
  gate before it appears.

## Success metrics (outcomes)

Outcome-based and beneficiary-centric. The **headline outcome is standards coverage that a real
teacher can use**, not the raw count of resources cataloged (an explicitly rejected vanity metric).

| Metric | Baseline | Target (first 6 months) |
| --- | --- | --- |
| **Standards coverage** — % of a chosen target standard set (start: CCSS Math, one grade band) with ≥ 1 license-verified, educator-approved aligned resource | 0% | ≥ 80% of the target band's standards covered |
| **Verified classroom adoption** (last-mile delivered) — distinct teachers/classrooms/programs that confirm they used a library resource to teach | 0 | ≥ 3 verified adoptions with evidence artifacts |
| **Findability** — task-based usability: a real teacher locates a usable resource for a given grade+standard | n/a | ≥ 80% task success, median ≤ 3 navigation steps, with ≥ 5 educator testers |
| **License/provenance integrity** — cataloged resources with a recorded, verifiable open license + provenance | n/a | 100% (any unverifiable resource is excluded, not admitted) |
| **License errors found in review** (mislabeled/non-open resource admitted) | n/a | 0 (a single admitted non-open resource is a Sev-1 defect) |
| **Subject libraries coordinated** through the shared schema + protocol | 0 | ≥ 2 (oer-math + 1 more) |
| **Accessibility** — discovery site WCAG 2.2 AA conformance (automated + manual audit) | n/a | 0 AA violations on core browse/landing flows |
| **Link health** — cataloged resources reachable + archival snapshot recorded | n/a | ≥ 98% reachable; 100% with a snapshot reference |
| **Student/teacher PII collected** | 0 (by design) | 0 (verifiable: no data-collection code paths exist) |

**Defining "verified classroom adoption" (the delivered signal) and its evidence artifact.** The
Steward records one canonical **adoption evidence artifact** per beneficiary in the outcome ledger
(committed `outcomes/<adoption-id>.json`: channel, who, what resource/standard, date, and a
verifiable reference). Acceptance is per channel: (a) **direct educator confirmation** — written
statement from a named teacher/coordinator that they taught from a library resource (evidence = the
archived message + the resource/standard IDs); (b) **partner program** — a teacher-serving nonprofit
confirms inclusion in their distributed materials (evidence = the published list/permalink);
(c) **demonstrable downstream reuse** — a third party forks/cites/embeds a library crosswalk or
collection (evidence = the commit/citation URL). Self-reported, unverifiable, or "we shipped it and
hope" never counts as delivered.

**Quantifying "findability" and "quality" so DoDs are checkable.** *Findability* is measured by a
scripted **task-based usability test** with ≥ 5 practicing educators (success rate + step count +
time), repeated each milestone. *Quality* is the per-resource **rubric score** (0–100; see quality
gates); only resources scoring **≥ 80** with educator sign-off are admitted to the library, and the
score is stored in the resource's catalog record.

## Scope

**In scope**
- A canonical **LearningResource metadata model** (schema.org + LRMI) and the catalog format
  (version-controlled JSON-LD), with an `alignmentObject` binding to standards.
- A **standards registry** (CASE/ASN-based, stable GUIDs) for: CCSS Mathematics, CCSS ELA/Literacy,
  NGSS, and CSTA K-12 CS — added in phases — plus a documented method for adding state frameworks.
- A **resource→standard crosswalk** (alignment) with provenance on each alignment claim.
- A **license + provenance + standards-IP gate** (per resource) and a **quality + grade-appropriateness
  rubric** with educator review.
- A **subject-library coordination protocol**: how `oer-math` and future libraries submit entries,
  who owns what, and how updates propagate.
- A **privacy-first static discovery site** (browse by grade/subject/standard; client-side search;
  no backend, no tracking) and small **validators** (schema, link/archival check, license-field,
  standards-GUID resolution).
- License, provenance, accessibility, and grade-appropriateness review and recording per resource.

**Out of scope**
- **Authoring or re-hosting subject content** (that belongs to the subject libraries). We link and
  describe; we do not mirror or rewrite.
- **Non-open resources**, or resources with unclear/unverifiable licensing.
- **Any collection of student/teacher personal data**, accounts, grading, LMS integration, or
  learner analytics.
- **Reproducing full standards text** where the framework's license forbids it (identifiers/structure
  + links only in that case).
- **Interpretation, ranking, or political framing** of contested curricular content; **medical/legal/
  safety advice**.
- **Automated, unattended publishing/ingestion.**

## Solution approach & architecture

This is a **coordination + metadata project with light software** (a schema, a standards registry,
crosswalks, validators, and a static site). It deliberately moves *no* data about people and runs *no*
backend service.

**Locked build decisions.**
- **Stack:** TypeScript, ESM, pnpm workspaces (Elyos conventions). Validators and tooling are small
  Node packages with minimal dependencies. The discovery site is a **static site (Astro)** —
  pre-rendered HTML, no server, no database. **Search is client-side and privacy-preserving**
  (prebuilt static index, e.g. Pagefind) — no query is sent to any server.
- **Metadata standard:** **schema.org/`LearningResource` + LRMI** (Learning Resource Metadata
  Initiative) for resource records; `alignmentObject` (`educationalAlignment`) for standards binding.
- **Standards format:** **1EdTech CASE 1.x** + **ASN (Achievement Standards Network)** GUIDs as the
  canonical identifiers; standards stored as a versioned registry keyed by GUID.
- **Content/metadata license:** **CC-BY-4.0** for our catalog, crosswalks, rubric, and docs; **MIT**
  for tooling/validators/site code. We only catalog resources that are themselves open.
- **No-backend, no-accounts, no-tracking** is a *locked architectural constraint*, chosen so child
  privacy is guaranteed by construction (see Security & privacy).

**Pipeline (per resource).**
1. **Submit / discover** — a subject library (via the coordination protocol) or a curator proposes a
   resource with source URL, author, and license claim.
2. **License + provenance + IP gate** — verify the license actually permits reuse/adaptation
   (PD/CC0/CC-BY/compatible CC-BY-SA), record license id + URL + a snapshot reference, capture
   provenance (author, source, retrieval date, version), and confirm we are not reproducing
   license-restricted standards text. PASS/FLAG/EXCLUDE artifact committed.
3. **Standards alignment** — bind the resource to one or more standards by GUID, with a short
   rationale per alignment (who aligned it, how verified). Alignments are claims with provenance.
4. **Quality + grade-appropriateness review** — educator scores against the rubric (accuracy, grade
   band, pedagogical fit, readability, bias/sensitivity); admit only if score ≥ 80 with sign-off.
5. **Accessibility check** — the *resource* is labeled for accessibility features
   (LRMI `accessibilityFeature`); the *discovery surface* is held to WCAG 2.2 AA.
6. **Catalog + crosswalk** — write the canonical `LearningResource` record + alignment; validators run
   in CI (schema-valid, link reachable + snapshot recorded, license field present, GUIDs resolve).
7. **Publish to discovery site** — static rebuild; the resource appears under its grade/subject/
   standard. A human accepts; nothing auto-publishes.
8. **Last-mile + outcome** — Steward routes the now-findable resource to a beneficiary and records
   adoption evidence.

**Canonical metadata model (source of truth; all outputs are projections of it).** Per resource:
`id`, `title`, `description`, `url`, `author`/`provider`, `license {id, url, permitsReuse:boolean,
permitsAdaptation:boolean, attribution, snapshotRef}`, `provenance {retrievedAt, version,
sourceLibrary, addedBy}`, `educationalLevel {gradeBand}`, `subject`, `learningResourceType`,
`educationalAlignment[] {framework, standardGuid, standardCode, alignmentType, rationale, verifiedBy}`,
`accessibility {features[], hazards[], summary}`, `language`, `qualityScore {value, rubricVersion,
reviewedBy}`, `linkHealth {lastChecked, status, snapshotRef}`, `specVersions {schemaOrg, lrmi, case,
asn}`. The standards registry stores per standard: `guid`, `framework`, `code`, `statementText?`
(only if license permits), `gradeBand`, `parent`, `frameworkLicense`, `sourceUrl`, `version`.

**Tech/spec versions (pinned; recorded in `specVersions`, bumped only by a deliberate task).**
schema.org (pinned release), LRMI (pinned), **CASE 1.0 (with 1.1 where a source provides it)**, ASN
identifiers, WCAG **2.2 AA**. Any drift is an isolated version-bump task, never a silent output change.

**Key decisions.**
- **Canonical-model-first** so we never hand-maintain parallel metadata formats (catalog, site,
  exports are projections).
- **GUID-based standards** so alignments survive renaming/restructuring and so external tools
  (OpenSALT/CASE consumers) can interoperate.
- **License/IP gate is a blocking, committed checklist artifact**, not an informal judgement.
- **Static + privacy-by-construction** so the most sensitive concern (children's data) cannot occur:
  there is nothing to collect because there is no collection surface.

## Data, licensing & compliance

**This is the critical section.** oer-everything links to and describes others' educational content
and references curriculum standards, so it must treat licensing, standards IP, and child privacy
conservatively.

**Resource licenses we accept (must permit reuse AND adaptation/derivatives):**
- **Public domain / CC0 1.0** — accepted (provenance still recorded).
- **CC-BY 4.0** (and compatible CC-BY versions) — accepted; attribution recorded and surfaced.
- **CC-BY-SA** — accepted **only** under the written share-alike acceptance policy (our metadata is
  CC-BY; we link to, never re-host, the SA content, so share-alike obligations stay with the source).
- **Open licenses for code-bearing resources** (e.g., MIT/Apache for CS exercises) — accepted.
- **Excluded:** CC-BY-ND (no derivatives), CC-BY-NC where the use is incompatible, "all rights
  reserved," unclear/unstated, or login/paywall-gated resources → **flagged and excluded, never
  guessed.** "Free to view" is not "open."

**Objective acceptance criterion.** A resource PASSes only if `license.permitsReuse: true` **and**
`license.permitsAdaptation: true` are recorded from a cited license id/URL, with a snapshot reference.
Missing/unparseable license evidence = FLAG/EXCLUDE (no default-allow).

**Curriculum-standards IP — handled explicitly (a real, often-missed nuance).** Standards frameworks
are *not* uniformly free to reproduce:
- **Standard identifiers, codes, and hierarchical structure are treated as facts** and may be used
  freely (e.g., the code `CCSS.MATH.CONTENT.4.NF.B.3`, its grade, its parent). This is the backbone of
  the crosswalk and is always permitted.
- **Full descriptive statement text is reproduced only where the framework's license permits it**, per
  this matrix (verified per framework, recorded in `frameworkLicense`):
  - **NGSS** — CC-BY-style permission for the standards (verify exact terms) → statement text may be
    reproduced with attribution.
  - **Common Core (CCSS Math & ELA)** — published under a public license with attribution + specific
    conditions (verify and record exact terms) → reproduce only as the license allows; otherwise use
    codes + link to the official text.
  - **CSTA K-12 CS standards** — verify terms; default to codes + link unless reproduction is clearly
    permitted.
  - **State frameworks** — terms vary widely; default to **identifiers + link to the official source**
    unless a specific state's license is verified to permit reproduction.
- **Default behavior when unverified: codes + structure + link only.** We never paste standards text
  whose license we have not verified. The standards-IP check is part of the per-framework gate.

**Provenance & attribution.** Every cataloged resource records source URL, author/provider, retrieval
date, version, license id+URL+snapshot reference, and the required attribution string (surfaced on the
discovery site). Every alignment claim records who aligned it and how it was verified. Our outputs are
**CC-BY-4.0** (catalog, crosswalks, rubric, docs); **MIT** (code).

**Child privacy (COPPA / FERPA / GDPR-K) — by construction, not by promise.** K-12 means children.
oer-everything therefore collects **no personal data of any kind**: no accounts, no logins, no
behavioral analytics, no advertising/third-party trackers, no cookies beyond strictly-necessary, no
contact forms that store data. The static, no-backend architecture means there is no server-side
collection surface at all. Because we collect nothing, COPPA/FERPA exposure is avoided by design.
Any future feature that would collect data is **out of scope** without a governance decision and a
privacy review. Cataloged third-party resources are labeled where we know they themselves collect
data, so teachers can choose accordingly.

**Content sensitivity & non-partisanship.** Some standards-aligned science content touches publicly
contested topics (e.g., evolution, climate science, human reproduction/health in some grade bands).
Policy: catalog **evidence-based, standards-aligned** material; remain **non-partisan**; **label**
sensitive-topic resources (`contentNotes`) so educators can apply local policy; never editorialize.
Anything that would constitute medical/legal/safety advice is out of scope (and would require the
`high` risk path, which this project does not take).

## Quality, review & risk gates

**Risk tier: low.** General open K-12 content with standard review. The genuine risk is *not*
technical — it is (a) admitting a mislabeled non-open resource, (b) reproducing license-restricted
standards text, (c) any child-data collection, or (d) inaccurate/grade-inappropriate content. The plan
front-loads gates for each.

**Required review before a resource is "in the library" (done):**
- **License + Provenance reviewer (mandatory, every resource):** confirms the license permits
  reuse+adaptation, records id/URL/snapshot, and confirms no license-restricted standards text is
  reproduced. **Hard, non-skippable gate.**
- **Educator / curriculum reviewer (mandatory, every resource):** confirms factual accuracy, correct
  grade band, pedagogical fit, readability, and bias/sensitivity; assigns the rubric score (admit only
  ≥ 80). Subject-matched (a math educator for math, etc.).
- **Accessibility reviewer (gate on the discovery surface; per-resource labeling):** confirms the site
  meets **WCAG 2.2 AA** and that resource accessibility metadata is recorded.
- **Technical reviewer:** confirms schema validity, link health + snapshot, GUID resolution, CI green.

**The quality rubric (scored, versioned).** Dimensions, each scored, summing to 100:
accuracy/correctness, standards-alignment fidelity, grade-band appropriateness, pedagogical
usefulness, clarity/readability, accessibility, and bias/sensitivity. The rubric is a committed,
versioned artifact (`rubricVersion`); the score and reviewer are stored per resource. Threshold to
admit: **≥ 80** with educator sign-off.

**Test fixtures / golden files (so "CI green" means something).** Validators ship committed
synthetic fixtures: known-valid `LearningResource` records that must pass and malformed ones that must
fail; GUID-resolution fixtures (valid + dangling); a license-field matrix (accepted vs excluded). No
real student data ever exists to fixture.

**Definition of Shipped.** A resource is *shipped* only when it is (1) license + provenance verified
with a committed gate artifact; (2) standards-aligned by GUID with provenance; (3) educator-approved at
rubric ≥ 80; (4) link-healthy with a snapshot reference; (5) live and findable on the WCAG-AA discovery
surface; and — for the **project's** delivered outcome — (6) the Steward has recorded at least one
**verified classroom adoption** for the library (per Success metrics). Cataloging is not shipped;
**a teacher teaching from it is.**

## Roadmap & milestones

**M0 — Foundation & cold-start (thin)**
- Goal: build the spine (schema, one standards framework, gate, rubric, protocol, thin site) and prove
  it end-to-end by ingesting the **live `oer-math` project** as the first content source.
- **Cold-start de-risking.** The pilot content source is **`oer-math`** — already a live Elyos
  project, so guaranteed openly-licensed content exists from day one; no third party must say yes for
  M0 to produce a real, findable, standards-aligned result. The CCSS Math framework is chosen first
  precisely to dovetail with `oer-math`.
- Exit criteria: (1) LearningResource metadata model + catalog format published; (2) standards
  registry stood up with **CCSS Math** imported (GUID-keyed); (3) license/provenance/IP gate +
  quality rubric exist and are applied to the first resources; (4) coordination protocol published and
  `oer-math` ingested end-to-end (≥ 5 resources cataloged, aligned, gate-passed, educator-approved,
  live on the thin site); (5) ≥ 1 educator reviewer and ≥ 1 license reviewer **named** (blocking roles
  filled before pilot review); (6) ≥ 1 beneficiary-outreach thread opened.

**M1 — Standards spine hardened + first reading coverage + first adoption**
- Goal: make standards import rigorous (CASE pipeline), add ELA/reading, reach AA accessibility, and
  land the first verified adoption.
- Exit criteria: (1) CASE 1.x import pipeline + GUID resolver with golden fixtures; (2) **CCSS ELA**
  added and a reading/decodable resource set crosswalked; (3) discovery site passes **WCAG 2.2 AA**
  (automated + manual audit, 0 AA violations on core flows); (4) ≥ 1 **verified classroom adoption**
  with evidence artifact; (5) standards-coverage report live (≥ 80% of the chosen CCSS Math band
  covered); (6) usability test run with ≥ 5 educators (≥ 80% task success).

**M2 — Multi-subject breadth (science + CS) & more libraries**
- Goal: extend to science and CS and onboard sibling libraries through the protocol.
- Exit criteria: (1) **NGSS** and **CSTA** frameworks added (with per-framework standards-IP terms
  recorded); (2) ≥ 2 *additional* subject libraries coordinated (e.g., `oer-science-labs`,
  `open-coding-curriculum`) — ≥ 2 cataloged resources each, gate-passed; (3) ≥ 4 subjects represented
  on the discovery site with working browse-by-standard; (4) client-side privacy-preserving search
  shipped; (5) ≥ 3 verified adoptions cumulatively.

**M3 — Coverage, reuse & sustainability**
- Goal: demonstrate breadth of coverage, real reuse, and a maintenance/governance model.
- Exit criteria: (1) standards-coverage targets met across ≥ 3 subjects (per the coverage report);
  (2) ≥ 3 verifiable external reuse events (forks/citations/embeds of crosswalks or collections);
  (3) link-rot/staleness + standards-version-drift refresh process documented and running;
  (4) inclusion/COI governance policy + steward model published; (5) ≥ 1 confirmed ongoing partner.

Dependencies: M1 depends on M0's schema + registry; M2's multi-subject work depends on M1's CASE
pipeline; M3 depends on a body of accepted, adopted resources from M1–M2. Coordination with
`oer-math` is a live dependency throughout (its content is the M0 proof and an ongoing source).

## Work breakdown

The itemized, schema-mapped backlog lives in `TASKS.md`, organized by the milestones above, each with
a task table (`ID | Title | Type | Size | Risk | Deliverable | Depends on | Reviewer`), acceptance
criteria for the most important tasks, and a milestone Definition of Done. A backlog of
sized-but-unscheduled tasks and one complete, schema-valid example Task JSON are included there. The
coordination protocol (how subject libraries submit) and the standards-IP matrix are the cross-cutting
artifacts that most tasks depend on.

## Governance, roles & stakeholders

- **Maintainer (Owner):** TBD — owns the schema, standards registry, validators, site, and backlog.
- **License + Provenance reviewer:** TBD (TO BE SECURED) — mandatory, **non-skippable** gatekeeper for
  every resource (license permits reuse+adaptation; no license-restricted standards text). Must be
  **filled before the M0 pilot is reviewed**. May rotate among ≥ 2 qualified reviewers, but ≥ 1 named
  reviewer must always exist or intake halts. Until named, all tasks stay `verifiedNeed:false`.
- **Educator / curriculum reviewer(s):** TBD (TO BE SECURED) — subject-matched practicing educators
  who verify accuracy, grade fit, and assign rubric scores. Also blocking before pilot review.
- **Accessibility reviewer:** TBD — owns WCAG 2.2 AA conformance of the discovery surface and
  resource accessibility labeling.
- **Technical reviewer(s):** rotation verifying schema validity, GUID resolution, link health, CI.
- **Steward (last-mile owner):** TBD — owns beneficiary relationships, confirms and records **verified
  classroom adoption** (the "delivered" signal). Critical because Definition of Shipped is adoption.
- **Subject-library liaisons:** named contacts for `oer-math` (first) and future libraries, who submit
  entries via the coordination protocol and own their content.
- **Partner / requestor:** TO BE SECURED — a named teacher/school/district/nonprofit beneficiary.

## Dependencies & integrations

- **External standards/specs (pinned — see Architecture):** schema.org/`LearningResource`, LRMI,
  1EdTech **CASE 1.x**, ASN GUIDs, WCAG **2.2 AA**. Versions recorded in `specVersions`; bumped only
  via a deliberate task.
- **Standards frameworks (each license-verified per the IP matrix):** CCSS Math, CCSS ELA, NGSS,
  CSTA K-12 CS; method documented for state frameworks.
- **Sibling Elyos projects (coordination, not dependency-injection):** `oer-math` (live; first
  content source + M0 proof), then `oer-science-labs`, `open-coding-curriculum`,
  `decodable-readers`/reading libraries; conceptual overlap with `curriculum-standards-map` (which may
  fold into this umbrella's standards registry — see Open questions).
- **External services:** none at runtime (static site; no backend). Build/CI only. Optional archival
  service (e.g., Wayback) for link snapshots.
- **Elyos pieces:** Task JSON schema (`packages/schema`), donated-lane CLI workspace/PR flow
  (`packages/cli`), good-deed definition + refusal guardrails. No funded-lane/runner dependency.

## Risks & mitigations

| Risk | Likelihood | Impact | Mitigation | Owner |
| --- | --- | --- | --- | --- |
| Admitting a mislabeled or non-open resource as "open" | Medium | High | Mandatory license reviewer; record license id+URL+snapshot; objective permits-reuse+adaptation criterion; exclude on any doubt | License+Provenance reviewer |
| Reproducing license-restricted standards text | Medium | High | Standards-IP matrix; default to codes+structure+link; per-framework license recorded before reproduction | License+Provenance reviewer |
| Any collection of student/teacher PII (COPPA/FERPA) | Low | High | No-backend, no-accounts, no-tracking architecture; data collection out of scope without governance + privacy review | Maintainer |
| Catalog produced but no teacher adopts it (fails "delivered") | High | High | M0 ingests live oer-math (guaranteed content); steward + outreach from M0; `verifiedNeed:false` until a beneficiary confirms | Steward |
| Inaccurate or grade-inappropriate content admitted | Medium | Medium | Mandatory subject-matched educator review; rubric ≥ 80 to admit; bias/sensitivity dimension | Educator reviewer |
| Link rot / cataloged resource disappears | High | Medium | Link-health checker in CI; archival snapshot reference per resource; refresh milestone (M3) | Maintainer |
| Inaccurate standards alignment (wrong standard) | Medium | Medium | Alignment claims carry rationale + verifiedBy; educator verifies alignment; GUID resolution checked | Educator reviewer |
| Scope creep into authoring/re-hosting content | Medium | Medium | Explicit non-goal; reviewers reject authoring; route to the subject library instead | Maintainer |
| Accessibility failures shut out disabled learners/teachers | Medium | Medium | WCAG 2.2 AA as a gate (automated + manual); accessibility reviewer role | Accessibility reviewer |
| Standards-framework version drift (CCSS/NGSS/CSTA updates) | Medium | Low | GUID-keyed registry; pinned versions; isolated version-bump task; drift detection | Maintainer |
| Sibling library abandoned/stale → dead links in umbrella | Medium | Medium | Coordination protocol defines liaison + update cadence; link-health flags stale entries to maintenance | Maintainer |
| Politicization of contested science topics | Low | Medium | Non-partisan, evidence-based, standards-aligned; label sensitive topics; no editorializing | Educator reviewer |

## Security & privacy

- **Threat surface is intentionally tiny.** No backend, no database, no user accounts, no runtime
  service — the discovery site is static HTML/JS/CSS served from a CDN/static host. The only surfaces
  are CI and the published static artifacts.
- **Child privacy by construction.** Because there is no collection surface, there is no student or
  teacher PII to leak. No analytics that identify users, no third-party trackers, no advertising, no
  cookies beyond strictly-necessary. This is a locked architectural constraint, not a policy that can
  silently erode.
- **Secrets handling.** Tooling needs no credentials by default. If an archival or standards API token
  is ever needed at build time, it is supplied via CI secrets and never written into logs, receipts,
  catalog records, or committed files (per Elyos rules).
- **Upstream content risk.** Cataloged third-party resources may themselves embed trackers or unsafe
  content; we label known data-collecting resources, exclude unsafe/inappropriate content via the
  educator gate, and never embed third-party scripts into our own pages.
- **Abuse/misuse prevention.** Refuse and flag any task that would launder non-open content as open,
  introduce user tracking, target/profile students or teachers, or push partisan/inaccurate material.
  The library stays descriptive, open, and standards-grounded.

## Sustainability & maintenance

- **Post-delivery ownership.** The maintainer keeps the schema, standards registry, validators, and
  site current with spec/framework versions; the steward maintains beneficiary relationships and the
  outcome ledger; subject-library liaisons keep their entries current via the protocol.
- **Refresh.** Link-health checks and standards-version-drift detection run in CI; stale entries
  become `maintenance` tasks. Standards updates are isolated version-bump tasks (GUID-keyed so
  alignments survive).
- **Outcome tracking.** The steward records verified adoptions and external reuse events against the
  success metrics each milestone; the standards-coverage report is the living view of beneficiary
  value (coverage gaps generate new alignment/authoring tasks — the latter routed to subject
  libraries, not authored here).
- **Low ongoing cost.** Static hosting is near-zero cost and high-longevity, suiting a public good
  meant to outlast any single maintainer.

## Open questions

- Which specific teacher/school/district/nonprofit will be the first confirmed adoption partner?
- Does the existing `curriculum-standards-map` roadmap project **merge into** oer-everything's
  standards registry, or remain a separate feeder? (Leaning: fold it in to avoid duplication.)
- For CCSS and CSTA specifically, do the published licenses permit reproducing full **statement text**,
  or must we use codes + links? (Default until verified: codes + links.)
- Exact division of ownership in the coordination protocol: does the subject library or the umbrella
  own the alignment claim and its maintenance?
- Internationalization: do we forward-design the schema for multilingual metadata and non-US
  frameworks now (recorded as a backlog), and which framework is the first non-US target?
- What is the canonical storage format for a resource link snapshot (committed copy + hash + Wayback
  URL, mirroring `open-data-datasheets`'s decided format)? (Leaning: adopt that decided format.)

## References

- Elyos work rules — `C:\code\elyos\CLAUDE.md`
- Good Deed Definition + risk tiers — `C:\code\elyos\docs\good-deed-definition.md`
- Task JSON schema — `C:\code\elyos\packages\schema\src\schemas.ts`
- Portfolio roadmap — `C:\code\elyos\planning\ROADMAP.md`
- Sibling project (first content source) — `oer-math` (live; seed task
  `registry\seed-tasks\oer-math\fractions-practice-set-001.json`)
- Convention exemplar — `C:\code\elyos\planning\projects\open-data-datasheets\{PLAN,TASKS}.md`
- schema.org/`LearningResource`; LRMI (Learning Resource Metadata Initiative)
- 1EdTech CASE 1.x; ASN (Achievement Standards Network) identifiers
- Standards frameworks: Common Core State Standards (Math, ELA); NGSS; CSTA K-12 CS Standards
- WCAG 2.2 (W3C) — Level AA
- Creative Commons CC0 / CC-BY 4.0 / CC-BY-SA license texts

---

## Appendix A — Improvements applied

The following 25 specific improvements were identified against the initial draft and **applied** in
the version above. Each line states the change and where it now lives.

1. **Headline outcome reframed to standards coverage, not resource count.** Success metrics now lead
   with "% of a target standard set with ≥ 1 verified aligned resource," explicitly rejecting raw
   counts as vanity. *(Success metrics)*
2. **Standards-IP nuance made explicit** — codes/structure as facts (always usable) vs. full statement
   text (license-gated per framework), with a per-framework matrix. *(Data, licensing & compliance)*
3. **Child-privacy by construction (COPPA/FERPA/GDPR-K)** — no-backend/no-accounts/no-tracking as a
   *locked architectural* guarantee, not a promise. *(Compliance; Security & privacy; Non-goals)*
4. **Per-channel "verified classroom adoption" definition + evidence artifact** added, so "delivered"
   is checkable. *(Success metrics; Definition of Shipped)*
5. **WCAG 2.2 AA promoted from aspiration to a gate** with automated + manual audit and a metric of 0
   AA violations on core flows. *(Metrics; Quality gates; Roadmap M1)*
6. **Cold-start de-risked by ingesting the live `oer-math` project** as the M0 content source — no
   third party must say yes for M0 to produce a real result. *(Roadmap M0; Risks)*
7. **Anti-duplication hardened** — "will not re-author/re-host content a subject library owns" stated
   as identity; coverage gaps route authoring to subject libraries, not here. *(Non-goals; Scope;
   Sustainability)*
8. **Coordination protocol elevated to a first-class artifact** (how subject libraries submit, who
   owns alignment), addressing the umbrella's core job. *(Scope; Architecture; Governance; Tasks)*
9. **Quality rubric made concrete and scored** (named dimensions, ≥ 80 threshold, versioned, stored
   per resource). *(Quality gates; Metrics)*
10. **Link-rot mitigation** added — CI link-health check + archival snapshot reference per resource +
    refresh milestone. *(Architecture; Metrics; Risks; Sustainability)*
11. **Spec versions pinned** (schema.org, LRMI, CASE 1.x, ASN, WCAG 2.2) with version-bump-as-task
    discipline. *(Architecture; Dependencies)*
12. **Sensitive-science-topics policy** — evidence-based, non-partisan, labeled — added to compliance
    and risks. *(Compliance; Risks)*
13. **Blocking reviewer roles must be filled before the M0 pilot is reviewed** (license + educator),
    not hired in parallel. *(Governance; Roadmap M0)*
14. **Outcome ledger** for adoptions + reuse events introduced and tied to the steward. *(Metrics;
    Sustainability)*
15. **Findability operationalized** as a task-based usability test with real educators (success rate,
    step count), repeated per milestone. *(Metrics; Roadmap M1/M2)*
16. **Grade-band + readability appropriateness checks** added to the rubric and the pipeline. *(Quality
    gates; Architecture; Risks)*
17. **Accessibility reviewer role** added to governance and the review chain. *(Governance; Quality
    gates)*
18. **Static + privacy-by-construction stack decision justified** (privacy + sustainability + tiny
    threat surface), with client-side search. *(Architecture; Security & privacy)*
19. **Per-resource provenance + per-alignment provenance** (who aligned it, how verified) added to the
    canonical model. *(Architecture; Compliance)*
20. **i18n / non-US frameworks forward-compatibility** raised as a deliberate schema concern and
    backlog item rather than ignored. *(Open questions; Tasks backlog)*
21. **Steward last-mile role** made explicit and tied to the delivered signal. *(Governance;
    Definition of Shipped)*
22. **Every risk has a named owner** and the table gained standards-IP, link-rot, accessibility,
    alignment-error, abandoned-library, and politicization rows. *(Risks)*
23. **Inclusion/COI governance policy** scheduled (M3) to decide what gets cataloged and avoid bias.
    *(Roadmap M3; Tasks)*
24. **Relationship to sibling roadmap projects clarified** — coordinates `oer-science-labs`/
    `open-coding-curriculum`/reading libraries; possible merge of `curriculum-standards-map`.
    *(Problem; Dependencies; Open questions)*
25. **Objective license acceptance criterion** (`permitsReuse` AND `permitsAdaptation` from cited
    evidence; no default-allow) + snapshot format aligned to the project's decided convention.
    *(Compliance; Open questions)*

---

## Review sign-off

Reviewed against the Elyos robustness bar (metrics, gates, risks, guardrails, sequencing, schema
validity). Findings and resolutions:

- **Measurable metrics?** Yes — every success metric has a baseline + 6-month target and a defined
  evidence source; the headline metric is a beneficiary outcome (standards coverage), and adoption is
  defined per channel with an evidence artifact. *Fixed during review:* added explicit tester counts
  (≥ 5 educators) and step-count thresholds to the findability metric.
- **Enforceable gates?** Yes — license/provenance, standards-IP, educator quality (≥ 80), and WCAG AA
  are blocking, with committed artifacts; reviewer roles must be filled before the M0 pilot review.
- **Risks with owners + mitigations?** Yes — 12-row table, each with likelihood, impact, mitigation,
  and a named owner; the top "no adoption" risk is mitigated structurally (M0 uses live `oer-math`).
- **License / PII / expert-review guardrails?** Yes — open/PD/CC-only with an objective permits-reuse+
  adaptation criterion; standards-IP matrix (codes always; text only where licensed); child privacy by
  construction (no data collection); educator (subject-matched) review mandatory; sensitive topics
  labeled, non-partisan; medical/legal/safety explicitly out of scope (no `high` path).
- **Sequencing?** Yes — M0 thin spine + live-content proof → M1 standards rigor + reading + AA + first
  adoption → M2 science/CS + more libraries → M3 coverage/reuse/sustainability; dependencies stated.
- **Schema-valid tasks?** Yes — `TASKS.md` maps every field to `packages/schema/src/schemas.ts`,
  includes a complete example Task JSON for the first M0 task, and honestly sets `verifiedNeed:false` /
  `requestor: TO BE SECURED` (no partner yet). *Fixed during review:* ensured every task's
  `deliverable` is one of `pr|document` (never `dataset`/`translation` except the backlog i18n task)
  and that funded budgets are absent (all tasks donated lane).
- **Honesty?** Partner/requestor and per-task delivery need are marked TO BE SECURED; the project's
  value is gated on real teacher adoption, not catalog size.

**Headline gate:** No resource enters the library without (a) a verified open license permitting reuse
**and** adaptation (no default-allow), (b) compliant standards-IP handling (codes always; text only
where licensed), and (c) subject-matched educator approval at rubric ≥ 80 — and the project's
*delivered* outcome requires a **verified classroom adoption**, not a published catalog.

**Sign-off:** Draft v0.1.0 complete; 25 improvements applied; review pass complete. Ready for
maintainer + reviewer staffing and beneficiary outreach. — Senior Staff Engineer + TPM (drafting)
