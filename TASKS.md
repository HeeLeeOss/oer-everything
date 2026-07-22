# TASKS — oer-everything

> Status: Draft · Version: 0.1.0 · Last updated: 2026-06-28 · Owner: TBD (maintainer) · Lane: donated

## How these tasks map to Hee-Lee Oss

Each task below becomes a Hee-Lee Oss **Task JSON** validated against
`packages/schema/src/schemas.ts`. Field mapping:

- `id` — stable slug ID from the tables (e.g. `oer-everything-schema-002`).
- `title` — the table's Title.
- `project` — `oer-everything`.
- `type` — one of `code | research | writing | data | design-spec | maintenance` (see each table).
- `lane` — `donated` for all tasks here (no funded escrow). A funded task would add `fundedBudgetUsd`.
- `priority` — `high | medium | low`.
- `domain` — array, e.g. `["education","oer","k12","standards"]`.
- `riskTier` — `low | medium | high`. This project is **low**; a couple of standards-IP / sensitive-
  content tasks are `medium` because they involve license/sensitivity judgement. No `high` tasks
  (no medical/legal/safety advice — those are out of scope).
- `urgent` — boolean; `false` for all current tasks.
- `deliverable` — `pr | dataset | document | translation`. We deliver `pr` (code: validators, site,
  pipelines) and `document` (schema, gate, rubric, crosswalks, protocols, reports). We never deliver
  `dataset` (we do not produce data). One backlog i18n task uses `translation`.
- `tokenEstimate` — `small | medium | large` (Size column).
- `status` — `open | in-progress | review | delivered | done`; all start `open`.
- `context`, `objective`, `acceptanceCriteria[]`, `resources[]`, `output` — per task.
- `requestor` — **TO BE SECURED** until a beneficiary (teacher/school/district/nonprofit) is confirmed.
- `verifiedNeed` — **`false`** until a named beneficiary confirms they will adopt the library
  (the macro-need is real; per-task delivery need is unproven).
- `outputLicense` — **`CC-BY-4.0`** for content/metadata/docs (schema, registry, crosswalks, rubric,
  protocol, reports); **`MIT`** for code (validators, pipelines, site).

---

## Milestone M0 — Foundation & cold-start

| ID | Title | Type | Size | Risk | Deliverable | Depends on | Reviewer |
| --- | --- | --- | --- | --- | --- | --- | --- |
| oer-everything-reviewer-001 | Name/secure License+Provenance reviewer and Educator reviewer (blocking, non-skippable gate roles) | research | small | low | document | — | Maintainer |
| oer-everything-schema-002 | Canonical LearningResource metadata model + catalog format (schema.org/LRMI) | design-spec | small | low | document | — | Technical |
| oer-everything-gate-003 | License + provenance + standards-IP triage checklist (blocking gate) | design-spec | small | medium | document | schema-002 | License+Provenance |
| oer-everything-rubric-004 | OER quality + grade-appropriateness rubric (scored, versioned) | writing | small | low | document | — | Educator |
| oer-everything-standards-005 | Standards registry model + import CCSS Math (CASE/ASN GUIDs) | code | medium | low | pr | schema-002 | Technical |
| oer-everything-coord-006 | Subject-library coordination/contribution protocol | design-spec | small | low | document | schema-002 | Maintainer |
| oer-everything-validate-007 | Catalog validators (schema, link/archival, license-field, GUID resolution) | code | medium | low | pr | schema-002, standards-005 | Technical |
| oer-everything-site-008 | Thin static discovery site (browse grade/subject/standard, no tracking) | code | medium | low | pr | schema-002, standards-005 | Technical, Accessibility |
| oer-everything-pilot-009 | Ingest oer-math end-to-end (catalog + crosswalk + gate + admit) | data | medium | low | document | schema-002, gate-003, rubric-004, standards-005, coord-006, validate-007, reviewer-001 | License+Provenance, Educator |
| oer-everything-outreach-010 | Beneficiary outreach + adoption-path shortlist | research | small | low | document | — | Steward |

**Acceptance criteria — key tasks**

- **schema-002 (canonical metadata model + catalog format)**
  - [ ] Canonical `LearningResource` model documents every field from PLAN: id, title, description,
        url, author/provider, `license {id,url,permitsReuse,permitsAdaptation,attribution,snapshotRef}`,
        `provenance {retrievedAt,version,sourceLibrary,addedBy}`, educationalLevel/gradeBand, subject,
        learningResourceType, `educationalAlignment[] {framework,standardGuid,standardCode,
        alignmentType,rationale,verifiedBy}`, accessibility, language, `qualityScore`, `linkHealth`,
        `specVersions {schemaOrg,lrmi,case,asn}`.
  - [ ] Catalog format is version-controlled JSON-LD; a filled worked-example record is included.
  - [ ] Explicitly states the deliverable is metadata/links, not re-hosted content; output CC-BY-4.0.
  - [ ] Pinned spec versions recorded; i18n/multilingual fields noted as forward-compatible (backlog).

- **gate-003 (license + provenance + standards-IP gate)**
  - [ ] Objective license criterion: PASS only if `permitsReuse:true` AND `permitsAdaptation:true` are
        set from a cited license id/URL; missing/unparseable = FLAG/EXCLUDE (no default-allow).
  - [ ] Accepted set (PD/CC0/CC-BY/compatible CC-BY-SA via the SA policy; open code licenses);
        excluded set (ND, incompatible NC, all-rights-reserved, unclear, paywall/login) enumerated.
  - [ ] Requires recording license id+URL+snapshot reference (committed copy + SHA-256 + Wayback URL,
        per the project's decided format) and the attribution string.
  - [ ] Standards-IP section: codes/structure always permitted; full statement text only where the
        framework license is verified to allow it (per-framework `frameworkLicense` recorded);
        default = codes + structure + link.
  - [ ] Produces a committed PASS/FLAG/EXCLUDE artifact per resource recording which checks ran.

- **standards-005 (standards registry + CCSS Math import)**
  - [ ] Registry stores per standard: guid, framework, code, gradeBand, parent, frameworkLicense,
        sourceUrl, version, and `statementText` only if the framework license permits.
  - [ ] CCSS Math imported and GUID-keyed (CASE/ASN); GUIDs resolve; a coverage query is possible.
  - [ ] `frameworkLicense` for CCSS Math recorded with cited terms (text reproduced only if permitted).
  - [ ] Code MIT-licensed; golden fixtures (valid + dangling GUID) in CI; `pnpm build && pnpm test &&
        pnpm lint` green; DCO signed-off.

- **pilot-009 (ingest oer-math end-to-end)**
  - [ ] ≥ 5 oer-math resources cataloged with full canonical records, each gate-passed (license
        verified, snapshot recorded) with a committed gate artifact.
  - [ ] Each resource aligned to ≥ 1 CCSS Math standard by GUID with rationale + verifiedBy.
  - [ ] Each resource educator-reviewed at rubric ≥ 80 with reviewer recorded; validators green in CI.
  - [ ] Resources live and findable on the thin discovery site under grade/subject/standard.
  - [ ] Coordination protocol exercised (oer-math submitted via coord-006); ownership of alignment
        recorded.
  - [ ] `verifiedNeed` stays `false` until a beneficiary confirms adoption; blocker surfaced if none.

**M0 Definition of Done:** License+Provenance and Educator reviewers named (blocking roles filled
before pilot review); metadata model + catalog format + license/IP gate + quality rubric + coordination
protocol published; standards registry stood up with CCSS Math (GUID-keyed) and validators green in CI
with golden fixtures; oer-math ingested end-to-end (≥ 5 resources cataloged, aligned, gate-passed,
educator-approved, live on the thin site); ≥ 1 beneficiary-outreach thread opened.

---

## Milestone M1 — Standards spine hardened + reading coverage + first adoption

| ID | Title | Type | Size | Risk | Deliverable | Depends on | Reviewer |
| --- | --- | --- | --- | --- | --- | --- | --- |
| oer-everything-case-011 | CASE 1.x import pipeline + GUID resolver | code | medium | low | pr | standards-005 | Technical |
| oer-everything-ela-012 | Add CCSS ELA framework + crosswalk a reading/decodable resource set | data | medium | low | document | case-011, gate-003, rubric-004 | License+Provenance, Educator |
| oer-everything-a11y-013 | WCAG 2.2 AA conformance + audit of the discovery site | code | small | medium | pr | site-008 | Accessibility |
| oer-everything-adopt-014 | Land + verify first classroom adoption (record evidence artifact) | research | small | low | document | pilot-009, outreach-010 | Steward |
| oer-everything-coverage-015 | Standards-coverage report + gap finder | code | small | low | pr | standards-005, validate-007 | Technical |
| oer-everything-usability-016 | Task-based findability usability test with ≥ 5 educators | research | small | low | document | site-008, pilot-009 | Educator, Steward |

**Acceptance criteria — key tasks**

- **case-011 (CASE pipeline + GUID resolver)**
  - [ ] Imports a CASE 1.x package into the registry, preserving GUIDs, hierarchy, and version.
  - [ ] GUID resolver maps codes ↔ GUIDs; golden fixtures (valid package + malformed + dangling GUID)
        exercised in CI; pinned CASE version recorded in `specVersions`.
  - [ ] Code MIT-licensed; no credentials embedded; CI green; DCO signed-off.

- **a11y-013 (WCAG 2.2 AA)**
  - [ ] Automated audit (axe/Lighthouse) reports 0 AA violations on core browse + landing flows.
  - [ ] Manual audit (keyboard nav, screen reader, contrast, focus order) documented with results.
  - [ ] Resource accessibility metadata (LRMI `accessibilityFeature`) surfaced on the site.

- **adopt-014 (first verified adoption)**
  - [ ] A named teacher/program confirms they taught from a library resource; evidence artifact
        (`outcomes/<adoption-id>.json`) committed with channel, resource/standard IDs, date, reference.
  - [ ] The relevant tasks/resources updated to `verifiedNeed: true` with `requestor` set.
  - [ ] Outcome recorded against the success metric (≥ 1 verified adoption).

- **coverage-015 (coverage report + gap finder)**
  - [ ] Computes % of a target standard band with ≥ 1 admitted, license-verified, educator-approved
        aligned resource; reports gaps as a list.
  - [ ] Gaps generate alignment tasks (or are routed to subject libraries for authoring — never
        authored in this repo); report regenerates in CI.

**M1 Definition of Done:** CASE 1.x pipeline + GUID resolver green with golden fixtures; CCSS ELA added
and a reading/decodable resource set crosswalked + admitted; discovery site passes WCAG 2.2 AA (0
violations on core flows, manual audit recorded); ≥ 1 verified classroom adoption with evidence
artifact; coverage report live showing ≥ 80% of the chosen CCSS Math band covered; usability test run
with ≥ 5 educators at ≥ 80% task success.

---

## Milestone M2 — Multi-subject breadth (science + CS) & more libraries

| ID | Title | Type | Size | Risk | Deliverable | Depends on | Reviewer |
| --- | --- | --- | --- | --- | --- | --- | --- |
| oer-everything-ngss-017 | Add NGSS framework + onboard oer-science-labs (≥ 2 resources) | data | large | medium | document | case-011, gate-003, coord-006 | License+Provenance, Educator |
| oer-everything-csta-018 | Add CSTA K-12 CS framework + onboard open-coding-curriculum (≥ 2 resources) | data | medium | low | document | case-011, gate-003, coord-006 | License+Provenance, Educator |
| oer-everything-search-019 | Client-side privacy-preserving search/discovery (no tracking) | code | medium | low | pr | site-008 | Technical, Accessibility |

**Acceptance criteria — key tasks**

- **ngss-017 (NGSS + science library)** *(pattern also applies to csta-018)*
  - [ ] NGSS framework imported via CASE pipeline, GUID-keyed; `frameworkLicense` recorded with cited
        terms; statement text reproduced only if the license permits, else codes + link.
  - [ ] ≥ 2 oer-science-labs resources cataloged via the coordination protocol, gate-passed (license
        verified, snapshot recorded), aligned to NGSS by GUID, educator-approved at rubric ≥ 80.
  - [ ] Sensitive-topic resources (e.g., evolution/climate/health) labeled with `contentNotes`;
        non-partisan, evidence-based, no editorializing. (`riskTier: medium` for the sensitivity
        judgement.)
  - [ ] Resources live and findable; validators green in CI.

- **search-019 (privacy-preserving search)**
  - [ ] Search is fully client-side over a prebuilt static index; no query leaves the browser; no
        analytics/trackers introduced.
  - [ ] Search results filterable by grade/subject/standard; accessible (keyboard + screen reader).

**M2 Definition of Done:** NGSS + CSTA frameworks added with per-framework standards-IP terms recorded;
≥ 2 additional subject libraries coordinated (≥ 2 gate-passed resources each); ≥ 4 subjects represented
on the site with working browse-by-standard; privacy-preserving client-side search shipped; ≥ 3 verified
adoptions cumulatively.

---

## Milestone M3 — Coverage, reuse & sustainability

| ID | Title | Type | Size | Risk | Deliverable | Depends on | Reviewer |
| --- | --- | --- | --- | --- | --- | --- | --- |
| oer-everything-reuse-020 | Track + verify external reuse events (forks/citations/embeds) | research | small | low | document | adopt-014, coverage-015 | Steward |
| oer-everything-refresh-021 | Link-rot/staleness + standards-version-drift refresh process | maintenance | small | low | document | validate-007, standards-005 | Maintainer |
| oer-everything-governance-022 | Inclusion policy, COI checklist + multi-subject governance/steward model | design-spec | small | low | document | coord-006 | Maintainer, Steward |

**Acceptance criteria — key tasks**

- **reuse-020 (reuse tracking)**
  - [ ] ≥ 3 verifiable external reuse events recorded in the outcome ledger (fork/citation/embed of a
        crosswalk or collection), each linked to externally verifiable evidence (no self-reported).

- **refresh-021 (refresh process)**
  - [ ] Documented process: CI link-health checker flags dead/changed resource links; stale entries
        become `maintenance` tasks; archival snapshots referenced.
  - [ ] Standards-version-drift detection: registry flags when a framework version changes; bumps are
        isolated tasks (GUID-keyed so alignments survive).

- **governance-022 (governance + inclusion policy)**
  - [ ] Inclusion policy defines what is cataloged (open-only, standards-aligned, accurate) and what is
        rejected; COI checklist for reviewers; steward model for multi-subject coordination.

**M3 Definition of Done:** standards-coverage targets met across ≥ 3 subjects; ≥ 3 verifiable external
reuse events; link-rot + standards-drift refresh process documented and running; inclusion/COI
governance + steward model published; ≥ 1 confirmed ongoing partner.

---

## Backlog / future

| ID | Title | Type | Size | Risk | Deliverable | Notes |
| --- | --- | --- | --- | --- | --- | --- |
| oer-everything-state-023 | State-standards crosswalk pack (one US state) | data | large | medium | document | Verify state framework license first (default: codes + link) |
| oer-everything-i18n-024 | Translate catalog metadata + UI strings (one language) | translation | medium | medium | translation | Needs language reviewer; schema forward-designed for i18n |
| oer-everything-case-export-025 | CASE/OpenSALT export of the standards registry | code | medium | low | pr | Interop for external standards consumers |
| oer-everything-collections-026 | Teacher "collections" (curated standard→resource sets), static | code | medium | low | pr | No accounts; collections are static, shareable URLs |
| oer-everything-offline-027 | Offline/printable bundle of a grade-band's resources | code | medium | low | pr | For low-connectivity classrooms |
| oer-everything-reading-lib-028 | Onboard a reading/decodable subject library beyond ELA pilot | data | medium | low | document | Extends coordinated libraries |
| oer-everything-csmap-merge-029 | Evaluate folding curriculum-standards-map into the registry | research | small | low | document | Avoid duplicate standards work (Open question) |

---

## Example task JSON

```json
{
  "id": "oer-everything-reviewer-001",
  "title": "Name/secure License+Provenance reviewer and Educator reviewer (blocking gate roles)",
  "project": "oer-everything",
  "type": "research",
  "lane": "donated",
  "priority": "high",
  "domain": ["education", "oer", "k12", "governance"],
  "riskTier": "low",
  "urgent": false,
  "deliverable": "document",
  "tokenEstimate": "small",
  "status": "open",
  "context": "oer-everything is an umbrella that catalogs and standards-aligns openly-licensed K-12 resources; it does not re-author content. Two reviews are non-skippable, blocking gates before any resource enters the library: a License+Provenance reviewer (confirms the resource license permits reuse AND adaptation, records id/URL/snapshot, and ensures no license-restricted standards text is reproduced) and a subject-matched Educator/curriculum reviewer (confirms accuracy, grade band, and assigns the rubric score). These roles must be filled before the M0 pilot (ingesting oer-math) is reviewed, or intake halts.",
  "objective": "Identify and secure at least one named, qualified License+Provenance reviewer and at least one named Educator/curriculum reviewer, and record their appointment (name + qualification) so the M0 pilot can be reviewed.",
  "acceptanceCriteria": [
    "At least one named License+Provenance reviewer who can read open licenses (CC0/CC-BY/CC-BY-SA/PD, open code licenses) and apply the standards-IP matrix is recorded with qualifications.",
    "At least one named, subject-matched Educator/curriculum reviewer (math first, to match the oer-math pilot) is recorded with qualifications.",
    "The appointment is documented in PLAN.md Governance, with a rotation note (>= 2 reviewers preferred) and a 'no named reviewer => intake halts' rule.",
    "Until reviewers are named, all tasks remain verifiedNeed:false and no resource passes the gate; this state is recorded.",
    "Deliverable is a governance document; output licensed CC-BY-4.0."
  ],
  "resources": [
    "C:\\code\\hee-lee-oss\\planning\\projects\\oer-everything\\PLAN.md",
    "C:\\code\\hee-lee-oss\\docs\\good-deed-definition.md",
    "oer-math (live sibling project; first content source)"
  ],
  "output": "A governance document naming the License+Provenance and Educator reviewers (with qualifications and rotation policy), committed to the project repo, enabling the M0 pilot review.",
  "requestor": "TO BE SECURED",
  "verifiedNeed": false,
  "outputLicense": "CC-BY-4.0"
}
```
