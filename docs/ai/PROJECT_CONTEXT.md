# PROJECT\_CONTEXT.md
> This document is the primary onboarding guide for AI assistants and new contributors working on Spy vs Spy Computers.
Before making architectural decisions, implementing features, or modifying existing code, read this document along with the project documentation referenced below.



\---
### Project Overview
Spy vs Spy Computers is an open-source digital investigation platform.
Its purpose is to help people understand digital evidence through transparent, privacy-respecting investigations.
The software is designed to explain evidence rather than simply produce scores or warnings.
The platform should educate users while helping them investigate suspicious digital artifacts.
\---

# Mission
\*\*Spy vs Spy Computers doesn't tell people what to think.\*\*
\*\*It shows them the evidence and explains why.\*\*

Every contribution should reinforce this mission.
\---

### Current Project Stage
The repository is currently in the \*\*Foundation Phase\*\*.
Primary work includes:
\* Documentation
\* Architecture
\* Security model
\* Database design
\* Engineering standards
\* Architecture Decision Records



Production code has intentionally been deferred until the project's foundation is complete.
\---

### Long-Term Vision
Spy vs Spy Computers is intended to become a unified investigation platform.
Future investigation types include:

\* Email
\* IP addresses
\* Domains
\* DNS
\* SSL certificates
\* URLs
\* Web servers
\* Log files
\* Indicators of Compromise (IOCs)
\* Threat intelligence

All investigation types should share a common investigation engine, evidence model, reporting framework, and user experience.

\---

### Guiding Principles

Every decision should reinforce these values:
\* Evidence over opinion
\* Transparency over mystery
\* Privacy over convenience
\* Education over fear
\* Security by design
\* Explainability
\* Modularity
\* Offline capability whenever practical
\---

### Architecture Philosophy
The platform follows a layered architecture.

Presentation Layer
↓
Investigation Engine
↓
Intelligence Layer
↓
Data Layer

The investigation engine is the heart of the platform.
External intelligence enriches investigations but never replaces evidence.

\---

### Security Philosophy
Assume all uploaded evidence is hostile.

Never:
\* Execute attachments
\* Render raw HTML email
\* Load remote content
\* Modify original evidence

Store only the minimum information required.
Privacy is the default.

\---
### Development Philosophy
Documentation drives implementation.
Every feature should answer:
1\. Why does this feature exist?
2\. What problem does it solve?
3\. How does it help the user?
4\. What are the security implications?
5\. How will we know it works?

Implementation follows documentation.
Not the other way around.
\---

### Architecture Decision Records
Architectural decisions are documented using ADRs.
Before making significant architectural changes:
\* Read existing ADRs.
\* Determine whether the change conflicts with previous decisions.
\* Create a new ADR if the decision has long-term architectural impact.

Do not silently reverse architectural decisions.

\---

# Coding Expectations
Follow:
\* CODING\_STANDARDS.md
\* SECURITY.md
\* GIT\_WORKFLOW.md
\* DATABASE.md
\* ARCHITECTURE.md

Consistency is preferred over cleverness.
Readable code is preferred over complex code.
Every significant feature should include tests.

\---

### AI Collaboration Guidelines
AI assistants are collaborators.
They are not decision makers.
AI-generated code must be:

\* Understood
\* Reviewed
\* Tested
\* Consistent with project principles

Never introduce unnecessary dependencies.
Never redesign architecture without discussion.
Never remove documentation.
Never weaken privacy or security for convenience.

\---

### Preferred Workflow
New work should generally follow this order:

1\. Identify the problem.
2\. Discuss the solution.
3\. Update documentation if necessary.
4\. Create or update ADRs when appropriate.
5\. Implement the feature.
6\. Write tests.
7\. Review.
8\. Commit.


\---

### Current Priorities

Current focus:
\* Complete project documentation
\* Finalize ADR series
\* Establish AI onboarding
\* Build project infrastructure



Future focus:
\* Bootstrap application
\* Authentication
\* Investigation engine
\* Email parser
\* Threat scoring
\* Reporting


\---

### Repository Philosophy
The repository should be understandable without talking to its authors.
Documentation is part of the product.
Every important decision should have an explanation.
Future contributors should understand not only \*\*what\*\* the system does, but also \*\*why\*\* it was designed that way.

\---

### Final Reminder
If a proposed change makes the project:
\* less transparent,
\* less explainable,
\* less secure,
\* less private,
\* or harder to understand,

it should be reconsidered before implementation.



\---

> \*\*Build software that earns trust through evidence, transparency, and thoughtful engineering.\*\*



