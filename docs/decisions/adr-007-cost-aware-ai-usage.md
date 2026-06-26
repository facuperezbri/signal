# ADR-007: Cost-aware AI usage

Status: Accepted
Date: 2026-06-26

## Context

Signal is an AI-assisted career intelligence system.

The product may perform work such as:

- discovering companies;
- researching culture;
- analyzing job openings;
- estimating compensation;
- evaluating fit;
- preparing briefings;
- generating resumes;
- drafting outreach messages;
- learning from feedback.

A naive implementation could call LLMs for every task.

That would create several problems:

- unnecessary token usage;
- unpredictable cost;
- slower execution;
- duplicated reasoning;
- inconsistent outputs;
- poor scalability;
- reduced user trust.

The user explicitly raised a concern about uncontrolled token usage.

The system should not "work indefinitely" in the background and accidentally generate large costs.

Signal must be intelligent not only in recommendations, but also in how it spends compute and model calls.

## Decision

Signal will use a cost-aware AI strategy.

The system should use the cheapest reliable method that can produce a good enough result.

LLMs should be reserved for tasks where judgment, synthesis, personalization, or language generation materially improves the outcome.

The system should not use AI by default.

It should decide whether AI is needed.

## Core principle

Every token must generate value.

Before using an LLM, Signal should ask:

1. Do we already know this?
2. Is the stored knowledge fresh enough?
3. Can deterministic logic answer this?
4. Can structured data answer this?
5. Can search or cached sources answer this?
6. Can a smaller model answer this?
7. Is a larger model truly needed?

Only then should expensive reasoning be used.

## Preferred execution order

Signal should prefer this order:

1. deterministic logic;
2. existing structured knowledge;
3. cached research;
4. structured APIs;
5. search;
6. embeddings or similarity search;
7. small or cheap models;
8. large reasoning models.

This order may vary for specific tasks, but the default should always be cost-conscious.

## Options considered

### Option 1: LLM-first implementation

Signal could call an LLM for every research, ranking, evaluation, and generation step.

This would be simple to prototype but expensive, inconsistent, and difficult to control.

Rejected.

### Option 2: Manual-first implementation

Signal could avoid AI as much as possible and rely mostly on deterministic rules and manual data entry.

This would reduce cost but would fail to deliver the product's core value: judgment, synthesis, personalization, and prepared briefings.

Rejected.

### Option 3: Cost-aware hybrid intelligence

Signal uses deterministic logic, stored knowledge, structured data, search, and smaller models before using expensive reasoning.

Large models are used only when they materially improve decision quality or user-facing output.

Accepted.

## Consequences

### Positive

- Lower and more predictable cost.
- Better scalability.
- More deliberate AI usage.
- Lower risk of runaway background execution.
- Encourages reusable knowledge.
- Encourages structured artifacts instead of disposable text.
- Makes the system easier to optimize over time.
- Creates a stronger engineering story.

### Negative

- More upfront architecture is required.
- Some workflows may be slower to design.
- The system needs cost estimation and execution rules.
- Developers must resist the temptation to solve every task with a prompt.
- Some early prototypes may take longer than a prompt-only version.

## Budget principle

Signal should support an explicit budget model.

At minimum, the system should be designed so future versions can support:

- daily budget;
- weekly budget;
- monthly budget;
- per-capability budget;
- per-company research budget;
- per-briefing cost tracking.

V1 does not need a full billing system, but it should not be architected in a way that makes cost tracking impossible.

## Background work principle

Signal should not run unbounded background reasoning.

Background work should be:

- scheduled;
- event-driven;
- bounded;
- logged;
- cost-estimated when possible;
- interruptible;
- auditable.

Examples of acceptable background work:

- checking known company career pages once per day;
- refreshing stale company profiles;
- scanning a limited number of job sources;
- updating activity records;
- preparing briefings for high-priority recommendations.

Examples of unacceptable background work:

- continuously asking an LLM to search for jobs;
- repeatedly reanalyzing the same company without new evidence;
- generating full application packages for every weak match;
- running open-ended research loops without a budget or stopping condition.

## Capability cost levels

Each capability should eventually be classified by approximate cost.

### Cost level 0: Free or near-free

Examples:

- deterministic filtering;
- checking stored knowledge;
- sorting recommendations;
- reading local data;
- applying business rules.

### Cost level 1: Low cost

Examples:

- structured API calls;
- lightweight scraping;
- simple parsing;
- database queries;
- cached search results.

### Cost level 2: Moderate cost

Examples:

- embeddings;
- similarity search;
- small-model classification;
- summarizing short text;
- extracting structured data from job posts.

### Cost level 3: High value / higher cost

Examples:

- deep company analysis;
- culture synthesis across sources;
- personalized fit evaluation;
- strategy reasoning;
- high-quality briefing generation;
- tailored resume generation;
- personalized outreach messages.

Cost level 3 capabilities should be used selectively.

## Research depth principle

Not every company deserves deep research.

Signal should use progressive research depth.

### Level 1: Basic screening

Goal: decide whether the company is worth more attention.

Possible checks:

- industry;
- role availability;
- remote policy;
- obvious dealbreakers;
- known blacklist;
- rough compensation signal.

### Level 2: Standard research

Goal: decide whether to evaluate the company seriously.

Possible checks:

- product;
- culture;
- benefits;
- engineering;
- role fit;
- salary range if available.

### Level 3: Deep research

Goal: prepare a Briefing or Strategy.

Possible checks:

- detailed culture analysis;
- contact path;
- compensation estimation;
- risk analysis;
- strategy selection;
- application package preparation.

Deep research should be reserved for companies or opportunities that pass earlier filters.

## Application package principle

Signal should not generate full application packages too early.

A tailored resume, cover letter, outreach message, and application answers should be prepared only when:

- the opportunity has strong enough fit;
- the user asks for it;
- the recommended strategy requires it;
- the system is preparing a high-priority Briefing.

This avoids spending tokens on assets the user will never use.

## Reuse principle

Before generating new analysis, Signal should check existing artifacts:

- Company;
- CompanyProfile;
- ResearchReport;
- Evaluation;
- Recommendation;
- Briefing;
- Strategy;
- ApplicationPackage;
- Feedback;
- Activity.

If existing artifacts are fresh enough, they should be reused.

If they are stale, Signal should refresh only the missing or outdated parts.

## User visibility

The user should be able to understand, at a high level, how Signal uses cost.

Signal may eventually show:

- companies scanned;
- companies deeply researched;
- briefings generated;
- approximate token/model usage;
- skipped expensive work because existing knowledge was reused.

The goal is not to make the user manage cost manually.

The goal is to build trust.

## Example

Signal discovers 1,000 job posts.

A bad implementation would send all 1,000 to a large model.

Signal should instead:

1. remove duplicates;
2. apply hard filters;
3. group by company;
4. check known company profiles;
5. discard known poor fits;
6. extract structured role data;
7. rank likely matches;
8. run deeper analysis only on the top candidates;
9. generate briefings only for the few worth reviewing.

The large model should see only the small subset where reasoning matters.

## Notes

Cost awareness is not only a financial concern.

It is also a product quality concern.

A system that uses AI carelessly is likely to be noisy, inconsistent, and hard to trust.

Signal should demonstrate that AI-native software can be thoughtful, bounded, and economically responsible.
