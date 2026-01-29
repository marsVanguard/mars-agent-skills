# Contributing to mars-agent-skills

Thanks for contributing! This repo focuses on **portable, deliverable-driven agent Skills**.

## What is a Skill in this repo?

A Skill is a folder containing a required `SKILL.md` (with YAML frontmatter) and optional resources.

Minimum structure:

```txt
skills/<skill-name>/
  SKILL.md
````

## Naming conventions

* Folder name: `kebab-case` (e.g., `metric-spec`, `project-scout`)
* YAML `name`: match the folder name
* Keep names short and action-oriented

## Required conventions (must follow)

### 1) Shared output strategy (OUTPUT_DIR)

Every Skill must include the same portable output rules:

* Default output: `docs/onboarding/`
* Support override: `OUTPUT_DIR=<path>`
* Fallback order if OUTPUT_DIR not provided:

  1. `docs/onboarding/` if exists
  2. `docs/` if exists
  3. repo root `./`
* If file writing is not supported:

  * Print `SAVE_AS: <OUTPUT_ROOT>/<filename>.md`
  * Print full Markdown content to copy/paste

### 2) Deliverable-driven

Each Skill should have exactly **one primary deliverable** (one Markdown file).

* Use a predictable filename (e.g., `01_xxx.md`)
* Include a strict deliverable template (ordered sections)

### 3) Evidence-first

For repo-scanning Skills, all key claims must include evidence:

* file path
* snippet/keyword/identifier

Never invent facts not present in the repo. Missing info must be labeled and turned into open questions.

### 4) Avoid tool-specific dependencies

Skills should be usable across different agent tools:

* Do not require proprietary UI features
* Prefer plain Markdown outputs
* If you reference scripts/assets, ensure they are optional and documented

## Adding a new Skill

1. Copy the template:

```bash
cp -r skills/_template-skill skills/<new-skill-name>
```

2. Edit `SKILL.md`:

* YAML: `name`, `description`
* Add/replace: constraints, procedure, deliverable template

3. Update docs:

* Add the Skill to `README.md`
* Add an entry to `CHANGELOG.md`

4. Submit a PR:

* Keep changes scoped and reviewable
* Include an example invocation in the PR description

## Changelog policy

Use Keep a Changelog style:

* Add entries under `Unreleased`
* Categorize as: Added / Changed / Fixed / Deprecated / Removed / Security

## Code of conduct

Be respectful and constructive. If you plan a big change, open an issue first.

````

---
