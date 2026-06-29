# BOB - UiPath AgentHack 2026 Submission Hub

This repository hosts the public GitHub Pages landing page for:

**BOB - Sovereign Compliance Agent for UiPath**

[![Live Site](https://img.shields.io/badge/Live-Submission_Page-00ff88?style=for-the-badge)](https://snapkittywest.github.io/bob-hackathon-demo/)
[![Source](https://img.shields.io/badge/Source-bob--orchestrator-111?style=for-the-badge)](https://github.com/SNAPKITTYWEST/bob-orchestrator)
[![Track](https://img.shields.io/badge/Track-Maestro_Case-ff6d00?style=for-the-badge)](https://uipath-agenthack.devpost.com/)

## Open

```text
https://snapkittywest.github.io/bob-hackathon-demo/
```

## Files

| File | Purpose |
|---|---|
| `index.html` | Single-file GitHub Pages landing page |
| `DEVPOST_SUBMISSION.md` | Copy/paste Devpost submission text |
| `PRESENTATION_OUTLINE.md` | Hackathon deck outline |

## Source Code

The actual BOB implementation lives here:

```text
https://github.com/SNAPKITTYWEST/bob-orchestrator
```

## What BOB Does

```mermaid
flowchart LR
  A["UiPath Robot"] --> B["BOB validate server"]
  B --> C["Claude Sonnet 4.6 via Bedrock"]
  B --> D["Trust Deed v1.0"]
  C --> E{"EVIDENCE or SILENCE"}
  D --> E
  E --> F["SHA-256 WORM seal"]
  E --> G["UiPath continue or human review"]
```

## Submission Checklist

- [x] Public GitHub Pages site
- [x] Public GitHub source repository
- [x] Written project description
- [x] Architecture diagram
- [x] UiPath components listed
- [x] Coding agent usage documented
- [ ] Demo video link added to Devpost
- [ ] Presentation deck link added to Devpost
