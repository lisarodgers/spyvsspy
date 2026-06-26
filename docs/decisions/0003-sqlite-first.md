\# ADR-0003: SQLite First



| Field             | Value                 |

| ----------------- | --------------------- |

| \*\*Status\*\*        | Accepted              |

| \*\*Date\*\*          | 2026-06-26            |

| \*\*Authors\*\*       | Lisa Rodgers, ChatGPT |

| \*\*Supersedes\*\*    | None                  |

| \*\*Superseded By\*\* | None                  |



\---



\# Context



Spy vs Spy Computers is intended to be a privacy-first, self-hostable investigation platform.



The first release focuses on building a reliable investigation engine rather than supporting high-volume enterprise deployments.



The project requires a database that is dependable, easy to deploy, simple to back up, and capable of operating completely offline.



\---



\# Decision



SQLite will be the default database for Version 1.



The application architecture will remain database-agnostic so that future versions can support PostgreSQL or MariaDB without requiring major changes to the investigation engine.



SQLite is the implementation choice.



It is not an architectural limitation.



\---



\# Rationale



\## Simplicity



SQLite requires no server installation.



A new investigator can clone the repository, start the application, and begin working immediately.



\---



\## Reliability



SQLite has an excellent reputation for stability and data integrity.



For a single-user or small-team investigation platform, it provides more than enough capability.



\---



\## Offline Capability



SQLite aligns naturally with the Offline First philosophy.



No database server is required.



No network configuration is required.



The application remains fully functional without Internet access.



\---



\## Self-Hosting



SQLite lowers the barrier to entry.



Users can deploy Spy vs Spy Computers on:



\* Personal computers

\* Laptops

\* Home servers

\* Raspberry Pi-class hardware

\* Small business systems



without requiring database administration.



\---



\## Development Speed



A simpler development environment allows the project to focus on investigation features rather than infrastructure.



\---



\# Consequences



\## Positive



\* Zero configuration

\* Easy backups

\* Portable database file

\* Excellent documentation

\* Mature ecosystem

\* Lower onboarding complexity



\---



\## Trade-offs



SQLite is not intended for large-scale concurrent write workloads.



Future enterprise deployments may require PostgreSQL or MariaDB.



The architecture will be designed to make that migration straightforward.



\---



\# Alternatives Considered



\## PostgreSQL



Advantages:



\* Enterprise scalability

\* Advanced indexing

\* High concurrency



Disadvantages:



\* More operational complexity

\* Higher onboarding barrier

\* Database server required



Deferred for future releases.



\---



\## MariaDB



Advantages:



\* Mature ecosystem

\* Broad hosting support



Disadvantages:



\* Additional administration

\* Greater deployment complexity



Deferred for future releases.



\---



\# Guiding Principles



Choose the simplest technology that fully supports the current mission.



Optimize for maintainability before scalability.



\---



\# Success Criteria



A new contributor should be able to:



\* Clone the repository

\* Install dependencies

\* Launch the application

\* Begin an investigation



without installing a separate database server.



\---



\# Related Documents



\* DATABASE.md

\* ARCHITECTURE.md

\* ADR-0001 Project Vision

\* ADR-0002 Offline First



\---



> \*\*The best default is the one that lets people start building immediately.\*\*



