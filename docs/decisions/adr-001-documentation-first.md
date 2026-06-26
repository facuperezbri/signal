# ADR-001: Documentation-first development

Status: Accepted  
Date: 2026-06-26

## Context

Signal is being built as a career intelligence system, not as a simple job application bot.

The project has a high risk of becoming too broad because it involves product strategy, AI capabilities, candidate modeling, company research, opportunity evaluation, outreach, resume generation, and tracking.

Starting directly with implementation would likely produce a system driven by prompts and UI decisions instead of a clear product and domain model.

The user also wants this project to serve two purposes:

1. Solve a real personal problem: finding the right job within six months.
2. Demonstrate product engineering judgment through a well-designed repository.

## Decision

We will follow a documentation-first development approach.

Before writing application code, the repository must contain the foundational product and architecture documents:

- Product Constitution;
- Product Vision;
- PRD;
- Domain Model;
- Capability Catalog;
- Architecture Decision Records;
- User Journeys;
- Roadmap.

These documents will act as the source of truth for implementation.

Claude Code or any other AI coding assistant should be treated as an engineer consuming these documents, not as the product designer inventing the system from scratch.

## Options considered

### Option 1: Start coding immediately

This would create fast initial momentum, but it would likely lead to premature technical decisions, unclear scope, and rework.

Rejected.

### Option 2: Ask an AI coding assistant to generate the whole application from a high-level prompt

This would be fast, but the result would likely reflect the assistant's assumptions rather than the product decisions made through discovery.

Rejected.

### Option 3: Build foundational documentation first

This is slower at the beginning, but it creates clearer scope, better architecture, stronger reasoning, and a repository that demonstrates product engineering maturity.

Accepted.

## Consequences

### Positive

- Better product clarity before implementation.
- Lower risk of building unnecessary features.
- Easier to onboard AI coding assistants later.
- Decisions become auditable.
- The repository tells a stronger product engineering story.
- The code can implement the documents instead of improvising the product.

### Negative

- Slower visible progress at the beginning.
- Requires discipline to avoid over-documenting.
- Some documents may change as the project evolves.
- The user must resist the urge to jump into implementation too early.

## Notes

Documents are not considered permanently finished.

They can move through maturity states:

- Draft;
- Review;
- Accepted;
- Superseded.

The goal is not to create perfect documentation.

The goal is to remove enough ambiguity so implementation can start with strong direction.
