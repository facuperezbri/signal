# ADR-003: Knowledge as an asset

Status: Accepted
Date: 2026-06-26

## Context

Signal depends on researching and understanding companies, opportunities, contacts, compensation, benefits, engineering quality, culture, and fit.

A naive AI implementation would repeatedly ask an LLM to analyze the same company, role, or opportunity every time it appears.

That approach has several problems:

- it wastes tokens;
- it creates inconsistent conclusions;
- it makes reasoning hard to audit;
- it prevents long-term learning;
- it makes the system overly dependent on prompt quality;
- it treats AI responses as disposable text instead of durable knowledge.

Signal needs to behave more like an analyst than a chatbot.

An analyst does not re-learn the same company every morning.

An analyst builds a file, updates it when new evidence appears, and reuses prior knowledge.

## Decision

Signal will treat knowledge as a durable product asset.

Research, evaluations, company profiles, recommendations, strategies, feedback, and activity should be stored as structured artifacts whenever possible.

The LLM is not the source of truth.

The LLM may help reason, synthesize, classify, explain, or generate drafts.

But the application should persist the resulting knowledge in structured form.

The system should prefer reusing existing knowledge before generating new AI reasoning.

## Options considered

### Option 1: Prompt-only system

Signal could use prompts to research and reason on demand every time the user asks a question or a new opportunity appears.

This would be simple to prototype but expensive, inconsistent, and hard to improve over time.

Rejected.

### Option 2: Store only final user-facing text

Signal could store generated briefings, messages, and summaries, but not the underlying structured reasoning.

This would preserve outputs but not make the knowledge reusable.

Rejected.

### Option 3: Store structured knowledge artifacts

Signal stores reusable artifacts such as ResearchReports, CompanyProfiles, Evaluations, Strategies, Recommendations, Briefings, Feedback, and Activity.

This creates a durable knowledge base that can be reused, refreshed, audited, and improved.

Accepted.

## Consequences

### Positive

- Lower token usage over time.
- Better consistency across recommendations.
- Ability to refresh only stale knowledge.
- Easier auditability.
- Stronger product memory.
- Better learning from user feedback.
- Less dependence on any single LLM provider.
- Easier future migration between models or interfaces.
- Stronger foundation for analytics and improvement.

### Negative

- More upfront modeling work.
- More complexity than a prompt-only prototype.
- Requires deciding what information is structured enough to persist.
- Requires freshness and staleness rules.
- Requires versioning or history for changing knowledge.
- Requires care to avoid storing low-quality or unsupported conclusions.

## Design implications

Signal should create and reuse structured artifacts such as:

- Candidate;
- Company;
- CompanyProfile;
- Opportunity;
- ResearchReport;
- Evaluation;
- Recommendation;
- Briefing;
- Strategy;
- ApplicationPackage;
- Contact;
- Application;
- Activity;
- Feedback.

Important knowledge should include:

- source references;
- confidence;
- freshness;
- created date;
- last updated date;
- reasoning;
- contradictions;
- warnings;
- user feedback.

## Example

If Signal researches Expensify today, it may create:

- a Company record;
- multiple ResearchReports;
- a CompanyProfile;
- a CompensationEstimate;
- a CultureAssessment;
- a RiskAssessment;
- known Contacts;
- relevant Opportunities.

If another Expensify opportunity appears next week, Signal should not restart from zero.

It should ask:

- What do we already know?
- Is the existing knowledge still fresh?
- Did anything important change?
- What additional research is needed for this specific opportunity?

## Freshness principle

Not all knowledge expires at the same speed.

Examples:

- a job opening may become stale quickly;
- salary information may become stale moderately quickly;
- company culture may change slowly;
- benefits may change occasionally;
- hiring process information may become stale after several months;
- user preferences may change based on explicit feedback.

Signal should refresh knowledge based on importance, age, confidence, and detected change.

## Cost principle

Before making an expensive AI call, Signal should check:

1. Do we already know this?
2. Is the existing knowledge fresh enough?
3. Can deterministic logic answer this?
4. Can a cheaper capability answer this?
5. Is LLM reasoning necessary?

Only then should the system use more expensive reasoning.

## Auditability principle

Stored knowledge should make recommendations explainable.

If Signal recommends a company, the user should be able to inspect:

- what was researched;
- what sources were used;
- what conclusions were drawn;
- how confident Signal is;
- what concerns exist;
- what has changed since the last evaluation;
- how user feedback affected the recommendation.

## Notes

This decision is central to Signal's identity.

Signal should not feel like a chatbot that generates answers from scratch.

It should feel like a career intelligence system that accumulates understanding over time.

The product should become more useful the longer it is used.
