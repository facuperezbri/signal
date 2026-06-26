# MVP Scope

Status: Draft
Last updated: 2026-06-26

## Purpose

This document defines the scope of the first usable version of Signal.

Signal’s long-term vision is to become a career intelligence system that continuously researches the market, understands companies, evaluates opportunities, prepares strategies, and helps the user find the right job without turning job hunting into a second job.

However, the first MVP must be much smaller.

The MVP should not attempt to automate the entire job search process.

The MVP exists to validate the smallest useful intelligence loop:

> Can Signal take a company or opportunity, research it, evaluate it against the candidate profile, and produce a useful briefing that helps the user make a better decision faster?

If the answer is yes, the product thesis is worth expanding.

If the answer is no, automation, dashboards, outreach, agents, and tracking do not matter yet.

---

# Product Context

The user is a senior frontend engineer specialized in React, with growing AI Engineering knowledge.

The user is currently employed and not urgently looking for a job.

They are comfortable enough in their current role and do not want job hunting to become a second job.

However, they want to avoid missing an exceptional opportunity.

The ideal outcome within six months is:

> The user starts working at a company with excellent culture, strong compensation, meaningful benefits, flexibility, an interesting product, and strong technical standards.

Signal should help the user get closer to that outcome by reducing manual research, improving decision quality, and preparing clear opportunity briefings.

---

# MVP Goal

The MVP goal is to validate whether Signal can help the user evaluate job opportunities better and faster than manual research.

The MVP is not a complete job-search automation system.

The MVP is a briefing generator and feedback loop.

It should help answer:

- Is this company worth my attention?
- Is this role aligned with my profile?
- What do we know about culture, product, benefits, salary, and technical fit?
- What are the risks?
- What information is missing?
- Should I pursue, reject, save, or research more?

---

# MVP Hypothesis

If Signal can transform a raw company or job opportunity into a structured, useful, explainable briefing, then the core product thesis is valid.

A useful briefing should save the user time and improve decision quality.

The MVP hypothesis is:

> A structured AI-assisted briefing can create enough value that the user would repeatedly use Signal to evaluate real job opportunities.

---

# MVP Positioning

The MVP should be understood as:

> A personal career opportunity briefing system.

It is not yet:

- a job board;
- a CRM;
- a full application tracker;
- an autonomous job-search agent;
- a LinkedIn outreach automation tool;
- a resume optimization platform;
- a WhatsApp assistant;
- a native app;
- a multi-user SaaS product.

The MVP is the smallest version of Signal that can prove whether the intelligence loop is valuable.

---

# MVP Core Loop

The MVP core loop is:

```text
User submits opportunity
        ↓
Signal researches company and role
        ↓
Signal evaluates fit against Candidate profile
        ↓
Signal generates structured Briefing
        ↓
User gives feedback
        ↓
Signal stores feedback and result
        ↓
Next briefing improves slightly
```

This loop must work before any discovery automation is built.

---

# Why This MVP Comes First

The original product vision includes discovery, company monitoring, outreach, application packages, activity summaries, learning loops, and eventually a conversational interface.

Those are valuable, but they depend on one core ability:

> Signal must be able to evaluate opportunities well.

If Signal cannot generate a valuable briefing from a known opportunity, then automatically discovering more opportunities would only create more noise.

Therefore, the MVP validates evaluation before automation.

---

# MVP Input

The MVP accepts manually provided or semi-manually collected opportunities.

An opportunity may include:

- company name;
- company website;
- job post URL;
- job description text;
- role title;
- salary information, if available;
- location;
- remote policy, if available;
- user notes;
- source;
- optional reason why the user is interested.

## Example Input

```json
{
  "companyName": "ExampleCo",
  "companyWebsite": "https://example.com",
  "jobPostUrl": "https://example.com/careers/senior-frontend-engineer",
  "roleTitle": "Senior Frontend Engineer",
  "jobDescription": "...",
  "salaryRange": null,
  "location": "Remote",
  "source": "LinkedIn",
  "userNotes": "The product looks interesting, but I do not know anything about the culture."
}
```

## Input Rules

The MVP does not need to automatically discover the entire market.

The user may manually paste opportunities at first.

This is acceptable because the MVP is validating briefing quality, not discovery automation.

---

# MVP Output

The MVP produces a structured Briefing.

A Briefing is the primary user-facing artifact.

The Briefing should be useful even if rendered as:

- markdown;
- web view;
- chat message;
- email;
- document;
- console output.

The interface is not the core value yet.

The structured evaluation is.

---

# MVP Briefing Structure

A V1 Briefing should include:

## 1. Executive Summary

A short explanation of whether the opportunity deserves attention.

Example:

> This opportunity is worth reviewing. The company appears to have strong product-market relevance, a frontend-heavy role, and promising culture signals. However, salary is not published and benefits information is incomplete.

## 2. Company Summary

What the company does.

Should include:

- product;
- target users;
- market;
- business type;
- maturity/stage when available.

## 3. Role Summary

What the role appears to involve.

Should include:

- title;
- seniority;
- main responsibilities;
- required skills;
- preferred skills;
- frontend relevance;
- AI relevance, if any;
- backend/full-stack expectations.

## 4. Fit Assessment

A structured assessment against the Candidate profile.

Should include:

- technical fit;
- product fit;
- culture fit;
- compensation fit;
- benefits fit;
- flexibility/work-life balance fit;
- growth/learning fit;
- overall recommendation.

## 5. Positive Signals

A list of reasons why the opportunity may be attractive.

Examples:

- React/TypeScript are central to the role.
- Company appears product-led.
- Culture signals are positive.
- Remote/flexible work appears supported.
- Product is used by real people or teams.
- Role aligns with frontend and AI interests.

## 6. Concerns and Risks

A list of reasons to be cautious.

Examples:

- Salary not published.
- Reviews are mixed.
- Role asks for backend skills outside the candidate’s strongest area.
- Company stage may imply instability.
- Work-life balance signals are unclear.
- Benefits information is incomplete.

## 7. Missing Information

A list of important unknowns.

Examples:

- exact salary range;
- benefits by country;
- team culture;
- hiring process;
- manager expectations;
- remote policy details;
- whether contractor employment is supported.

## 8. Recommended Action

One clear next step.

Possible actions:

- pursue;
- reject;
- save for later;
- research more;
- ask for compensation details;
- look for internal contacts;
- wait until more information is available.

## 9. Confidence Level

A simple confidence label.

Suggested values:

- High;
- Medium;
- Low.

Confidence should reflect the quality and completeness of evidence, not how exciting the company is.

## 10. Feedback Prompt

The Briefing should end by asking for feedback.

Example:

> Do you want to pursue this, reject it, save it for later, or ask me to research one specific area more deeply?

---

# MVP Candidate Profile

The MVP requires a basic Candidate profile.

This profile can initially be stored as a structured markdown or JSON file.

It does not need a full UI.

## Candidate Profile Must Include

- professional identity;
- current role;
- core skills;
- preferred roles;
- preferred company types;
- avoided company types;
- values;
- constraints;
- compensation importance;
- culture importance;
- product importance;
- flexibility importance;
- work-life balance importance;
- AI interest;
- approval preferences.

## Initial Candidate Summary

```text
The candidate is a Senior Frontend Engineer specialized in React, with growing AI Engineering knowledge.

They want to work at a product company where the product has impact, the culture is excellent, compensation is strong, benefits are meaningful, and work-life balance is respected.

They prefer companies where they can feel valued, learn, work with strong technical teams, and contribute to products people actually use.

They want to avoid consulting companies, outsourcing companies, traditional banking environments, toxic cultures, and legacy-only maintenance roles.

They are not urgently job hunting, so Signal must protect their attention and surface only opportunities worth reviewing.
```

---

# MVP Entities

The MVP should use a reduced subset of the full domain model.

## Required for MVP

### Candidate

Represents the user profile, goals, values, preferences, skills, and constraints.

### Company

Represents basic factual company information.

### Opportunity

Represents the submitted job opening or company opportunity.

### ResearchReport

Represents structured research findings.

### Evaluation

Represents fit analysis against the Candidate.

### Briefing

Represents the final user-facing decision artifact.

### Feedback

Represents the user’s reaction to the Briefing.

### Activity

Represents important system actions for auditability.

---

## Deferred Entities

These entities may exist conceptually but should not be fully implemented in the first MVP unless absolutely necessary:

### Strategy

May be represented as a simple section inside the Briefing for now.

### ApplicationPackage

Deferred. No tailored resume or cover letter generation in MVP unless manually triggered later.

### Contact

Deferred. No contact discovery in MVP.

### Application

Deferred. No full application tracking in MVP.

### Historical CompanyProfile

Deferred. Basic company understanding can exist inside ResearchReport and Evaluation first.

---

# MVP Capabilities

The MVP should implement only the capabilities needed for the core loop.

## Must Have

### 1. Build Candidate Profile

Create or load the user’s initial Candidate profile.

### 2. Input Opportunity

Allow the user to provide a company and/or job opportunity.

### 3. Research Company Basics

Gather basic information about the company.

Research should focus on:

- product;
- company description;
- industry;
- users/customers;
- culture signals;
- benefits signals;
- remote/flexibility signals;
- engineering signals.

### 4. Research Role Basics

Analyze the job post when available.

Research should focus on:

- role responsibilities;
- required skills;
- seniority;
- frontend relevance;
- AI relevance;
- backend/full-stack expectations;
- salary if published;
- location and remote constraints.

### 5. Evaluate Company Fit

Evaluate the company against the Candidate profile.

### 6. Evaluate Opportunity Fit

Evaluate the role or opportunity against the Candidate profile.

### 7. Generate Briefing

Generate the structured user-facing Briefing.

### 8. Capture Feedback

Allow the user to respond to the Briefing.

Basic feedback options:

- pursue;
- reject;
- save for later;
- research more;
- disagree;
- blacklist company;
- mark as exciting.

### 9. Store Activity

Record key actions.

Examples:

- opportunity submitted;
- research completed;
- briefing generated;
- feedback captured.

### 10. Reuse Existing Knowledge

If the same company is evaluated again, reuse existing stored information when possible.

---

## Should Have

These are useful but not required for the first working MVP:

- ask targeted follow-up questions when information is missing;
- show previous evaluations for the same company;
- compare two opportunities;
- regenerate Briefing after feedback;
- store user preference insights;
- basic cost logging;
- basic source citations or source list;
- manually refresh company research.

---

## Could Have

These are explicitly optional:

- prepare outreach message;
- prepare resume angle;
- generate cover letter;
- find recruiter or engineering manager;
- track application status;
- generate weekly summary;
- estimate salary from external sources;
- advanced learning from contradiction;
- confidence calibration over time.

---

# Out of Scope for MVP

The MVP does not include:

- automatic job discovery;
- scraping LinkedIn at scale;
- automatic applications;
- automatic LinkedIn outreach;
- sending messages;
- email integration;
- Gmail integration;
- Google Calendar integration;
- WhatsApp integration;
- Telegram integration;
- native mobile app;
- native macOS app;
- full dashboard;
- CRM pipeline;
- multi-user support;
- authentication;
- billing;
- public SaaS onboarding;
- advanced analytics;
- salary negotiation assistant;
- long-term career advisor;
- conference or event recommendations;
- public content strategy;
- LinkedIn profile optimization;
- automatic portfolio updates.

---

# MVP User Experience

The MVP user experience should be intentionally simple.

A first version could work through:

- markdown files;
- a CLI;
- a minimal web form;
- a local script;
- a simple internal web page;
- a chat-like interface later.

The interface is secondary.

The MVP should prove that the Briefing is valuable.

## Minimal UX Flow

1. User submits an opportunity.
2. System confirms received input.
3. System researches and evaluates.
4. System returns a Briefing.
5. User gives feedback.
6. System stores feedback.
7. User submits another opportunity.

## Example MVP Interaction

User submits:

```text
Company: ExampleCo
Role: Senior Frontend Engineer
Job URL: https://example.com/careers/senior-frontend-engineer
Notes: Product looks interesting, but I do not know if the culture is good.
```

Signal returns:

```text
Briefing: ExampleCo — Senior Frontend Engineer

Recommendation: Worth reviewing

Why:
- Strong frontend alignment.
- Product appears relevant and mature.
- Culture signals are mostly positive, but not enough evidence yet.
- Salary is not published.

Concerns:
- Backend expectations are unclear.
- Benefits information is incomplete.
- Hiring process may be demanding.

Recommended next step:
Research compensation and team culture before applying.

Feedback:
Pursue / Reject / Save / Research more / Disagree
```

---

# MVP Learning

The MVP should learn, but only in a basic and cautious way.

## What MVP Learning Means

The MVP should store:

- which opportunities the user pursued;
- which opportunities the user rejected;
- why the user rejected something;
- which companies were marked exciting;
- which companies were blacklisted;
- which concerns mattered most.

## What MVP Learning Does Not Mean Yet

The MVP does not need advanced automatic preference modeling.

It does not need complex machine learning.

It does not need to dynamically adjust every score.

It only needs to preserve feedback in a way that can inform future evaluations.

## Example Feedback Record

```json
{
  "target": "briefing_exampleco_001",
  "action": "reject",
  "reason": "culture",
  "comment": "Reviews feel too mixed and I do not want to risk another bad culture.",
  "createdAt": "2026-06-26"
}
```

---

# MVP Cost Rules

The MVP should follow cost-aware principles from day one.

## Rules

1. Do not deeply research every submitted opportunity unless needed.
2. Reuse existing company research when possible.
3. Do not generate application assets unless explicitly requested.
4. Do not call expensive models for deterministic parsing when simpler methods are enough.
5. Log meaningful AI usage if possible.
6. Prefer structured outputs over long unstructured prose.
7. Avoid open-ended research loops.

## MVP Cost Goal

The MVP should be cheap enough to run casually while testing real opportunities.

It should not create anxiety about token usage.

---

# MVP Quality Bar

The MVP is successful only if the Briefings are genuinely useful.

A Briefing is useful if:

- it saves the user time;
- it summarizes the company clearly;
- it identifies relevant fit and gaps;
- it surfaces risks;
- it distinguishes facts from interpretation;
- it is honest about uncertainty;
- it recommends a clear next action;
- it helps the user decide what to do.

A Briefing is not useful if:

- it repeats the job description;
- it sounds generic;
- it overstates confidence;
- it hides missing information;
- it produces vague advice;
- it recommends everything;
- it fails to reflect the Candidate profile.

---

# MVP Success Criteria

The MVP succeeds if, after testing with real opportunities:

1. The user wants to submit another opportunity.
2. The user feels the Briefing saved time.
3. The user learns something useful from the Briefing.
4. The user can make a clearer decision.
5. The Briefing reflects the Candidate’s actual preferences.
6. The system stores feedback for future use.
7. The cost remains controlled.
8. The MVP reveals what should be automated next.

## Strong Success Signal

The strongest early success signal is:

> The user finds a real opportunity and says: “I would not have evaluated this this well on my own, and this helped me decide what to do.”

---

# MVP Failure Criteria

The MVP fails if:

- Briefings are generic;
- Briefings do not save time;
- the user still has to manually research everything;
- every opportunity receives the same recommendation;
- the system cannot explain its reasoning;
- feedback does not affect future outputs;
- the system feels like a wrapper around a job description;
- token cost feels uncontrolled;
- the user does not want to use it for a second opportunity.

---

# MVP Validation Plan

The MVP should be tested with a small number of real opportunities.

## Suggested Validation Batch

Test with 10 opportunities:

- 3 aspirational companies;
- 3 realistic strong-fit companies;
- 2 uncertain companies;
- 1 company with good product but questionable culture;
- 1 company with no salary information.

## For each opportunity, evaluate:

- Was the Briefing useful?
- Did it save time?
- Was the recommendation clear?
- Were the risks accurate?
- Was the confidence appropriate?
- Did it reflect the Candidate profile?
- What information was missing?
- Would the user pursue, reject, save, or research more?

## Validation Output

After 10 opportunities, Signal should produce a simple review:

- how many were pursued;
- how many were rejected;
- common rejection reasons;
- which signals mattered most;
- which Briefing sections were most useful;
- what should be automated next.

---

# MVP Roadmap

## MVP 0.1 — Manual Briefing Generator

Input is manual.

User provides company and/or job opportunity.

Signal produces a structured Briefing.

Feedback is captured manually or semi-manually.

Goal:

> Validate briefing quality.

---

## MVP 0.2 — Stored Knowledge and Reuse

Signal stores company research and feedback.

If the same company appears again, prior knowledge is reused.

Goal:

> Validate knowledge as an asset.

---

## MVP 0.3 — Semi-Automated Research

Signal assists with research more automatically.

May include search, source extraction, structured research reports, and freshness indicators.

Goal:

> Reduce manual research work.

---

## MVP 0.4 — Basic Opportunity Queue

User can add multiple opportunities.

Signal processes them and returns a small ranked set of Briefings.

Goal:

> Validate prioritization.

---

## MVP 0.5 — Basic Strategy Suggestions

Signal recommends simple next actions:

- pursue;
- reject;
- research more;
- contact someone;
- save for later.

Goal:

> Validate whether Signal can help decide what to do next.

---

# Key Product Constraint

The MVP should not become a mini version of the entire product.

It should remain focused on one question:

> Can Signal produce a useful, personalized, explainable opportunity briefing?

Until that question is answered, broader automation should wait.

---

# Open Questions

1. What is the simplest interface for MVP 0.1?
2. Should opportunity input be markdown, JSON, form-based, or chat-based?
3. What exact Candidate profile format should be used first?
4. What research sources should be allowed in MVP 0.1?
5. Should the MVP use web search from the beginning or start with user-provided content?
6. How much evidence is required before generating a Briefing?
7. How should confidence be represented?
8. Should the first Briefing be generated synchronously or as a saved artifact?
9. How should feedback be stored?
10. How many opportunities should be tested before expanding scope?
11. What sections of the Briefing are mandatory?
12. What is the maximum acceptable cost per Briefing?
13. How should the system distinguish between facts, assumptions, and opinions?
14. What is the first technical implementation path after this document is accepted?
