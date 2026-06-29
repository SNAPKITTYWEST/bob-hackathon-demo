# BOB AgentHack Presentation Outline

## Slide 1 - Title

BOB - Sovereign Compliance Agent for UiPath

Track 1: Maestro Case

## Slide 2 - Problem

Enterprise AI agents can approve, route, and escalate business actions, but most cannot prove why a decision happened or whether the audit trail was tampered with.

## Slide 3 - Core Rule

Evidence or Silence.

EVIDENCE lets UiPath continue.
SILENCE routes to human review.

## Slide 4 - Workflow

UiPath Robot submits document -> BOB validates -> Bedrock Claude Sonnet 4.6 reasons -> Trust Deed applies -> WORM seal emitted -> UiPath continues or escalates.

## Slide 5 - Architecture

Show:

UiPath Studio
BOB validate-server.mjs
AWS Bedrock
Trust Deed v1.0
NATS event mesh
ABZU Phoenix bridge
Human review queue

## Slide 6 - Theorems

Verdict Completeness
WORM Integrity
Trust Deed Soundness
Human-in-Loop Guarantee
Zero Hallucination Corollary

## Slide 7 - Demo Script

1. Start BOB on `localhost:7474`.
2. Send compliant document query.
3. Show EVIDENCE response and seal.
4. Send unknown vendor or incomplete document.
5. Show SILENCE response.
6. Show UiPath route to human review.
7. Show NATS/Discord/Telegram verdict feed if available.

## Slide 8 - What Was Built

Node validate server, Bedrock integration, Trust Deed governance, SHA-256 WORM seals, NATS dual channel, ABZU Phoenix bridge, UiPath routing pattern.

## Slide 9 - What Is Next

Full Maestro Case invoice-to-payment, Document Understanding OCR, public Trust Deed registry, real-time ABZU dashboard.

## Slide 10 - Links

Repo: https://github.com/SNAPKITTYWEST/bob-orchestrator
Submission: https://snapkittywest.github.io/bob-hackathon-demo/
