# Claude Code Prompt — MVP Implementation Plan

You are acting as a Staff Product Engineer joining the Signal project.

Signal is a career intelligence system designed to help a senior frontend engineer evaluate exceptional job opportunities without turning job hunting into a second job.

The long-term vision is intentionally ambitious, but the current goal is much smaller.

Your task is NOT to build the full product.

Your task is to read the repository documentation and produce a technical implementation plan for MVP 0.1.

---

# Required Reading

Before proposing anything, read these files carefully:

```text
README.md

docs/product/constitution.md
docs/product/vision.md
docs/product/mvp-scope.md
docs/product/prd.md
docs/product/user-journeys.md

docs/architecture/domain-model.md
docs/architecture/capability-catalog.md
docs/architecture/mvp-architecture.md

docs/decisions/adr-001-documentation-first.md
docs/decisions/adr-002-intelligence-engine-before-ui.md
docs/decisions/adr-003-knowledge-as-asset.md
docs/decisions/adr-004-company-first-model.md
docs/decisions/adr-005-human-approval-for-external-actions.md
docs/decisions/adr-006-briefings-over-dashboards.md
docs/decisions/adr-007-cost-aware-ai-usage.md

data/candidate/profile.md
data/opportunities/_template.md
data/research-reports/_template.md
data/evaluations/_template.md
data/feedback/_template.md
data/activity/_template.md
output/briefings/_template.md
```

---

# Current MVP Goal

The MVP goal is to validate the smallest useful intelligence loop:

```text
Opportunity → ResearchReport → Evaluation → Briefing → Feedback
```

The MVP should answer one question:

> Can Signal take a manually provided company or job opportunity, research it, evaluate it against the Candidate profile, and produce a useful, personalized, explainable briefing?

Do not expand the scope.

Do not introduce automatic discovery, outreach, dashboards, WhatsApp, native apps, agents, multi-user support, authentication, billing, or full CRM functionality.

---

# Your Task

Produce a technical implementation plan for MVP 0.1.

Do not write application code yet.

The output should be a document that explains how to implement the MVP with the least amount of complexity possible.

The plan should include:

1. Recommended initial technical approach.
2. Proposed file/folder structure.
3. Minimal data formats.
4. Minimal scripts or commands.
5. How the Candidate profile will be loaded.
6. How an Opportunity input will be processed.
7. How ResearchReports will be generated or stored.
8. How Evaluations will be generated.
9. How Briefings will be produced.
10. How Feedback will be captured.
11. How Activity will be logged.
12. How existing knowledge will be reused.
13. How AI usage should be bounded.
14. What should be implemented first.
15. What should explicitly NOT be implemented yet.

---

# Critical Constraints

## 1. Start boring

Prefer the simplest possible implementation.

Good options may include:

- markdown files;
- JSON files;
- local scripts;
- CLI commands;
- minimal Node.js or Python tooling;
- no database at first;
- no frontend at first;
- no background jobs.

The first implementation should optimize for learning, not polish.

---

## 2. Do not over-engineer

Avoid:

- multi-agent architecture;
- queues;
- background workers;
- auth;
- SaaS structure;
- database schema unless clearly justified;
- Next.js app unless clearly justified;
- Swift app;
- WhatsApp integration;
- browser automation;
- LinkedIn scraping;
- automatic applications;
- external message sending.

---

## 3. Preserve the domain model

Even if the implementation is simple, it should preserve the core domain artifacts:

- Candidate;
- Opportunity;
- ResearchReport;
- Evaluation;
- Briefing;
- Feedback;
- Activity.

These can be represented as markdown or JSON files in MVP 0.1.

---

## 4. Briefing quality matters most

The first implementation succeeds only if the generated Briefing is useful.

A useful Briefing should:

- save time;
- reflect the Candidate profile;
- summarize company and role clearly;
- identify positives;
- identify concerns;
- expose missing information;
- make uncertainty clear;
- recommend a next action;
- ask for feedback.

---

## 5. Human approval

The MVP must not perform any external action.

It must not:

- apply to jobs;
- send messages;
- contact recruiters;
- submit forms;
- publish anything;
- modify public profiles.

---

## 6. Cost-aware AI usage

The implementation should avoid unnecessary AI calls.

Before using AI, prefer:

1. existing stored data;
2. manually provided content;
3. deterministic parsing;
4. structured extraction;
5. targeted AI generation only where it adds value.

The system should not run open-ended research loops.

---

# Expected Output Format

Create a new document:

```text
docs/architecture/mvp-implementation-plan.md
```

The document should include the following sections:

```text
# MVP Implementation Plan

## 1. Summary

## 2. Recommended Approach

## 3. Proposed Technical Shape

## 4. File and Data Structure

## 5. MVP Commands or Scripts

## 6. Data Flow

## 7. Artifact Formats

## 8. AI Usage Plan

## 9. Knowledge Reuse Plan

## 10. Feedback Loop

## 11. Implementation Phases

## 12. What Not To Build Yet

## 13. Risks

## 14. Open Questions

## 15. Recommended First Implementation Task
```

Be specific.

Make trade-offs explicit.

If there are multiple viable approaches, compare them and recommend one.

Do not write code yet.

Do not modify existing files unless necessary.

Focus only on the implementation plan.
