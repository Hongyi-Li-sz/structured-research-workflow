---
name: structured-research-workflow
description: Research paper workflow for action plans, evidence triage, content locks, baseline audits, reproducible experiments, and paper hygiene.
---

# Structured Research Workflow

A reusable, project-agnostic skill for managing research projects that produce a paper with reproducible experiments. It encodes patterns for document-driven execution, evidence triage, content locking, baseline provenance, and result hygiene..

## Core Principle

**Start from the action plan.** Treat one document as the project entry point, recovery log, and active execution plan. Every session begins there; every meaningful change updates it.

Define a narrow, defensible **north-star claim** early and write it down. Do not drift into broader claims without updating the plan.

## Getting Started: Customize for Your Project

This skill is a template. Before using it, customize these sections for your project:

1. **North-star claim** — replace with your paper's central thesis.
2. **Startup checklist** — point to your actual document paths.
3. **Locked content** — identify your stable code, results, and generated artifacts.
4. **Baseline tiers** — classify your baselines by relationship to the claim.
5. **Evidence classification** — map your datasets/experiments to claim roles.
6. **Reporting template** — if your numbers/format differ.

See [references/project-map-template.md](references/project-map-template.md) for a fill-in-the-blank project map.

## Startup Checklist

Every session:

1. Read the active action plan (e.g., `ACTION-PLAN.md`).
2. Read the content-lock document (e.g., `STABLE-CODE-LOCK.md`) before changing code or generated results.
3. Use search (`rg`/`grep`) to find current references before editing docs or scripts.
4. If the task touches current evidence, read the method brief and strategy documents.
5. For file maps and artifact status, read the project-map reference.

## Execution Protocol

Follow this loop for each research step:

### 1. Scoping

- Identify whether the requested work touches locked code, locked JSON, or paper-facing generated artifacts.
- If it does, make the smallest possible change, use scripts rather than hand-editing, and record the reason.

### 2. Implementation

- Make the smallest code/document change that advances the plan.
- Keep exploratory or weak results under an archive path (e.g., `archive/probe_results/`).
- Put formal, paper-facing results under designated experiment and output directories (e.g., `experiments/results/`, `paper/tables/`, `paper/figures/`).
- Never hand-edit generated benchmark values; regenerate tables with scripts.

### 3. Validation

Run the narrowest useful validation:
- **Code syntax:** `python -m py_compile <script>` (or equivalent for your language)
- **Core behavior:** `python -m pytest tests -q` (or your test suite)
- **Paper build:** `pdflatex -interaction=nonstopmode -halt-on-error main.tex` (or your build tool)
- **Script dry-run:** a single-seed smoke test before a full benchmark

### 4. Hygiene

- Clean cache files (`__pycache__`, `.pytest_cache`, build artifacts) after validation when they are not useful artifacts.
- Keep the archive directory organized with date-stamped subdirectories.

### 5. Document Sync

After meaningful changes, update these documents as needed:
- Action plan (current status, completed items, next plan)
- Method brief (if the method description changed)
- Strategy document (if evidence boundaries shifted)
- Content-lock document (if new artifacts joined the lock list)
- Cleanup manifest (if files moved or were archived)
- README (if commands or artifact maps changed)

## Evidence Triage

Use this classification when interpreting results:

| Tier | Role | Action |
|------|------|--------|
| **Main evidence** | Directly supports the central claim | Feature prominently in the main paper |
| **Boundary case** | Clarifies when the method should *not* dominate | Include with explicit limitations language |
| **Appendix / context** | Useful reviewer context, not central | Place in appendix; label clearly |
| **Archive / probe** | Exploratory, failed, underpowered, or potentially misleading | Archive only; do not cite as evidence |

**Rule:** When evidence does not support the paper's claim, do not hide it. Downgrade it to boundary, appendix, or archive and update the docs.

Each dataset or experiment should have a designated role. Examples:
- **Strong positive case** (cleanest, most convincing result)
- **Practical support** (real-world dataset with small but positive margin)
- **Repair case** (method improves a weak baseline but doesn't beat alternatives)
- **Boundary case** (shows where the method is not the best route)
- **Diagnostic only** (small-data, unstable, or synthetic substitute)

## Baseline Policy

Classify baselines into tiers to keep comparisons honest and claims scoped:

### Tier A: In-Family Baselines (required in main comparison)

These directly test the paper's core claim. They share the same model family or mechanism.
- Example: random-init vs. proposed-init variants of the same architecture.

### Tier B: External Context Baselines

Standard methods from the broader literature. Useful context, not the main claim.
- Examples: CART, Random Forest, XGBoost, LightGBM for tabular tasks.
- Do not frame the proposed method as a universal replacement for these.

### Tier C: Related-Architecture Context

Methods that share architectural ideas but differ in implementation.
- Label clearly if implementations are simplified or unofficial.
- Track provenance: publication status, implementation source, adapter used.

**Provenance tracking:** Maintain a baseline audit document that records for each baseline:
- Publication status (venue, year)
- Implementation source (official, third-party, simplified in-repo)
- Adapter or wrapper used
- Decision: keep / pending / archived

Keep a baseline audit document (e.g., `BASELINE-AUDIT.md`) as the authoritative provenance record.

## Paper Policy

### Evidence-First Writing

- Keep the cleanest positive case as the headline result.
- Treat practical-support datasets as supporting, not primary.
- Treat repair cases honestly — describe them as repair, not as wins.
- Keep boundary cases visible; they strengthen the paper's credibility.
- Keep unstable, synthetic-substitute, or diagnostic-only datasets out of the main claim.

### Scope Discipline

Only polish prose after experiment coverage and evidence boundaries are stable. Wait until:
- The main benchmark table is final.
- All baseline rows are run and verified.
- Evidence boundaries are explicit and agreed upon.

### Draft State Tracking

In the strategy document, track:
- Current draft page count and compilation status.
- What content is in main body vs. appendix.
- What is still undecided (pending experiments, pending baseline verification).
- Rejection risks and planned responses.

## Content Locking

### Purpose

Prevent accidental overwrites of stable artifacts. A content-lock document lists:
- Locked core code (key modules, APIs)
- Locked test suites
- Locked main scripts (benchmarks, analysis, figure generation)
- Locked result artifacts (JSON results, summary files)
- Locked generated artifacts (tables, figures for the paper)
- Locked paper draft

### Modification Rules

**Allowed without special concern:**
- Add new experiment scripts.
- Add new analysis scripts.
- Add appendix/probe experiments under archive paths.
- Add paper text that cites locked artifacts.

**Requires extra care:**
- Any change to the core method implementation.
- Any change to formal benchmark JSON.
- Any change to paper-facing tables.
- Any hand edit to generated table contents (regenerate via scripts instead).
- Any change that reinterprets weak/unstable results as main evidence.
- Any broad rewrite that changes the locked central claim.

## Cleanup Hygiene

Maintain a cleanup manifest that records:
- Which root-level documents are current (delete obsolete ones).
- Which results are in `experiments/results/` (paper-facing) vs. `archive/` (exploratory).
- Which generated tables and figures are active vs. archived.
- What was deleted/archived and why.

**Rules:**
- Root docs should stay short and current.
- Historical exploratory results should live under `archive/`.
- Paper-facing results should live under designated experiment directories.
- Generated paper tables/figures should live under designated output directories.
- Caches can be removed after tests.

## Reporting

When finishing a significant run or session, report:

1. **What changed** (code, data, docs, results).
2. **Latest key numbers** (the 2-3 most important metrics).
3. **Evidence impact** — does the result strengthen, weaken, or only contextualize the claim?
4. **Validation commands and outcomes** (test suite, paper compile, script smoke).
5. **Next small plan** — the immediate next step from the action plan.

## Directory Conventions

Adopt a consistent structure (adapt paths to your project):

```
project-root/
  experiments/
    results/          # formal, paper-facing results (locked)
  paper/
    tables/           # generated paper tables (locked)
    figures/          # generated paper figures (locked)
    main.tex          # paper draft
  archive/
    probe_results/    # exploratory, failed, or underpowered runs
    legacy_results/   # old results preserved for traceability
  tests/              # test suite
```

## Anti-Patterns

- **Claim creep:** silently expanding the paper's claim as new results come in.
- **Baseline hiding:** burying a strong baseline that weakens the claim.
- **Hand-editing generated results:** editing benchmark numbers in tables directly instead of regenerating.
- **Weak-results-as-main:** promoting unstable, underpowered, or substitute results to main evidence.
- **Doc rot:** letting the action plan, method brief, or strategy doc go stale while the code advances.
- **Archive pollution:** mixing exploratory failures with formal results in the same directory.
