# ADR-006: Briefings over dashboards

Status: Accepted
Date: 2026-06-26

## Context

Signal is designed for a user who is not actively job hunting.

The user already has a job, is comfortable enough, and does not want job searching to become a second job.

Traditional job-search tools usually present dashboards, lists, filters, cards, statuses, and pipelines.

That model assumes the user wants to actively manage the job search process.

Signal has a different goal.

The user wants the system to do the heavy work, reduce noise, and only ask for attention when something meaningful appears.

During product discovery, the user expressed that a conversational, WhatsApp-like experience may be more valuable than a traditional application dashboard.

The user also wants to see evidence that the system is working, especially during the early learning phase.

This creates a product tension:

- too little visibility makes the system feel inactive;
- too much visibility turns Signal into another tool to manage.

## Decision

Signal will prioritize briefings over dashboards.

The primary user-facing artifact should be a `Briefing`.

A Briefing is a concise, structured, explainable decision memo prepared by the system.

It should tell the user:

- why this company or opportunity deserves attention;
- what Signal investigated;
- what Signal likes;
- what Signal is concerned about;
- what salary or compensation information is known;
- what strategy Signal recommends;
- what assets Signal prepared;
- what decision the user needs to make.

Dashboards may exist later as secondary views, but they should not be the primary product experience.

## Options considered

### Option 1: Dashboard-first experience

Signal could present a dashboard with companies, opportunities, scores, filters, statuses, and actions.

This would be familiar and useful for structured review.

However, it risks making the user responsible for managing the system.

It also creates a product experience similar to existing job-search CRMs and productivity tools.

Rejected as the primary experience.

### Option 2: Pure chat experience

Signal could exist only as a conversational interface.

This aligns well with the user's desire for low-friction interaction and mobile access.

However, pure chat may become insufficient for reviewing structured artifacts, comparing opportunities, inspecting research, managing application packages, or auditing decisions.

Not rejected, but deferred as an interaction-layer decision.

### Option 3: Briefing-first experience

Signal produces structured briefings as the primary output.

Briefings can be rendered in multiple interfaces:

- chat;
- email;
- web;
- native app;
- notification;
- document view.

This preserves structure while allowing a conversational experience.

Accepted.

## Consequences

### Positive

- Protects user attention.
- Avoids turning job search into another management workflow.
- Makes recommendations feel thoughtful and prepared.
- Supports both conversational and structured interfaces.
- Keeps the intelligence layer independent from the UI.
- Encourages the system to complete research before interrupting.
- Creates a premium analyst-like experience.

### Negative

- Requires clear rules for when a briefing is ready.
- Requires thoughtful summarization.
- May hide too much detail if not designed carefully.
- Users may still need secondary views for history, tracking, and auditability.
- The system must balance concision with transparency.

## Design implications

The `Briefing` entity becomes a first-class domain artifact.

A Briefing should not be raw text from an LLM.

It should be generated from structured artifacts such as:

- Company;
- CompanyProfile;
- Opportunity;
- ResearchReports;
- Evaluation;
- Recommendation;
- Strategy;
- ApplicationPackage;
- Activity;
- Feedback.

The same Briefing should be renderable in different formats.

Examples:

- short chat message;
- expanded web view;
- email summary;
- native app card;
- markdown document.

## Briefing structure

A V1 Briefing should include:

1. Title
2. Company
3. Opportunity type
4. Executive summary
5. Why this appeared
6. Company fit
7. Role or opportunity fit
8. Salary or compensation information
9. Culture signals
10. Benefits signals
11. Technical fit
12. Concerns and warnings
13. Recommended strategy
14. Prepared assets
15. Decision needed
16. Feedback options

## Example

```text
I found a company worth reviewing.

Company: ExampleCo
Opportunity: Senior Frontend Engineer
Recommended strategy: Apply through the official careers page and contact the frontend engineering manager.

Why this deserves attention:
- Strong product fit.
- Excellent culture signals.
- React and TypeScript are central to the role.
- Compensation appears aligned with your expectations.
- The company has strong benefits and remote flexibility.

What worries me:
- Reviews mention a demanding hiring process.
- Salary is not published, but external estimates are promising.

I prepared:
- a tailored resume angle;
- a short outreach message;
- notes on what to emphasize.

Decision needed:
Do you want to review the full package, ask me to research more, or discard this?
```

## Activity visibility

Briefings should be complemented by lightweight activity visibility.

The user should be able to see that Signal is working without being forced to manage it.

Activity summaries may include:

- companies analyzed;
- companies discarded;
- company profiles updated;
- opportunities found;
- recommendations created;
- briefings prepared;
- research refreshed;
- feedback incorporated.

Activity should build trust.

It should not become a task list.

## Early learning phase

During the early phase, Signal should show more exploratory briefings.

The goal is to learn the user's preferences and build trust.

These briefings may explicitly say:

> I am not fully confident this is a perfect fit, but I want to test whether this type of company interests you.

## Mature phase

As Signal gains confidence, it should become more selective.

The system should interrupt less often and only surface stronger opportunities.

The user should feel:

> Signal is quiet because it is filtering aggressively, not because it is inactive.

## Notes

This ADR does not eliminate dashboards forever.

It defines the primary experience.

Dashboards, tables, and structured views may exist later to support:

- reviewing history;
- auditing decisions;
- managing applications;
- comparing companies;
- inspecting research.

However, the product should not start from the assumption that the user wants to manage a dashboard.

Signal should start from the assumption that the user wants a high-quality briefing that helps them decide what to do next.
