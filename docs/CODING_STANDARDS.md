\# Spy vs Spy Computers



\# CODING\_STANDARDS.md



\## Purpose



This document defines the engineering standards for all software developed within the Spy vs Spy Computers platform.



These standards exist to ensure the codebase remains readable, maintainable, secure, and consistent regardless of who writes the code.



The primary goals are:



\* Readability

\* Maintainability

\* Testability

\* Security

\* Consistency



\---



\# Philosophy



Code is written once.



It is read hundreds of times.



Optimize for the reader.



Future developers—including your future self—should be able to understand the code quickly.



\---



\# General Principles



\* Prefer clarity over cleverness.

\* Write self-documenting code.

\* Avoid unnecessary abstraction.

\* Keep functions small and focused.

\* Favor composition over inheritance.

\* Avoid duplicated logic.

\* Make side effects explicit.



\---



\# Language Standards



\* Use Python 3.11+ features where practical.

\* Use type hints for all public functions.

\* Follow PEP 8.

\* Use `black` for formatting.

\* Use `ruff` for linting.

\* Use `isort` for import ordering.



\---



\# Naming Conventions



\## Variables



Use descriptive `snake\_case`.



Good:



```python

investigation\_id

smtp\_hops

threat\_score

```



Avoid:



```python

x

tmp

data2

```



\---



\## Functions



Function names should describe an action.



Examples:



\* parse\_email()

\* calculate\_score()

\* build\_report()

\* extract\_headers()



\---



\## Classes



Use PascalCase.



Examples:



\* EmailParser

\* ThreatEngine

\* InvestigationReport



\---



\## Constants



Use ALL\_CAPS.



Examples:



```python

MAX\_UPLOAD\_SIZE

DEFAULT\_TIMEOUT

```



\---



\# Function Design



Functions should do one thing well.



Aim for functions under 40 lines where practical.



Large functions should usually be split into smaller units.



\---



\# Comments



Comments should explain \*\*why\*\*, not \*\*what\*\*.



Good:



```python

\# Preserve original evidence for reproducibility.

```



Avoid:



```python

\# Increment counter.

counter += 1

```



\---



\# Documentation



Every public class and function should include a docstring describing:



\* Purpose

\* Parameters

\* Return value

\* Exceptions



\---



\# Error Handling



Never silently ignore exceptions.



Handle expected errors gracefully.



Log unexpected errors.



Never expose stack traces to end users.



\---



\# Logging



Log meaningful events.



Do not log:



\* Passwords

\* API keys

\* Session tokens

\* Full email bodies

\* Attachments



Use structured logging where practical.



\---



\# Security



Assume all external input is untrusted.



Validate:



\* File uploads

\* Form input

\* URLs

\* Query parameters



Escape output before rendering.



\---



\# Database



Use parameterized queries or an ORM.



Never concatenate SQL strings.



Keep database logic separate from business logic.



\---



\# Project Structure



Keep responsibilities separate.



\* Routes handle HTTP requests.

\* Services contain business logic.

\* Models represent data.

\* Templates render views.

\* Utilities contain reusable helpers.



\---



\# Testing



Every new feature should include tests.



Focus on:



\* Expected behavior

\* Edge cases

\* Error handling

\* Security-sensitive logic



Bug fixes should include a regression test.



\---



\# Git



\* One logical change per commit.

\* Write meaningful commit messages.

\* Keep feature branches focused.

\* Merge only after review and tests.



\---



\# Performance



Optimize only after measuring.



Prefer simple, correct code over premature optimization.



\---



\# Dependencies



Add third-party libraries only when they provide significant value.



Prefer mature, actively maintained packages.



Remove unused dependencies promptly.



\---



\# AI-Assisted Development



AI tools are collaborators, not decision makers.



All AI-generated code must be:



\* Reviewed

\* Understood

\* Tested

\* Refactored if necessary



Never merge code you do not understand.



\---



\# Definition of Done



A feature is complete only when:



\* It works as intended.

\* It follows coding standards.

\* It passes tests.

\* It is documented.

\* It meets security requirements.

\* It aligns with the Product Principles.



\---



\# Engineering Motto



Write code that your future self will thank you for.



Consistency beats cleverness.



Quality beats speed.



Understanding beats complexity.



