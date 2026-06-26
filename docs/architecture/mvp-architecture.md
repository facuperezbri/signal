# MVP Architecture

Status: Draft
Last updated: 2026-06-26

# Signal — MVP Architecture

## 1. Purpose

This document defines the minimum architecture needed to build Signal MVP 0.1.

The MVP goal is not to build the full career intelligence system.

The MVP goal is to validate the core intelligence loop:

> Can Signal transform a manually provided company or job opportunity into a useful, personalized, explainable briefing?

This architecture should support that loop with the least amount of complexity possible while still respecting the product principles.

---

# 2. Architecture Goals

The MVP architecture should optimize for:

- speed of implementation;
- clear domain boundaries;
- reusable knowledge;
- structured outputs;
- low cost;
- auditability;
- easy iteration;
- minimal UI assumptions.

The architecture should avoid:

- premature automation;
- complex orchestration;
- multi-agent systems;
- overbuilt dashboards;
- full CRM workflows;
- external actions;
- unnecessary infrastructure;
- tight coupling to a specific interface.

---

# 3. MVP Core Loop

```text
User submits opportunity
        ↓
Load Candidate profile
        ↓
Normalize opportunity input
        ↓
Research company and role
        ↓
Evaluate against Candidate profile
        ↓
Generate structured Briefing
        ↓
Capture Feedback
        ↓
Store artifacts
```

This loop is the only thing the MVP must prove.

Everything else is secondary.

---

# 4. Architectural Principle

## Start boring

The first implementation should be intentionally boring.

It does not need:

- agents;
- autonomous workflows;
- queues;
- background jobs;
- complex UI;
- real-time updates;
- chat integration;
- LinkedIn automation;
- application tracking.

It needs to generate a high-quality briefing from a real opportunity.

If the briefing is not useful, no amount of automation matters.

---

# 5. Suggested MVP Shape

The MVP can start as a local or simple internal tool.

Acceptable first interfaces:

- markdown-driven workflow;
- CLI command;
- minimal local web form;
- simple script;
- lightweight internal web page.

The first interface should be selected based on speed and clarity, not polish.

## Recommended initial approach

For MVP 0.1, the simplest useful architecture is:

```text
/input
  candidate-profile.md
  opportunities/*.md

/output
  briefings/*.md
  feedback/*.md

/data
  companies/*.json
  research-reports/*.json
  evaluations/*.json
  activities/*.json
```

This lets Signal work as a document-driven system before committing to a full application interface.

---

# 6. MVP Components

## 6.1 Candidate Profile Loader

### Responsibility

Load the Candidate profile from a structured file.

### Input

```text
data/candidate/profile.md
```

or

```text
data/candidate/profile.json
```

### Output

Structured Candidate object.

### Notes

For MVP 0.1, this can be manually edited.

No onboarding UI is required.

---

## 6.2 Opportunity Input Parser

### Responsibility

Read a manually submitted opportunity.

### Input

A markdown or JSON file containing:

- company name;
- company website;
- job URL;
- job description;
- role title;
- salary range, if known;
- location;
- remote policy, if known;
- source;
- user notes.

### Output

Structured Opportunity object.

### Notes

The parser should tolerate missing fields.

The system should not fail because salary or remote policy is unknown.

---

## 6.3 Research Module

### Responsibility

Gather or structure information about the company and role.

### MVP Scope

For MVP 0.1, research can be partially manual, assisted, or AI-generated from available inputs.

The module should produce structured ResearchReports.

### Research areas

- company summary;
- product;
- culture signals;
- benefits signals;
- engineering signals;
- compensation signals;
- role responsibilities;
- technical requirements;
- risks;
- missing information.

### Output

ResearchReport artifacts.

### Important Rule

Research should distinguish between:

- facts;
- assumptions;
- weak signals;
- missing information;
- interpretation.

---

## 6.4 Evaluation Module

### Responsibility

Compare the researched company and opportunity against the Candidate profile.

### Inputs

- Candidate;
- Opportunity;
- ResearchReports.

### Output

Evaluation artifact.

### Evaluation dimensions

- technical fit;
- product fit;
- culture fit;
- compensation fit;
- benefits fit;
- flexibility fit;
- work-life balance fit;
- AI relevance;
- risk level;
- confidence.

### Important Rule

The Evaluation should not be a generic job match.

It must reflect the Candidate’s actual values:

- culture matters heavily;
- compensation matters;
- product matters;
- flexibility matters;
- frontend/React expertise matters;
- AI interest matters;
- consulting, outsourcing, traditional banking, toxic culture, and legacy-only work are negative signals.

---

## 6.5 Briefing Generator

### Responsibility

Generate the user-facing Briefing.

### Inputs

- Candidate;
- Company;
- Opportunity;
- ResearchReports;
- Evaluation.

### Output

Markdown Briefing.

### Required sections

1. Executive Summary
2. Company Summary
3. Role Summary
4. Fit Assessment
5. Positive Signals
6. Concerns and Risks
7. Missing Information
8. Recommended Action
9. Confidence Level
10. Feedback Prompt

### Important Rule

The Briefing must be useful, calm, honest, and specific.

It should not sound like a generic LLM summary.

---

## 6.6 Feedback Capture

### Responsibility

Capture the user’s reaction to a Briefing.

### MVP Feedback Actions

- pursue;
- reject;
- save for later;
- research more;
- disagree;
- blacklist company;
- mark as exciting.

### Output

Feedback artifact.

### Notes

Feedback may initially be captured manually in markdown or JSON.

The important part is that feedback is stored and available for future evaluations.

---

## 6.7 Activity Logger

### Responsibility

Record important system events.

### Activity examples

- candidate profile loaded;
- opportunity submitted;
- research report created;
- evaluation created;
- briefing generated;
- feedback captured.

### Output

Activity records.

### Notes

Activity is not a dashboard.

It is an audit trail.

---

# 7. Data Artifacts

The MVP should produce durable artifacts.

## Candidate

Represents the user profile.

Suggested location:

```text
data/candidate/profile.md
```

or:

```text
data/candidate/profile.json
```

---

## Opportunity

Represents a submitted opportunity.

Suggested location:

```text
data/opportunities/
```

Example:

```text
data/opportunities/2026-06-26-exampleco-senior-frontend.md
```

---

## ResearchReport

Represents structured research.

Suggested location:

```text
data/research-reports/
```

Example:

```text
data/research-reports/exampleco-company-research.json
```

---

## Evaluation

Represents fit evaluation.

Suggested location:

```text
data/evaluations/
```

Example:

```text
data/evaluations/exampleco-senior-frontend-evaluation.json
```

---

## Briefing

Represents the final user-facing output.

Suggested location:

```text
output/briefings/
```

Example:

```text
output/briefings/2026-06-26-exampleco-senior-frontend.md
```

---

## Feedback

Represents user feedback.

Suggested location:

```text
data/feedback/
```

Example:

```text
data/feedback/2026-06-26-exampleco-feedback.json
```

---

## Activity

Represents audit trail events.

Suggested location:

```text
data/activity/
```

or:

```text
data/activity.log
```

---

# 8. Suggested File Structure

```text
signal/
│
├── README.md
│
├── docs/
│   ├── product/
│   │   ├── constitution.md
│   │   ├── vision.md
│   │   ├── mvp-scope.md
│   │   ├── prd.md
│   │   └── user-journeys.md
│   │
│   ├── architecture/
│   │   ├── domain-model.md
│   │   ├── capability-catalog.md
│   │   └── mvp-architecture.md
│   │
│   └── decisions/
│       ├── adr-001-documentation-first.md
│       ├── adr-002-intelligence-engine-before-ui.md
│       ├── adr-003-knowledge-as-asset.md
│       ├── adr-004-company-first-model.md
│       ├── adr-005-human-approval-for-external-actions.md
│       ├── adr-006-briefings-over-dashboards.md
│       └── adr-007-cost-aware-ai-usage.md
│
├── data/
│   ├── candidate/
│   │   └── profile.md
│   │
│   ├── opportunities/
│   │
│   ├── companies/
│   │
│   ├── research-reports/
│   │
│   ├── evaluations/
│   │
│   ├── feedback/
│   │
│   └── activity/
│
├── output/
│   └── briefings/
│
├── scripts/
│
├── apps/
│
├── packages/
│
└── services/
```

---

# 9. MVP Execution Flow

## Step 1: Add Opportunity

The user creates an opportunity input file.

Example:

```text
data/opportunities/2026-06-26-exampleco-senior-frontend.md
```

---

## Step 2: Run Briefing Generation

The system processes the opportunity.

Example future command:

```bash
signal generate-briefing data/opportunities/2026-06-26-exampleco-senior-frontend.md
```

This command does not need to exist immediately, but the architecture should support this flow.

---

## Step 3: Generate Artifacts

The system creates:

- ResearchReport;
- Evaluation;
- Briefing;
- Activity records.

---

## Step 4: Review Briefing

The user reads the generated Briefing.

---

## Step 5: Capture Feedback

The user provides feedback.

Example future command:

```bash
signal feedback output/briefings/2026-06-26-exampleco-senior-frontend.md --action reject --reason culture
```

Or the user manually creates a feedback file.

---

## Step 6: Reuse Feedback

Future evaluations should be able to reference previous feedback.

---

# 10. Technology Constraints

This document intentionally does not choose the final product interface.

The MVP may eventually use:

- web;
- native app;
- chat;
- CLI;
- email;
- WhatsApp;
- Telegram.

However, MVP 0.1 should avoid committing to a complex interface.

The first technical implementation should prioritize:

- high-quality briefings;
- structured artifacts;
- easy iteration;
- low setup cost.

---

# 11. AI Usage

The MVP may use AI for:

- extracting structured data from job descriptions;
- summarizing company/product information;
- evaluating fit;
- generating briefings;
- identifying risks;
- identifying missing information.

The MVP should avoid AI for:

- simple file reading;
- deterministic validation;
- sorting;
- status changes;
- activity logging;
- feedback storage;
- repeated analysis of already-fresh knowledge.

---

# 12. Research Strategy for MVP

The MVP can start with limited research.

Possible modes:

## Mode 1: User-provided content only

The system uses:

- job description;
- company website text manually provided by user;
- user notes.

Pros:

- simple;
- cheap;
- avoids web-search complexity.

Cons:

- less useful;
- more manual work;
- weaker company research.

---

## Mode 2: Assisted web research

The system uses search or browsing to collect company information.

Pros:

- more useful;
- less manual effort;
- closer to product vision.

Cons:

- more complex;
- source reliability matters;
- cost and latency increase.

---

## Mode 3: Hybrid

The user provides the job post, and the system researches company basics.

Pros:

- practical;
- useful;
- balanced.

Cons:

- still requires source quality rules.

## Recommended MVP mode

Start with Hybrid.

The user provides the opportunity.

Signal researches only the minimum needed to generate a useful Briefing.

---

# 13. Source Handling

The MVP should be honest about source quality.

For each researched claim, Signal should ideally know:

- source;
- freshness;
- confidence;
- whether the information is fact or interpretation.

In MVP 0.1, full source management may be simple, but the Briefing should still avoid unsupported claims.

## Required behavior

Signal must not invent facts.

If salary, benefits, or culture are unclear, it should say so.

---

# 14. Confidence Model

MVP confidence can be simple.

Suggested values:

- High;
- Medium;
- Low.

Confidence is based on evidence quality and completeness.

Confidence is not the same as recommendation strength.

Example:

A company can be exciting but low-confidence if information is missing.

---

# 15. Recommendation Model

The MVP should use simple recommendation labels.

Suggested values:

- Pursue;
- Worth reviewing;
- Save for later;
- Research more;
- Reject.

## Rule

The system should avoid recommending everything.

If all opportunities are “worth reviewing,” the evaluation is not useful.

---

# 16. Cost Controls

The MVP should follow these constraints:

- no unbounded background work;
- no automatic deep research for every input;
- no application package generation by default;
- no outreach generation by default;
- reuse existing company research when available;
- prefer structured outputs;
- keep AI calls limited and intentional.

---

# 17. What This Architecture Does Not Include

The MVP architecture does not include:

- autonomous agents;
- multi-agent orchestration;
- scheduled background jobs;
- automatic opportunity discovery;
- LinkedIn scraping;
- external message sending;
- application submission;
- full dashboard;
- auth;
- multi-user support;
- billing;
- deployment architecture;
- mobile app architecture.

---

# 18. Validation Architecture

The MVP should support testing 10 real opportunities.

For each opportunity, the system should store:

- input;
- research;
- evaluation;
- briefing;
- feedback.

After 10 opportunities, the system should support a manual or semi-manual review:

- pursued count;
- rejected count;
- saved count;
- research-more count;
- common rejection reasons;
- most useful briefing sections;
- weakest briefing sections;
- next automation candidate.

This does not need to be automated in MVP 0.1, but the data should make it possible.

---

# 19. Definition of Done

The MVP architecture is sufficient when it can support:

- loading Candidate profile;
- submitting one opportunity;
- producing research artifacts;
- producing an Evaluation;
- producing a Briefing;
- storing Feedback;
- storing Activity;
- testing 10 real opportunities.

---

# 20. Final Architectural Constraint

The MVP must not become a smaller version of the full product.

It must remain focused on the smallest useful intelligence loop:

```text
Opportunity → Research → Evaluation → Briefing → Feedback
```

Until that loop produces genuinely useful results, broader automation should not be built.
