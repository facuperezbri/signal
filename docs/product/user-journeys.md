# User Journeys

Status: Draft
Last updated: 2026-06-26

## Purpose

This document describes the intended user experience of Signal across the most important product moments.

Signal is not designed for a user who is urgently unemployed.

Signal is designed for a senior engineer who is currently employed, comfortable enough, and not actively job hunting, but who does not want to miss an exceptional opportunity.

The product should help the user feel:

> I am not actively job hunting, but I am not missing the right opportunity.

---

# Journey 1: Day 0 — Initial Setup

## Context

The user has just created Signal.

They are excited about the idea, but the system does not know enough yet to make high-confidence recommendations.

The goal of Day 0 is not to generate perfect job recommendations.

The goal is to build the initial Candidate model and create enough structure for Signal to start learning.

## User mindset

The user is thinking:

- I want a better job, but I do not want job hunting to become another job.
- I care deeply about company culture.
- I want a product company.
- I want strong compensation and benefits.
- I want flexibility and work-life balance.
- I want a company where my work matters.
- I want to keep control over every external action.
- I want the system to prepare things, but I decide.

## What Signal needs to learn

Signal should build an initial Candidate model using:

- resume;
- LinkedIn profile;
- portfolio;
- preferred roles;
- target companies;
- disliked company categories;
- values;
- compensation expectations;
- preferred work style;
- location and timezone constraints;
- remote/hybrid preferences;
- feedback from conversation.

## Minimum Candidate Profile

Signal should know at least:

- professional identity;
- current role;
- core skills;
- preferred next roles;
- preferred company types;
- companies the user admires;
- companies or categories the user wants to avoid;
- compensation importance;
- culture importance;
- product importance;
- flexibility importance;
- work-life balance importance;
- AI interest;
- approval preferences.

## Example initial Candidate summary

> You are a Senior Frontend Engineer specialized in React, with growing AI Engineering knowledge. You want to move toward product companies where culture, compensation, benefits, flexibility, and product quality are strong. You are not actively job hunting, so Signal should filter aggressively and only surface opportunities worth your time.

## Desired Day 0 experience

Signal should not overwhelm the user with configuration.

The first interaction should feel conversational and purposeful.

Example:

> I need to understand what an exceptional opportunity means for you.
>
> I already know some things:
>
> - You are a Senior Frontend Engineer specialized in React.
> - You are interested in AI Product Engineering.
> - You care deeply about culture, benefits, flexibility, compensation, and product quality.
> - You prefer product companies over consulting, outsourcing, and traditional banking environments.
>
> I will use this as your initial profile and start exploring the market. During the first phase, I will show more exploratory opportunities so I can learn what you like and dislike.

## Day 0 output

By the end of Day 0, Signal should have created:

- Candidate;
- initial Candidate preferences;
- initial whitelist or aspirational companies;
- initial blacklist or avoided categories;
- initial search targets;
- initial activity record;
- first research queue.

## Day 0 success criteria

Day 0 succeeds if:

- the user feels understood;
- the system has enough information to start researching;
- the user does not feel forced into a long form;
- the user understands that early recommendations may be exploratory;
- no external action has occurred;
- no unnecessary application code or UI complexity is required.

---

# Journey 2: First Research Run

## Context

Signal has enough Candidate information to begin exploring the market.

The system starts discovering companies, opportunities, and possible paths.

## User mindset

The user is not waiting for Signal in real time.

They expect Signal to work between interactions, but they do not want unbounded background work or uncontrolled token usage.

## System behavior

Signal should:

1. discover candidate companies;
2. discover job openings;
3. apply cheap filters first;
4. reuse existing knowledge;
5. research only promising companies;
6. create Activity records;
7. prepare exploratory recommendations;
8. generate briefings only when useful.

## What Signal should avoid

Signal should not:

- call expensive models for every job post;
- deeply research every company;
- generate full application packages too early;
- show raw search results;
- pretend uncertain recommendations are high-confidence;
- send anything externally;
- create daily noise.

## Example activity summary

> I scanned 312 companies and openings.
>
> I removed duplicates and filtered obvious poor fits.
>
> I found 18 companies worth a closer look.
>
> I researched 7 of them more deeply.
>
> I prepared 4 exploratory briefings for you to review.

## Success criteria

The first research run succeeds if:

- the user sees evidence that Signal is working;
- the user receives a small number of useful opportunities;
- uncertainty is clearly labeled;
- the system learns from the user's reactions;
- token usage remains bounded and explainable.

---

# Journey 3: Learning Phase

## Context

The system does not yet fully understand the user's preferences.

During this phase, Signal should show more opportunities than it eventually will.

The purpose is to learn.

## User mindset

The user is open to reviewing a few opportunities, even if they are not perfect, because each decision helps Signal improve.

The user wants to feel that the system is making progress.

## System behavior

Signal should show between 3 and 5 opportunities per meaningful review cycle.

In the early phase, some briefings may be exploratory.

Signal should clearly label them.

Example:

> I am showing this as an exploratory recommendation.
>
> It does not perfectly match the pattern I have seen so far, but the culture and benefits look strong enough that I want to understand whether this type of company interests you.

## Feedback loop

For each briefing, the user should be able to respond with simple actions:

- pursue;
- save for later;
- reject;
- ask for more research;
- disagree with reasoning;
- blacklist company;
- mark as exciting.

If the user rejects or disagrees, Signal should ask why.

The system should not ask too many questions at once.

## Example correction flow

Signal:

> I recommended this because the company has strong culture signals, good compensation, and a frontend-heavy role.

User:

> I disagree.

Signal:

> What feels wrong?
>
> - Product
> - Culture
> - Salary
> - Role
> - Stack
> - Company reputation
> - Other

User:

> Company reputation.

Signal:

> Got it. I will treat company reputation as a stronger negative signal here. Do you want me to blacklist this company or just reduce its priority?

## Learning principles

Signal should learn cautiously.

It should not overfit.

Example:

If the user rejects several companies with fewer than 500 employees, Signal may detect a pattern.

But it should not permanently decide that small companies are bad.

Instead, it should say:

> I noticed you have rejected several smaller companies. I will reduce their priority, but I may still show exceptional outliers with a warning.

## Success criteria

The learning phase succeeds if:

- the user sees useful recommendations early;
- the system improves through feedback;
- the user feels in control;
- the system becomes less noisy over time;
- the system does not overfit from weak signals;
- the user starts trusting the reasoning.

---

# Journey 4: Mature Trusted Advisor Phase

## Context

After enough feedback, Signal has a stronger understanding of the Candidate.

It should become more selective.

The system should interrupt less often.

## User mindset

The user trusts that Signal is working even when it is quiet.

They do not expect daily job alerts.

They expect high-quality interruptions.

## System behavior

Signal should:

- continue monitoring the market;
- update company knowledge;
- refresh stale research;
- track target companies;
- detect meaningful changes;
- prepare briefings only for high-value opportunities;
- show activity summaries when the user asks or returns after time away.

## Example mature interaction

> I analyzed 486 companies and openings this week.
>
> I discarded most of them because they did not meet your culture, compensation, or product criteria.
>
> I found one company that deserves your attention.
>
> This is one of the strongest matches I have seen this month.

## What changes from the learning phase

During the learning phase:

- more exploratory recommendations;
- more feedback prompts;
- more visible activity;
- lower confidence threshold.

During the mature phase:

- fewer interruptions;
- stronger filtering;
- higher confidence threshold;
- more prepared strategies;
- less need for correction.

## Success criteria

The mature phase succeeds if:

- Signal protects the user's attention;
- the user trusts silence;
- briefings feel rare and valuable;
- recommendations are strongly aligned with user preferences;
- the system can explain every recommendation;
- the user does not feel like they are managing another tool.

---

# Journey 5: Exceptional Opportunity Briefing

## Context

Signal finds a company or opportunity that strongly matches the Candidate.

It has completed enough research to prepare a briefing.

## User mindset

The user is busy.

They need to understand quickly whether this is worth attention.

## Briefing goals

A Briefing should answer:

1. Why am I seeing this?
2. What company is this?
3. What is the opportunity?
4. What is the salary or compensation signal?
5. Why does this match me?
6. What are the risks?
7. What strategy do you recommend?
8. What have you prepared?
9. What decision do you need from me?

## Example Briefing

> I found a company worth reviewing.
>
> **Company:** ExampleCo
> **Opportunity:** Senior Frontend Engineer
> **Recommended strategy:** Apply officially and contact the frontend engineering manager.
>
> **Why this deserves attention**
>
> - Strong culture signals.
> - Product appears aligned with your interest in tools people actually use.
> - React and TypeScript are central to the role.
> - Compensation appears likely to be above your current range.
> - The company offers strong flexibility and benefits.
>
> **What concerns me**
>
> - Salary is not published.
> - Reviews mention a demanding hiring process.
> - The role asks for some backend experience, which is not your strongest area.
>
> **Why I still recommend reviewing it**
>
> The company fit is strong enough that the backend gap may not be fatal, especially if your frontend and AI product experience are positioned well.
>
> **I prepared**
>
> - resume angle;
> - outreach message;
> - notes on what to emphasize;
> - questions to ask before applying.
>
> **Decision needed**
>
> Do you want to pursue this, ask me to research compensation more, or discard it?

## Briefing rules

A Briefing should not be generated if research is too incomplete.

If uncertainty remains, it must be explicit.

A Briefing should never exaggerate.

Signal should avoid language like:

> perfect opportunity

Unless there is exceptional evidence.

Preferred language:

> This deserves your attention.

## Success criteria

A Briefing succeeds if:

- the user understands the opportunity in under two minutes;
- the recommendation is explainable;
- the risks are clear;
- the next action is obvious;
- the user does not need to do additional basic research manually.

---

# Journey 6: Pursuing an Opportunity

## Context

The user approves pursuing an opportunity.

At this point, Signal transitions from recommendation to execution preparation.

## User mindset

The user wants to act, but does not want to start from scratch.

## System behavior

Signal should create or update:

- Application;
- Strategy;
- ApplicationPackage;
- Contact records;
- Activity;
- follow-up plan.

## Possible strategies

- apply through careers page;
- apply through LinkedIn;
- contact recruiter;
- contact engineering manager;
- contact CTO/founder;
- ask for referral;
- monitor for future role.

## User approval

Before external action, Signal must show:

- exact message or content;
- recipient or destination;
- reasoning;
- risks;
- alternatives.

The user can:

- approve;
- edit;
- reject;
- ask for a different tone;
- ask for more research;
- postpone.

## Example

Signal:

> I recommend contacting the engineering manager before applying. This is a smaller company, and a thoughtful direct message may have a better chance than applying cold.
>
> I drafted this:
>
> "Hi Laura — I came across ExampleCo and was especially interested in..."
>
> Do you want to send this, edit it, or try a recruiter-first strategy instead?

## Success criteria

This journey succeeds if:

- the user acts faster than they would manually;
- the outreach or application is highly personalized;
- no external action happens without approval;
- the action is tracked;
- follow-up is planned.

---

# Journey 7: Company With No Open Role

## Context

Signal discovers a company that strongly fits the Candidate, but there are no relevant open roles.

## User mindset

The user still wants to know if the company is exceptional.

They are open to a thoughtful outreach strategy.

## System behavior

Signal should:

1. confirm there are no open relevant roles;
2. evaluate whether the company is strong enough to justify outreach;
3. discover relevant contacts;
4. recommend a strategy;
5. prepare a personalized message;
6. track the outreach if approved.

## Example

> I found a company that looks highly aligned with what you want, but they do not currently have relevant open roles.
>
> I still think it is worth considering because:
>
> - culture signals are strong;
> - the product is excellent;
> - frontend appears strategically important;
> - they recently hired engineering leadership;
> - they seem likely to grow the product team.
>
> I found two possible contacts:
>
> - Head of Engineering
> - Frontend Engineering Manager
>
> I recommend a short direct message to the Frontend Engineering Manager rather than applying through a generic form.

## Success criteria

This journey succeeds if:

- strong companies are not ignored only because there is no open role;
- outreach is strategic, not spammy;
- the user understands why the company is worth attention;
- every contact action requires approval.

---

# Journey 8: Uncertain or Contradictory Signals

## Context

Signal finds a company that looks promising, but the evidence is mixed.

Examples:

- great product, mixed culture reviews;
- high salary, poor work-life balance signals;
- strong role, unclear benefits;
- exciting company, unstable business;
- good fit, but missing salary information.

## User mindset

The user wants honesty.

They do not want Signal to hide concerns.

## System behavior

Signal should not automatically discard uncertain opportunities.

It should research more when possible.

If uncertainty remains, it should show the opportunity with a warning.

## Example

> I am showing this with a warning.
>
> The product and role look strong, but culture signals are divided.
>
> Positive signals:
>
> - employees mention high ownership;
> - engineering quality appears strong;
> - compensation looks above average.
>
> Negative signals:
>
> - several reviews mention high pressure;
> - work-life balance appears inconsistent across teams.
>
> My recommendation:
>
> Review it, but do not pursue until we learn more about the specific team.

## Success criteria

This journey succeeds if:

- Signal is honest about uncertainty;
- the user sees both upside and risk;
- the system does not overstate confidence;
- the user can request more research;
- uncertainty becomes useful, not vague.

---

# Journey 9: Activity Without Noise

## Context

The user wants to feel that Signal is working.

But they do not want to receive meaningless updates.

## User mindset

The user may think:

> If I hear nothing, is the system doing anything?

Signal needs to build trust without creating noise.

## System behavior

Signal should maintain Activity records.

Activity should be summarized, not dumped.

## Example activity summary

> Since your last check-in:
>
> - I analyzed 214 new openings.
> - I updated 12 company profiles.
> - I discarded 186 items that did not meet your culture, compensation, or role criteria.
> - I found 3 opportunities worth reviewing.
> - I need feedback on 2 exploratory recommendations to improve your profile.

## Activity rules

Activity should:

- prove that work is happening;
- explain why few items reached the user;
- highlight meaningful changes;
- avoid low-level operational noise;
- avoid making the user feel responsible for managing the system.

## Success criteria

This journey succeeds if:

- the user trusts the system is active;
- the user is not overwhelmed;
- activity creates confidence;
- activity does not become another dashboard to manage.

---

# Journey 10: Feedback and Learning

## Context

The user gives feedback on recommendations.

This is how Signal improves.

## User mindset

The user wants to correct the system quickly.

They do not want a long survey.

## System behavior

Signal should treat feedback as a first-class product moment.

Feedback should be easy, specific, and useful.

## Feedback examples

User says:

> I do not like this company.

Signal asks:

> What is the main reason?
>
> - Product
> - Culture
> - Salary
> - Role
> - Stack
> - Company reputation
> - Other

User says:

> Culture.

Signal asks:

> Should I treat this as a company-specific concern or a broader pattern?

## Learning behavior

Signal should distinguish between:

- explicit preference;
- weak pattern;
- strong pattern;
- temporary context;
- contradiction;
- blacklist;
- whitelist.

## Example learning insight

> I noticed that you are rejecting companies with strong technical fit when culture signals are weak. I will increase the weight of culture in future evaluations.

## Success criteria

Feedback succeeds if:

- it takes little time;
- it improves future recommendations;
- the user feels heard;
- the system does not overfit;
- the feedback is auditable later.

---

# Journey 11: Two Months Without Strong Opportunities

## Context

Signal has not found strong enough opportunities for an extended period.

## User mindset

The user may wonder whether the system is failing or whether the market is weak.

## System behavior

Signal should not silently continue forever.

It should generate a strategic review.

## Example

> I have not found a strong opportunity in the last eight weeks.
>
> I do not think the issue is your profile.
>
> The current search space may be too narrow.
>
> I recommend adjusting strategy in one of three ways:
>
> 1. Expand target countries.
> 2. Include Product Engineer roles in addition to Senior Frontend.
> 3. Track more companies in developer tools and AI product infrastructure.
>
> I can test these changes for two weeks and compare results.

## Success criteria

This journey succeeds if:

- the user does not feel stuck;
- Signal proposes a strategy change;
- the recommendation is based on evidence;
- the user remains in control.

---

# Journey 12: Successful Outcome

## Context

The user gets an interview or job through Signal.

## User mindset

The user should feel that Signal created leverage.

## Desired story

The user should be able to say:

> I was not actively job hunting.
>
> Signal kept watching the market for me.
>
> It found a company I would not have discovered or seriously evaluated on my own.
>
> It researched the company, explained why it fit me, warned me about the risks, prepared a strategy, helped me contact the right person, and tracked the process.
>
> I got an interview because of that.
>
> Eventually, I got the job.

## Success criteria

Signal succeeds if it helps the user get closer to or achieve:

- excellent culture;
- very strong compensation;
- strong benefits;
- meaningful flexibility;
- interesting product;
- strong technical environment;
- role aligned with frontend and AI interests.

---

# V1 Journey Priorities

## Must support

- Day 0 setup;
- first research run;
- learning phase;
- briefing generation;
- uncertain signals;
- company with no open role;
- pursuing an opportunity;
- feedback and learning;
- activity without noise.

## Should support

- mature trusted advisor phase;
- two-month strategy review;
- follow-up suggestions.

## Out of scope for V1

- long-term career advisor after accepting a job;
- conference and event recommendations;
- salary negotiation assistant;
- public content strategy;
- multi-user SaaS onboarding;
- native mobile app-specific flows;
- fully automated external actions.

---

# Open Questions

1. What is the minimum Day 0 input required before Signal can start?
2. How much activity should be shown during the learning phase?
3. How often should Signal produce exploratory briefings?
4. What exact feedback options should be available in V1?
5. What confidence threshold is required for a mature Briefing?
6. How should Signal detect that it is ready to move from learning phase to trusted advisor phase?
7. What should be the first actual interaction layer: web, chat, CLI, or document-based workflow?
8. How should Signal present salary uncertainty?
9. What should trigger the two-month strategy review?
10. What is the smallest useful version of the “company with no open role” journey?
