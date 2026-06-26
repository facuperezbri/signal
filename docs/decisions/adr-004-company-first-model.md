# ADR-004: Company-first model

Status: Accepted
Date: 2026-06-26

## Context

Most job-search tools are job-posting first.

They start from a list of openings and then let the user inspect the company behind each role.

That model optimizes for volume:

- more jobs;
- more filters;
- more alerts;
- more applications.

Signal has a different goal.

The user is not actively job hunting and does not want to turn job search into a second job.

The user wants to find an exceptional place to work within six months: a company with excellent culture, strong compensation, meaningful benefits, an interesting product, strong technical standards, and a role aligned with their profile.

During product discovery, the user repeatedly emphasized that company quality, culture, benefits, product, and day-to-day work environment matter more than simply matching a job description.

The user also stated that a company with a normal product but excellent culture is preferable to a company with an incredible product but poor culture.

This means the company is the durable object of interest.

Job openings are temporary.

Companies persist.

## Decision

Signal will use a company-first model.

The system should discover, research, understand, and evaluate companies before recommending specific opportunities.

A job opening is one possible path into a company.

It is not the primary entity of the product.

Signal should maintain a company universe and build structured knowledge about companies over time.

When a relevant opportunity appears, Signal should reuse existing company knowledge and only research what is new, missing, or stale.

## Options considered

### Option 1: Job-first model

Signal could start by collecting job posts and ranking them based on skill match.

This is familiar and easier to implement, but it would overemphasize role requirements and underemphasize culture, product, benefits, and long-term company fit.

Rejected.

### Option 2: Candidate-first model

Signal could start from the candidate profile and search broadly for matching roles.

This is useful, but still risks reducing the system to a profile-to-job matching engine.

Rejected as the primary model.

### Option 3: Company-first model

Signal starts by building and maintaining a universe of companies.

For each company, it stores factual information, research reports, company profiles, contacts, known opportunities, risks, and user-specific evaluations.

Accepted.

## Consequences

### Positive

- Better alignment with the user's real priorities.
- Stronger focus on culture, benefits, product, and engineering quality.
- Research becomes reusable across multiple opportunities.
- Companies with no open roles can still become actionable through outreach.
- Better support for long-term monitoring.
- Better ability to avoid companies with known poor fit.
- Better storytelling for briefings.

### Negative

- More upfront research is required.
- The system may need to evaluate companies before there is a concrete job opening.
- It is more complex than scraping and ranking job posts.
- Some companies may look attractive but have no viable path in the short term.
- The system must avoid spending too much research effort on companies that are unlikely to become actionable.

## Design implications

The domain model must treat `Company` as a first-class entity.

A Company may exist without:

- an active job opening;
- a current recommendation;
- an application;
- a known contact.

A Company may have:

- one or more CompanyProfiles;
- many ResearchReports;
- many Opportunities;
- many Contacts;
- many Evaluations;
- many Applications over time;
- activity history;
- user feedback.

## Company vs CompanyProfile

Signal separates objective company facts from Signal's interpretation.

### Company

Stores mostly factual information:

- name;
- website;
- industry;
- products;
- size;
- headquarters;
- remote policy;
- hiring pages;
- public profiles;
- known job boards;
- known contacts.

### CompanyProfile

Stores Signal's current understanding and interpretation:

- product assessment;
- culture assessment;
- engineering assessment;
- benefits assessment;
- compensation assessment;
- remote/flexibility assessment;
- risk assessment;
- attractiveness;
- confidence;
- strengths;
- concerns;
- last evaluated date.

This separation makes the system more auditable and prevents factual records from being mixed with subjective conclusions.

## Opportunity definition

In a company-first model, an Opportunity is not limited to a published job opening.

An Opportunity is a concrete path that could increase the candidate's probability of getting the right job.

In V1, valid Opportunity types include:

- published job opening;
- company with no open role but strong fit;
- recruiter contact;
- engineering manager contact;
- CTO/founder contact;
- referral path.

Out of scope for V1:

- conferences;
- events;
- courses;
- public content strategy;
- long-term career coaching.

## Briefing impact

Briefings should be company-first.

A Briefing should answer:

1. Why does this company deserve attention?
2. What do we know about its culture, product, benefits, and engineering quality?
3. Is there a concrete role or path right now?
4. What strategy is most likely to create a real conversation?
5. What should the user do next?

This is different from a traditional job alert, which usually answers only:

> "Does this job match your keywords?"

## Cost implications

A company-first model supports better cost control.

Once Signal researches a company, the knowledge can be reused.

When a new job appears at that company, Signal should not re-run full research.

It should ask:

- What do we already know?
- Is that knowledge still fresh?
- What changed?
- What is specific to this opportunity?
- Do we need more research before creating a Briefing?

## User experience implications

The user should feel that Signal has a point of view about companies.

Signal should not say:

> "Here are five React jobs."

It should say:

> "I found three companies worth your attention. Two have open roles. One has no open role, but the company fit is strong enough that I recommend outreach."

## Notes

This decision reflects the user's explicit priorities.

The product is not optimized for finding any job.

It is optimized for finding the right company, role, culture, compensation, and product fit.

The company-first model is central to that goal.
