# BOB - Sovereign Compliance Agent for UiPath

## Track

Track 1: UiPath Maestro Case

## Tagline

Evidence-or-Silence compliance automation for UiPath, sealed with SHA-256 WORM audit receipts.

## Inspiration

We built BOB in one day for UiPath AgentHack 2026. The idea was simple: every enterprise AI agent makes decisions, but almost none of them can prove what happened afterward.

When an AI approves an invoice, routes a compliance case, or escalates a vendor exception, the audit record needs more than a transcript. It needs a governed verdict, a human-in-loop path, and tamper evidence.

BOB fixes that with one rule:

Evidence or Silence. Nothing in between.

## What it does

A UiPath Robot submits a document or compliance query. BOB evaluates it under the Bel Esprit D'Accord Trust Deed v1.0, a six-article governing charter, then calls Claude Sonnet 4.6 through AWS Bedrock.

BOB returns strict JSON:

```json
{
  "verdict": "EVIDENCE",
  "score": 0.87,
  "reasoning": "The invoice contains the required vendor, amount, and invoice ID fields."
}
```

If the score is at or above `0.42`, BOB returns `EVIDENCE` and UiPath may continue. If the evidence is weak, the vendor is unknown, fields are missing, or the model cannot ground the answer, BOB returns `SILENCE` and the workflow routes to human review.

Every verdict is sealed:

```text
seal(v,s,q,t) = SHA256(v | s | q | t)
```

Tamper with the verdict, score, query, or timestamp and the seal breaks.

## How we built it

BOB is a Node.js validate server with two channels:

- HTTP fallback: `POST localhost:7474/validate`
- NATS mesh: `snapkitty.agents.operator` in, `snapkitty.bifrost.sealed` out

The reasoning path uses AWS Bedrock with Claude Sonnet 4.6. The policy layer is the Bel Esprit D'Accord Trust Deed v1.0. The audit layer uses SHA-256 WORM seals. UiPath Studio orchestrates the case routing. ABZU Sovereign IDE adds an optional Phoenix bridge at `/api/validate`, publishing requests through NATS and returning the sealed verdict back to UiPath.

We used Claude Code as the coding agent during the build, qualifying the project for the UiPath for Coding Agents bonus track. Codex consolidated the final submission package and public GitHub Pages site.

## UiPath components used

- UiPath Studio / Studio Web workflow
- UiPath Robot execution path
- Track 1 Maestro Case pattern for dynamic case routing
- Human review queue for `SILENCE`
- HTTP integration to BOB validate endpoint
- Optional ABZU Phoenix API bridge for NATS-based orchestration

## Agents involved

- UiPath Robot: submits the document and waits for a verdict
- BOB: sovereign compliance reasoning agent
- Claude Sonnet 4.6 on AWS Bedrock: reasoning engine
- Trust Deed policy layer: binding governance charter
- Human reviewer: required when BOB returns `SILENCE`

## Architecture

```text
UiPath Studio -> Main.xaml -> POST localhost:7474/validate
                                  |
                                  v
                    BOB validate-server.mjs
                    Claude Sonnet 4.6 via AWS Bedrock
                    Trust Deed v1.0
                    SHA-256 WORM seal
                                  |
                                  v
                    NATS snapkitty.bifrost.sealed
                    |-- Discord #chain verdict feed
                    |-- Telegram alert path
                    |-- ABZU Phoenix API bridge
```

## Challenges

- Exposing BOB to UiPath Automation Cloud through a Cloudflare Tunnel during a one-day build.
- Updating the NATS client integration after codec behavior changed in the current package version.
- Making UiPath parse live JSON verdicts from an AI backend without allowing ambiguous model prose.
- Keeping human-in-loop routing deterministic instead of relying on a prompt instruction.

## Accomplishments

- BOB validate server is live.
- Every verdict is either `EVIDENCE` or `SILENCE`.
- Every verdict receives a SHA-256 WORM seal.
- NATS publishes sealed verdicts to the sovereign event mesh.
- ABZU Phoenix API bridge can route UiPath requests through NATS and fall back to direct HTTP.
- Built in under 24 hours with Claude Code as the coding agent.

## Formal theorems

```text
Verdict Completeness:
Every submitted document receives EVIDENCE or SILENCE.

WORM Integrity:
seal(v,s,q,t) = SHA256(v | s | q | t)
Changing v, s, q, or t breaks verification.

Trust Deed Soundness:
score >= 0.42 permits EVIDENCE.
score < 0.42 forces SILENCE.

Human-in-Loop Guarantee:
BOB(d) = SILENCE implies d enters the human review queue.

Zero Hallucination Corollary:
BOB cannot issue a confident unsupported approval because below-threshold
or unsupported claims collapse to SILENCE.
```

## What we learned

UiPath is a serious orchestration layer for enterprise agent workflows. The key is not making the AI sound confident; the key is deciding when the robot is allowed to continue. A Trust Deed changes the design from "prompt this model" to "govern this workflow."

## What's next

- Full Maestro Case for invoice-to-payment lifecycle.
- UiPath Document Understanding for OCR ingestion.
- Public Trust Deed registry so enterprises can publish and verify their own governance charters.
- Expanded ABZU LiveView dashboard for real-time verdict monitoring.
- Telegram alert environment completion.

## Links

- Project repo: https://github.com/SNAPKITTYWEST/bob-orchestrator
- Submission site: https://snapkittywest.github.io/bob-hackathon-demo/
- Related bridge: https://github.com/SNAPKITTYWEST/abzu-sovereign-ide

## Video and deck placeholders

- Demo video: paste YouTube/Vimeo link here before final Devpost submit.
- Presentation deck: paste shared deck link here before final Devpost submit.
