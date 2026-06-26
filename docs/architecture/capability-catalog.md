# Capability Catalog

Status: Draft
Last updated: 2026-06-26

## Purpose

This document defines the core capabilities Signal needs in order to transform job market noise into high-quality, explainable career opportunities.

A capability describes what the system can do.

It does not define implementation details.

A capability should be stable even if the underlying technology changes.

For example:

- `Research Company Culture` may initially be done manually or with web search.
- Later it may use structured APIs, scraping, embeddings, or LLM-based synthesis.
- The capability remains the same.

## Capability design principles

### 1. Capabilities are not agents

A capability is a system ability.

It may be executed by:

- deterministic logic;
- an API call;
- a script;
- an LLM;
- a human-assisted workflow;
- a future autonomous worker.

### 2. Capabilities produce artifacts

Whenever possible, a capability should produce a structured domain artifact.

Examples:

- ResearchReport;
- CompanyProfile;
- Evaluation;
- Recommendation;
- Briefing;
- Strategy;
- ApplicationPackage;
- Activity;
- Feedback.

### 3. Capabilities must be auditable

Every important capability should record:

- what it did;
- what input it used;
- what output it produced;
- what confidence it has;
- what sources were used;
- when it was executed;
- whether the result may become stale.

### 4. Cheap first

Capabilities should use the cheapest reliable method before using expensive AI reasoning.

Preferred order:

1. deterministic logic;
2. stored knowledge;
3. structured data;
4. search;
5. embeddings;
6. smaller models;
7. larger models.

### 5. Human approval for external action

Capabilities may prepare external actions.

They may not execute external actions without explicit user approval.

---

# Capability Groups

Signal capabilities are grouped into the following categories:

1. Candidate Intelligence
2. Company Discovery
3. Company Research
4. Opportunity Discovery
5. Evaluation
6. Strategy
7. Preparation
8. Tracking
9. Feedback & Learning
10. Activity & Briefing
11. Cost & Quality Control

---

# 1. Candidate Intelligence

Candidate Intelligence capabilities maintain Signal's understanding of the user.

The Candidate is not a resume. It is a living model of the user's skills, values, goals, constraints, preferences, and decision history.

---

## 1.1 Build Candidate Profile

### Purpose

Create the initial structured Candidate model.

### Inputs

- resume;
- LinkedIn profile;
- user conversation;
- portfolio;
- manual preferences;
- known constraints.

### Outputs

- Candidate;
- Activity.

### Notes

In V1, this may begin as a manually curated document or seed file.

The system should not require a long onboarding form if the same information can be built conversationally.

---

## 1.2 Update Candidate Preferences

### Purpose

Update preferences based on explicit user feedback.

### Inputs

- Feedback;
- rejected recommendations;
- accepted recommendations;
- user corrections;
- free-text comments.

### Outputs

- updated Candidate;
- PreferenceChange record;
- Activity.

### Rules

The system should learn cautiously.

It should avoid overfitting from small samples.

Example:

If the user rejects several companies under 500 employees, Signal may detect a possible pattern but should not permanently conclude that small companies are undesirable.

---

## 1.3 Detect Preference Pattern

### Purpose

Identify repeated user behavior that may indicate a preference.

### Inputs

- decision history;
- feedback history;
- company attributes;
- opportunity attributes.

### Outputs

- PreferenceInsight;
- optional Candidate update;
- Activity.

### Example

> The user has rejected 8 of the last 10 opportunities from consulting companies. This reinforces the existing preference to avoid consulting companies.

### Rule

Detected patterns should be treated as hypotheses, not permanent truth.

---

## 1.4 Capture Explicit Correction

### Purpose

Allow the user to correct the system when a recommendation feels wrong.

### Inputs

- target object;
- correction reason;
- optional explanation.

### Outputs

- Feedback;
- updated Evaluation notes;
- Activity.

### Example reasons

- product mismatch;
- culture concern;
- salary concern;
- role mismatch;
- stack mismatch;
- company reputation;
- personal context;
- other.

---

# 2. Company Discovery

Company Discovery capabilities identify companies that may deserve research.

---

## 2.1 Discover Companies

### Purpose

Find companies that may be relevant to the Candidate.

### Inputs

- target roles;
- preferred industries;
- known aspirational companies;
- job boards;
- public company lists;
- startup directories;
- hiring pages;
- previous companies;
- similar companies.

### Outputs

- CompanyCandidate;
- Activity.

### Notes

Discovery should not immediately create a Recommendation.

Discovery only adds possible companies to the universe.

---

## 2.2 Expand From Aspirational Companies

### Purpose

Find companies similar to known aspirational companies.

### Inputs

- whitelist;
- aspirational companies;
- company category;
- product type;
- industry;
- tech ecosystem.

### Outputs

- CompanyCandidate;
- ResearchReport;
- Activity.

### Example

If the Candidate likes Vercel, Signal may search for companies in:

- developer tools;
- frontend infrastructure;
- cloud deployment;
- product-led engineering tools.

---

## 2.3 Maintain Company Universe

### Purpose

Maintain the set of companies Signal knows about.

### Inputs

- CompanyCandidate;
- existing Company records;
- blacklist;
- whitelist;
- previous evaluations.

### Outputs

- Company;
- Activity.

### Rules

Companies should not be duplicated.

Blacklisted companies should not be recommended unless meaningful new evidence appears.

---

# 3. Company Research

Company Research capabilities transform a raw Company into structured knowledge.

---

## 3.1 Research Product

### Purpose

Understand what the company builds and whether the product is interesting to the Candidate.

### Inputs

- Company;
- website;
- product pages;
- docs;
- public demos;
- user reviews;
- app store/product reviews where applicable;
- public customer stories.

### Outputs

- ResearchReport;
- CompanyProfile update.

### Research questions

- What does the product do?
- Who uses it?
- Is the product something the Candidate could care about?
- Is the product used by developers, consumers, companies, or a niche audience?
- Does the product appear to have traction?

---

## 3.2 Research Culture

### Purpose

Understand whether the company appears to be a healthy place to work.

### Inputs

- employee reviews;
- public employee posts;
- company values;
- benefits pages;
- leadership communication;
- layoff history;
- public controversy;
- hiring pages.

### Outputs

- ResearchReport;
- CompanyProfile update.

### Research questions

- Do employees speak positively about the company?
- Are there repeated complaints?
- Are there signals of toxicity?
- Is there evidence of autonomy, respect, flexibility, and work-life balance?
- Are reviews divided?

### Rule

Contradictory cultural signals should not be hidden.

They should become explicit warnings.

---

## 3.3 Research Benefits

### Purpose

Understand compensation-adjacent value.

### Inputs

- careers page;
- benefits page;
- job posts;
- employee reviews;
- compensation platforms;
- public candidate reports.

### Outputs

- ResearchReport;
- CompanyProfile update.

### Research questions

- What benefits are offered?
- Is the company remote-friendly?
- Are there strong PTO, healthcare, learning, or flexibility benefits?
- Does the company appear to value employee well-being?

---

## 3.4 Research Engineering

### Purpose

Understand the technical environment.

### Inputs

- engineering blog;
- GitHub organization;
- open-source projects;
- tech talks;
- job descriptions;
- developer documentation;
- public team members.

### Outputs

- ResearchReport;
- CompanyProfile update.

### Research questions

- Does the company have strong engineering standards?
- Is frontend important?
- Is React/TypeScript relevant?
- Is AI part of the product or engineering workflow?
- Does the company publish technical content?
- Would this environment help the Candidate grow?

---

## 3.5 Research Compensation

### Purpose

Estimate compensation when salary is published or unpublished.

### Inputs

- job post salary range;
- compensation platforms;
- public salary reports;
- location;
- company stage;
- role seniority;
- previous known ranges.

### Outputs

- ResearchReport;
- CompensationEstimate;
- CompanyProfile update.

### Rule

Unknown salary is not a dealbreaker.

If salary remains unknown, Signal should show the opportunity with a warning.

---

## 3.6 Research Company Risk

### Purpose

Identify risks that could make the company less attractive.

### Inputs

- layoffs;
- funding history;
- company news;
- leadership changes;
- employee reviews;
- public controversy;
- hiring freezes;
- product decline.

### Outputs

- ResearchReport;
- RiskAssessment;
- CompanyProfile update.

### Rule

Risk should reduce confidence, not automatically discard a company unless it is clearly severe.

---

# 4. Opportunity Discovery

Opportunity Discovery capabilities identify concrete paths into a company.

---

## 4.1 Discover Job Openings

### Purpose

Find relevant published roles.

### Inputs

- Company;
- careers page;
- job boards;
- LinkedIn;
- Lever;
- Greenhouse;
- Ashby;
- Workable;
- role keywords.

### Outputs

- Opportunity;
- Activity.

### Relevant role families

- Senior Frontend Engineer;
- Frontend Engineer;
- Product Engineer;
- AI Product Engineer;
- Full Stack Engineer, when frontend-heavy;
- React Engineer.

---

## 4.2 Discover Contact Path

### Purpose

Find people who may represent a viable entry path into a company.

### Inputs

- Company;
- LinkedIn;
- public team pages;
- GitHub;
- company leadership pages;
- existing contacts.

### Outputs

- Contact;
- Opportunity;
- Activity.

### Relevant contacts

- recruiter;
- engineering manager;
- frontend lead;
- product engineering lead;
- CTO;
- founder;
- employee who could provide referral.

### Rule

Contact discovery does not mean outreach happens automatically.

---

## 4.3 Detect No Open Roles But Strong Fit

### Purpose

Create an opportunity when a company is excellent but has no currently relevant job opening.

### Inputs

- CompanyProfile;
- Candidate;
- Contact discovery;
- company hiring signals.

### Outputs

- Opportunity;
- Strategy;
- Recommendation.

### Example

A company has no open role, but it strongly matches the Candidate's values, product interests, and technical background. Signal may suggest contacting a relevant person.

---

# 5. Evaluation

Evaluation capabilities compare companies, opportunities, and strategies against the Candidate.

---

## 5.1 Evaluate Company Fit

### Purpose

Determine whether a company deserves attention.

### Inputs

- Candidate;
- Company;
- CompanyProfile;
- ResearchReports.

### Outputs

- Evaluation.

### Evaluation dimensions

- culture;
- product;
- compensation;
- benefits;
- technical quality;
- frontend relevance;
- AI relevance;
- stability;
- flexibility;
- work-life balance;
- personal excitement.

### Rule

Culture should have very high weight for this Candidate.

A company with an average product but excellent culture may be more attractive than a company with an incredible product and poor culture.

---

## 5.2 Evaluate Opportunity Fit

### Purpose

Determine whether a concrete opportunity is worth pursuing.

### Inputs

- Candidate;
- Opportunity;
- CompanyProfile;
- ResearchReports.

### Outputs

- Evaluation.

### Evaluation dimensions

- role fit;
- stack fit;
- seniority fit;
- salary fit;
- location/remote fit;
- requirements gap;
- growth potential;
- company fit.

### Rule

Strong skill gaps require explanation, not automatic rejection.

---

## 5.3 Evaluate Strategy Fit

### Purpose

Decide the best path to pursue an opportunity.

### Inputs

- Candidate;
- Company;
- Opportunity;
- Contacts;
- CompanyProfile.

### Outputs

- Strategy Evaluation.

### Strategy options

- apply normally;
- contact recruiter;
- contact engineering manager;
- contact CTO/founder;
- ask for referral;
- monitor;
- do not pursue.

### Rule

The best strategy is the one most likely to create a real conversation, not necessarily the easiest one.

---

## 5.4 Generate Recommendation

### Purpose

Create an internal recommendation based on research and evaluation.

### Inputs

- CompanyProfile;
- Opportunity;
- Evaluation;
- Strategy Evaluation.

### Outputs

- Recommendation.

### Rule

Not every recommendation becomes a user-facing Briefing.

---

# 6. Strategy

Strategy capabilities decide how to act.

---

## 6.1 Select Pursuit Strategy

### Purpose

Choose the best strategy for a given company or opportunity.

### Inputs

- Company;
- Opportunity;
- Contacts;
- Evaluation;
- Candidate.

### Outputs

- Strategy.

### Examples

For a large company:

> Apply through the official careers page and optionally find a recruiter.

For an early-stage startup:

> Contact the CTO or founder with a highly personalized message.

For a strong company with no open roles:

> Contact a relevant engineering leader and monitor future openings.

---

## 6.2 Explain Strategy

### Purpose

Explain why the selected strategy is recommended.

### Inputs

- Strategy;
- Evaluation;
- CompanyProfile;
- Candidate.

### Outputs

- Strategy explanation;
- Briefing section.

### Rule

Strategy must be understandable before the user approves it.

---

# 7. Preparation

Preparation capabilities create the assets needed to execute a strategy.

---

## 7.1 Prepare Tailored Resume

### Purpose

Adapt the Candidate's resume for a specific opportunity.

### Inputs

- Candidate;
- base resume;
- Opportunity;
- CompanyProfile;
- Strategy.

### Outputs

- tailored resume draft;
- ApplicationPackage.

### Rule

The system may reorganize emphasis.

It must not invent experience.

---

## 7.2 Prepare Cover Letter

### Purpose

Generate a specific cover letter when useful.

### Inputs

- Candidate;
- Company;
- Opportunity;
- CompanyProfile;
- Strategy.

### Outputs

- cover letter draft;
- ApplicationPackage.

### Rule

Cover letters should be concise, specific, and non-generic.

---

## 7.3 Prepare Outreach Message

### Purpose

Generate a personalized message for a recruiter, engineering manager, CTO, founder, or potential referrer.

### Inputs

- Candidate;
- Contact;
- Company;
- CompanyProfile;
- Strategy.

### Outputs

- message draft;
- ApplicationPackage.

### Rule

Messages should be short, specific, respectful, and clearly human-approved before sending.

---

## 7.4 Prepare Application Answers

### Purpose

Draft answers for common application form questions.

### Inputs

- Candidate;
- Opportunity;
- CompanyProfile;
- job application questions.

### Outputs

- answer drafts;
- ApplicationPackage.

### Rule

Answers should be truthful and aligned with the Candidate's actual experience.

---

# 8. Tracking

Tracking capabilities maintain the state of applications and outreach.

---

## 8.1 Create Application

### Purpose

Start tracking once the user approves pursuing an opportunity.

### Inputs

- approved Strategy;
- ApplicationPackage;
- Opportunity;
- Company.

### Outputs

- Application;
- Activity.

### Rule

An Application begins only after user approval.

---

## 8.2 Track Application Status

### Purpose

Maintain application progress.

### Inputs

- user updates;
- email updates, if integrated later;
- manual status changes;
- calendar events, if integrated later.

### Outputs

- updated Application;
- Activity.

### Stages

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

## 8.3 Suggest Follow-Up

### Purpose

Suggest when and how to follow up.

### Inputs

- Application;
- last action date;
- strategy type;
- previous messages.

### Outputs

- follow-up recommendation;
- message draft when needed;
- Activity.

### Rule

Follow-up suggestions should require approval before sending.

---

# 9. Feedback & Learning

Feedback capabilities help Signal improve.

---

## 9.1 Capture Recommendation Feedback

### Purpose

Capture whether the user agrees with a recommendation.

### Inputs

- Briefing;
- user action;
- explicit reason;
- optional comment.

### Outputs

- Feedback;
- Activity.

### Example actions

- approve;
- reject;
- disagree;
- ask for more research;
- save for later;
- blacklist;
- mark as exciting.

---

## 9.2 Learn From Contradiction

### Purpose

Detect when user behavior contradicts system reasoning.

### Inputs

- Recommendation;
- Evaluation;
- user action.

### Outputs

- LearningSignal;
- PreferenceInsight;
- Activity.

### Example

Signal marks an opportunity as uncertain due to company size.

The user decides to pursue it anyway.

Signal records that company size may be less important than other signals in this context.

---

## 9.3 Adjust Recommendation Threshold

### Purpose

Change how selective Signal is based on confidence in the Candidate model.

### Inputs

- Candidate profile confidence;
- feedback volume;
- acceptance rate;
- rejection reasons.

### Outputs

- updated threshold;
- Activity.

### Rule

Early stage should show more exploratory opportunities.

Mature stage should be more selective.

---

# 10. Activity & Briefing

Activity and Briefing capabilities control what the user sees.

---

## 10.1 Generate Activity Feed

### Purpose

Show evidence of system work without creating noise.

### Inputs

- Activity records.

### Outputs

- activity summary.

### Examples

- "Analyzed 143 companies."
- "Updated culture research for 7 companies."
- "Discarded 38 openings due to poor salary fit."
- "Found 3 opportunities worth reviewing."

### Rule

The Activity Feed should build trust, not create another task list.

---

## 10.2 Generate Briefing

### Purpose

Create the user-facing artifact for a high-value recommendation.

### Inputs

- Recommendation;
- CompanyProfile;
- Evaluation;
- Strategy;
- ApplicationPackage, when available;
- ResearchReports.

### Outputs

- Briefing.

### Briefing sections

- why this appeared;
- executive summary;
- company fit;
- role/opportunity fit;
- salary information;
- culture signals;
- concerns;
- recommended strategy;
- prepared assets;
- decision needed.

### Rule

A Briefing should never feel like raw model output.

It should feel like an analyst prepared a decision memo.

---

## 10.3 Generate Conversational Summary

### Purpose

Present briefings and activity in a conversational interface.

### Inputs

- Briefings;
- Activity;
- Candidate context.

### Outputs

- conversational message.

### Example

> I found four companies worth reviewing today. Two have open roles, one has no open role but looks like a strong fit, and one has conflicting culture signals. I prepared strategies for each.

### Rule

The conversation should be calm, concise, and useful.

---

# 11. Cost & Quality Control

Cost and quality capabilities prevent the system from becoming expensive, noisy, or unreliable.

---

## 11.1 Estimate Capability Cost

### Purpose

Estimate the cost of executing a capability.

### Inputs

- capability type;
- expected sources;
- expected model usage;
- cached knowledge availability.

### Outputs

- cost estimate.

### Rule

The system should avoid expensive reasoning when cheaper methods are enough.

---

## 11.2 Reuse Existing Knowledge

### Purpose

Avoid researching the same thing repeatedly.

### Inputs

- requested research;
- existing ResearchReports;
- freshness status.

### Outputs

- reused report;
- refresh decision;
- Activity.

### Rule

Cached knowledge should be reused unless stale or contradicted by new evidence.

---

## 11.3 Detect Stale Knowledge

### Purpose

Identify when knowledge should be refreshed.

### Inputs

- ResearchReport;
- CompanyProfile;
- time since last update;
- company importance;
- new opportunity detected;
- new external signals.

### Outputs

- refresh recommendation;
- Activity.

---

## 11.4 Quality Check Briefing

### Purpose

Ensure a Briefing is useful before showing it to the user.

### Inputs

- Briefing draft;
- supporting artifacts;
- confidence;
- missing information.

### Outputs

- approved Briefing;
- request for more research;
- warning labels.

### Rule

If a Briefing has insufficient evidence, Signal should research more or explicitly disclose uncertainty.

---

# V1 Capability Priorities

## Must have

- Build Candidate Profile
- Discover Companies
- Maintain Company Universe
- Research Product
- Research Culture
- Research Benefits
- Research Engineering
- Research Compensation
- Discover Job Openings
- Discover Contact Path
- Evaluate Company Fit
- Evaluate Opportunity Fit
- Select Pursuit Strategy
- Prepare Outreach Message
- Prepare Tailored Resume
- Generate Briefing
- Capture Recommendation Feedback
- Generate Activity Feed
- Reuse Existing Knowledge

## Should have

- Prepare Cover Letter
- Prepare Application Answers
- Track Application Status
- Suggest Follow-Up
- Learn From Contradiction
- Detect Stale Knowledge
- Quality Check Briefing

## Could have

- Adjust Recommendation Threshold
- Research Company Risk
- Expand From Aspirational Companies
- Generate Conversational Summary

## Out of scope for V1

- fully automatic applications;
- sending messages without approval;
- conference/event discovery;
- long-term career coaching;
- salary negotiation;
- multi-user SaaS support;
- native mobile app;
- public social posting strategy;
- automatic LinkedIn profile optimization.

---

# Open Questions

1. Which capabilities should be implemented manually first before automation?
2. What is the minimum research depth required before a Briefing?
3. How should capability execution be scheduled?
4. Which sources are reliable enough for culture research?
5. How should Signal represent confidence to the user?
6. What is the maximum acceptable daily/weekly token budget?
7. What data should be manually seeded before the first automated run?
8. Should the first version use a web UI, chat interface, CLI, or document-driven workflow?
9. Which ApplicationPackage assets are required for the first usable version?
10. How should the user approve or reject a strategy?
