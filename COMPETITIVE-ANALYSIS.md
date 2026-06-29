# Competitive + Improvement Analysis — `oer-everything`

> Scope: Elyos good-deed project that aims to build the **umbrella / coordination layer** (shared
> LRMI metadata model, standards registry with CASE/ASN GUIDs, resource→standard crosswalk, a
> license/provenance gate, an educator-scored quality rubric, and a privacy-first static discovery
> site) over openly-licensed K-12 educational content — *coordinating* sibling Elyos authoring
> projects (`oer-math` live; `oer-science-labs`, `open-coding-curriculum`, reading libraries) rather
> than authoring content itself.
> Guardrails: open license (CC/PD only), accuracy, educator review, accessibility, standards-alignment.
> Sources are cited inline; this analysis is grounded in web research (June 2026).

---

## 1. Correctness & completeness review of PLAN.md

The plan is unusually mature for a v0.1 draft: it already absorbed 25 self-identified improvements and
has enforceable gates, named risk owners, an honest `verifiedNeed:false` posture, and an outcome
("delivered, not merged") rather than a vanity ("resources cataloged") headline metric. The single
most important architectural decision — **reframing "OER for everything" from an authoring effort into
a coordination/metadata spine** — is correct and is what makes the project tractable at all. Findings,
roughly in priority order:

**(a) Scope realism — the central risk, only partly mitigated.** The reframe to "umbrella, not
content" is the right move, but the *committed surface area is still very large for a 6-month,
donated-labor effort*: four standards frameworks (CCSS Math, CCSS ELA, NGSS, CSTA) plus a "method for
state frameworks," a CASE 1.x import pipeline + GUID resolver, a metadata model, validators, a static
site with privacy-preserving search, a WCAG 2.2 AA audit, a coordination protocol, and a quality
rubric — across M0-M2. The plan wisely narrows the *headline metric* to one band of CCSS Math, but the
roadmap text does not similarly narrow the *build*. Recommendation: make M0/M1 ruthlessly single-track
(CCSS Math only, `oer-math` only) explicit in the roadmap, and demote ELA/NGSS/CSTA to "schema must
not preclude" rather than "ship in 6 months."

**(b) The true throughput limiter is educator review, and it is under-quantified.** Every resource
needs a subject-matched educator at rubric ≥ 80 *plus* a license/provenance reviewer — both roles are
"TBD / TO BE SECURED" volunteers, and the plan says intake *halts* if the single named license
reviewer disappears. Standards coverage of even one CCSS Math grade band (~30-40 standards × ≥1
educator-approved aligned resource) is gated on volunteer educator-hours that are never estimated. No
per-resource review-time budget, no reviewer-capacity model, no batching strategy. This is the most
likely cause of M0/M1 slippage and deserves an explicit estimate and a recruiting plan, not just a
role placeholder.

**(c) Not-duplicating existing OER — handled for *content*, missed for the *function*.** The plan
guards hard against duplicating *content* (won't re-author/re-host). But its **core function** —
LRMI metadata + Common Core alignment + a quality rubric + a discovery site — is substantially what
**OER Commons** has done since 2007 (100,000+ resources, 350+ providers, 5M users, all resources
LRMI-mapped, an embedded Common Core alignment tool, and the Achieve OER rubric) [OER Commons /
ISKME](https://www.iskme.org/iskme-receives-award-honoring-oer-commons-best-website-teaching-and-learning/),
[LRMI case study](https://lornamcampbell.wordpress.com/2014/10/03/lrmi-implementation-case-study-iskme-oer-commons/).
The plan never names OER Commons as the incumbent it most overlaps with, nor articulates why a teacher
would use this over it. The differentiator must be sharper than "findability" (see §4).

**(d) The `permitsAdaptation:true` gate is correct in principle but will exclude the most-used
resources.** Requiring reuse **and** adaptation excludes, by design: MIT OCW (CC BY-**NC**-SA, 2,500+
courses) [MIT OCW](https://ocw.mit.edu/), Siyavula's *branded* CC-BY-**ND** textbooks (which the South
African DBE printed ~10M copies of) [Siyavula](https://www.siyavula.com/read), and essentially all of
Khan Academy (proprietary). This is defensible for a purist open library, but it means the catalog
*omits* several resources teachers most want. Consider a labeled second tier ("free to use, not
adaptable") that is surfaced-but-flagged rather than excluded — or at least document the trade-off so
it is a decision, not an accident.

**(e) Standards-IP stance is *over*-conservative for CCSS and NGSS.** The plan defaults to "codes +
link only, never paste standards text until verified." Research shows that default is stricter than
the actual licenses: the **CCSS public license** grants a royalty-free license to copy/publish/display
the standards provided the © notice is included (and adopting states are exempt)
[CCSS public license](https://www.thecorestandards.org/public-license/); **NGSS** explicitly lets
states, districts, schools, teachers and non-profits "copy, reproduce, alter, adapt, edit... without
permission" [NGSS copyright](https://www.nextgenscience.org/ngss-trademarks-and-copyright/ngss-trademarks-and-copyright).
So for CCSS and NGSS the registry *can* store statement text (with the required notice) — which
materially improves teacher UX (they want to see the standard, not just a code). Keep the conservative
default for state/CSTA frameworks; relax it for the two frameworks whose terms are now verified.

**(f) Avoiding low-quality AI content — guardrail is sound and well-motivated.** The "no
auto-publish, every resource educator-reviewed, no AI-authored content admitted unreviewed" stance is
correct and timely: recent studies find ~53% of studied AI errors in educational settings are
hallucinations, with factual incorrectness the single largest category
[AI hallucinations in education](https://www.researchgate.net/publication/398611293_The_Impact_of_AI-Generated_Hallucinations_in_Educational_Settings_Trends_Gaps_and_Future_Directions).
The plan should state explicitly that *AI-assisted metadata/tagging is allowed but AI-asserted
accuracy/alignment/license claims are not authoritative until a human verifies* (see §5).

**(g) Discoverability / LRMI / metadata — well chosen, but interop is the real prize.** schema.org
`LearningResource` + LRMI + CASE/ASN GUIDs is exactly the right stack and is shared with OER Commons,
LRMI adopters, and OpenSALT/CASE consumers. The plan's strongest, least-duplicative idea is the
**machine-readable, GUID-stable crosswalk as a consumable artifact** (others can ingest it) — but this
is buried; it should be elevated from "we have a discovery site" to "we publish an open, versioned
crosswalk dataset other tools can consume."

**(h) Accessibility — correctly promoted to a gate** (WCAG 2.2 AA, automated + manual, 0 AA
violations on core flows). Good. One gap: the plan gates *its own site* to AA but only *labels*
resource accessibility (LRMI `accessibilityFeature`) — it does not require cataloged resources to meet
any accessibility floor. That is a reasonable scoping choice but should be stated as one (the umbrella
is accessible; the linked resource may not be).

**(i) Sustainability — strong.** Static hosting (near-zero cost, high longevity), link-health + drift
detection in CI, GUID-keyed registry so alignments survive renumbering, an outcome ledger, and a
steward role. The realistic risk is **maintainer/reviewer bus-factor**, not hosting cost: the whole
thing depends on a tiny set of unnamed volunteers. The governance/COI policy is deferred to M3, which
is late given reviewers are blocking from M0.

**(j) Completeness nits.** "Verified classroom adoption ≥ 3 in 6 months" with *no partner secured* and
`verifiedNeed:false` is honest but high-risk — adoption, not catalog size, is the Definition of
Shipped, yet outreach is a single small M0 task. Findability target (≥80% task success, ≤3 steps, ≥5
educators) is good and testable. The plan is internally consistent and schema-mapped.

---

## 2. Competitive landscape

The K-12/OER space is crowded; almost no one solves *cross-repository, standards-keyed, license-verified
findability* well — but several solve large parts of it. Strengths/weaknesses relative to
`oer-everything`:

**OER Commons (ISKME)** — *the closest incumbent.* 100,000+ resources from 350+ providers, 5M users,
**all resources LRMI-mapped**, an embedded **Common Core alignment** tool, and the **Achieve OER
rubric** for quality
[ISKME](https://www.iskme.org/iskme-receives-award-honoring-oer-commons-best-website-teaching-and-learning/),
[case study](https://lornamcampbell.wordpress.com/2014/10/03/lrmi-implementation-case-study-iskme-oer-commons/),
[Achieve rubrics](https://help.oercommons.org/support/solutions/articles/42000046874-use-the-achieve-rubrics).
*Strengths:* exactly the metadata+alignment+rubric+discovery stack `oer-everything` proposes, at
scale, for ~20 years. *Weaknesses:* a hosted platform with accounts; alignment is crowd-sourced and
uneven; **license labeling is not rigorously verified** (mixed/unclear licenses appear); not a
machine-consumable GUID crosswalk; not privacy-by-construction.

**OpenStax (Rice)** — 80+ peer-reviewed open textbooks, **43.3M learners, 169 countries, 72% of U.S.
colleges**, K-12 use ~1.7M students, **~$3.4B** cumulative student savings
[Rice News 2025](https://news.rice.edu/news/2025/openstax-surpasses-3b-student-savings-grows-beyond-textbooks),
[AVDF](https://www.avdf.org/news/openstax-textbooks-transforms-access-and-affordability-in-higher-ed/).
*Strengths:* gold-standard accuracy/peer review, CC-BY, brand trust. *Weaknesses:* whole *textbooks*,
mostly higher-ed; **not granular standards-aligned discovery**; you can't browse to "the standard I
teach Tuesday." A *content source* to catalog, not a competitor to the spine.

**Khan Academy** — math 2nd-grade-PreCalc aligned to Common Core and mapped to most state standards,
plus new Common-Core ELA; strong practice + mastery
[Khan standards alignment](https://support.khanacademy.org/hc/en-us/articles/16758363457805-Is-Khan-Academy-math-content-aligned-to-Common-Core-or-other-U-S-state-standards),
[Khan Common Core map](https://www.khanacademy.org/commoncore/). *Strengths:* best-in-class
standards-aligned practice, huge reach. *Weaknesses:* **proprietary, not openly licensed** — fails the
adaptation gate; can't be cataloged as OER. A reference for what "aligned practice" should feel like.

**CK-12 Foundation** — free, openly-licensed FlexBooks aligned to Common Core + NGSS, 200,000+
customizable books, adaptive practice and simulations, no premium tier
[CK-12](https://www.ck12.org/), [CK-12 standards](https://help.ck12.org/hc/en-us/articles/200344205-Do-FlexBook-Textbooks-Adhere-to-State-and-National-K-12-Standards).
*Strengths:* free, standards-aligned, K-12, remixable, practice included. *Weaknesses:* a single
walled garden (its own content/platform), not a cross-repository index; accounts/analytics.

**LibreTexts** — 16 libraries, **100M+ pageviews/yr**, chemistry ~75% of traffic; higher-ed focus
[LibreTexts/ConfChem](https://confchem.ccce.divched.org/2020CCCENLP5),
[Statistics LibreTexts](https://stats.libretexts.org/). *Strengths:* huge remixable open corpus,
strong in college STEM. *Weaknesses:* higher-ed, uneven subject coverage, not K-12 standards-keyed.

**MIT OpenCourseWare** — 2,500+ courses, **CC BY-NC-SA** [MIT OCW](https://ocw.mit.edu/).
*Strengths:* prestige, breadth. *Weaknesses:* **NC license fails the adaptation/commercial gate**;
university-level; not K-12 standards-aligned.

**Siyavula** — CC-BY/CC-BY-ND math & science textbooks; **DBE printed ~10M copies**, 800k+ monthly
online readers, adaptive practice [Siyavula](https://www.siyavula.com/read),
[Siyavula Foundation](https://www.siyavulafoundation.org/). *Strengths:* proven last-mile delivery to
under-resourced learners — a *model* for `oer-everything`'s "delivered" bar; localized to a national
curriculum. *Weaknesses:* single-country (South African CAPS) and two subjects; branded version is ND.

**Saylor Academy** — ~100 full college courses, mostly **CC-BY** [Saylor](https://www.saylor.org/).
**Curriki** — K-12 CC-licensed, peer-reviewed community content + CurrikiStudio authoring
[Curriki](https://www.curriki.org/). **MERLOT (CSU)** — 40,000+ **peer-reviewed** OER since 1997
[MERLOT](https://www.merlot.org/). All three: *strengths* in curation/peer-review; *weaknesses* —
aging UX, weak granular K-12 standards keying, variable license rigor.

**UNESCO OER Recommendation (2019) + Dynamic Coalition** — normative global framework; one of its five
action areas is precisely *discoverability/quality of OER*
[UNESCO OER Recommendation](https://oerdynamiccoalition.org/resources/2019-unesco-recommendation-open-educational-resources-oer-supporting-universal-access).
*Strengths:* legitimizes the mission, potential alignment/partner channel. *Weaknesses:* policy, not a
product — a tailwind, not a competitor.

**Wikimedia / Wikiversity** — CC-BY-SA open content. *Strengths:* free, vast. *Weaknesses:* uneven
quality, no standards alignment, no review gate — a low-bar reference point.

**Standards-alignment hubs (Achieve/EQuIP, 1EdTech CASE/OpenSALT)** — not content libraries but the
machine-readable standards rails `oer-everything` should ride. Reusing CASE/ASN here is correct.

---

## 3. Gaps we can fill (where existing OER is genuinely thin)

1. **Verified, machine-readable license+provenance.** Across OER Commons / MERLOT / Wikiversity,
   licenses are inconsistently labeled and rarely *verified* with a snapshot. A gate that records
   `permitsReuse`/`permitsAdaptation` from a cited license id/URL + SHA-256 + Wayback snapshot is a
   real, currently-missing trust layer.
2. **GUID-stable, consumable crosswalk (not a destination site).** Existing alignment lives *inside*
   platforms. A published, versioned, CASE/ASN-keyed crosswalk that *other* tools can ingest is thin
   to nonexistent and is the most defensible asset.
3. **Cross-repository granular standards browse.** "Grade → subject → exact standard → a vetted free
   resource" *across* sources (not within one walled garden) is what teachers ask for and what's
   fragmented today.
4. **Privacy-by-construction discovery for children's contexts.** Most platforms use accounts +
   analytics; a no-backend, no-tracking surface that sidesteps COPPA/FERPA by design is differentiated.
5. **Under-served subjects, grade bands, and languages.** Higher-ed STEM is saturated (LibreTexts,
   OpenStax); **K-12 elementary, ELA/decodable reading, CS (CSTA), and non-English/non-US frameworks**
   are comparatively thin. Siyavula proves localized national-curriculum delivery works but covers one
   country/two subjects.
6. **Standards *coverage gaps* as a routing signal.** Nobody publishes "here is the standard with *no*
   good open resource." That gap report is both a beneficiary tool and a work-router to sibling
   authoring projects.
7. **Link-rot / staleness hygiene.** OER directories are full of dead links; CI link-health + archival
   snapshots is mundane but genuinely missing.

---

## 4. Differentiators to win (don't recreate OpenStax — or OER Commons)

The honest competitive truth: the *discovery-site* part substantially duplicates OER Commons. To win,
lead with what OER Commons and the walled gardens structurally do **not** do:

1. **A verifiable license/provenance gate as the product, not a checkbox.** "Every resource here has a
   cited, snapshotted, machine-checkable open license permitting reuse+adaptation" — a trust guarantee
   incumbents can't make. Make this the headline.
2. **Interoperable GUID crosswalk as an open dataset (the moat).** Position `oer-everything` as the
   *rails* (a CASE/ASN-keyed, versioned crosswalk other tools consume), not another destination.
   Reuse beats traffic: M3 already counts "external reuse events" — make that the north star.
3. **Coordination of sibling authoring projects.** No competitor sits over a *family* of open
   authoring shops with one schema + protocol; turning standards-coverage gaps into authoring tasks
   routed to `oer-math`/`oer-science-labs`/etc. is a unique closed loop.
4. **Privacy-by-construction.** A zero-data-collection, static, account-free surface is a real
   differentiator in a children's-data-sensitive market.
5. **Last-mile delivery discipline ("delivered, not merged").** Siyavula shows delivery to
   under-resourced classrooms is the win that matters; the steward + verified-adoption bar
   operationalizes it where most OER directories stop at "published."
6. **Gap-filling + localization, not breadth.** Compete where OER is thin (elementary, ELA/decodable,
   CS, non-US frameworks), not where OpenStax/LibreTexts are strong.

---

## 5. Claude API leverage — and the hard limits

**Where Claude adds leverage (assistive, human-verified):**
- **Metadata drafting & LRMI tagging at scale.** Draft `LearningResource` records — title,
  description, `learningResourceType`, `educationalLevel/gradeBand`, `accessibilityFeature` labels,
  candidate subject tags — from a resource URL, for human acceptance.
- **Candidate standards-alignment suggestions.** Propose `educationalAlignment[]` GUID matches with a
  rationale string, as a *first-pass* that an educator confirms/rejects (the rationale + `verifiedBy`
  fields are designed exactly for this human-in-the-loop pattern).
- **License/provenance triage assistant.** Extract and *quote* the license statement from a source
  page, flag NC/ND/unclear, pre-fill `permitsReuse`/`permitsAdaptation` *as a draft* with the exact
  cited text — speeding the human reviewer, never replacing the gate.
- **Accessibility uplift.** Generate alt-text candidates, plain-language summaries, and reading-level
  estimates for the discovery surface; check copy against WCAG-friendly patterns.
- **Leveling, adapting, and translation drafts** of *openly-licensed* content (grade-band re-leveling,
  multilingual metadata) — routed to the owning subject library for review, never published unreviewed.
- **Coverage-gap synthesis & coordination glue.** Summarize "standards with no/weak resource," draft
  the coordination-protocol intake, normalize incoming submissions to the canonical model.
- **Link-rot/drift triage.** Summarize what changed when a snapshot diverges from a live URL.

**Where Claude must NOT decide (guardrails — must stay human-owned):**
- **Factual/pedagogical accuracy and grade-appropriateness** — the rubric ≥ 80 sign-off is a
  *subject-matched educator's*; AI accuracy claims are not authoritative (hallucination evidence above).
- **Final standards-alignment** — Claude *suggests*, an educator *verifies*; an unverified AI
  alignment must never be admitted (`alignmentType`/`verifiedBy` must name a human).
- **License determination** — the `permitsReuse`+`permitsAdaptation` PASS is a human license
  reviewer's call from cited evidence; **no AI default-allow, no "best-guess."**
- **No AI-authored educational content admitted as a resource** — the umbrella catalogs others' vetted
  content; it does not launder AI-generated material into the library.
- **No partisan/sensitive-topic editorializing**; Claude must not adjudicate contested curricular
  framing — it labels, humans decide.
- **No student/teacher data** ever touches a model in a way that could identify a person (architecture
  guarantees there is none to send).

---

## 6. Ten concrete optimizations

1. **Name OER Commons as the incumbent and write the one-paragraph "why us" in the PLAN.** Lead with
   verified-license + consumable-crosswalk + privacy, not "findability."
2. **Reposition the deliverable from "discovery site" to "open, versioned, GUID-keyed crosswalk
   dataset."** Make external reuse (forks/citations/embeds) the headline outcome; the site is one
   projection of it.
3. **Narrow M0/M1 to a single track in the roadmap text (CCSS Math + `oer-math` only).** Demote
   ELA/NGSS/CSTA to "schema must not preclude"; ship breadth only after the spine proves out.
4. **Add an explicit educator-review capacity model** — estimated review-minutes per resource, target
   reviewers, batching plan — and treat reviewer recruitment as the M0 critical path, not a placeholder.
5. **Relax the standards-IP default for CCSS and NGSS** (verified reproducible-with-notice): store
   statement text for those two frameworks; keep codes-only for state/CSTA until verified. Improves
   teacher UX materially.
6. **Introduce a labeled "use-but-not-adapt" tier** (or explicitly document excluding ND/NC) so
   high-value resources (Siyavula branded, MIT OCW) are surfaced-and-flagged rather than silently lost.
7. **Ship the standards-coverage *gap* report in M0, not M3,** and wire it to auto-open authoring tasks
   in sibling libraries — this is the unique closed loop and the project's clearest value.
8. **Lock the snapshot format now** (committed copy + SHA-256 + Wayback URL, per `open-data-datasheets`)
   and put it in the gate's acceptance criteria — resolve that open question before pilot ingestion.
9. **Add a "license-mislabel regression corpus"** to CI fixtures — known mislabeled real-world cases
   (e.g., "free to view" ≠ open, NC/ND traps) that the gate must catch — so the Sev-1 metric is tested.
10. **Pursue a named beneficiary in parallel with M0 build** (UNESCO OER Dynamic Coalition, a
    teacher-serving nonprofit, or homeschool/refugee-ed network) — the project's Definition of Shipped
    is adoption, and outreach is currently one small task against a "TO BE SECURED" partner.

---

## 7. Parallel & perpendicular spin-offs

**Parallel (siblings the umbrella coordinates):**
- **`oer-science-labs` / `oer-math`** — content sources; the umbrella supplies their shared schema +
  standards registry + gate, and routes NGSS/CCSS coverage gaps back to them as authoring tasks.
- **`open-coding-curriculum`** — the CSTA-aligned source for the CS subject; first real test that the
  schema/crosswalk generalizes beyond math/science to a code-bearing (MIT/Apache) resource type.
- **`decodable-readers` / reading libraries** — the ELA/decodable source for M1; under-served niche
  where the umbrella's standards-keyed browse has high marginal value.

**Perpendicular (new artifacts the spine makes possible):**
- **`curriculum-standards-map`** — the plan already proposes folding this into the umbrella's standards
  registry; do it, to avoid duplicate CASE/ASN work (resolve the open question toward merge).
- **`teacher-lesson-plans`** — once resources are GUID-aligned, auto-assemble a standard-by-standard
  "lesson skeleton" of vetted free resources — an *assembly* layer no incumbent offers.
- **`quiz-bank-open`** — practice/assessment items keyed to the same GUIDs (the gap Khan fills but
  proprietarily); the crosswalk lets open practice plug straight in.
- **Reusable OER-assembly pipeline** — the validators + gate + crosswalk + static-site generator,
  packaged so *any* org can stand up a license-verified, standards-keyed open library (the rails as a
  product).
- **An MCP server over the crosswalk** — expose "resources for standard X / coverage gaps / license
  status" as MCP tools so *any* agent (a teacher's Claude, an LMS) can query the open catalog
  programmatically. This operationalizes the "consumable crosswalk" differentiator and is the highest-
  leverage perpendicular bet.

---

## 8. Open questions

1. **Why us over OER Commons?** Needs an explicit, defensible answer in the PLAN beyond "findability"
   (verified license + consumable GUID crosswalk + privacy + sibling coordination).
2. **Destination vs. rails.** Is success measured in site traffic or in *external reuse* of the
   crosswalk? (Recommendation: rails — but the team must commit.)
3. **The adaptation gate trade-off.** Hard-exclude all ND/NC, or surface a labeled non-adaptable tier?
   This decides whether the most-used resources (Siyavula branded, MIT OCW) are in or out.
4. **CCSS/CSTA statement-text reproduction.** CCSS *is* reproducible-with-notice and NGSS broadly so;
   confirm CSTA terms and decide per-framework rather than blanket codes-only.
5. **Reviewer capacity & bus-factor.** How many educator/license reviewers, at what review-rate, and
   what happens to coverage targets if recruitment lags? Governance/COI policy is deferred to M3 — too
   late for blocking M0 roles.
6. **Named first beneficiary.** Which teacher/school/nonprofit confirms adoption, and via which channel
   (UNESCO Dynamic Coalition? homeschool/refugee-ed network? a district curriculum office)?
7. **Internationalization timing.** Forward-design multilingual metadata + non-US frameworks now (cost
   to schema) or defer? Which non-US framework is the first target?
8. **Snapshot canonical format** — adopt `open-data-datasheets`' committed-copy + hash + Wayback format
   now (recommended) to unblock the pilot.
