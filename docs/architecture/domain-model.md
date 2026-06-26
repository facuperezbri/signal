# Domain Model

Status: Draft
Last updated: 2026-06-26

## Purpose

This document defines the core domain entities of Signal.

Signal is a career intelligence system. Its value does not come from isolated prompts, dashboards, or automations. Its value comes from building and maintaining structured knowledge about the candidate, companies, opportunities, strategies, and outcomes.

The domain model should support the V1 goal:

> Help the user find the right job within six months without turning job hunting into a second job.

## Core principle

Signal does not work directly with raw job posts.

Signal transforms raw market information into structured, explainable, reusable career intelligence.

The system pipeline is:

```text
Discover
  ↓
Research
  ↓
Understand
  ↓
Evaluate
  ↓
Recommend
  ↓
Strategize
  ↓
Prepare
  ↓
Track
  ↓
Learn
```

Each stage should produce a durable artifact whenever possible.

---

# Core Entities

## 1. Candidate

The Candidate represents the person Signal is helping.

In V1, Signal is optimized for a single candidate. Multi-user support is explicitly out of scope for the MVP, but the model should not make future multi-user support impossible.

### Candidate contains

- identity;
- professional profile;
- experience;
- skills;
- career goals;
- values;
- preferences;
- constraints;
- compensation expectations;
- company whitelist;
- company blacklist;
- feedback history;
- decision history.

### Important distinction

The Candidate is not the resume.

The resume is one representation of the Candidate.

Signal should maintain a richer model than what appears in a CV.

### Example Candidate knowledge

```json
{
  "professionalIdentity": "Senior Frontend Engineer specialized in React, evolving toward AI Product Engineering",
  "primaryGoal": "Find a high-quality product company with excellent culture, compensation, benefits, and technical standards",
  "preferredRoles": [
    "Senior Frontend Engineer",
    "Product Engineer",
    "AI Product Engineer",
    "Frontend Engineer with AI exposure"
  ],
  "values": [
    "excellent culture",
    "feeling valued",
    "work-life balance",
    "flexibility",
    "product impact",
    "strong benefits"
  ],
  "avoid": [
    "consulting companies",
    "outsourcing companies",
    "traditional banking environments",
    "legacy-only maintenance roles",
    "toxic culture"
  ]
}
```

---

## 2. Company

A Company is an objective organization in the market.

It exists independently of whether there are open roles.

The Company entity stores factual or mostly factual information.

### Company contains

- name;
- website;
- industry;
- products;
- company size;
- headquarters;
- remote policy;
- funding stage;
- public links;
- known hiring pages;
- known social profiles;
- known job boards;
- known contacts;
- last discovered date;
- last updated date.

### Rule

A Company should not contain the system's opinion.

Opinions belong to CompanyProfile, ResearchReport, Evaluation, or Recommendation.

---

## 3. CompanyProfile

A CompanyProfile is Signal's current understanding of a company.

It is interpretive, not purely factual.

The CompanyProfile answers:

> What kind of company is this, and how does it appear to work?

### CompanyProfile contains

- product assessment;
- culture assessment;
- engineering assessment;
- benefits assessment;
- compensation assessment;
- remote/flexibility assessment;
- risk assessment;
- overall attractiveness;
- confidence;
- supporting reasons;
- concerns;
- last evaluated date;
- freshness status.

### Example

```json
{
  "companyId": "vercel",
  "summary": "Developer tools company with strong frontend focus, high technical standards, strong product culture, and significant influence in the React ecosystem.",
  "productScore": 9.8,
  "cultureScore": 8.8,
  "engineeringScore": 9.7,
  "benefitsScore": 8.5,
  "riskScore": 6.5,
  "confidence": 0.82,
  "strengths": [
    "Strong alignment with frontend engineering",
    "Product used by developers globally",
    "High technical reputation"
  ],
  "concerns": [
    "Likely highly competitive hiring process",
    "Potentially high performance expectations"
  ]
}
```

### Rule

CompanyProfile should be refreshed when:

- new relevant information appears;
- the profile becomes stale;
- a new opportunity appears at the company;
- the user asks for a refresh;
- the company becomes strategically important.

---

## 4. Opportunity

An Opportunity is a concrete path that could increase the candidate's probability of getting the right job.

In V1, opportunities should be limited to practical job-search actions.

### V1 opportunity types

- published job opening;
- company with no open role but strong fit;
- recruiter contact;
- engineering manager contact;
- CTO/founder contact;
- referral path.

### Explicitly out of scope for V1

- conferences;
- events;
- courses;
- long-term career coaching;
- salary negotiation workflows;
- public content strategy.

### Opportunity contains

- company;
- type;
- source;
- role title, when applicable;
- job description, when applicable;
- salary range, when available;
- location;
- remote policy;
- seniority;
- requirements;
- responsibilities;
- detected fit;
- detected gaps;
- current status;
- discovered date;
- expiration date, when applicable.

### Rule

A job opening is one type of Opportunity.

It is not the only type.

---

## 5. ResearchReport

A ResearchReport is a structured artifact produced by research.

It captures what was researched, what was found, how reliable it is, and when it should be revisited.

### ResearchReport contains

- subject type;
- subject id;
- research category;
- sources;
- findings;
- confidence;
- contradictions;
- freshness;
- cost;
- created date;
- expiration/staleness date.

### Research categories

- product;
- culture;
- benefits;
- compensation;
- engineering;
- hiring process;
- remote policy;
- company risk;
- role requirements;
- contact discovery.

### Rule

Research should be reusable.

If Signal researches a company's culture today, that knowledge should be available to future evaluations.

---

## 6. Evaluation

An Evaluation compares something against the Candidate.

Evaluation answers:

> Given what we know about the candidate, how good is this company or opportunity?

### Evaluation can evaluate

- a Company;
- an Opportunity;
- a Strategy;
- an ApplicationPackage.

### Evaluation contains

- subject;
- candidate id;
- score;
- confidence;
- positive signals;
- negative signals;
- warnings;
- dealbreakers;
- missing information;
- recommendation level;
- explanation.

### Recommendation levels

- strongly recommend;
- recommend;
- worth reviewing;
- uncertain;
- not recommended.

### Rule

The system may recommend something despite gaps if it can explain why.

Example:

A role asks for Go experience, which the candidate does not have. Signal should not automatically discard it. It may recommend reviewing the opportunity if the company, role, product, or hiring strategy suggests there is still a credible path.

---

## 7. Recommendation

A Recommendation is an internal decision that something may deserve the user's attention.

Not every Recommendation becomes a Briefing.

### Recommendation contains

- company;
- opportunity, when applicable;
- evaluation;
- proposed strategy;
- priority;
- confidence;
- reasons;
- warnings;
- status;
- created date.

### Rule

Recommendations are not raw search results.

They are the product of research, understanding, evaluation, and prioritization.

---

## 8. Briefing

A Briefing is what the user actually receives.

It is the user-facing artifact.

A Briefing should feel like a thoughtful analyst prepared the user for a decision.

### Briefing answers

- Why am I seeing this?
- What did Signal investigate?
- Why might this be a fit?
- What are the risks?
- What is the recommended strategy?
- What is already prepared?
- What decision does Signal need from me?

### Briefing contains

- title;
- company;
- opportunity;
- executive summary;
- scores or ratings;
- key reasons;
- concerns;
- salary information;
- recommended strategy;
- prepared assets;
- next actions;
- confidence;
- feedback options.

### Rule

The user should not receive unfinished thinking.

If the system does not know enough, it should research more before generating a Briefing.

If uncertainty remains, the Briefing must explicitly say so.

---

## 9. Strategy

A Strategy defines the best way to pursue an Opportunity.

Applying through a job form is only one possible strategy.

### Strategy types

- apply through official careers page;
- apply through LinkedIn;
- contact recruiter;
- contact engineering manager;
- contact CTO/founder;
- ask for referral;
- monitor company until a better opening appears;
- do not pursue.

### Strategy contains

- opportunity;
- recommended action;
- rationale;
- expected upside;
- expected risk;
- effort;
- confidence;
- required assets;
- approval status.

### Rule

The system should recommend the strategy most likely to increase the probability of getting a conversation, not merely the easiest action.

---

## 10. ApplicationPackage

An ApplicationPackage contains everything needed to execute a Strategy.

### ApplicationPackage may contain

- tailored resume;
- cover letter;
- LinkedIn message;
- email;
- answers to application questions;
- portfolio links;
- notes on what to emphasize;
- notes on what not to emphasize.

### Rule

No ApplicationPackage should be sent externally without explicit user approval.

---

## 11. Contact

A Contact is a person related to a company or opportunity.

### Contact types

- recruiter;
- engineering manager;
- CTO;
- founder;
- employee;
- potential referrer.

### Contact contains

- name;
- role;
- company;
- LinkedIn URL;
- email, when available and appropriate;
- relevance;
- relationship status;
- outreach history;
- notes;
- last contacted date;
- next follow-up date.

### Rule

The system may suggest contacting someone, but it should not send messages without approval.

---

## 12. Application

An Application begins only when the user decides to pursue an Opportunity.

Before that, the system is researching and recommending.

### Application contains

- company;
- opportunity;
- strategy;
- package used;
- current stage;
- actions taken;
- messages sent;
- responses received;
- follow-ups;
- outcome;
- timeline.

### Application stages

- not started;
- prepared;
- approved;
- sent;
- replied;
- interview scheduled;
- rejected;
- paused;
- closed;
- offer.

---

## 13. Activity

Activity represents what the system has done.

It exists to build trust and auditability.

### Activity examples

- discovered company;
- researched company;
- updated company profile;
- discarded opportunity;
- created recommendation;
- generated briefing;
- prepared application package;
- user gave feedback;
- strategy changed;
- follow-up due.

### Rule

The user should be able to see that Signal is working without being overwhelmed by operational noise.

---

## 14. Feedback

Feedback is how the user teaches Signal.

### Feedback types

- approve;
- reject;
- disagree;
- ask for more research;
- mark as interesting;
- blacklist company;
- whitelist company;
- adjust preference;
- correct reasoning.

### Feedback should capture

- target;
- user action;
- explicit reason;
- optional free-text explanation;
- strength of signal;
- created date.

### Rule

Signal should learn from both explicit feedback and behavioral contradiction.

Example:

If the system says "not recommended" and the user still chooses to pursue the opportunity, that contradiction should be stored and reviewed.

---

# Key Relationships

## Company → CompanyProfile

A Company can have one current CompanyProfile and many historical CompanyProfiles.

## Company → Opportunity

A Company can have many Opportunities.

An Opportunity belongs to one Company.

## Company → Contact

A Company can have many Contacts.

A Contact may become part of a Strategy.

## Company / Opportunity → ResearchReport

ResearchReports can belong to a Company, Opportunity, Contact, or Strategy.

## Candidate → Evaluation

Evaluations are candidate-specific.

The same company can be excellent for one candidate and poor for another.

## Evaluation → Recommendation

A Recommendation is created from one or more Evaluations.

## Recommendation → Briefing

Only selected Recommendations become Briefings.

## Briefing → Feedback

The user gives Feedback on Briefings, Recommendations, Strategies, Companies, or Opportunities.

## Strategy → ApplicationPackage

A Strategy determines what assets need to be prepared.

## ApplicationPackage → Application

An ApplicationPackage becomes part of an Application only after the user approves pursuing the Opportunity.

---

# Business Rules

## Rule 1: Human approval is required for external action

Signal may prepare messages, resumes, cover letters, and application answers.

Signal may not send, submit, or contact anyone without explicit user approval.

## Rule 2: Salary unknown is not a dealbreaker

If salary is not published, Signal should research external compensation signals.

If salary remains unknown, the opportunity may still be shown with a warning.

## Rule 3: Divided culture signals require warning

If reviews or cultural signals are contradictory, Signal should not hide the opportunity.

It should show the opportunity with a clear warning and explain the contradiction.

## Rule 4: Strong gaps require explanation, not automatic rejection

If an opportunity asks for skills the candidate lacks, Signal should evaluate whether the gap is fatal.

If it still recommends the opportunity, it must explain why.

## Rule 5: The system should learn cautiously

Signal may detect preference patterns, but it should avoid overfitting.

If the user repeatedly rejects a category, Signal may reduce priority for that category.

However, it should still surface exceptional outliers with explanation.

## Rule 6: The early product should show more opportunities

During the learning phase, Signal should show more exploratory recommendations.

The purpose is to learn the candidate's preferences and build trust.

## Rule 7: The mature product should be more selective

As Signal gains confidence in the candidate model, it should interrupt less often and only surface stronger recommendations.

## Rule 8: Activity should be visible, but not noisy

The system should show evidence of work performed.

It should not require the user to manage or supervise the system.

---

# Open Questions

These questions are intentionally unresolved.

They should be answered before implementation.

1. How should candidate preference confidence be represented?
2. How should freshness and staleness be calculated for company research?
3. What minimum evidence is required before creating a Briefing?
4. How should Signal estimate compensation when salary is not published?
5. How should Signal prioritize between culture, compensation, product, and technical fit?
6. What feedback options should appear in the first version?
7. What should be considered a high-confidence recommendation?
8. How should blacklisted companies be handled if new evidence suggests meaningful change?
9. How should the system represent uncertainty in a way that feels useful rather than vague?
10. What is the minimum viable ApplicationPackage?
