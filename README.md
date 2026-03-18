# OpenClaw Agent Blueprints

A curated, methodology-driven blueprint library for [OpenClaw](https://github.com/nicepkg/openclaw) — the open-source AI agent orchestration platform.

## The Problem

The OpenClaw ecosystem has 120+ agent templates across dozens of community repos. That's great for breadth, but terrible for getting started:

1. **Which agent fits my workflow?** Template names alone don't tell you enough.
2. **How do I customize it?** Every team has different tools, tone, and constraints.
3. **How do agents work together?** Single agents hit a ceiling; teams multiply value.

## Our Solution

**18 curated blueprints across 12 domains**, selected through a repeatable methodology and adapted for OpenClaw's multi-agent architecture.

| Domain | Blueprints |
|--------|-----------|
| Engineering | Frontend Developer, DevOps Automator |
| Design | UX Researcher |
| Marketing | Content Creator, Growth Hacker |
| Sales | Sales Coach, Pipeline Analyst |
| Product | Sprint Prioritizer |
| Project Management | Senior Project Manager |
| Testing | Reality Checker |
| Support | Support Responder, Executive Summary Generator |
| Spatial Computing | visionOS Spatial Engineer |
| Paid Media | PPC Campaign Strategist |
| Specialized | ZK Steward, Automation Governance Architect |
| China Market | Xiaohongshu Specialist, Feishu Integration Developer |

## For Onboarding Agents

If you are an OpenClaw onboarding Agent (e.g., Ops Agent), start here:

**[`ops-interface/INSTRUCTIONS.md`](./ops-interface/INSTRUCTIONS.md)** — Complete operational guide for environment detection, blueprint selection, materialization, registration, and validation.

## For Humans

If you're a human exploring this repo:

**[`METHODOLOGY.md`](./METHODOLOGY.md)** — Design rationale, selection framework, customization principles, and OpenClaw adaptation guidelines.

## Architecture

Each blueprint uses a dual-layer design:

```
blueprints/{domain}/{role}/
├── definition.json          # Metadata, params, onboarding questions, tools_deny
├── SOUL.md.tmpl             # 人格、职责、自主权边界、输出风格
├── AGENTS.md.tmpl           # Every Session 流程、任务处理、Spawn 调度
├── IDENTITY.md.tmpl         # name / emoji / vibe
├── TOOLS.md.tmpl            # 工具指导（实际可用性由 openclaw.json 控制）
└── bindings/openclaw/
    └── README.md            # Materialization instructions
```

**`definition.json`** is the machine-readable metadata layer. It includes:
- Blueprint parameters with typed defaults
- `onboarding.questions` — what to ask the user during setup (with `auto_detect` hints)
- `tools_deny` — explicit tool restrictions for safety boundaries
- `when_to_use` / `tags` — for intent matching and discovery

**`*.md.tmpl`** files are OpenClaw workspace templates. They follow OpenClaw conventions:
- SOUL.md: 80-120 lines max, includes 自主权边界 (autonomy boundaries)
- AGENTS.md: includes Every Session flow and Spawn 调度
- All use `{{variable}}` placeholders resolved during materialization

**File hierarchy:**

| Layer | Files | Source | Purpose |
|-------|-------|--------|---------|
| Layer 1: Blueprint | SOUL.md, AGENTS.md, IDENTITY.md, TOOLS.md | This repo's templates | Who the agent is, how it works |
| Layer 2: Onboarding | USER.md, HEARTBEAT.md, openclaw.json config | Generated at deploy time | Adapts to user environment |
| Layer 3: Runtime | MEMORY.md, memory/, skills/ | Agent maintains itself | Accumulates over time |

## Quick Start

```bash
# 1. Clone
git clone https://github.com/AlexAnys/openclaw-agent-blueprints.git
cd openclaw-agent-blueprints

# 2. Pick a blueprint
cat blueprints/engineering/frontend-developer/definition.json

# 3. Copy templates to your workspace
cp blueprints/engineering/frontend-developer/*.tmpl \
  ~/.openclaw/workspace-frontend-developer/

# 4. Rename .tmpl → .md and replace {{variables}}
# e.g., {{tech_stack}} → "React + TypeScript + Tailwind"

# 5. Register in openclaw.json (agents.list + bindings)

# 6. Restart Gateway and test
```

For automated onboarding, point your Ops Agent at `ops-interface/INSTRUCTIONS.md`.

## Team Compositions (Planned)

Pre-built multi-agent team templates are planned in `teams/`:

| Team | Agents | Coordination |
|------|--------|-------------|
| China Content Engine | Xiaohongshu + Content Creator + Growth Hacker | Collaborative |
| Dev Squad | Frontend + DevOps + Reality Checker | Sequential pipeline |
| Startup MVP | Sprint Prioritizer + Frontend + Growth Hacker | Hierarchical |

## Roadmap

- [ ] Populate team composition templates with shared protocols
- [ ] Materializer CLI for automated parameter resolution
- [ ] Community-contributed blueprints with quality tiers
- [ ] Additional platform bindings (Dify, Coze, custom runtimes)

## Contributing

We welcome contributions — new blueprints, improved templates, team compositions, and methodology refinements. Please follow the structure described in `METHODOLOGY.md`.

## License

MIT
