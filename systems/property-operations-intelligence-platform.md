---
layout: default
title: Property Operations Intelligence Platform
---
# Property Operations Intelligence Platform

**An intelligence and orchestration layer built above existing property-management software**

Status: Prototype / research system

## Purpose
Connect physical-world edge signals (QR/NFC curb-sign scans), leasing/disposition data, and
workflow automation into one attribution and human-decision layer — without replacing the
client's existing PMS, which remains the system of record.

## Systems of Record
- Native PMS (Yardi, RealPage, Entrata, AppFolio, Buildium, and others) — property/unit/lease
  truth, integrated with rather than replaced
- Caphè database — structured events, signals, and workflow truth
- CRM integration (e.g. Follow Up Boss) — lead truth, once connected
- Conversational SMS gateway (e.g. Twilio) — qualification truth, once connected

## Core Data Objects
Client · PilotDeployment · PilotAsset · Property · Unit · Prospect · Inquiry · EdgeInteraction ·
Event · Signal · HumanTask · Outcome

## Architecture
`QR/NFC SCAN → SLUG RESOLUTION → STRUCTURED EVENT → ATTRIBUTION SIGNAL → HUMAN REVIEW → CRM/SMS ACTION → OUTCOME`

## Modules
Edge Capture · Attribution Intelligence · Leasing-Attention Intelligence · CRM Integration ·
Conversational SMS Qualification · Weekly Institutional Reporting

## Human Authority
Every signal opens a human task rather than triggering an automated message or CRM action.
No SMS or lead-record write happens without a person's follow-through — enforced structurally,
not just as policy, by the current adapters raising rather than silently succeeding.

## Real pilot engagement
A real institutional real-estate disposition client is running an active first pilot on this
platform. Client-identifying details and pilot-specific terms live in the private build
records, not on this public page.

## Evidence to add
- [x] Architecture diagram — a schema-validated enterprise-architecture graph in the shared Caphè Canvas
- [x] Data model — real SQL + SQLAlchemy schema, seeded with a real client's real onboarding profile
- [x] End-to-end pipeline run — QR-slug resolution → structured event → attribution signal → weekly report, run live, automated tests passing
- [ ] CRM adapter live (interface and request shape built, pending client API credentials)
- [ ] SMS integration live (interface and intent-classification logic built and tested, pending account credentials)
- [ ] Deployed public edge endpoint (sub-500ms slug resolution, geo-fencing)
- [ ] PDF/CSV weekly export (real metrics computed today; formatted export not yet built)
- [ ] Demo video
- [ ] Case study (in progress — first real pilot data lands during the active pilot window)
