\# Spy vs Spy Computers



\# ARCHITECTURE.md



\## Overview



The Spy vs Spy Computers platform is designed as a modular, privacy-first investigation suite. Every component should be independently testable, reusable, and deployable while sharing a common investigation engine.



The first application is \*\*Abuse Triage Analyzer\*\*, but the architecture is intended to support future products such as IP Intelligence, Header Explorer, Reputation Watch, and Threat Library.



\---



\# Core Philosophy



> \*\*Spy vs Spy Computers doesn't tell people what to think. It shows them the evidence and explains why.\*\*



Every architectural decision should reinforce:



\* Privacy

\* Transparency

\* Explainability

\* Security

\* Maintainability



\---



\# High-Level Architecture



```text

&#x20;                Internet

&#x20;                    │

&#x20;         SpyVsSpyComputers.com

&#x20;                    │

&#x20;            Flask Web Application

&#x20;                    │

&#x20;       ┌────────────┴────────────┐

&#x20;       │                         │

&#x20;    Authentication         Investigation Engine

&#x20;                                     │

&#x20;       ┌──────────────┬──────────────┼──────────────┐

&#x20;       │              │              │              │

&#x20;  Email Parser   Threat Scoring   Reporting   Intelligence

&#x20;       │

&#x20;  SQLite Database

```



\---



\# Application Layers



\## Presentation Layer



Responsibilities:



\* User authentication

\* Dashboard

\* Upload interface

\* Investigation reports

\* Search

\* Administration



No investigation logic belongs here.



\---



\## Investigation Engine



The heart of the platform.



Responsibilities:



\* Parse email

\* Parse headers

\* Extract indicators

\* Calculate threat score

\* Produce explainable findings



Every module should return:



\* Findings

\* Confidence

\* Evidence

\* Explanation



\---



\## Intelligence Layer



Responsible for enrichment.



Examples:



\* WHOIS

\* RDAP

\* ASN

\* Reverse DNS

\* Abuse contacts

\* Local reputation history



This layer should never modify original evidence.



Only enrich it.



\---



\## Data Layer



SQLite initially.



Future support:



\* PostgreSQL

\* MariaDB



Store:



\* Metadata

\* Investigation reports

\* Threat scores

\* Indicators

\* User notes



Do not store original emails by default.



\---



\# Project Structure



```text

apps/

packages/

website/

docs/

database/

config/

tests/

knowledge/

assets/

```



\---



\# Shared Packages



\## parser



Parses:



\* .eml

\* Headers

\* Authentication results

\* SMTP path



\---



\## scoring



Produces:



\* Threat score

\* Confidence

\* Explanation



\---



\## reporting



Produces:



\* Investigation report

\* PDF

\* JSON

\* Abuse report



\---



\## common



Shared helpers.



\---



\## ui-components



Reusable interface components.



\---



\# Security Model



Uploads are considered hostile.



Rules:



\* Never execute attachments.

\* Never render HTML email.

\* Never load remote images.

\* Sanitize all output.

\* Delete uploaded files after parsing.

\* Store only metadata unless explicitly configured otherwise.



\---



\# Investigation Pipeline



```text

Upload



↓



Validation



↓



Email Parser



↓



Header Parser



↓



Indicator Extraction



↓



Threat Scoring



↓



Evidence Generation



↓



Report Builder



↓



History Database

```



\---



\# Future Expansion



The investigation engine should eventually support:



\* URLs

\* Domains

\* DNS

\* SSL Certificates

\* Web Servers

\* Log Files

\* IOC Collections



The user experience should remain consistent regardless of evidence type.



\---



\# Design Principles



\* Modular

\* Testable

\* Explainable

\* Privacy-first

\* Secure by default

\* Self-hostable

\* Vendor-neutral



\---



\# Long-Term Vision



Spy vs Spy Computers is not a collection of unrelated tools.



It is a unified digital investigation platform where every product shares:



\* A common investigation engine

\* A common evidence model

\* A common scoring framework

\* A consistent user experience



Each new product should integrate naturally into the ecosystem rather than being built as a standalone application.



\---



\# Architecture Rule



Every new feature must answer at least one of these questions:



1\. What happened?

2\. Why do we believe that?

3\. What should the user do next?



If a feature does not improve one of those answers, it should be reconsidered.



\---



\# Mission



\*\*Spy vs Spy Computers doesn't tell people what to think.\*\*



\*\*It shows them the evidence and explains why.\*\*



