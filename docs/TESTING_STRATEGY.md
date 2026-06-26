\# Spy vs Spy Computers



\# TESTING\_STRATEGY.md



\## Purpose



This document defines how Spy vs Spy Computers tests software.



Testing exists to protect users, preserve trust, and keep the platform maintainable as it grows.



\---



\# Testing Philosophy



Tests should prove that the system behaves correctly, safely, and predictably.



The most important areas to test are:



\* Security-sensitive code

\* Email parsing

\* Header parsing

\* Threat scoring

\* Data storage

\* User authentication

\* Upload handling



\---



\# Core Principles



\* Test behavior, not implementation details.

\* Keep tests readable.

\* Use safe synthetic data.

\* Never use real private emails in tests.

\* Add regression tests for bugs.

\* Security features require tests.

\* Every parser should handle malformed input safely.



\---



\# Test Types



\## Unit Tests



Test one function or module at a time.



Examples:



\* Extract subject from email

\* Detect Bitcoin wallet

\* Detect null Return-Path

\* Parse SpamAssassin score

\* Calculate threat score



\---



\## Integration Tests



Test multiple parts working together.



Examples:



\* Upload email

\* Parse metadata

\* Generate indicators

\* Calculate score

\* Save investigation record



\---



\## Security Tests



Test unsafe input.



Examples:



\* Oversized upload

\* HTML email with script

\* Malformed MIME structure

\* Header injection attempt

\* Suspicious filename

\* Empty email

\* Binary upload disguised as `.eml`



\---



\## UI Tests



Initially manual.



Later automated if needed.



Check:



\* Pages load

\* Navigation works

\* Forms validate input

\* Errors are readable

\* Reports display safely

\* HTML email content is not rendered



\---



\# Test Data Rules



Do not commit real private emails.



Allowed:



\* Synthetic `.eml` fixtures

\* Redacted samples

\* Fake IP addresses

\* Fake domains

\* Fake names

\* Fake Bitcoin wallets



Use reserved domains where possible:



\* example.com

\* example.net

\* example.org



\---



\# Fixture Structure



```text

tests/

├── fixtures/

│   ├── emails/

│   │   ├── bitcoin\_sextortion.eml

│   │   ├── phishing\_fake\_login.eml

│   │   ├── blank\_headers.eml

│   │   ├── malformed\_mime.eml

│   │   └── legitimate\_newsletter.eml

│   └── headers/

│       ├── spamassassin\_headers.txt

│       ├── authentication\_pass.txt

│       └── authentication\_fail.txt

```



\---



\# Minimum Test Coverage for Version 1



Version 1 should include tests for:



\* Upload validation

\* File size limits

\* Email metadata extraction

\* Received header parsing

\* Trusted vs untrusted header marking

\* SpamAssassin score extraction

\* Bitcoin wallet detection

\* Sextortion phrase detection

\* Threat scoring

\* Safe excerpt generation

\* Database insert/read for investigations



\---



\# Parser Safety Requirements



Parsers must never:



\* Execute content

\* Fetch remote URLs

\* Load remote images

\* Render HTML

\* Open attachments

\* Trust malformed headers blindly



Tests should verify that hostile inputs are treated as data only.



\---



\# Threat Scoring Tests



Threat scoring must be explainable and reproducible.



Each score should include:



\* Final score

\* Confidence

\* Triggered indicators

\* Score reasons



Test example:



```text

Given:

\- Bitcoin wallet found

\- Sextortion phrase found

\- Null Return-Path found



Expected:

\- Classification: Bitcoin Sextortion

\- Score: High

\- Explanation includes all three indicators

```



\---



\# Regression Tests



Every fixed bug should get a test.



Example:



If a malformed `Received` header crashes the parser, add a test proving that same header no longer crashes the parser.



\---



\# Manual Testing Checklist



Before each milestone:



\* Start app locally

\* Login works

\* Dashboard loads

\* Upload rejects invalid files

\* Upload accepts valid `.eml`

\* Original upload is deleted after parsing

\* Report displays safely

\* No HTML is rendered

\* No attachments are opened

\* History page works

\* Logs contain no sensitive full email bodies



\---



\# Tools



Recommended tools:



\* pytest

\* coverage

\* ruff

\* black



Future tools:



\* Playwright for browser testing

\* Bandit for Python security checks

\* pip-audit for dependency scanning



\---



\# CI Goals



Future GitHub Actions should run:



\* Linting

\* Formatting check

\* Unit tests

\* Security checks

\* Dependency audit



No code should merge into `main` unless tests pass.



\---



\# Definition of Done



A feature is not complete until:



\* Expected behavior is tested

\* Failure cases are tested

\* Security impact is considered

\* Documentation is updated if needed

\* Tests pass locally



\---



\# Mission



Testing protects the promise of Spy vs Spy Computers:



\*\*Show the evidence. Explain why. Protect the user.\*\*



