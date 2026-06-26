# Spy vs Spy Computers

# DATABASE.md

## Purpose

This document defines the logical database architecture for the Spy vs Spy Computers platform.

The database is designed to support long-term growth while remaining lightweight enough to run on SQLite during early development.

The central concept of the database is the **Investigation**.

Everything else is evidence attached to an investigation.

---

# Database Philosophy

The database should be:

* Privacy First
* Explainable
* Extensible
* Normalized where practical
* Easy to migrate to PostgreSQL or MariaDB
* Suitable for offline operation

The database should never require cloud services.

---

# Core Entity

## Investigation

Every action performed within the application creates an Investigation.

Examples:

* Email Analysis
* Header Analysis
* IP Investigation
* Domain Lookup
* SSL Inspection
* DNS Analysis
* Future Log Analysis

Everything connects back to this table.

---

# Entity Relationship Overview

```text
Users
  │
  ├────────────┐
  │            │
Investigations │
  │            │
  ├── Emails
  ├── Indicators
  ├── Findings
  ├── Threat Scores
  ├── SMTP Hops
  ├── IP Addresses
  ├── Reports
  ├── Notes
  └── Attachments (metadata only)
```

---

# Tables

## users

Purpose:

Application users.

Fields

* id
* username
* password_hash
* email
* role
* created_at
* last_login

---

## investigations

Purpose:

Master record for every investigation.

Fields

* id
* investigation_type
* title
* status
* created_by
* created_at
* updated_at
* completed_at

Examples

EMAIL

DOMAIN

URL

IP

SSL

DNS

LOG

---

## emails

Purpose

Stores metadata extracted from uploaded emails.

Fields

* id
* investigation_id
* subject
* sender_name
* sender_address
* recipient_address
* message_id
* return_path
* sent_date
* safe_excerpt

Do not store:

* HTML
* Attachments
* Original .eml

---

## smtp_hops

Purpose

One row per Received header.

Fields

* id
* investigation_id
* hop_number
* hostname
* ip_address
* trusted
* timestamp

Allows visualization of the SMTP route.

---

## ip_addresses

Purpose

Unique IP database.

Fields

* id
* ip
* version
* reverse_dns
* country
* asn
* provider
* abuse_contact
* first_seen
* last_seen

This table is shared across all investigations.

---

## indicators

Purpose

Evidence discovered during analysis.

Examples

Bitcoin Wallet

Failed SPF

Null Return Path

Known Campaign

Suspicious URL

Blank From Header

Fields

* id
* investigation_id
* indicator_type
* severity
* confidence
* evidence
* explanation

---

## threat_scores

Purpose

Stores calculated risk.

Fields

* id
* investigation_id
* score
* confidence
* recommendation
* calculated_at

The score is reproducible from the indicators.

---

## findings

Purpose

Human-readable conclusions.

Example

"The email appears to be a known Bitcoin sextortion campaign."

Fields

* id
* investigation_id
* title
* summary
* confidence

---

## reports

Purpose

Generated investigation reports.

Fields

* id
* investigation_id
* report_type
* created_at
* json_path
* pdf_path

Future versions may support digitally signed reports.

---

## notes

Purpose

Investigator notes.

Fields

* id
* investigation_id
* created_by
* note
* created_at

---

## tags

Purpose

User-defined organization.

Examples

Bitcoin

Phishing

Customer

Training

Malware

---

## investigation_tags

Many-to-many relationship between investigations and tags.

---

## campaigns

Purpose

Groups related investigations.

Examples

Bitcoin Sextortion

Office365 Credential Harvesting

Fake PayPal Invoice

Fields

* id
* name
* description
* first_seen
* last_seen

---

## campaign_members

Maps investigations to campaigns.

One investigation may belong to one or more campaigns.

---

## knowledge_articles

Purpose

Educational content.

Examples

What is SPF?

What is DKIM?

What is DMARC?

Bitcoin Sextortion Explained

Fields

* id
* slug
* title
* category
* markdown_path

---

# Future Tables

Reserved for future versions.

* domains
* dns_records
* ssl_certificates
* urls
* web_servers
* log_events
* malware_hashes
* iocs
* reputation_history

---

# Primary Relationships

One User

↓

Many Investigations

One Investigation

↓

Many Indicators

One Investigation

↓

Many SMTP Hops

One Investigation

↓

Many Findings

One Investigation

↓

One Threat Score

One Investigation

↓

Many Notes

One Campaign

↓

Many Investigations

One IP Address

↓

Many Investigations

---

# Data Retention

Default

Store

* Metadata
* Indicators
* Findings
* Threat Scores
* Notes

Delete

* Original uploads
* HTML bodies
* Attachments

Retention should be configurable.

---

# Performance

SQLite will support Version 1.

Design should allow migration to:

* PostgreSQL
* MariaDB

without schema redesign.

---

# Indexes

Initial indexes

* investigations.created_at
* investigations.investigation_type
* ip_addresses.ip
* emails.message_id
* campaigns.name
* threat_scores.score

---

# Migration Strategy

All schema changes should use migrations.

Never modify production databases manually.

---

# Design Rule

The database exists to preserve evidence.

It should never alter, reinterpret, or overwrite original observations.

Derived conclusions belong in Findings and Threat Scores.

Raw observations belong in Indicators.

---

# Mission

**Spy vs Spy Computers doesn't tell people what to think.**

**It shows them the evidence and explains why.**
