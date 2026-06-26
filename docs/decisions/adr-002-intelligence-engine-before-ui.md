# ADR-002: Intelligence engine before UI

Status: Accepted
Date: 2026-06-26

## Context

Signal could eventually be experienced through multiple interfaces:

- a web application;
- a native macOS or iOS application;
- a WhatsApp-like chat;
- email briefings;
- Slack or Telegram;
- a CLI;
- a hybrid interface.

During product discovery, the user expressed that a conversational experience may be more valuable than a traditional dashboard.

The user does not want to actively manage another tool. They want the system to work in the background, research opportunities, and surface concise briefings when something deserves attention.

This creates a risk: choosing a UI too early could distort the product.

If Signal is designed first as a web app, the system may become dashboard-driven.

If Signal is designed first as a chat app, it may become too conversational and lose structure.

If Signal is designed first as a native app, the project may spend too much effort on platform-specific UX before proving the intelligence layer.

## Decision

Signal will be designed first as an intelligence engine.

The core system should be able to:

- discover companies and opportunities;
- research companies;
- build structured knowledge;
- evaluate fit;
- create recommendations;
- generate briefings;
- prepare application assets;
- track actions and outcomes;
- learn from feedback.

The interaction layer will be treated as a separate concern.

The first implementation may use any practical interface, but the domain model and capabilities should not depend on a specific UI.

## Options considered

### Option 1: Build a web application first

A web application would provide flexibility, speed of development, and good visibility into data.

However, starting with a web UI risks overemphasizing dashboards, tables, filters, and manual management.

Rejected as the primary product framing.

### Option 2: Build a native application first

A native app could feel premium and personal.

However, it would create platform-specific complexity before the core intelligence engine is validated.

Rejected for V1 framing.

### Option 3: Build a chat-first experience

A chat-first interface aligns strongly with the desired user experience: briefings, selective interruption, and low-friction interaction.

However, a pure chat interface may be insufficient for reviewing structured artifacts such as company profiles, application packages, timelines, and feedback history.

Not rejected, but deferred as an interaction-layer decision.

### Option 4: Build the intelligence engine first

This keeps the core product independent from the interface.

It allows Signal to later expose the same intelligence through web, chat, email, native app, or other channels.

Accepted.

## Consequences

### Positive

- Prevents premature UI decisions.
- Keeps the domain model stable across future interfaces.
- Allows faster experimentation with different interaction layers.
- Encourages structured outputs instead of UI-specific text.
- Makes the system more portable.
- Supports a future where Signal may use multiple interfaces.

### Negative

- The product may feel abstract early in development.
- Extra discipline is required to avoid building too much backend logic without a usable experience.
- A first interaction layer will still need to be chosen before the product becomes useful.
- Some UX questions remain unresolved until later.

## Design implications

The system should produce durable artifacts before rendering them in any interface.

Examples:

- CompanyProfile;
- ResearchReport;
- Evaluation;
- Recommendation;
- Briefing;
- Strategy;
- ApplicationPackage;
- Feedback;
- Activity.

A Briefing should exist independently of whether it is displayed in:

- a web page;
- a chat message;
- an email;
- a push notification;
- a native app screen.

## Notes

This decision does not mean the UI is unimportant.

The user experience is critical.

However, the UI should express the intelligence of the system, not define it prematurely.

The first user-facing interface should be selected after the product documents, domain model, capability catalog, and user journeys are mature enough to clarify what the interface must support.
