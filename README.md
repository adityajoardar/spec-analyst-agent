# Spec Analyst — AI Automation-Opportunity Agent

An AI agent that reads a functional specification document, breaks it into discrete requirements, and recommends where automation genuinely adds value — with effort and risk ratings for each — while deliberately flagging where simple rules beat AI.

**Live demo:** https://YOUR-USERNAME.github.io/spec-analyst-agent/
_(update this link after enabling GitHub Pages — see below)_

---

## What it does

- **Ingests a specification** in PDF, DOCX, or TXT and extracts the text in the browser.
- **Decomposes it into discrete requirements** — each manual process, decision point, or repetitive step.
- **Assesses AI-fit per requirement** — recommends a concrete technique (NLP, anomaly detection, rules-based STP) _or explicitly flags where no AI is needed_.
- **Scores effort and risk** (Low / Medium / High) and ties every finding back to a verbatim snippet in the source document.
- **Answers follow-up questions** through a chat panel that can re-run the analysis with a different focus (e.g. compliance-only).

The demo is pre-loaded with a section of the publicly available Oracle FLEXCUBE CASA user guide, and you can upload your own document to analyse.

## How it works

The design separates three concerns — **parsing, reasoning, and rendering** — so each can change independently:

1. **Browser (static HTML)** — document parsing (pdf.js / mammoth.js), the results canvas, the chat panel, and summary metrics.
2. **Edge proxy (Cloudflare Worker)** — holds the API key server-side as an encrypted secret and forwards requests, so no credentials are exposed in the client.
3. **Model (Claude / Anthropic API)** — a system prompt enforces requirement extraction, AI-fit assessment, the "don't force AI where rules suffice" rule, and structured JSON output.

A full BPMN 2.0 process model of the end-to-end workflow is included in this repo (`spec_analyst_agent.bpmn`) — a two-pool collaboration diagram connecting the human analyst workflow with the agent pipeline via message flows. Open it in [Camunda Modeler](https://camunda.com/download/modeler/) or [draw.io](https://app.diagrams.net/).

## Repository contents

| File | Description |
|------|-------------|
| `index.html` | The Spec Analyst tool (single-file web app) |
| `spec_analyst_agent.bpmn` | BPMN 2.0 process model (open in Camunda Modeler / draw.io) |
| `README.md` | This file |

## Running it yourself

The hosted demo works out of the box. To run your own copy, you'll need an [Anthropic API key](https://console.anthropic.com/) and a proxy to hold it (a small Cloudflare Worker; the browser never sees the key). See the architecture notes for the proxy pattern.

## Tech stack

JavaScript · Claude (Anthropic API) · Cloudflare Workers · pdf.js · mammoth.js · BPMN 2.0

## Note

Spec Analyst is a self-initiated portfolio project, built to demonstrate an end-to-end approach to automation-opportunity analysis — from stakeholder-facing process modelling through to a working prototype. It is not a client deliverable, and the example document is publicly available Oracle product documentation.

---

_Built by Aditya Joardar — Senior Business Analyst & AI Automation Consultant, UK._
