# Blueprint Selection and Customization Methodology

This document describes the repeatable framework used to select, customize, and onboard agent blueprints. Whether you're picking your first blueprint or designing a multi-agent team, follow this methodology to avoid common pitfalls.

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

**Resolution process:**

1. Open `definition.json` and read the `parameters` section.
2. For each parameter, note its `description`, `type`, and `default` (if any).
3. Prepare your values. Common parameters include:
   - `{{tech_stack}}` — Your technology stack (e.g., "React, TypeScript, Tailwind")
   - `{{team_context}}` — How your team operates (e.g., "5-person startup, async-first")
   - `{{output_language}}` — Preferred response language
   - `{{domain_constraints}}` — Industry or compliance requirements
4. Replace all `{{variable}}` occurrences in the binding files with your values.

**Tip:** Don't leave any unresolved `{{variables}}` — the agent will either error or hallucinate values.

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

## Part 3: Onboarding Workflow

### Step 1: Get the Blueprint Files

```bash
# Option A: Clone the full repo
git clone https://github.com/AlexAnys/openclaw-agent-blueprints.git

# Option B: Fetch a single blueprint (raw files)
curl -O https://raw.githubusercontent.com/.../definition.json
```

### Step 2: Materialize the Blueprint

**Automated (recommended):**

```bash
# Using the ops-agent or materializer CLI (when available)
openclaw-blueprints materialize \
  --blueprint engineering/frontend-developer \
  --params tech_stack="React + TypeScript" \
  --params team_context="Startup, 3 engineers" \
  --output ~/.openclaw/workspace/agents/frontend-developer/
```

**Manual:**

1. Copy the `bindings/openclaw/` directory to your agent workspace.
2. Open each `.md` file and replace `{{variables}}` with your values.
3. Review every file to ensure no placeholders remain.

### Step 3: Place Workspace Files

The materialized files go into OpenClaw's workspace directory:

```
~/.openclaw/workspace/agents/{agent-id}/
├── SOUL.md
├── AGENTS.md
└── TOOLS.md
```

The `{agent-id}` should be a kebab-case identifier matching the blueprint role (e.g., `frontend-developer`, `ux-researcher`).

### Step 4: Register in openclaw.json

Add the agent to your OpenClaw configuration:

```json
{
  "agents": {
    "list": [
      {
        "id": "frontend-developer",
        "name": "Frontend Developer",
        "description": "React/TypeScript frontend development assistant"
      }
    ]
  }
}
```

Configure any bindings, model preferences, or tool permissions as needed.

### Step 5: Test with a Real Task

Don't test with toy examples. Give the agent a real task from your backlog within the first 5 minutes:

```bash
openclaw chat --agent frontend-developer
> "Refactor the dashboard component to use the new design tokens from our design system."
```

Evaluate the response against these criteria:
- Does it understand your tech stack context?
- Does the tone match your expectations?
- Are the deliverables in a usable format?
- Does it stay within its defined boundaries?

If anything is off, go back to Part 2 and adjust the relevant file.

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
