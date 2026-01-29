# examples/sample-invocations.md

This file provides copy-paste examples for running Skills from this repo in different tools.
Because each tool’s UI/commands may vary by version, these examples focus on **portable prompting**:
- explicitly name the Skill
- optionally provide `OUTPUT_DIR=<path>`
- remind the agent about the shared output behavior (default + fallback + copy/paste mode)

---

## Common conventions used by all Skills in this repo

### OUTPUT_DIR (portable output control)
- Default output directory: `docs/onboarding/`
- Override by specifying: `OUTPUT_DIR=<path>` in your request

Examples:
- `OUTPUT_DIR=docs/start-here`
- `OUTPUT_DIR=.docs/onboarding`
- `OUTPUT_DIR=./docs/onboarding`

### Fallback behavior (when OUTPUT_DIR is not provided)
If you do **not** specify OUTPUT_DIR, the Skill chooses output root in this order:
1) `docs/onboarding/` (if exists)
2) `docs/` (if exists)
3) repository root `./`

### If the tool cannot write files
The Skill will:
1) Print `SAVE_AS: <OUTPUT_ROOT>/<filename>.md`
2) Print the full Markdown content for copy/paste

---

## Cursor (Agent Chat) — suggested usage

> Note: Cursor versions differ. Some support slash commands or UI “Skills” pickers.
> If you don’t see a Skill picker, just use the “portable prompt” examples below.

### A) Portable prompt (works even without a Skill picker)

#### 1) project-scout (default output)
Copy/paste into Cursor chat:

> Run the skill **project-scout** on this repository.  
> Produce exactly one deliverable following the skill instructions.  
> If you can write files, save it to the default output directory. If not, print `SAVE_AS:` and the full Markdown content.

#### 2) project-scout with OUTPUT_DIR override
> Run the skill **project-scout** on this repository.  
> OUTPUT_DIR=docs/start-here  
> Produce exactly one deliverable. If file writing is unavailable, print `SAVE_AS:` and full Markdown.

#### 3) runbook-builder
> Run the skill **runbook-builder**.  
> OUTPUT_DIR=docs/onboarding  
> Generate an executable runbook from repo evidence only.  
> Save the output file if possible; otherwise print `SAVE_AS:` and full Markdown.

#### 4) domain-glossary
> Run the skill **domain-glossary**.  
> OUTPUT_DIR=docs/onboarding  
> Extract concept-level terms and scenarios only (no API/DB schema details).  
> Save file if possible; otherwise print `SAVE_AS:` and full Markdown.

### B) Optional: “strict evidence” reinforcement
Use this if you want extra rigor:

> While running the skill, every key claim must include EVIDENCE (path + snippet/identifier).  
> If info is missing, label it as [ASSUMPTION] and list it under [OPEN QUESTIONS].

---

## Claude Code — suggested usage

Claude Code supports running tasks against your local repo context.
The exact invocation may vary by how you launch Claude Code, but the **portable prompt** is the same.

### A) project-scout (default output)
> Please run the skill **project-scout** for this codebase.  
> Produce one deliverable as instructed.  
> Default output: `docs/onboarding/`. If you cannot write files, print `SAVE_AS:` and the full Markdown.

### B) project-scout with OUTPUT_DIR override
> Run the skill **project-scout**. OUTPUT_DIR=docs/start-here  
> Follow the skill’s procedure and produce exactly one deliverable.  
> If file writing isn’t supported, print `SAVE_AS:` + full Markdown content.

### C) runbook-builder
> Run the skill **runbook-builder**. OUTPUT_DIR=docs/onboarding  
> Generate a runnable local dev runbook based on repo evidence.  
> Save it to the output directory if possible; otherwise print `SAVE_AS:` and full Markdown.

### D) domain-glossary
> Run the skill **domain-glossary**. OUTPUT_DIR=docs/onboarding  
> Output only concept-level domain glossary + prioritized scenarios.  
> Save it if possible; otherwise print `SAVE_AS:` and full Markdown.

---

## Trae CN — suggested usage

Trae CN (and similar agent tools) may not use the same “Skill picker” terminology,
but you can still run these Skills by explicitly instructing the agent to follow
the SOP defined in `SKILL.md`.

### A) Portable prompt pattern for Trae CN

**Pattern**
> Read and follow: `skills/<skill-name>/SKILL.md`  
> Run this skill against the current repository context.  
> OUTPUT_DIR=<path> (optional)  
> Produce exactly one deliverable. If you can’t write files, print `SAVE_AS:` and full Markdown.

### B) project-scout (default output)
> Read and follow: `skills/project-scout/SKILL.md`  
> Run this skill against the current repository.  
> Produce exactly one deliverable.  
> Default output is `docs/onboarding/`; if you can’t write files, print `SAVE_AS:` and full Markdown.

### C) project-scout with OUTPUT_DIR override
> Read and follow: `skills/project-scout/SKILL.md`  
> OUTPUT_DIR=docs/start-here  
> Run this skill and produce exactly one deliverable.  
> If you can’t write files, print `SAVE_AS:` and full Markdown.

### D) runbook-builder
> Read and follow: `skills/runbook-builder/SKILL.md`  
> OUTPUT_DIR=docs/onboarding  
> Generate an executable developer runbook from repo evidence only.  
> Save file if possible; otherwise print `SAVE_AS:` and full Markdown.

### E) domain-glossary
> Read and follow: `skills/domain-glossary/SKILL.md`  
> OUTPUT_DIR=docs/onboarding  
> Extract a concept-level glossary + prioritized scenarios only.  
> Save file if possible; otherwise print `SAVE_AS:` and full Markdown.

---

## Tips for best results (tool-agnostic)

1) Start with **project-scout** first (module map + entrypoints), then:
   - runbook-builder (how to run)
   - domain-glossary (terms + scenarios)

2) If the repo is large, tell the agent:
   - “Start with README/docs and the entrypoints first.”
   - “Pick 2–3 core flows only for v1.”

3) Always end with [OPEN QUESTIONS] so you know what to ask teammates next.
