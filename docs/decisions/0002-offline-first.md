\# ADR-0002: Offline First



| Field | Value |

|-------|-------|

| \*\*Status\*\* | Accepted |

| \*\*Date\*\* | 2026-06-26 |

| \*\*Authors\*\* | Lisa Rodgers, ChatGPT |

| \*\*Supersedes\*\* | None |

| \*\*Superseded By\*\* | None |



\---



\# Context



Digital investigations frequently involve sensitive information, including email headers, message content, IP addresses, domain names, and other evidence that users may not wish to share with third-party services.



Many existing investigation platforms require evidence to be uploaded to remote servers before analysis can begin. While this approach offers convenience, it introduces concerns around privacy, trust, regulatory compliance, and long-term availability.



Spy vs Spy Computers is intended to give investigators control over their own data while maintaining transparency throughout the investigation process.



\---



\# Decision



Spy vs Spy Computers will adopt an \*\*Offline First\*\* architecture.



The platform must be fully functional without an Internet connection for all core investigation capabilities.



Core investigation features—including parsing, evidence collection, threat scoring, reporting, and local history—must operate entirely on the user's machine.



Internet connectivity should enhance investigations but must never be required for them.



\---



\# Definition of Offline First



Offline First means:



\* Core functionality works without Internet access.

\* External services are optional enhancements.

\* User data remains under user control.

\* The application does not assume continuous connectivity.



Offline First does \*\*not\*\* mean the application can never use the Internet.



Instead, network-based features are treated as optional enrichment layers.



\---



\# Rationale



\## Privacy



Users should not have to upload potentially sensitive evidence to a third party simply to understand it.



Investigation data belongs to the investigator.



\---



\## Transparency



Local analysis makes it easier to understand exactly what the software is doing.



No hidden cloud processing.



No undisclosed remote analysis.



\---



\## Reliability



The platform should remain useful:



\* during Internet outages

\* in isolated environments

\* within secure corporate networks

\* inside research labs

\* in educational settings



\---



\## Longevity



A local investigation platform remains useful regardless of the availability or pricing of external services.



The project should not become dependent on a particular API provider or cloud platform.



\---



\# External Intelligence



Some investigations benefit from additional context, including:



\* WHOIS

\* RDAP

\* ASN information

\* Reverse DNS

\* Certificate Transparency logs

\* Reputation databases

\* Threat intelligence feeds



These services are considered \*\*enrichment providers\*\*.



Rules:



\* User initiated

\* Clearly identified

\* Individually configurable

\* Fully disableable

\* Never modify original evidence



The investigation should always distinguish between:



\* Local evidence

\* External enrichment



\---



\# AI Integration



Artificial intelligence should follow the same philosophy.



Local AI models are preferred whenever practical.



Cloud-based AI services are optional tools that users may enable intentionally.



The platform must never require a cloud AI service to complete a core investigation.



\---



\# Consequences



\## Positive



\* Strong privacy

\* Works without Internet

\* Easier regulatory compliance

\* Better user trust

\* Self-host friendly

\* Lower vendor lock-in

\* Long-term sustainability



\---



\## Trade-offs



Some enrichment data will be unavailable while offline.



Users who enable online intelligence may receive additional context that is not available during a fully offline investigation.



This trade-off is intentional.



Evidence quality should never depend on Internet access.



\---



\# Alternatives Considered



\## Cloud First



All investigations occur on remote infrastructure.



Advantages:



\* Centralized updates

\* Shared intelligence

\* Minimal local requirements



Disadvantages:



\* Privacy concerns

\* Vendor dependence

\* Internet required

\* Difficult self-hosting



Rejected.



\---



\## Hybrid by Default



Core analysis occurs locally while background requests automatically enrich investigations.



Advantages:



\* Better default experience

\* Additional context



Disadvantages:



\* Less transparent

\* Potential privacy surprises

\* Harder to reason about network activity



Rejected.



Spy vs Spy Computers should never contact external services without the user's knowledge.



\---



\# Guiding Principles



Offline capability is a feature.



Privacy is the default.



Internet connectivity enhances investigations.



It does not define them.



\---



\# Success Criteria



A user with no Internet connection should still be able to:



\* Create an investigation

\* Analyze an email

\* Review evidence

\* Generate findings

\* Produce a report

\* Save investigation history



External intelligence should improve investigations but never be required to complete them.



\---



\# Related Documents



\* ARCHITECTURE.md

\* SECURITY.md

\* DATABASE.md

\* PRODUCT\_PRINCIPLES.md

\* ADR-0001 Project Vision



\---



> \*\*The investigator owns the evidence.\*\*



> \*\*The software should help explain it—not take control of it.\*\*



