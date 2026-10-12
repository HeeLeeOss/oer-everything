# Governance — oer-everything Reviewer Roles

> **Status:** Framework established · **Version:** 0.1.0 · **Last updated:** 2026-07-24  
> **License:** CC-BY-4.0 · **Owner:** TBD (Maintainer)

## Overview

This document establishes the governance framework for the oer-everything project, focusing on the two mandatory, non-skippable blocking reviewer roles that must be filled before the M0 pilot can proceed. These roles are load-bearing for the project's integrity: the License+Provenance reviewer ensures only openly-licensed, legally sound content enters the library; the Educator reviewer ensures pedagogical accuracy, grade-appropriateness, and quality.

**Critical rule:** If either role is empty (no named reviewer exists), **intake halts** — no resource passes the gate, and all tasks remain marked `verifiedNeed:false`. This rule is recorded here and enforced in the backlog.

---

## Required Reviewer Roles

### 1. License + Provenance Reviewer

**Role description:** Mandatory gatekeeper who verifies every resource's license and provenance before it enters the library.

**Qualifications (minimum bar):**
- Demonstrated knowledge of open licenses: CC0, CC-BY, CC-BY-SA, public domain, and open-source code licenses (MIT, Apache, GPL).
- Ability to read and interpret license text (or access to standard license summaries like Creative Commons definitions) to determine whether a resource permits **both reuse AND adaptation**.
- Understanding of copyright, attribution requirements, and the distinction between "free to view" and "open to adapt."
- Experience or study of curriculum standards licensing — specifically the ability to verify whether standards-text reproduction is permitted (e.g., CCSS terms, NGSS terms).
- Attention to detail: ability to spot missing, unclear, or conflicting license claims and escalate them as FLAG/EXCLUDE (no default-allow).
- Willingness to apply the standards-IP matrix documented in PLAN.md § Data, licensing & compliance.

**Scope (per-resource responsibility):**
- Verify the resource's stated license against the accepted set (PD/CC0/CC-BY/compatible CC-BY-SA/open code licenses).
- Confirm `license.permitsReuse: true` AND `license.permitsAdaptation: true` are recorded from a cited license id/URL.
- Record or verify a snapshot reference (committed copy + SHA-256 hash + Wayback URL per the project's decided format).
- Check that no license-restricted standards text is reproduced; apply the per-framework standards-IP matrix.
- Produce a committed PASS/FLAG/EXCLUDE gate artifact per resource.

**Authority & decision-making:**
- Full authority to EXCLUDE a resource on license grounds (no escalation needed; this is a gate, not advisory).
- PASS = the resource is legally clear and proceeds to educator review.
- FLAG = the license is unclear or requires researcher review; resource does not proceed until FLAG is resolved or converted to EXCLUDE.

**Time commitment:** Approximately 20–30 minutes per resource (varies by license complexity). M0 pilot: ~5 resources = 2–3 hours total.

**Rotation & succession:**
- Minimum **1 named reviewer** (gatekeeper) must exist at all times, or intake halts.
- **Preferred: ≥ 2 qualified reviewers** so reviews can rotate, preventing bottleneck and allowing leave/availability gaps.
- If a reviewer becomes unavailable, a successor must be identified and onboarded **before** the current reviewer steps down (no overlap = intake halts).
- Onboarding checklist for new reviewers includes: review of licenses, standards-IP matrix, past gate artifacts (to calibrate consistency), and one supervised review before solo authority.

**Accountability:**
- If a non-open resource is admitted with a passed gate (a Sev-1 defect), the reviewer and maintainer conduct a post-mortem.
- Reviewers are expected to flag uncertainty and ask questions rather than guess.

---

### 2. Educator / Curriculum Reviewer

**Role description:** Subject-matched educator who verifies pedagogical accuracy, grade-appropriateness, and quality before a resource is admitted.

**Qualifications (minimum bar):**
- **Practicing or recently-practicing K-12 educator** in the subject being reviewed (for M0: mathematics; later: science, ELA, CS).
- Familiarity with the relevant curriculum standards (for M0: Common Core State Standards in Mathematics or state equivalent).
- Ability to assess content for **factual correctness**, **grade-band appropriateness** (e.g., is this really 4th-grade, or is it 3rd-grade-hard or 5th-grade-light?), and **pedagogical usefulness** (would this resource actually help a teacher teach the standard?).
- Understanding of how to evaluate resource quality across dimensions: accuracy, clarity, accessibility, potential bias or sensitivity, and alignment fidelity (does it actually teach what it claims?).
- Willingness to use the project's **quality rubric** (scored, versioned; dimensions: accuracy, standards-alignment fidelity, grade appropriateness, pedagogical usefulness, clarity/readability, accessibility, bias/sensitivity). Scoring scale: 0–100; admission threshold: **≥ 80** with reviewer sign-off.

**Subject-matching requirement:**
- A math educator reviews math resources, a science educator reviews science resources, etc.
- For M0 (math pilot), the reviewer must have math teaching experience or equivalent recent subject expertise.
- For future subjects (science, ELA, CS), reviewers must be matched to subject.

**Scope (per-resource responsibility):**
- Read/examine the resource and assess its accuracy, grade fit, and pedagogical value against the rubric.
- Assign a rubric score (0–100) with a short rationale (e.g., "Accurate, aligns well to CCSS.MATH.4.NF.B.3, but readability is below grade level; score 72 — needs revision or student scaffolding").
- Recommend ADMIT (≥ 80) or REVISE/EXCLUDE (< 80) with sign-off.
- If ADMIT: your name and score are recorded in the resource's canonical record (`qualityScore {value, rubricVersion, reviewedBy}`).
- Flag any bias, sensitivity, or accessibility concerns so they can be labeled (`contentNotes`, `accessibilityFeatures`) on the discovery site.

**Authority & decision-making:**
- Full authority to EXCLUDE or recommend revision if the resource scores < 80 or has factual errors / inappropriate grade-band / significant clarity issues.
- ADMIT = the resource passes quality and proceeds to publishing on the discovery site.
- Reviewers are expected to be honest, not performative; a resource that is borderline (≥ 78) scores 78, not 80.

**Time commitment:** Approximately 30–45 minutes per resource (varies by resource length and complexity). M0 pilot: ~5 resources = 2.5–4 hours total.

**Rotation & succession:**
- Minimum **1 named educator reviewer** (subject-matched) must exist per subject at all times, or intake halts for that subject.
- **Preferred: ≥ 2 qualified reviewers** per subject so reviews rotate and prevent bottleneck.
- If a reviewer becomes unavailable, a successor must be identified and onboarded **before** the current reviewer steps down.
- Onboarding checklist for new reviewers includes: review of the rubric, past scoring examples (to calibrate consistency), one sample resource review with feedback, and one supervised review before solo authority.

**Accountability:**
- If an inaccurate or grade-inappropriate resource is admitted at ≥ 80, the reviewer and maintainer conduct a post-mortem.
- Reviewers are expected to apply the rubric consistently and document their reasoning.

---

## Current Status

**As of 2026-07-24:**

- **License + Provenance Reviewer:** TO BE SECURED (no named reviewer yet)
- **Educator/Curriculum Reviewer (Math):** TO BE SECURED (no named reviewer yet)
- **Intake Status:** HALTED (cannot proceed with M0 pilot review until both roles are filled)
- **Task Status:** oer-everything-reviewer-001 (research: identify and secure reviewers)

---

## Securing Reviewers — Process & Timeline

### Identification Process

1. **License + Provenance Reviewer:**
   - Candidate channels: open-education subject-matter experts, librarians, licensing specialists, legal professionals with open-source/IP background.
   - Screening: share the qualifications and PLAN.md § Data, licensing & compliance; ask candidates to review 1–2 sample licenses and standards-IP edge cases to self-assess fit.
   - Onboarding: walkthrough of the project's standards-IP matrix, review of 1–2 past gate artifacts (if available), and supervised review of first real resource before solo authority.

2. **Educator / Curriculum Reviewer (Math):**
   - Candidate channels: practicing K-12 math teachers (public, charter, or independent schools), math curriculum coordinators, teacher-serving nonprofit staff, math education faculty.
   - Screening: share the qualifications, rubric, and a sample resource; ask candidates to score it against the rubric and explain their reasoning. This calibrates consistency and tests fit.
   - Onboarding: walkthrough of the rubric and its dimensions, review of 1–2 past scoring examples (if available), and one supervised review of a real resource with feedback before solo authority.

### Timeline for M0

- **Identification & outreach:** 1–2 weeks (send out requests to candidate channels, gather self-assessments).
- **Screening & interviews:** 1 week (review responses, conduct brief calls or async Q&A to confirm fit).
- **Onboarding:** 3–5 days (walkthrough, sample review, feedback loop).
- **Go-live:** Both reviewers named and ready to review oer-math resources (target: within 2–3 weeks).

**Blocking point:** M0 pilot (ingesting oer-math end-to-end) **cannot begin** until both reviewers are named and onboarded. All tasks remain `verifiedNeed:false` and intake is halted until this is done.

---

## Rotation & Succession Planning

### Policy

1. **Minimum staffing:** 1 named reviewer per role at all times, or intake halts.
2. **Preferred staffing:** ≥ 2 qualified reviewers per role for rotation, leave coverage, and consistency-checking.
3. **Succession rule:** If a reviewer becomes unavailable (burnout, schedule conflict, resignation), their successor must be identified, screened, and onboarded **before** the departing reviewer steps down. No gap = no bottleneck.
4. **Calibration:** When 2+ reviewers exist, periodically (quarterly) review a sample of each reviewer's gate/scoring decisions together to spot drift or disagreement, and course-correct.

### Rotation Mechanics

- License + Provenance reviewer(s) rotate per resource (or per batch of resources, as their schedule allows).
- Educator reviewer(s) rotate per resource per subject (math, then science, then ELA, etc.).
- Reviewers are encouraged to ask questions and escalate edge cases rather than guess.
- The Maintainer tracks reviewer bandwidth and workload, and escalates if a single reviewer is overloaded.

---

## Intake-Halt Rule

**Statement:** If fewer than 1 named, qualified reviewer exists for either the License+Provenance role or the Educator role (for the current subject), **intake halts — no resource passes the gate, and all backlog tasks remain `verifiedNeed:false`.**

**Rationale:** These are blocking gates. A resource without license verification or educator approval does not enter the library. These roles are not advisory; they are gatekeepers. If they are empty, the integrity of the project is at risk, and it is better to be transparent and halt than to lower the bar.

**Enforcement:**
- The Maintainer updates PLAN.md and the backlog's `verifiedNeed` field to explicitly record if intake is halted.
- A task tagged `verifiedNeed:false` cannot move to "delivered" (it can only be marked "open" or "in-progress", but never "done").
- If intake is halted, it is flagged in the project status and all stakeholders are notified.

**Recovery:** Once a reviewer is named and onboarded, intake resumes and `verifiedNeed` can be set to `true` for tasks that were blocked.

---

## Integration with PLAN.md

The governance section of PLAN.md (§ Governance, roles & stakeholders) is the canonical source for current reviewer names and status. This document provides the **framework and qualifications**; PLAN.md provides the **current assignments**.

When a reviewer is secured:
1. Update PLAN.md § Governance with their name, subject/domain, and start date.
2. Update the Intake Status in this document to reflect that both roles are filled.
3. Update TASKS.md: set `status: done` for oer-everything-reviewer-001 and resume blocked tasks by setting `verifiedNeed: true`.

---

## Quality & Consistency

### Rubric Versioning & Stability

The quality rubric (oer-everything-rubric-004) is versioned and committed. Reviewers use the version matching the resource's `rubricVersion` field. If the rubric changes, new versions are clearly marked with a date and changelog, and past resources retain their scored version for auditability.

### First-Pass Calibration

Before the first M0 resources are reviewed, the License+Provenance reviewer and Educator reviewer(s) **conduct a joint calibration session** with the Maintainer:
- License reviewer walks through a sample resource's license and standards-IP decisions.
- Educator reviewer(s) score a sample resource and discuss their reasoning.
- Together, they align on the standards-IP matrix, rubric interpretation, and edge-case handling.

This prevents downstream drift and sets a shared baseline.

### Conflict Resolution

If a License reviewer FLAGs a resource and an Educator reviewer still wants to ADMIT it (e.g., "the license is unclear, but the resource is so good we should try"), the Maintainer makes the final call:
- Option A: Confirm the FLAG is justified and EXCLUDE (most likely).
- Option B: Escalate to a licensing specialist for expert review before deciding.
- Option C: Proceed with a caveat (rare; reserved for strategic resources where legal risk is assessed and accepted).

If two Educator reviewers disagree on a score (e.g., one scores 76, one scores 82), they discuss their reasoning. The Maintainer can ask for a re-score or split the difference if there's genuine disagreement. Consistency is favored; a resource that divides reviewers 76 vs 82 likely should be revised rather than admitted at the lower score.

---

## Acknowledgments & Licensing

This governance framework is derived from the oer-everything PLAN.md (v0.1.0, drafted by Hee-Lee Oss Senior Staff Engineer + TPM, 2026-06-28) and the project's Acceptance criteria (TASKS.md, oer-everything-reviewer-001).

**Output license:** CC-BY-4.0 (same as PLAN.md and project documentation).

---

## Appendix A — Reviewer Onboarding Checklist

### License + Provenance Reviewer Onboarding

- [ ] Read PLAN.md § Data, licensing & compliance (resource licenses, standards-IP matrix).
- [ ] Read PLAN.md § Solution approach & architecture (gate artifact format and workflow).
- [ ] Review sample gate artifacts from past projects (if available; else, create synthetic examples).
- [ ] Review the standards-IP matrix with Maintainer; ask clarifying questions on edge cases.
- [ ] Self-assess against the Qualifications section above; confirm fit.
- [ ] Co-review one sample resource with Maintainer; document the gate decision (PASS/FLAG/EXCLUDE) with rationale.
- [ ] Receive feedback; revise if needed.
- [ ] Conduct supervised review of first real oer-math resource; Maintainer reviews your gate artifact and provides feedback.
- [ ] Approved for solo review (no further supervision needed, but escalate edge cases).

### Educator / Curriculum Reviewer Onboarding

- [ ] Read PLAN.md § Quality, review & risk gates (rubric, threshold, process).
- [ ] Read oer-everything-rubric-004 (the versioned quality rubric); understand dimensions and scoring.
- [ ] Review sample resources and past scoring examples (if available); align on how to interpret dimensions.
- [ ] Self-assess against the Qualifications section above; confirm fit and subject match.
- [ ] Score a sample resource against the rubric; document your reasoning for each dimension.
- [ ] Discuss your score with Maintainer and (if available) other Educator reviewers; calibrate.
- [ ] Conduct one supervised review of a real oer-math resource; Maintainer reviews your rubric scoring and reasoning.
- [ ] Receive feedback; revise if needed.
- [ ] Approved for solo review (no further supervision needed, but escalate edge cases).

---

*This document is part of the oer-everything project governance. For the project plan, see PLAN.md. For the task backlog, see TASKS.md. For the current status of reviewer assignments, see PLAN.md § Governance, roles & stakeholders.*
