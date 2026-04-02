# Blueprint Selection and Customization Methodology

This document describes the repeatable framework used to select, customize, and onboard agent blueprints. Whether you're picking your first blueprint or designing a multi-agent team, follow this methodology to avoid common pitfalls.

> **操作指令**：如果你是 onboarding Agent，请直接阅读 `ops-interface/INSTRUCTIONS.md`。本文档面向人类读者，解释设计理念和决策依据。

---

## Part 1: Blueprint Selection Framework

### Step 1: Role Identification

Start by identifying which part of your workflow needs AI assistance. Ask:

- **What task consumes the most time?** Look for repetitive, structured work that follows patterns.
- **Where are the bottlenecks?** Identify handoff points, review cycles, or knowledge gaps.
- **What requires expertise you don't have in-house?** Agents excel at applying specialized knowledge consistently.

Write down the role in plain language: "I need an agent that can _____."

### Step 2: Domain Mapping

Match your identified need to one of the 12 domains in this library:

| Domain | Covers |
|--------|--------|
| Engineering | Code generation, review, CI/CD, infrastructure |
| Design | User research, prototyping, design systems |
| Marketing | Content creation, SEO, social media, campaigns |
| Sales | Coaching, pipeline analysis, outreach |
| Product | Prioritization, roadmapping, stakeholder alignment |
| Project Management | Planning, tracking, risk management, reporting |
| Testing | QA, test generation, edge case discovery |
| Support | Ticket response, escalation, knowledge base |
| Spatial Computing | visionOS, AR/VR, 3D interfaces |
| Paid Media | PPC, ad copy, budget optimization |
| Specialized | Niche domains (ZK proofs, governance, compliance) |
| China Market | Platform-specific (Xiaohongshu, Feishu, WeChat) |

If your need spans multiple domains, you likely need a **team composition** (see Part 4).

### Step 3: Template Matching

Within your target domain, evaluate blueprints using these signals from `definition.json`:

- **`when_to_use`**: Does the described scenario match yours?
- **`tags`**: Do the tags overlap with your tech stack, industry, or workflow?
- **`parameters`**: Can you fill in all required parameters with your context?
- **`complexity`**: Is the blueprint's expected scope aligned with your needs?

Pick the **closest match**, not a perfect match. You'll customize in Part 2.

### Step 4: Complexity Assessment

Decide whether you need a single agent or a team:

| Signal | Single Agent | Team Composition |
|--------|-------------|-----------------|
| Task scope | One well-defined function | Multiple interdependent functions |
| Output consumers | You or your team directly | Other agents in a pipeline |
| Context required | Domain-specific | Cross-domain |
| Iteration cycle | Human-in-the-loop | Agent-to-agent handoff |

If single agent, proceed to Part 2. If team, see Part 4 first to understand composition, then customize each agent individually.

---

## Part 2: Customization Guide

### Parameter Resolution

Every blueprint defines parameters in `definition.json` as `{{variable}}` placeholders. These appear in the binding files (SOUL.md, AGENTS.md, TOOLS.md) and must be resolved before the agent is usable.

**Key principles:**

1. Read the `parameters` section in `definition.json` — note each parameter's `description`, `type`, and `default`.
2. Common parameters include:
   - `{{tech_stack}}` — Your technology stack (e.g., "React, TypeScript, Tailwind")
   - `{{team_context}}` — How your team operates (e.g., "5-person startup, async-first")
   - `{{output_language}}` — Preferred response language
   - `{{domain_constraints}}` — Industry or compliance requirements
3. **No unresolved `{{variables}}`** — the agent will either error or hallucinate values.

### SOUL.md Tuning

SOUL.md defines the agent's personality, communication style, and behavioral boundaries. Customize:

- **Tone**: Formal vs. casual, verbose vs. terse. Match your team culture.
- **Boundaries**: What the agent should refuse to do. Add domain-specific limits.
- **Identity**: How the agent introduces itself and frames its expertise.
- **Language**: If your team operates in a specific language, set it here.

**What to preserve:** The core competency description and ethical guardrails. These ensure the agent stays effective and safe.

### AGENTS.md Tuning

AGENTS.md defines the agent's operational workflows, expected deliverables, and success metrics. Customize:

- **Workflows**: Adapt the step-by-step processes to match your actual workflow. Remove steps you don't need; add steps specific to your tooling.
- **Deliverables**: Adjust output formats to match what your team consumes (Markdown, JSON, Jira tickets, etc.).
- **Metrics**: Replace generic KPIs with metrics your team actually tracks.
- **Examples**: Add real examples from your domain to improve output quality.

### TOOLS.md Configuration

TOOLS.md specifies which skills and external tools the agent can access. Customize:

- **Enable/disable tools**: Only give the agent access to tools it actually needs.
- **API credentials**: Reference environment variables or secret stores — never hardcode.
- **Rate limits**: Set appropriate limits for external API calls.
- **Fallback behavior**: Define what the agent should do when a tool is unavailable.

---

## Part 3: OpenClaw 适配原则

当从通用 Agent 模板（如 agency-agents）适配为 OpenClaw blueprint 时，需要注意以下原则。

### 必须添加的

- **自主权边界**：OpenClaw 多 Agent 环境需要明确每个 Agent 能做什么、不能做什么。在 SOUL.md 中用"允许/禁止"列表定义操作权限级别，避免 Agent 越权。
- **Spawn 调度**：OpenClaw 支持 subagent 并发，需要在 AGENTS.md 中定义何时 spawn、可以 spawn 谁（如 research、ko 等通用 subagent），以及什么任务自己处理。
- **Session 启动流程**：每次会话需要按固定顺序加载 workspace 文件（SOUL → USER → MEMORY），在 AGENTS.md 的 "Every Session" 部分定义。
- **自我迭代机制**：Agent 修改自身规则文件（SOUL/AGENTS/MEMORY）时必须写 Self-Update，确保变更可追溯。

### 必须去掉的

- **激活指令**：不要写 "activate XX mode" — OpenClaw 用 binding 自动路由，不需要手动激活。
- **过长的代码示例**：SOUL.md 控制在 80-120 行，详细示例和参考资料放 `skills/`，不要塞进核心文件。
- **硬编码路径**：workspace 路径因用户而异，不要在模板中硬编码。多 Agent 模式下，每个 Agent 的 workspace 默认在 `~/.openclaw/workspace-{agentId}/`，具体路径可在 `openclaw.json` 的 `agents.list[].workspace` 中自定义。

### 文件层次

Blueprint 产出的文件按来源和生命周期分为三层：

| 层次 | 文件 | 来源 | 说明 |
|------|------|------|------|
| Layer 1: Blueprint 预定义 | SOUL.md, AGENTS.md, IDENTITY.md, TOOLS.md | 从 blueprint 模板生成 | 定义 Agent 是谁、怎么工作 |
| Layer 2: Onboarding 时生成 | USER.md, HEARTBEAT.md, openclaw.json 配置 | Onboarding Agent 动态生成 | 适配用户环境 |
| Layer 3: 运行时自然生长 | MEMORY.md 内容, memory/ 日志, skills/ | Agent 自己维护 | 持续积累 |

**设计原则**：Blueprint 仓库只负责 Layer 1 的模板内容。Layer 2 由 onboarding Agent 在部署时根据用户环境动态生成（详见 `ops-interface/INSTRUCTIONS.md`）。Layer 3 由 Agent 在运行过程中自然积累，无需预定义。

---

## Part 4: Team Composition

### When to Use a Team

Use a team composition when:

- A task requires **handoffs** between different expertise areas (e.g., design -> development -> QA).
- You need **parallel processing** where multiple agents work on different aspects simultaneously.
- The output of one agent is the **input** of another (pipeline pattern).
- You want **checks and balances** — e.g., a reality-checker agent reviewing a content-creator's output.

### How Teams Coordinate

Teams in this repo use three coordination mechanisms:

1. **Shared files** (`teams/{team-name}/shared/`): Configuration, context, and protocols that all agents in the team can reference.
2. **Handoff protocols**: Defined in each agent's AGENTS.md — what format to produce output in so the next agent can consume it.
3. **Orchestration**: The team's `composition.json` defines execution order, parallel groups, and conditional routing.

### Pre-Built Teams

| Team | Agents | Coordination Pattern |
|------|--------|---------------------|
| **China Content Engine** | Xiaohongshu Specialist, Content Creator | Pipeline: research -> localize -> publish |
| **Dev Squad** | Frontend Developer, DevOps Automator, Reality Checker | Parallel dev + serial QA gate |
| **Startup MVP** | Sprint Prioritizer, Frontend Developer, Growth Hacker | Cycle: prioritize -> build -> measure -> repeat |

### Building Custom Teams

1. Select 2-5 agents that cover your workflow end-to-end.
2. Define handoff formats in each agent's AGENTS.md.
3. Create a `composition.json` in `teams/{your-team}/` specifying execution order.
4. Add shared context files in `teams/{your-team}/shared/`.
5. Test the full pipeline with a real scenario before deploying.

---

## Appendix: Blueprint Quality Criteria

Every blueprint in this repo meets these minimum quality standards:

| Criterion | Requirement |
|-----------|------------|
| Completeness | All three binding files (SOUL.md, AGENTS.md, TOOLS.md) present |
| Parameters | All `{{variables}}` documented in definition.json with descriptions |
| Testability | Can be onboarded and tested within 5 minutes |
| Specificity | Clearly scoped to a defined role — not a generic "assistant" |
| Boundaries | Explicit about what the agent will and won't do |
| Reusability | Parameterized enough to work across different teams and contexts |
