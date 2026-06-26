\# Spy vs Spy Computers



\# SECURITY.md



\## Security Philosophy



Security is not a feature.



It is a design requirement.



Every component of Spy vs Spy Computers must be designed under the assumption that the data it receives may be malicious.



We trust evidence.



We do not trust input.



\---



\# Core Principles



\## Privacy First



User data belongs to the user.



The application should never transmit email content to third-party services unless the user explicitly enables and requests it.



All investigations should be capable of running completely offline.



\---



\## Secure by Default



The safest configuration should also be the default configuration.



Examples:



\* Uploads deleted automatically

\* No HTML rendering

\* No attachment execution

\* Authentication enabled

\* Rate limiting enabled

\* CSRF protection enabled



\---



\## Principle of Least Privilege



Every component should operate with only the permissions it requires.



The web application should never run as root.



Uploaded files should never be executable.



Only the application should have permission to access investigation files.



\---



\## Transparency



Security decisions should be visible.



Users should know:



\* What was analyzed

\* What was ignored

\* Why a conclusion was reached

\* What evidence supports that conclusion



\---



\# Threat Model



Assume every uploaded email may contain:



\* Malicious HTML

\* JavaScript

\* Dangerous attachments

\* Embedded tracking pixels

\* Phishing links

\* Malformed MIME structures

\* Header injection attempts

\* Unicode spoofing

\* Extremely large payloads



The parser must safely process all of these without executing or rendering them.



\---



\# Upload Security



Accepted formats:



\* .eml

\* Raw RFC 5322 message

\* Plain-text email headers



Rejected:



\* ZIP

\* EXE

\* Office documents

\* PDFs

\* Images

\* Scripts

\* Unknown file types



Maximum upload size should be configurable.



Uploads should be stored outside the public web root.



Uploads should be deleted immediately after successful parsing unless explicitly retained by an administrator.



\---



\# HTML Email



Never render HTML email directly.



Instead:



\* Extract plain text

\* Sanitize HTML if preview is required

\* Remove scripts

\* Remove forms

\* Remove remote resources

\* Remove tracking pixels

\* Disable automatic image loading



No remote content should ever be fetched during analysis.



\---



\# Attachments



Attachments are not executed.



Attachments are not opened.



Attachments are not previewed.



Future versions may calculate:



\* SHA-256

\* SHA-1

\* MD5



without opening the file.



\---



\# External Requests



The investigation engine should never contact external systems during parsing.



Optional enrichment modules (WHOIS, RDAP, reputation services) must be:



\* Clearly identified

\* User initiated

\* Configurable

\* Disableable



The parser itself must remain fully offline capable.



\---



\# Authentication



Requirements:



\* Strong password hashing

\* Secure cookies

\* CSRF protection

\* Session timeout

\* Login rate limiting

\* Optional multi-factor authentication in future versions



Administrative interfaces must never be publicly accessible without authentication.



\---



\# Data Storage



Store only what is required.



Default storage:



\* Metadata

\* Investigation results

\* Threat score

\* Indicators

\* Safe text excerpt



Do not store:



\* Original .eml

\* Attachments

\* HTML body

\* Embedded images



Retention policies should be configurable.



\---



\# Logging



Logs should contain operational information only.



Never log:



\* Passwords

\* Session tokens

\* Authentication secrets

\* Complete email bodies

\* Attachments



Sensitive values should be masked where practical.



\---



\# Secrets



Secrets must never be committed to Git.



Use:



\* .env

\* Environment variables

\* Secret management for future deployments



Example secrets:



\* Flask secret key

\* Database credentials

\* API keys



\---



\# Input Validation



Every user input must be treated as untrusted.



Validate:



\* Uploads

\* Forms

\* URLs

\* Search fields

\* Configuration values



Escape all output before rendering.



\---



\# Dependencies



Only actively maintained libraries should be used.



Regularly:



\* Review dependencies

\* Apply security updates

\* Remove unused packages

\* Monitor known vulnerabilities



\---



\# Deployment



Development:



\* Local environment

\* Debug mode enabled



Production:



\* HTTPS only

\* HSTS enabled

\* Secure cookies

\* Debug disabled

\* Error details hidden from users

\* Security headers enabled



\---



\# Future Security Goals



\* Docker container hardening

\* Reverse proxy security

\* Multi-factor authentication

\* Role-based access control

\* Encrypted investigation database

\* Digital signatures for reports

\* Audit logging

\* Automated dependency scanning

\* Security dashboard



\---



\# Security Review Checklist



Before every release:



\* All tests pass

\* No secrets committed

\* Dependencies reviewed

\* Upload handling verified

\* Authentication tested

\* Authorization tested

\* HTTPS verified

\* Security headers verified

\* Error handling reviewed

\* Logs reviewed



\---



\# Security Promise



Spy vs Spy Computers is designed with the assumption that investigators should not have to sacrifice privacy in order to investigate suspicious digital evidence.



The software should help users understand threats while keeping control of their own data.



\---



\# Mission



\*\*Spy vs Spy Computers doesn't tell people what to think.\*\*



\*\*It shows them the evidence and explains why.\*\*



