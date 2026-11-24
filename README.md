# design-system-spec

An agent skill that builds a complete, implementation-ready **design-system spec**: machine-readable tokens plus human rules plus testable acceptance criteria, so an AI agent (or a developer) can build UI without guessing.

It started from a Dribbble shot of design-system cards (Tokens & Variables, Color, Typography, Grid/Layout/Spacing, Icons & Media Assets, Components) and adds everything those cards leave out.

## What it produces

| File | Purpose |
|---|---|
| `DESIGN.md` | Google DESIGN.md format: YAML tokens + ordered prose sections. Lint-checked. |
| `design-system/SPEC.md` | Full spec, 25 sections, each with acceptance criteria |
| `tokens.json` | W3C DTCG 2025.10 tokens (exported) |
| `tailwind.theme.json` | Optional Tailwind export |
| `design-system/audit.mjs` | Drift check: exact / near-miss / unknown values, ratchet baseline, exit 1 on new violations |

## What it covers

- **Core six:** tokens & variables (3 tiers), color, typography, grid/layout/spacing, icons & media, components (anatomy, states, tokens, keyboard/ARIA, edge cases).
- **Usually missing:** principles, elevation/radius/borders, motion (+ reduced motion), theming/modes, WCAG 2.2 AA, interaction patterns, content/UX writing, data viz, responsive/platform, performance budgets, implementation mapping, governance, anti-patterns, QA checklist.
- **Enforcement:** closed token layer, three-layer variable indirection, audit script + gates, Figma `codeSyntax` bridge, 10-category audit scoring.

Three modes: **Build**, **Audit**, **Reconcile** (Figma vs code, report only).

## Install

**Claude Code / Codex / OpenCode (any agent that loads `SKILL.md` folders)**
```bash
git clone https://github.com/tonyd2f/design-system-spec.git
cp -r design-system-spec/design-system-spec ~/.claude/skills/
```
Restart the agent or start a new session.

**claude.ai:** zip the inner `design-system-spec/` folder (SKILL.md at its root) and upload it under Settings → Capabilities → Skills.

## Use

> use design-system-spec to build a design system spec for this project

> use design-system-spec to audit this repo against our tokens

It asks at most 3 multiple-choice questions (platform, dark/light as brand or preference, stack), inspects your existing code and assets first, then builds and lints.

## Requirements

- Node.js (for `npx -y @google/design.md lint|export` and `audit.mjs`)
- Network access to npm for the DESIGN.md CLI

## Verified

- The example front matter in `SKILL.md` passes `npx @google/design.md lint` (0 errors, 0 warnings).
- The embedded `audit.mjs` was run on a sample project: exact match, near-miss, unknown value, and baseline ratchet all behave as described.
- The full skill has not yet been run end to end on a real project.

## Standards and sources

- W3C Design Tokens Format Module 2025.10 (stable): https://www.designtokens.org/tr/2025.10/
- Google DESIGN.md (spec is `alpha`, so check for changes): https://github.com/google-labs-code/design.md
- WCAG 2.2: https://www.w3.org/TR/WCAG22/

Ideas adapted from:
- ds-specs: https://github.com/ejun-9/ds-specs (method by Hardik Pandya: https://hvpandya.com/llm-design-systems)
- token-system: https://github.com/MiikkasGIT/token-system
- material-3-skill: https://github.com/hamen/material-3-skill
- Hermes design-md skill: https://hermes-agent.nousresearch.com/docs/user-guide/skills/bundled/creative/creative-design-md
- Design system checklists: https://eleken.co/blog-posts/design-system-checklist, https://www.lullabot.com/articles/start-lean-scale-smart-practical-guide-scoping-design-systems

Only ideas were adapted; no text was copied from those projects.

## License

MIT
