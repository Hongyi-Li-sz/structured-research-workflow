# Project Map Template

Fill this in for your research project. It serves as a quick-reference companion to the action plan.

## Locked Core Code

List the key modules and classes that should not be casually rewritten:

- `<path/to/module.py>`: `<ClassName>`, `<function_name>`.
- `<path/to/module.py>`: `<ClassName>`, `<key_method>`.

Avoid broad rewrites here. If a fix is necessary, make the smallest change and update tests/docs.

## Main Scripts

List the scripts that produce paper-facing results:

- `<experiments/benchmark_*.py>`: description.
- `<experiments/analyze_*.py>`: description, regenerates tables.
- `<experiments/plot_*.py>`: description, generates figures.
- `<experiments/<other>.py>`: description.

## Paper-Facing Results

### JSON Results

- `<experiments/results/<main_benchmark>.json>`
- `<experiments/results/<main_benchmark>_summary.json>`
- `<experiments/results/<mechanism_sweep>.json>`

### Generated Tables

- `<paper/tables/<main_table>.{md,tex}>`
- `<paper/tables/<diagnostics_table>.{md,tex}>`
- `<paper/tables/<appendix_table>.{md,tex}>`
- `<paper/tables/<context_baselines_table>.{md,tex}>`

### Generated Figures

- `<paper/figures/<main_figure>.{png,pdf}>`
- `<paper/figures/<mechanism_figure>.{png,pdf}>`

## Key Current Numbers

### Main Positive

- `<dataset_1>`: `<baseline_1>` `X.XXXX +/- Y.YYYY`; `<proposed_method>` `X.XXXX +/- Y.YYYY`.

### Practical Support

- `<dataset_2>`: `<baseline>` `X.XXXX +/- Y.YYYY`; `<proposed_method>` `X.XXXX +/- Y.YYYY`.

### Boundaries

- `<dataset_3>`: description of why the method does not dominate here.
- `<dataset_4>`: description of a boundary case.

### Context Baselines

- `<dataset_1>` best external: `<method>` `X.XXXX +/- Y.YYYY`.
- `<dataset_2>` best external: `<method>` `X.XXXX +/- Y.YYYY`.

## Current Next Priorities

1. Priority 1: description.
2. Priority 2: description.
3. Priority 3: description.
4. Priority 4: description.
5. Priority 5: description.

## Document Map

- `<ACTION-PLAN.md>`: current execution plan and content-lock protocol.
- `<METHOD-BRIEF.md>`: concise method description.
- `<STRATEGY.md>`: submission strategy, claims, caveats, and next experiments.
- `<STABLE-CODE-LOCK.md>`: files/results that should not be changed casually.
- `<CLEANUP-MANIFEST.md>`: cleanup decisions and result-folder hygiene.
- `<BASELINE-AUDIT.md>`: baseline publication and implementation provenance.

Current paper draft:

- `<paper/main.tex>`
- `<paper/main.pdf>`
