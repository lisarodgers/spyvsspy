\# Spy vs Spy Computers



\# GIT\_WORKFLOW.md



\## Purpose



This document defines how Git is used for the Spy vs Spy Computers project.



The goal is to keep development organized, understandable, reversible, and safe.



Git should tell the story of the project clearly.



\---



\# Core Principles



\* Keep commits small.

\* Use clear commit messages.

\* Work in branches.

\* Keep `main` stable.

\* Never commit secrets.

\* Review AI-generated code before committing.

\* Every commit should represent one logical change.



\---



\# Repository Strategy



Spy vs Spy Computers uses a single repository.



This repository contains:



\* Applications

\* Shared packages

\* Documentation

\* Tests

\* Website assets

\* Infrastructure files



This approach keeps the platform cohesive and makes shared code easier to manage.



\---



\# Main Branch



The `main` branch is the stable branch.



Rules:



\* `main` should always run.

\* `main` should not contain broken experiments.

\* `main` should be deployable.

\* Direct commits to `main` should be avoided once feature work begins.



\---



\# Development Branch



Optional but recommended:



Use a `develop` branch for active integration.



```bash

git checkout -b develop

```



Feature branches can merge into `develop`.



Stable releases can merge from `develop` into `main`.



\---



\# Branch Naming



Use descriptive branch names.



\## Feature Branches



```text

feature/email-parser

feature/dashboard-shell

feature/threat-scoring

feature/ip-lookup

feature/login-system

```



\## Fix Branches



```text

fix/upload-validation

fix/session-timeout

fix/spamassassin-parser

```



\## Documentation Branches



```text

docs/database-design

docs/security-update

docs/git-workflow

```



\## Experiment Branches



```text

experiment/flask-layout

experiment/report-ui

```



Experiments may be discarded.



\---



\# Commit Message Format



Use a simple conventional commit style.



Format:



```text

type(scope): short description

```



Examples:



```text

docs(git): add Git workflow

docs(security): add upload threat model

feat(auth): add login page

feat(parser): extract email subject

fix(upload): reject oversized files

test(parser): add bitcoin wallet detection test

refactor(scoring): simplify score calculation

chore(project): update gitignore

```



\---



\# Commit Types



Use these common types:



```text

feat      New feature

fix       Bug fix

docs      Documentation only

test      Tests

refactor  Code change without behavior change

chore     Maintenance

style     Formatting only

security  Security-specific change

```



\---



\# Good Commit Habits



Good commits are:



\* Focused

\* Reversible

\* Easy to understand

\* Small enough to review



Avoid commits like:



```text

stuff

updates

fixes

misc

work

changes

```



\---



\# When to Commit



Commit after completing a small logical unit.



Examples:



\* Created project structure

\* Added vision document

\* Added database design

\* Added Flask app shell

\* Added upload validation

\* Added parser tests



Do not wait until the end of a large work session.



\---



\# Before Committing



Run:



```bash

git status

```



Review changed files:



```bash

git diff

```



Stage intentionally:



```bash

git add path/to/file

```



Commit:



```bash

git commit -m "docs(git): add Git workflow"

```



\---



\# First Commit



Suggested first commit:



```bash

git add .

git commit -m "chore(project): initialize Spy vs Spy Computers repository"

```



\---



\# Working With Codex



Codex should work on one branch at a time.



Before asking Codex to implement a feature:



1\. Create a feature branch.

2\. Tell Codex which files it may edit.

3\. Provide the relevant docs.

4\. Ask for tests where appropriate.

5\. Review the diff before committing.



Example:



```bash

git checkout -b feature/dashboard-shell

```



Prompt Codex:



```text

Implement the dashboard shell for Abuse Triage Analyzer.



Follow:

\- docs/CODING\_STANDARDS.md

\- docs/UX\_GUIDELINES.md

\- docs/SECURITY.md



Do not implement uploads yet.

Do not add database logic yet.

Keep this focused on layout and routing only.

```



\---



\# Reviewing Changes



Before every commit:



```bash

git diff

```



Check:



\* Did only expected files change?

\* Are there any secrets?

\* Is the code understandable?

\* Are there unnecessary dependencies?

\* Are generated files accidentally included?



\---



\# Secrets



Never commit:



\* `.env`

\* Passwords

\* API keys

\* Session secrets

\* Private certificates

\* Real email samples

\* Real `.eml` files containing personal data



Use `.env.example` for safe placeholder values.



\---



\# Email Samples



Real email samples may contain sensitive data.



Rules:



\* Do not commit real `.eml` files.

\* Use redacted fixtures only.

\* Remove names, addresses, tokens, links, and tracking IDs.

\* Keep test data synthetic whenever possible.



\---



\# Tags and Releases



Use semantic versioning when the project reaches release stage.



Format:



```text

v0.1.0

v0.2.0

v1.0.0

```



Suggested early milestones:



```text

v0.1.0  Dashboard shell

v0.2.0  Upload validation

v0.3.0  Email metadata parser

v0.4.0  Header parser

v0.5.0  Threat scoring

v1.0.0  First usable private analyzer

```



Create a tag:



```bash

git tag -a v0.1.0 -m "First dashboard shell"

git push origin v0.1.0

```



\---



\# Pull Requests



Even if working alone, use pull requests when possible.



Pull requests create a useful review record.



Each pull request should include:



\* What changed

\* Why it changed

\* How it was tested

\* Security considerations

\* Screenshots for UI changes



\---



\# Pull Request Template



```markdown

\## Summary



Describe what changed.



\## Why



Explain why this change was needed.



\## Testing



Describe how this was tested.



\## Security Notes



Mention any security impact.



\## Screenshots



Add screenshots for UI changes.

```



\---



\# Merge Strategy



Prefer squash merges for small features.



Use normal merge commits for larger milestone branches if preserving history is useful.



Avoid force pushing shared branches unless necessary.



\---



\# Rollback Strategy



Every change should be reversible.



For bad commits:



```bash

git revert <commit\_hash>

```



Avoid rewriting history on `main`.



\---



\# Documentation Changes



Documentation changes should be committed like code.



Example:



```bash

git commit -m "docs(database): define investigation-centered schema"

```



Docs are part of the product.



\---



\# Definition of Done



A change is done when:



\* It solves one clear problem.

\* It follows the coding standards.

\* It aligns with product principles.

\* It passes tests where applicable.

\* It does not introduce secrets.

\* It has been reviewed.

\* It is committed with a clear message.



\---



\# Recommended Daily Workflow



```bash

git status

git pull

git checkout -b feature/name-of-work

\# make changes

git diff

git add path/to/files

git commit -m "type(scope): description"

git checkout develop

git merge feature/name-of-work

```



\---



\# Mission



Git history should explain how the platform evolved.



A clean Git workflow protects the project from confusion, accidental data leaks, and hard-to-reverse changes.



