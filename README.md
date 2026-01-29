# mars-agent-skills

A curated, portable collection of agent Skills focused on **new-project onboarding** and **documentation-first workflows**.

These Skills are designed to be reusable across tools (e.g., Cursor, Claude Code, Trae) as they are primarily **structured SOPs + strict deliverables**.

## What you get

This repo currently includes 3 onboarding Skills:

- **project-scout**  
  Evidence-based repo reconnaissance: module map, entrypoints, core flow candidates, dependencies, open questions.

- **runbook-builder**  
  Generates an executable developer runbook: setup, run, test, debug, FAQ.

- **domain-glossary**  
  Extracts concept-level domain glossary + prioritized core scenarios (no API/DB schema details).

All Skills share a consistent output strategy (see **OUTPUT_DIR** below).

---

## Repository layout

```txt
mars-agent-skills/
  README.md
  LICENSE
  CHANGELOG.md
  CONTRIBUTING.md
  skills/
    project-scout/
      SKILL.md
    runbook-builder/
      SKILL.md
    domain-glossary/
      SKILL.md
    _template-skill/
      SKILL.md
  examples/
    sample-invocations.md
````

> Your tool (e.g., Cursor) typically discovers Skills when they are placed under:
>
> * project: `.cursor/skills/`
> * global: `~/.cursor/skills/`
>
> This repo stores Skills under `skills/` so you can easily copy/sync them into your tool-specific Skills directory.

---

## Install

### Option A — Project-level install (recommended for teams)

1. Copy the desired Skill folders into your project:

```txt
<your-project>/.cursor/skills/
  project-scout/
  runbook-builder/
  domain-glossary/
```

2. Commit the `.cursor/skills/` folder so the whole team shares the same Skills.

### Option B — Global install (recommended for individuals)

Copy the Skill folders into your global skills directory, e.g.:

* macOS / Linux:

```txt
~/.cursor/skills/
  project-scout/
  runbook-builder/
  domain-glossary/
```

> If your tool uses a different global directory, keep the same Skill folder structure:
> `<skill-name>/SKILL.md` must exist.

---

## How to use

### Basic usage (no parameters)

Ask your agent to run a Skill by name (tool-specific syntax varies). Example prompts:

* **project-scout**

  > Run skill: project-scout. Scan this repository and produce the deliverable.

* **runbook-builder**

  > Run skill: runbook-builder. Generate a local dev runbook based on repo evidence.

* **domain-glossary**

  > Run skill: domain-glossary. Extract a concept-level glossary and core scenarios.

### OUTPUT_DIR (portable output control)

All Skills support a shared convention:

* Default output directory: `docs/onboarding/`
* Override by specifying `OUTPUT_DIR=<path>` in your request

Examples:

* Write outputs into `docs/start-here/`:

  > Run skill: project-scout. OUTPUT_DIR=docs/start-here

* Write outputs into `.docs/onboarding/`:

  > Run skill: runbook-builder. OUTPUT_DIR=.docs/onboarding

### Fallback behavior (when OUTPUT_DIR is not provided)

If you do **not** specify `OUTPUT_DIR`, the Skill will choose OUTPUT_ROOT in this order:

1. `docs/onboarding/` (if it exists)
2. `docs/` (if it exists)
3. repository root `./`

### If the tool cannot write files

If file writing is not supported, each Skill will:

1. Print `SAVE_AS: <OUTPUT_ROOT>/<filename>.md`
2. Print the **full Markdown content** that you can copy and save manually.

---

## Expected deliverables

Each Skill produces exactly one Markdown document:

* `01_project_scout.md`
* `02_runbook.md`
* `03_domain_glossary.md`

By default these land in `docs/onboarding/`.

---

## Add a new Skill (quick start)

1. Copy the template:

```bash
cp -r skills/_template-skill skills/<new-skill-name>
```

2. Edit `skills/<new-skill-name>/SKILL.md`:

* Update YAML frontmatter: `name`, `description`
* Replace placeholders with your SOP + deliverable template

3. Update this README:

* Add the Skill to the list
* Add a short description

4. Update `CHANGELOG.md` and open a PR.

---

## Design principles

* **Evidence-first**: key claims must cite paths/snippets/identifiers.
* **Deliverable-driven**: each Skill outputs one reviewable artifact.
* **Portable**: minimal tool-specific assumptions; OUTPUT_DIR convention.
* **No hallucinations**: missing info must be labeled and turned into open questions.

---

## License

MIT (see `LICENSE`).

````

---
