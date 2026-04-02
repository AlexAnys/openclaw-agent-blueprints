# openclaw-agent-blueprints

Curated blueprint library for OpenClaw agents. 18 blueprints across 12 domains, adapted from agency-agents (~120 templates) with OpenClaw-specific conventions.

## Harness

This repo uses a Plan→Build→QA harness. All non-trivial changes go through:

1. **@planner** — writes specs with acceptance criteria to `.harness/contracts/`
2. **@builder** — implements changes following conventions in `.claude/agents/builder.md`
3. **@qa** — verifies using automated checks + manual content review, scores 0-10

Progress tracked in `.harness/progress.tsv`. QA reports in `.harness/reports/`.

### Quick routing:
- Typo/config (< 3 lines): edit directly, QA verifies on stop
- Bug fix (schema violation, manifest drift): @builder fixes, @qa re-checks
- New blueprint: @planner specs it, @builder implements, @qa scores
- Content improvement: @builder rewrites, @qa compares before/after

## Architecture

```
blueprints/{domain}/{role}/
├── definition.json          # Machine-readable metadata + onboarding questions
├── SOUL.md.tmpl             # 人格模板 (80-120 lines max)
├── AGENTS.md.tmpl           # 工作流模板
├── IDENTITY.md.tmpl         # name/emoji/vibe
├── TOOLS.md.tmpl            # 工具指导
└── bindings/openclaw/README.md  # Points to ops-interface/INSTRUCTIONS.md
```

## Key Conventions

- SOUL.md.tmpl sections: 你是谁 / 核心职责 / 硬红线 / 自主权边界 / 输出风格 / 自我迭代
- AGENTS.md.tmpl sections: Every Session / 任务处理流程 / 交付物标准 / 成功指标 / Spawn 调度
- definition.json: must validate against schema/blueprint.schema.json
- manifest.json: must stay in sync with all 18 definition.json files
- No hardcoded workspace paths — OpenClaw workspace is `~/.openclaw/workspace-{agentId}/`
- No "activate XX mode" — OpenClaw uses binding auto-routing
- No Claude attribution in any file
- China market agents use native Chinese terminology

## Quality Thresholds

Per-blueprint score (0-10): Schema validity (2) + Manifest sync (1) + Template completeness (2) + Content quality (3) + Param coverage (1) + Onboarding readiness (1)

PASS: >= 7/10, no dimension at 0.
