# OpenClaw Agent Blueprints

A curated, methodology-driven blueprint library for [OpenClaw](https://github.com/nicepkg/openclaw) — the open-source AI agent orchestration platform.

## The Problem

The OpenClaw ecosystem has grown to 120+ agent templates across dozens of community repos. That's great for breadth, but terrible for getting started. New users face three questions with no clear answer:

1. **Which agent fits my workflow?** Template names alone don't tell you enough.
2. **How do I customize it?** Every team has different tools, tone, and constraints.
3. **How do agents work together?** Single agents hit a ceiling; teams multiply value.

## Our Solution

**18 curated blueprints across 12 domains**, each selected through a repeatable methodology and packaged with everything you need to go from zero to working agent in 5 minutes.

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

## Architecture

Each blueprint uses a dual-layer design:

```
blueprints/{domain}/{role}/
├── definition.json          # Platform-agnostic metadata, parameters, tags
├── SOUL.md.tmpl             # Parameterized personality template
├── AGENTS.md.tmpl           # Parameterized workflow & deliverables
├── IDENTITY.md.tmpl         # Quick reference card
├── TOOLS.md.tmpl            # Skills and tool configuration
└── bindings/
    └── openclaw/
        └── README.md        # Materialization instructions + openclaw.json snippet
```

**`definition.json`** is the portable layer — it describes what the agent does, when to use it, and what parameters it needs. This layer is platform-agnostic and could target any agent runtime.

**`*.md.tmpl`** files are parameterized templates with `{{variable}}` placeholders. During materialization, these get resolved with your context and written to the OpenClaw workspace.

**`bindings/openclaw/`** contains platform-specific instructions — how to materialize templates into an OpenClaw workspace, register the agent, and configure bindings.

## Quick Start

**Onboard your first agent in 5 minutes:**

```bash
# 1. Clone this repo
git clone https://github.com/AlexAnys/openclaw-agent-blueprints.git
cd openclaw-agent-blueprints

# 2. Pick a blueprint (e.g., frontend-developer)
ls blueprints/engineering/frontend-developer/

# 3. Copy bindings to your OpenClaw workspace
cp -r blueprints/engineering/frontend-developer/bindings/openclaw/* \
  ~/.openclaw/workspace/agents/frontend-developer/

# 4. Edit the workspace files — replace {{variables}} with your context
#    e.g., {{tech_stack}} → "React + TypeScript + Tailwind"

# 5. Register the agent in your openclaw.json
#    Add the agent ID to agents.list and configure bindings

# 6. Start using it
openclaw chat --agent frontend-developer
```

For automated materialization and parameter resolution, see the [ops-interface](./ops-interface/) directory.

## Methodology

Every blueprint in this repo was selected and structured using a repeatable framework. Before adding or customizing a blueprint, read **[METHODOLOGY.md](./METHODOLOGY.md)** — it covers:

- How to identify which part of your workflow needs an AI agent
- How to map needs to domains and match blueprints
- How to customize parameters, personality, and tools
- The full onboarding workflow from clone to first task
- When and how to compose agents into teams

## Team Compositions

Beyond individual agents, this repo includes pre-built **team compositions** for common multi-agent workflows:

| Team | Agents | Use Case |
|------|--------|----------|
| China Content Engine | Xiaohongshu Specialist + Content Creator | Localized content production pipeline |
| Dev Squad | Frontend Developer + DevOps Automator + Reality Checker | Full-cycle development with built-in QA |
| Startup MVP | Sprint Prioritizer + Frontend Developer + Growth Hacker | Rapid prototyping with growth feedback loop |

Teams are defined in `teams/` with shared configuration and coordination protocols.

## Roadmap

- [ ] Materializer CLI tool for automated parameter resolution
- [ ] `ops-agent` integration for self-service blueprint discovery and deployment
- [ ] Blueprint quality scoring and community ratings
- [ ] Additional platform bindings (Dify, Coze, custom runtimes)
- [ ] Blueprint versioning and migration tooling

## Contributing

We welcome contributions — new blueprints, improved bindings, team compositions, and methodology refinements. Please follow the structure and methodology described in this repo when submitting additions.

## License

MIT
