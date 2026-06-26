# Product Requirements Document

Status: Draft
Last updated: 2026-06-26

# Signal — MVP PRD

## 1. Overview

Signal is a career intelligence system designed to help a senior engineer evaluate exceptional job opportunities without turning job hunting into a second job.

The long-term vision is to build a system that continuously researches the market, understands companies, evaluates opportunities, prepares strategies, and helps the user pursue the right roles.

The MVP is intentionally smaller.

The MVP focuses on one core capability:

> Transform a manually provided company or job opportunity into a useful, personalized, explainable briefing.

The MVP should validate whether Signal can help the user make better opportunity decisions faster than manual research.

---

# 2. Problem Statement

The user is currently employed and not urgently looking for a job.

They are comfortable enough in their current role, but they want to avoid missing an exceptional opportunity.

The problem is that evaluating a good opportunity requires time-consuming research:

- What does the company do?
- Is the product interesting?
- Is the culture healthy?
- Are benefits and compensation strong?
- Is the role aligned with the user’s profile?
- Are there hidden risks?
- Is it worth applying or contacting someone?

The user does not want to spend hours researching every possible opportunity.

Most job platforms optimize for volume, not judgment.

Signal should help the user evaluate fewer opportunities more deeply.

---

# 3. MVP Goal

The MVP goal is to prove that Signal can produce useful opportunity briefings.

A useful briefing should:

- save time;
- summarize relevant company and role information;
- evaluate fit against the user’s actual preferences;
- surface risks and missing information;
- recommend a clear next action;
- capture feedback for future improvement.

The MVP does not need to automatically discover opportunities.

The MVP starts with user-provided opportunities.

---

# 4. MVP Hypothesis

If Signal can take a company and/or job opportunity, research it, evaluate it against the Candidate profile, and generate a useful briefing, then the core product thesis is valid.

The hypothesis is:

> The user will repeatedly use Signal if its briefings help them decide faster and better than manual research.

---

# 5. Target User

## Primary User

A senior frontend engineer specialized in React, with growing AI Engineering knowledge.

The user:

- has good English;
- is currently employed;
- is not urgently job hunting;
- wants a better opportunity within six months;
- values excellent company culture;
- wants strong compensation;
- wants meaningful benefits;
- wants flexibility and work-life balance;
- prefers product companies;
- wants to avoid consulting, outsourcing, traditional banking environments, toxic cultures, and legacy-only maintenance roles;
- wants to work on products that feel meaningful, useful, or exciting;
- wants the system to prepare everything, but keep final control.

## User Context

The user is not looking for “any job”.

The user is looking for a company where they could genuinely see themselves working happily.

A company with a normal product and excellent culture may be preferable to a company with an incredible product and poor culture.

---

# 6. Product Principles

The MVP must respect the existing Product Constitution.

Most relevant principles for MVP:

## Quality over quantity

The MVP should evaluate a small number of real opportunities well.

## Company first, role second

The briefing should evaluate the company, not just the job post.

## Human approval

No external action happens in the MVP.

## Explainability

Every recommendation must be understandable.

## Cost awareness

The MVP should avoid unnecessary AI usage.

## Knowledge as an asset

Research and feedback should be stored in a way that can be reused later.

## MVP focus

The MVP validates the briefing loop before broader automation.

---

# 7. Core MVP Workflow

```text
User submits opportunity
        ↓
Signal loads Candidate profile
        ↓
Signal researches company and role
        ↓
Signal evaluates fit
        ↓
Signal generates briefing
        ↓
User gives feedback
        ↓
Signal stores result and feedback
```

---

# 8. Functional Requirements

## FR1 — Candidate Profile

Signal must have access to a basic Candidate profile.

The Candidate profile may initially be stored as a structured markdown or JSON file.

### Required Candidate data

- professional identity;
- current role;
- core skills;
- preferred roles;
- target company types;
- avoided company types;
- values;
- constraints;
- compensation priorities;
- culture priorities;
- product priorities;
- flexibility priorities;
- AI interest;
- approval preferences.

### Acceptance Criteria

- The system can load the Candidate profile.
- The Candidate profile is used during evaluation.
- Briefings reflect the Candidate’s actual preferences.
- The Candidate profile can be edited manually.

---

## FR2 — Opportunity Input

Signal must allow the user to submit an opportunity.

For MVP, this can be manual.

### Input fields

- company name;
- company website;
- job post URL;
- job description text;
- role title;
- salary range, if available;
- location;
- remote policy, if available;
- source;
- user notes;
- reason for interest, optional.

### Acceptance Criteria

- The user can submit an opportunity with partial information.
- The system can handle missing salary.
- The system can handle missing job URL if company information is provided.
- The system does not require perfect structured data to start.

---

## FR3 — Company Research

Signal must research or summarize basic company information.

### Research areas

- what the company does;
- product;
- target users/customers;
- industry;
- company maturity/stage, when available;
- culture signals;
- benefits signals;
- remote/flexibility signals;
- engineering signals;
- risk signals, when obvious.

### Acceptance Criteria

- The briefing includes a company summary.
- The briefing distinguishes known information from assumptions.
- The briefing identifies missing information.
- The system stores company research as a reusable artifact.

---

## FR4 — Role Research

If a job post is provided, Signal must analyze the role.

### Research areas

- title;
- seniority;
- responsibilities;
- required skills;
- preferred skills;
- frontend relevance;
- React/TypeScript relevance;
- AI relevance;
- backend/full-stack expectations;
- salary if published;
- location and remote constraints.

### Acceptance Criteria

- The briefing includes a role summary.
- The briefing identifies strong matches.
- The briefing identifies gaps.
- The system does not automatically reject a role because of one gap.
- The system explains whether a gap is serious.

---

## FR5 — Fit Evaluation

Signal must evaluate the company and opportunity against the Candidate profile.

### Evaluation dimensions

- company culture;
- product interest;
- technical fit;
- role fit;
- compensation signal;
- benefits signal;
- flexibility/work-life balance;
- growth potential;
- AI relevance;
- overall attractiveness;
- risk level;
- confidence.

### Acceptance Criteria

- The evaluation is personalized to the Candidate.
- Culture has high importance.
- Product and compensation have high importance.
- Technical fit is considered but does not dominate everything.
- The recommendation is explainable.
- Uncertainty is explicitly represented.

---

## FR6 — Briefing Generation

Signal must generate a structured Briefing.

The Briefing is the primary MVP output.

### Required Briefing sections

1. Executive Summary
2. Company Summary
3. Role Summary, when applicable
4. Fit Assessment
5. Positive Signals
6. Concerns and Risks
7. Missing Information
8. Recommended Action
9. Confidence Level
10. Feedback Prompt

### Acceptance Criteria

- The Briefing can be read in under five minutes.
- The Executive Summary can be understood in under one minute.
- The Briefing does not simply repeat the job description.
- The Briefing clearly says whether the opportunity is worth pursuing, rejecting, saving, or researching more.
- The Briefing is honest about uncertainty.
- The Briefing includes enough reasoning to be auditable.

---

## FR7 — Feedback Capture

Signal must capture user feedback on a Briefing.

### Feedback actions

- pursue;
- reject;
- save for later;
- research more;
- disagree;
- blacklist company;
- mark as exciting.

### Optional feedback details

- reason;
- free-text comment;
- specific dimension affected.

### Feedback reasons

- product;
- culture;
- salary;
- benefits;
- role;
- stack;
- company reputation;
- remote/flexibility;
- work-life balance;
- other.

### Acceptance Criteria

- The user can give feedback after each Briefing.
- Feedback is stored.
- Feedback can be reviewed later.
- Feedback can inform future briefings, even if manually at first.

---

## FR8 — Activity Logging

Signal must record key activity.

### Activity examples

- opportunity submitted;
- Candidate profile loaded;
- company research completed;
- role research completed;
- evaluation created;
- briefing generated;
- feedback captured.

### Acceptance Criteria

- Important actions are recorded.
- Activity can be inspected later.
- Activity is not treated as the main product experience.

---

## FR9 — Knowledge Reuse

Signal should reuse existing company research when the same company appears again.

### Acceptance Criteria

- If the same company is submitted again, previous research can be referenced.
- The system should avoid treating every opportunity as completely new.
- The MVP may implement this simply at first.
- The system should make it possible to refresh research later.

---

# 9. Non-Functional Requirements

## NFR1 — Simplicity

The MVP should be simple enough to build and use quickly.

No complex interface is required.

## NFR2 — Explainability

Every recommendation must include reasoning.

No opaque score-only output.

## NFR3 — Cost Control

The MVP should avoid unnecessary AI usage.

It should not run unbounded background tasks.

## NFR4 — Truthfulness

The system must not invent candidate experience, salary data, company facts, or application details.

When uncertain, it must say so.

## NFR5 — Portability

Briefings should be generated as structured artifacts that could later be rendered in web, chat, email, markdown, or native UI.

## NFR6 — Manual Override

The user must be able to correct or override the system’s reasoning.

---

# 10. MVP Non-Goals

The MVP does not include:

- automatic job discovery;
- automatic company discovery;
- automatic LinkedIn scraping;
- automatic applications;
- automatic outreach;
- sending emails;
- sending LinkedIn messages;
- Gmail integration;
- Google Calendar integration;
- WhatsApp integration;
- Telegram integration;
- native macOS app;
- native mobile app;
- authentication;
- billing;
- multi-user support;
- full CRM;
- advanced dashboard;
- salary negotiation;
- long-term career coaching;
- conference or event recommendations;
- public content strategy;
- automatic LinkedIn profile optimization;
- full resume versioning;
- complete application tracking.

---

# 11. MVP Data Model

The MVP should use a reduced subset of the full domain model.

## Required MVP entities

### Candidate

The user profile.

### Company

The company being evaluated.

### Opportunity

The submitted opportunity.

### ResearchReport

Structured findings from company and role research.

### Evaluation

Fit analysis against the Candidate.

### Briefing

The final user-facing artifact.

### Feedback

The user’s reaction.

### Activity

System audit trail.

## Deferred entities

- Strategy;
- ApplicationPackage;
- Contact;
- Application;
- historical CompanyProfiles;
- advanced PreferenceInsight;
- advanced LearningSignal.

These may be introduced later.

---

# 12. MVP Experience

The MVP does not require a polished UI.

Acceptable early interfaces:

- markdown-driven workflow;
- CLI;
- simple local script;
- minimal web form;
- simple internal web page.

The first version should prioritize output quality over interface polish.

## Minimal interaction

```text
User adds opportunity
Signal generates briefing
User gives feedback
Signal stores feedback
```

## Experience principles

- The user should not configure a complex system.
- The user should not manage a dashboard.
- The user should receive a clear briefing.
- The user should always know what to do next.
- The system should not pretend to be more confident than it is.

---

# 13. Briefing Quality Bar

A Briefing is good if it:

- saves time;
- explains the company clearly;
- explains the role clearly;
- reflects the Candidate profile;
- identifies real positives;
- identifies real concerns;
- shows what is missing;
- recommends a clear next action;
- distinguishes facts from assumptions;
- uses a calm, honest tone.

A Briefing is bad if it:

- sounds generic;
- repeats the job description;
- recommends everything;
- hides uncertainty;
- invents information;
- overstates confidence;
- ignores culture;
- ignores salary;
- ignores the Candidate’s actual preferences;
- creates more work than it saves.

---

# 14. Success Metrics

## Primary MVP Success Metric

The user wants to submit another opportunity after receiving a Briefing.

This is the strongest early signal.

## Supporting Metrics

- Time saved compared to manual research.
- Number of useful insights per Briefing.
- Number of Briefings that lead to a clear decision.
- Number of Briefings rejected as generic.
- Number of times user asks for more research.
- Number of opportunities pursued.
- Number of opportunities rejected with clear reasons.
- User-rated usefulness of each Briefing.

## Qualitative Success Signal

The MVP is working if the user says:

> This helped me understand the opportunity better than I would have on my own.

## Failure Signal

The MVP is failing if the user says:

> I could have gotten the same result by pasting the job post into ChatGPT.

---

# 15. Validation Plan

The MVP should be tested with 10 real opportunities.

## Test Batch

- 3 aspirational companies;
- 3 realistic strong-fit companies;
- 2 uncertain companies;
- 1 company with good product but questionable culture;
- 1 company with missing salary information.

## For each Briefing, evaluate:

- Was it useful?
- Did it save time?
- Was the recommendation clear?
- Were the concerns fair?
- Was uncertainty handled honestly?
- Did it reflect the Candidate profile?
- Would the user pursue, reject, save, or research more?
- What was missing?
- What should improve?

## After 10 opportunities

Signal should produce a simple validation review:

- pursued count;
- rejected count;
- saved count;
- research-more count;
- common rejection reasons;
- most valuable Briefing sections;
- weakest Briefing sections;
- what should be automated next.

---

# 16. Release Plan

## MVP 0.1 — Manual Briefing Generator

### Scope

- Candidate profile file;
- opportunity input;
- basic company research;
- role research;
- fit evaluation;
- briefing generation;
- feedback capture.

### Goal

Validate briefing quality.

---

## MVP 0.2 — Knowledge Reuse

### Scope

- store previous company research;
- reuse known company information;
- update company records;
- compare new opportunities from same company.

### Goal

Validate knowledge as an asset.

---

## MVP 0.3 — Semi-Automated Research

### Scope

- assisted search;
- source collection;
- structured research reports;
- basic freshness tracking.

### Goal

Reduce manual research effort.

---

## MVP 0.4 — Opportunity Queue

### Scope

- submit multiple opportunities;
- process queue;
- rank briefings;
- show top opportunities.

### Goal

Validate prioritization.

---

## MVP 0.5 — Strategy Suggestions

### Scope

- recommend pursue/reject/research more;
- simple outreach suggestion;
- simple application suggestion;
- no external action.

### Goal

Validate next-action guidance.

---

# 17. Key Risks

## Risk 1 — Briefings are generic

If briefings feel like generic ChatGPT summaries, the MVP fails.

## Risk 2 — Research is unreliable

If company culture, salary, or benefits research is weak, recommendations may lose credibility.

## Risk 3 — Scope expands too early

If discovery, outreach, CRM, or UI polish enter too early, the MVP may become too large.

## Risk 4 — User feedback is too sparse

If feedback is not captured consistently, Signal will not improve.

## Risk 5 — Too much structure too early

If the system over-engineers domain artifacts before proving briefing quality, progress may slow unnecessarily.

## Risk 6 — Too much manual work

If the MVP requires the user to provide too much input, it may not feel valuable.

---

# 18. Open Questions

1. What is the first implementation interface: CLI, markdown, or minimal web form?
2. Should MVP 0.1 use live web search or only user-provided content?
3. What is the first Candidate profile format?
4. What is the first Opportunity input format?
5. Where should Briefings be stored?
6. Where should Feedback be stored?
7. What is the maximum acceptable cost per Briefing?
8. How many sources are required before evaluating culture?
9. How should confidence be represented visually or textually?
10. What is the minimum useful research depth?
11. Should the first version include source links?
12. Should the first version generate markdown files as outputs?
13. How should the system avoid inventing salary estimates?
14. What should happen when information is insufficient?
15. What should be automated immediately after MVP 0.1 validates?

---

# 19. Definition of Done for MVP 0.1

MVP 0.1 is done when:

- the Candidate profile exists;
- the user can submit one opportunity;
- Signal can research or process the company and role;
- Signal can generate a structured Briefing;
- the Briefing reflects the Candidate profile;
- the user can provide feedback;
- feedback is stored;
- activity is logged;
- at least 10 real opportunities have been tested;
- a validation review has been produced.

---

# 20. Final Constraint

The MVP should not become a smaller version of the full product.

It should remain focused on one core question:

> Can Signal produce a useful, personalized, explainable opportunity briefing?

Until this is proven, broader automation should not be prioritized.
