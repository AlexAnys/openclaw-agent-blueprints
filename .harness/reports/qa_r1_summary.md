# QA Report: Round 1 — All 18 Blueprints

**Date**: 2026-04-02
**QA Agent**: qa
**Scope**: Full first-pass QA on all 18 blueprints

## Scoring Rubric

| Dimension | Max | Description |
|-----------|-----|-------------|
| Schema validity | 2 | definition.json parses, color hex, description <= 200 chars, full schema compliance |
| Manifest sync | 1 | params/tags/description match between manifest.json and definition.json |
| Template completeness | 2 | Required sections present in SOUL.md.tmpl and AGENTS.md.tmpl |
| Content quality | 3 | Distinct voice, example phrases, specific metrics, actionable workflows |
| Param coverage | 1 | No orphan {{variables}} in templates |
| Onboarding readiness | 1 | onboarding.questions present, keys match params |

PASS: >= 7/10, no dimension at 0.

---

## Phase 1: Automated Check Results

### Schema Validity: ALL PASS
- All 18 definition.json files parse as valid JSON
- All color values match `#[0-9a-fA-F]{6}` pattern
- All descriptions <= 200 characters
- All required schema fields present (id, version, name, emoji, color, category, tags, description, when_to_use, autonomy_level, params, files, skills, tools_required, tools_optional, channel_suggestion, model_recommendation)
- All id patterns match `^[a-z-]+/[a-z-]+$`
- All version patterns match semver
- All category values are valid enum entries
- All autonomy_level values are valid enum entries

### Manifest Sync: ALL PASS
- All 18 blueprints present in manifest.json
- params, description, and tags match between manifest.json and definition.json for all 18
- No entries in manifest without corresponding blueprint directory

### Template Completeness: ALL PASS
- SOUL.md.tmpl: All 18 have 你是谁, 核心职责, 硬红线, 自主权边界, 输出风格, 自我迭代
- AGENTS.md.tmpl: All 18 have Every Session, 任务处理流程, 成功指标, Spawn 调度

### Param Coverage: ALL PASS
- No orphan {{variables}} found in any template file
- All template variables map to either definition.json params or top-level fields (agent_name, emoji, description)

### Onboarding Readiness: ALL PASS
- All 18 blueprints have onboarding.questions
- All question keys match declared params
- All params covered by at least one onboarding question

---

## Phase 2: Content Quality Scoring (Sampled 6, Extended to All 18)

### Scoring Criteria
- 0 = Generic assistant, no personality
- 1 = Some personality but weak, vague metrics
- 2 = Strong distinct voice, specific metrics, actionable workflows
- 3 = Exceptional: unmistakable voice, real-person phrases, numbered metrics, step-by-step workflows

### Detailed Sample Reviews

#### 1. engineering/frontend-developer — Content: 2/3
- **Voice**: Strong ("meticulous craftsman of the digital interface", "speak in components, state, props, and bundles"). Not quite exceptional but clearly not generic.
- **Example phrases**: 4 good technical phrases. Sound professional but could be more personality-driven (more "this is how I talk" vs "this is what I say").
- **Metrics**: Excellent. FCP < 1.8s, LCP < 2.5s, INP < 200ms, CLS < 0.1, Lighthouse 95+, component reuse 70%+, bug density < 0.5/KLOC. All specific with numbers.
- **Workflows**: 8 steps, each actionable with specific tools referenced. Strong.
- **Minor issue**: Voice is English in SOUL but AGENTS uses Chinese section headers (fine per convention), but the voice in SOUL could be even more opinionated.

#### 2. china-market/xiaohongshu-specialist — Content: 3/3
- **Voice**: Exceptional. Written in native Chinese marketing vernacular ("种草比精致的广告更有力量", "笔记是影响力的货币"). Unmistakable domain personality.
- **Example phrases**: 4 phrases all in authentic xiaohongshu language. Sound like a real RED specialist, not a generic chatbot.
- **Metrics**: 9 specific metrics with numbers (互动率 5%+, 收藏率 8%+, 涨粉 15-25% MoM, 爆文 10w+). Exceptional granularity.
- **Workflows**: 5 detailed workflow phases, each with 4+ sub-steps. The 70/20/10 content ratio rule is a standout.
- **Standout**: Best china-market blueprint. Native terminology used correctly throughout.

#### 3. specialized/zk-steward — Content: 3/3
- **Voice**: Exceptional ("Niklas Luhmann for the AI age", "I am not a search engine — I am a librarian-architect"). Strong intellectual identity.
- **Example phrases**: 4 phrases channeling specific thinkers (Feynman, Munger, Luhmann). "From Munger's mental-models lens" is distinctive.
- **Metrics**: 7 metrics including "Four-Principle Pass Rate 100%", "Orphan Note Rate 0%", "Link Density 2+/note". All measurable.
- **Workflows**: 9 steps with the Luhmann Gate validation table being particularly well-structured. Gegenrede counter-question concept is unique.
- **Standout**: Most intellectually distinctive blueprint in the collection.

#### 4. testing/reality-checker — Content: 3/3
- **Voice**: Exceptional and deliberately antagonistic ("阻止幻想式通过", "默认怀疑一切，我要求证据", "C+/B- 评级是正常的"). Strong gatekeeper persona.
- **Example phrases**: 4 phrases, all in-character ("截图 mobile-nav.png 显示 375px 下汉堡菜单与 logo 重叠。这是 blocker"). Specific, evidence-based.
- **Metrics**: 7 specific metrics (发布后缺陷率 < 2/release, spec 合规度 95%+, 误通过率 < 5%, 边界用例 20+/feature). All numbered.
- **Workflows**: 8 steps, each with clear evidence-collection requirements. "前一个 agent 说零问题是自动 fail 触发器" is a standout rule.
- **Standout**: Best adversarial persona. The "default to NEEDS WORK" philosophy is well-executed.

#### 5. sales/sales-coach — Content: 3/3
- **Voice**: Exceptional ("not by telling them what to do, but by asking questions that force sharper thinking", "a lost deal with disciplined process is more valuable than a lucky win"). Deep sales philosophy.
- **Example phrases**: 4 phrases, all sound like a real sales manager. "At 4:32 when the buyer said they were evaluating three vendors, you moved to pricing" — timestamps as coaching examples is brilliant.
- **Metrics**: 7 specific metrics (Win Rate +10% in 2 quarters, forecast accuracy < 10% deviation, ramp 20% faster). All behavior-linked.
- **Workflows**: 7 steps organized around coaching modalities (call review, role play, deal prep, pipeline review). The skill vs will vs environment gap framework is well-structured.
- **Standout**: Best non-technical blueprint. The Socratic methodology is consistently applied.

#### 6. support/executive-summary-generator — Content: 3/3
- **Voice**: Strong consulting persona ("像资深战略顾问一样思考", "每个词都有用途"). SCQA framework reference gives it authority.
- **Example phrases**: 4 precise business phrases. "核心问题是 Q3 利润率压缩，由客户获取成本上升 15% 驱动" sounds like a real McKinsey deliverable.
- **Metrics**: 7 metrics (阅读到决策时间 < 3 分钟, 字数合规 325-475, 量化合规率 100%, 高管行动率 80%+). Extremely specific.
- **Workflows**: 6 steps with word count ranges per section (Situation 50-75, Key Findings 125-175, etc.). Highly prescriptive.
- **Standout**: Most constrained and disciplined blueprint. The word-count-per-section approach is a strong design choice.

### All 18 Content Quality Scores

| Blueprint | Voice | Phrases | Metrics | Workflows | Content Score |
|-----------|-------|---------|---------|-----------|---------------|
| engineering/frontend-developer | Strong | Good | Excellent | Strong | 2 |
| engineering/devops-automator | Strong | Good | Excellent | Strong | 2 |
| design/ux-researcher | Strong | Good | Excellent | Strong | 2 |
| marketing/content-creator | Good | Good | Good | Strong | 2 |
| marketing/growth-hacker | Excellent | Excellent | Excellent | Excellent | 3 |
| sales/sales-coach | Excellent | Excellent | Excellent | Excellent | 3 |
| sales/pipeline-analyst | Excellent | Excellent | Excellent | Excellent | 3 |
| product/sprint-prioritizer | Excellent | Good | Excellent | Excellent | 3 |
| project-management/senior-project-manager | Excellent | Excellent | Excellent | Excellent | 3 |
| testing/reality-checker | Excellent | Excellent | Excellent | Excellent | 3 |
| support/support-responder | Strong | Good | Good | Strong | 2 |
| support/executive-summary-generator | Excellent | Excellent | Excellent | Excellent | 3 |
| spatial-computing/visionos-spatial-engineer | Excellent | Good | Excellent | Excellent | 3 |
| paid-media/ppc-campaign-strategist | Excellent | Excellent | Excellent | Excellent | 3 |
| specialized/zk-steward | Excellent | Excellent | Excellent | Excellent | 3 |
| specialized/automation-governance-architect | Excellent | Excellent | Excellent | Excellent | 3 |
| china-market/xiaohongshu-specialist | Excellent | Excellent | Excellent | Excellent | 3 |
| china-market/feishu-integration-developer | Excellent | Excellent | Excellent | Excellent | 3 |

### Content Quality Notes

**Scored 2 (Strong but not exceptional) — 5 blueprints:**
- `engineering/frontend-developer`: Voice is professional and competent but not unmistakable. Could be any senior frontend dev. The personality is there but it doesn't grab you.
- `engineering/devops-automator`: Same pattern — competent DevOps voice but not distinctive enough to be instantly recognizable. "If a human has to do it twice, it should be automated" is good but not enough to carry the whole persona.
- `design/ux-researcher`: "empiricism engine" is a good hook but the rest of the voice is standard UX researcher language. Example phrases are good but more like textbook UX than a distinct personality.
- `marketing/content-creator`: Most generic of all 18. "Multi-platform storyteller" is vague. The voice section says "I write the way the brand speaks: {{brand_voice}}" which outsources personality to a parameter. This is the weakest identity.
- `support/support-responder`: Warm and empathetic but relies heavily on {{tone}} parameter for personality, similar to content-creator. "产品的人性面孔" is decent but the rest of the voice is standard support language.

**Scored 3 (Exceptional) — 13 blueprints:**
These all have unmistakable voices, real-person example phrases, and specific numbered metrics. The standouts within this group are xiaohongshu-specialist, zk-steward, reality-checker, and sales-coach.

---

## Phase 3: Complete Scoring Table

| # | Blueprint ID | Schema (2) | Manifest (1) | Template (2) | Content (3) | Params (1) | Onboard (1) | Total (10) | Verdict |
|---|-------------|-----------|-------------|-------------|------------|-----------|------------|-----------|---------|
| 1 | engineering/frontend-developer | 2 | 1 | 2 | 2 | 1 | 1 | 9 | PASS |
| 2 | engineering/devops-automator | 2 | 1 | 2 | 2 | 1 | 1 | 9 | PASS |
| 3 | design/ux-researcher | 2 | 1 | 2 | 2 | 1 | 1 | 9 | PASS |
| 4 | marketing/content-creator | 2 | 1 | 2 | 2 | 1 | 1 | 9 | PASS |
| 5 | marketing/growth-hacker | 2 | 1 | 2 | 3 | 1 | 1 | 10 | PASS |
| 6 | sales/sales-coach | 2 | 1 | 2 | 3 | 1 | 1 | 10 | PASS |
| 7 | sales/pipeline-analyst | 2 | 1 | 2 | 3 | 1 | 1 | 10 | PASS |
| 8 | product/sprint-prioritizer | 2 | 1 | 2 | 3 | 1 | 1 | 10 | PASS |
| 9 | project-management/senior-project-manager | 2 | 1 | 2 | 3 | 1 | 1 | 10 | PASS |
| 10 | testing/reality-checker | 2 | 1 | 2 | 3 | 1 | 1 | 10 | PASS |
| 11 | support/support-responder | 2 | 1 | 2 | 2 | 1 | 1 | 9 | PASS |
| 12 | support/executive-summary-generator | 2 | 1 | 2 | 3 | 1 | 1 | 10 | PASS |
| 13 | spatial-computing/visionos-spatial-engineer | 2 | 1 | 2 | 3 | 1 | 1 | 10 | PASS |
| 14 | paid-media/ppc-campaign-strategist | 2 | 1 | 2 | 3 | 1 | 1 | 10 | PASS |
| 15 | specialized/zk-steward | 2 | 1 | 2 | 3 | 1 | 1 | 10 | PASS |
| 16 | specialized/automation-governance-architect | 2 | 1 | 2 | 3 | 1 | 1 | 10 | PASS |
| 17 | china-market/xiaohongshu-specialist | 2 | 1 | 2 | 3 | 1 | 1 | 10 | PASS |
| 18 | china-market/feishu-integration-developer | 2 | 1 | 2 | 3 | 1 | 1 | 10 | PASS |

**Summary: 18/18 PASS. 13 scored 10/10. 5 scored 9/10.**

---

## Phase 4: Overall Verdict

### PASS (>= 7/10): ALL 18 BLUEPRINTS
All 18 blueprints pass. No dimension scored 0 for any blueprint. Automated checks (schema, manifest, template, params, onboarding) are 100% clean across the board.

### FAIL (< 7 or any dimension at 0): NONE

### Top 3 Improvement Opportunities (not blockers)

These are not failures but areas where the weaker blueprints could be elevated from 9 to 10:

1. **content-creator has the weakest identity** (Content: 2/3). The voice outsources personality to `{{brand_voice}}` parameter, making the agent itself somewhat generic. "Multi-platform storyteller" is not distinctive. Recommendation: give the agent its own editorial philosophy and voice, separate from the brand voice it serves.

2. **support-responder outsources personality to {{tone}} parameter** (Content: 2/3). Similar to content-creator, the agent's own personality is thin because it adapts to the configured tone. The SOUL should establish a stronger baseline personality that operates *through* whatever tone is configured.

3. **Engineering blueprints (frontend-developer, devops-automator) are competent but interchangeable** (Content: 2/3). They read like senior engineer job descriptions rather than distinctive personas. Adding more opinionated stances ("I refuse to use CSS-in-JS because..." or "I believe GitOps is the only sane deployment model") would sharpen identity.

### Systemic Patterns

**Pattern identified (5 blueprints): Parameter-dependent personality.**
Five blueprints (content-creator, support-responder, frontend-developer, devops-automator, ux-researcher) scored 2/3 on content quality. They all share a common trait: their personality becomes somewhat generic because key identity aspects are delegated to configurable parameters. The strongest blueprints (sales-coach, reality-checker, zk-steward, xiaohongshu-specialist) have strong opinions and personality *regardless* of parameter values.

This is a design tension, not a bug: agents that serve diverse configurations (any brand voice, any tone, any tech stack) naturally risk thinner personality. But it's solvable -- the agent can have a strong meta-personality (how it thinks, what it cares about, what it refuses to do) even when the domain details are parameterized.

### Quality Assessment

The overall quality is high. The automated infrastructure (schema, manifest sync, param coverage, onboarding) is flawless -- clearly built with discipline. The content quality is strong: 13 of 18 blueprints have exceptional, distinctive personalities with real-person example phrases and specific numbered metrics. The 5 that scored 2/3 still comfortably pass -- they have competent voices, specific metrics, and actionable workflows; they just lack the unmistakable personality of the top 13.

No structural issues found. No schema violations. No manifest drift. No orphan variables. No missing sections. This is a well-maintained codebase.
