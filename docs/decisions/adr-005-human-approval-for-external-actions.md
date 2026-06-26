# ADR-005: Human approval for external actions

Status: Accepted
Date: 2026-06-26

## Context

Signal is designed to help the user find and pursue exceptional job opportunities.

Some capabilities may prepare external actions, such as:

- applying to a job;
- sending a LinkedIn message;
- emailing a recruiter;
- contacting an engineering manager;
- contacting a CTO or founder;
- asking someone for a referral;
- submitting a resume;
- submitting a cover letter;
- answering application questions;
- following up after no response.

These actions can materially affect the user's professional reputation.

A poorly timed, inaccurate, generic, or unwanted message could harm the user's chances with a company.

The user explicitly wants the system to prepare everything, but keep final control.

The desired control model is:

> The system prepares. The user approves. Only then can something external happen.

## Decision

Signal will require explicit human approval before any external action.

The system may:

- discover opportunities;
- research companies;
- recommend strategies;
- prepare resumes;
- draft cover letters;
- draft outreach messages;
- draft follow-ups;
- prepare application answers;
- suggest next actions.

The system may not, without explicit approval:

- apply to a job;
- submit a form;
- send an email;
- send a LinkedIn message;
- contact a person;
- request a referral;
- modify a public profile;
- publish content;
- schedule a meeting;
- perform any action visible to another person or company.

## Options considered

### Option 1: Fully autonomous execution

Signal could automatically apply to jobs and send outreach messages when confidence is high.

This may increase speed, but it introduces serious risks:

- reputational damage;
- low-quality outreach;
- accidental spam;
- wrong company targeting;
- wrong tone;
- inaccurate claims;
- unwanted applications;
- loss of user trust.

Rejected.

### Option 2: Manual-only system

Signal could only provide suggestions, leaving all writing, tracking, and execution to the user.

This would be safer, but it would fail to reduce enough work.

Rejected.

### Option 3: Human-approved execution

Signal prepares the work and asks the user to approve before any external action.

This preserves user control while still reducing effort.

Accepted.

## Consequences

### Positive

- Preserves user trust.
- Protects professional reputation.
- Reduces risk of spammy or inaccurate outreach.
- Keeps the user in control of meaningful career decisions.
- Makes the system safer to expand with more automation later.
- Aligns with the product principle: "The system prepares. The user decides."

### Negative

- Slower than fully autonomous execution.
- Requires an approval flow.
- Some actions may remain manual in the first version.
- The system must clearly distinguish between prepared assets and executed actions.
- The user may need to review more items during the early learning phase.

## Design implications

Signal must represent approval status explicitly.

Possible statuses:

- draft;
- pending review;
- approved;
- rejected;
- sent/submitted;
- paused;
- expired.

Prepared assets should not be confused with executed actions.

For example:

An `ApplicationPackage` may contain a tailored resume and outreach message, but that does not mean the user has applied.

An `Application` should only move to an externally visible state after user approval.

## External action definition

An external action is any action that creates, modifies, sends, submits, publishes, or schedules something outside Signal.

Examples include:

- sending a message;
- submitting a resume;
- applying through a job portal;
- emailing a recruiter;
- connecting with someone on LinkedIn;
- updating a public profile;
- booking a meeting;
- publishing a post.

## Approval requirements

Before approval, Signal should show:

- what action will be taken;
- who or what it will affect;
- the exact content to be sent or submitted;
- why the action is recommended;
- what risks exist;
- what alternatives exist, when relevant.

The user should be able to:

- approve;
- reject;
- edit;
- ask for a different tone;
- ask for more research;
- postpone;
- mark the strategy as wrong.

## Example

Signal finds a strong company with no open role.

It identifies a relevant engineering manager and drafts a message.

Signal may show:

> I recommend contacting this engineering manager because the company has no open frontend role, but the product and culture fit are strong. I prepared a short message focused on your React experience and AI product interests.

Signal may not send that message until the user explicitly approves it.

## Learning implications

Approval and rejection are important learning signals.

If the user repeatedly rejects prepared outreach messages because they feel too generic, Signal should adapt.

If the user approves recruiter outreach but rejects CTO outreach, Signal should learn that preference cautiously.

If the user edits messages before approving them, those edits may become feedback for future tone and positioning.

## Notes

This ADR does not prevent future automation.

It defines the trust boundary.

Future versions may support higher automation levels, but only if the user explicitly opts in and the system provides strong safeguards.

For V1, human approval is mandatory for every external action.
