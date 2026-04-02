# openclaw-agent-blueprints Harness Spec

## Classification: Operations (Ongoing)

This is a curated blueprint library that continuously evolves. Changes include:
- Adding new blueprints
- Improving existing templates (SOUL/AGENTS content)
- Schema evolution
- manifest.json sync
- Documentation updates

## Progress Metric

Blueprint Quality Score (per blueprint, 0-10):

| Dimension | Weight | Criteria |
|-----------|--------|----------|
| Schema validity | 2 | definition.json passes blueprint.schema.json |
| Manifest sync | 1 | manifest.json params/tags/description match definition.json |
| Template completeness | 2 | All 4 .md.tmpl files present with correct OpenClaw structure |
| Content quality | 3 | Distinct personality, concrete metrics, actionable workflows |
| Param coverage | 1 | All {{variables}} in templates declared in definition.json params |
| Onboarding readiness | 1 | onboarding.questions present and useful |

**PASS threshold: 7/10 per blueprint, no single dimension at 0.**

## Units of Work

Each blueprint is one unit. "Done" for a blueprint means:
1. definition.json valid against schema
2. SOUL.md.tmpl follows OpenClaw structure (你是谁/核心职责/硬红线/自主权边界/输出风格/自我迭代)
3. AGENTS.md.tmpl follows OpenClaw structure (Every Session/任务处理流程/交付物标准/成功指标/Spawn 调度)
4. IDENTITY.md.tmpl has name/emoji/vibe
5. TOOLS.md.tmpl has 必需工具/可选工具 + policy note
6. manifest.json entry matches definition.json
7. No unresolved {{variable}} that isn't in params
8. onboarding.questions keys match params keys

## Domain-Specific Failure Modes

1. **Personality collapse**: Multiple blueprints sound the same (generic "helpful assistant")
2. **Metric vagueness**: Success metrics without numbers ("improve performance" vs "LCP < 2.5s")
3. **Schema drift**: definition.json fields don't match schema (color not hex, description > 200 chars)
4. **Manifest stale**: manifest.json and definition.json diverge after edits
5. **Template orphan**: {{variable}} used in template but not in params
6. **OpenClaw convention miss**: Missing Every Session, Spawn 调度, or 自主权边界
7. **Hardcoded paths**: ~/.openclaw/workspace/agents/ instead of dynamic paths
8. **Tools confusion**: Claude Code tool names vs OpenClaw tool names
