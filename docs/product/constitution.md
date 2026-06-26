# Product Constitution

Status: Draft  
Last updated: 2026-06-26

## 1. Purpose

Signal exists to help the user find the best possible job opportunity without turning job hunting into a second job.

It does not exist to automate applications for the sake of automation.

It does not exist to showcase AI.

It exists to increase the probability of finding the right company, role, culture, compensation, and product fit.

## 2. Quality over quantity

Three exceptional opportunities are better than fifty mediocre ones.

The system should filter aggressively and protect the user's attention.

## 3. Company first, role second

The company is more important than the job opening.

Openings appear and disappear.
Company culture, product quality, engineering standards, and benefits are more persistent.

Signal should start by understanding companies before recommending specific opportunities.

## 4. Human approval

The system prepares.
The user decides.

No external action should happen without explicit approval.

External actions include, but are not limited to:

- applying to a job;
- sending a message;
- contacting a recruiter;
- contacting an engineering manager;
- modifying or submitting a resume;
- sending a cover letter.

## 5. Explainability

Every recommendation must be explainable.

The user should always be able to understand:

- why this company appeared;
- what was researched;
- what the system likes;
- what the system is worried about;
- what the recommended strategy is;
- how confident the system is.

No unexplained score is acceptable.

## 6. Every token must generate value

The system should not use LLM calls when cheaper methods are enough.

Preferred order:

1. deterministic logic;
2. structured data;
3. cached knowledge;
4. search;
5. embeddings;
6. smaller models;
7. larger models.

LLMs should be used when judgment, synthesis, personalization, or reasoning materially improves the outcome.

## 7. Knowledge is an asset

Research should be stored and reused.

If the system researches a company today, it should not pay again tomorrow to learn the same thing.

The system should only re-research when:

- new information appears;
- existing information becomes stale;
- the user asks for a refresh;
- the company becomes strategically important.

## 8. The system protects attention

The user is not actively job hunting.

The system should not create another daily obligation.

It should show enough activity to build trust, especially during the learning phase, but it should avoid overwhelming the user.

## 9. The MVP has one job

The V1 exists to help the user find the right job within six months.

Anything that does not significantly increase that probability is out of scope for V1.

## 10. The system learns from disagreement

The goal is not for the system to be right from day one.

The goal is for the system to improve when it is wrong.

When the user rejects, accepts, corrects, or contradicts a recommendation, the system should use that feedback to refine future recommendations.
