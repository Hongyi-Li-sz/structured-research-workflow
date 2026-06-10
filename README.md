# Structured Research Workflow

A reusable **Agent Skill** for managing research projects that produce papers with reproducible experiments. It works with **Claude Code** and **OpenAI Codex** because it follows the `SKILL.md`-based Agent Skills format.

## What This Is

This skill encodes repeatable research-project workflow patterns:

- **Document-driven execution** — every session starts from an action plan; every meaningful change updates it.
- **Evidence triage** — classify results as main evidence, boundary cases, appendix context, or archived probes.
- **Content locking** — protect stable code, results, generated tables, figures, and paper-facing artifacts.
- **Baseline auditing** — tier baselines by relationship to the claim and track implementation provenance.
- **Paper hygiene** — keep generated artifacts, exploratory outputs, and drafts synchronized.
- **Cleanup discipline** — maintain a manifest for what stays, what moves, and what gets archived.

This is an instruction-only skill: it ships no executable scripts, no dependencies, and no binaries.

## Compatibility

| Environment | Personal install path | Project / repository install path |
|---|---|---|
| Claude Code | `~/.claude/skills/structured-research-workflow/` | `.claude/skills/structured-research-workflow/` |
| OpenAI Codex | `~/.agents/skills/structured-research-workflow/` | `.agents/skills/structured-research-workflow/` |

Both tools use the same skill folder:

```text
structured-research-workflow/
  SKILL.md
  references/
    project-map-template.md
  agents/
    openai.yaml
```

## Quick Start

### Claude Code

Install for one project:

```bash
mkdir -p .claude/skills
cp -R structured-research-workflow .claude/skills/
```

Or install globally:

```bash
mkdir -p ~/.claude/skills
cp -R structured-research-workflow ~/.claude/skills/
```

Use it explicitly:

```text
/structured-research-workflow
```

Claude Code can also invoke it automatically when your request matches the skill description.

### OpenAI Codex

Install for one repository:

```bash
mkdir -p .agents/skills
cp -R structured-research-workflow .agents/skills/
```

Or install globally:

```bash
mkdir -p ~/.agents/skills
cp -R structured-research-workflow ~/.agents/skills/
```

Use it explicitly from Codex by mentioning the skill, for example:

```text
Use the structured-research-workflow skill to organize this research project.
```

Codex can also select it implicitly when your task matches the `description` in `SKILL.md`.

## Recommended Project Documents

Create or adapt these files in your research repository:

- `ACTION-PLAN.md` — active execution plan, current status, next steps.
- `METHOD-BRIEF.md` — concise method description.
- `STRATEGY.md` — claim, evidence boundaries, caveats, and writing plan.
- `STABLE-CODE-LOCK.md` — locked code, results, generated artifacts, and modification rules.
- `CLEANUP-MANIFEST.md` — cleanup decisions and archive map.
- `BASELINE-AUDIT.md` — baseline tiers, source, provenance, and inclusion decision.

Use [`references/project-map-template.md`](references/project-map-template.md) as a fill-in companion map for code, experiments, paper artifacts, and current priorities.

## Example Prompts

```text
Use structured-research-workflow to create an ACTION-PLAN.md for my project.
```

```text
Use structured-research-workflow to audit my experiment results and classify them as main evidence, boundary cases, appendix context, or archive probes.
```

```text
Use structured-research-workflow to review my baseline comparisons and identify provenance gaps before I update the paper.
```

## Customization Checklist

- [ ] Write a narrow, defensible north-star claim.
- [ ] Point the startup checklist to your actual document paths.
- [ ] List locked code, stable results, generated tables, and figures.
- [ ] Define baseline tiers and provenance requirements.
- [ ] Assign every dataset/experiment an evidence role.
- [ ] Separate paper-facing outputs from exploratory/archive outputs.
- [ ] Update the README if your project uses different commands or directories.

## File Structure

```text
structured-research-workflow/
  .gitignore
  CHANGELOG.md
  LICENSE
  README.md
  SKILL.md
  agents/
    openai.yaml
  references/
    project-map-template.md
```

## Design Notes

The skill is intentionally conservative. It does not try to maximize claims; it tries to keep claims, evidence, baselines, generated artifacts, and paper text aligned across many agent-assisted sessions.

It is most useful when a project has multiple experiments, changing baselines, generated paper assets, and a paper draft that must stay reproducible.

## Related Documentation

- Claude Code Skills: https://code.claude.com/docs/en/skills
- Codex Agent Skills: https://developers.openai.com/codex/skills
- Codex AGENTS.md guidance: https://developers.openai.com/codex/guides/agents-md

## License

MIT — see [LICENSE](LICENSE).
