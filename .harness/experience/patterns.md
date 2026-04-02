# Experience Patterns

Accumulated from QA cycles. Updated periodically.

## Known Systemic Issues

### P1: Parameter-Dependent Personality (5 blueprints, R1)

**Affected**: content-creator, support-responder, frontend-developer, devops-automator, ux-researcher

**Pattern**: These 5 blueprints scored 2/3 on content quality because their personality is partially outsourced to configurable parameters. content-creator delegates voice to `{{brand_voice}}`, support-responder delegates to `{{tone}}`, and the engineering blueprints become generic when their tech stack params are abstracted out.

**Contrast**: The strongest blueprints (sales-coach, reality-checker, zk-steward, xiaohongshu-specialist) have strong meta-personality — how they think, what they refuse to do, their philosophical stance — that is independent of parameter values.

**Impact**: Not a blocker (all 5 still score 9/10 total), but a clear pattern separating "good" from "exceptional".

**Recommended fix**: Add 2-3 more opinionated stances to the 你是谁 section of each affected blueprint that define how the agent thinks and what it values, independent of the parameterized domain. For example:
- content-creator: "I believe the best content starts with a question the audience is already asking"
- frontend-developer: "I believe every CSS hack is a design system failure waiting to be fixed"
- devops-automator: "I believe observability is not optional — a system you can't monitor is a system you don't understand"

**Severity**: Low. Cosmetic improvement, not a functional gap.

## Effective Patterns

### E1: Evidence-Driven Persona (R1)
The most distinctive blueprints (reality-checker, sales-coach, pipeline-analyst) establish their personality through a philosophical stance toward evidence and truth. "I default to NEEDS WORK" and "I coach the behavior, not the outcome" are identity-defining statements that make the agent unmistakable. This pattern is worth replicating.

### E2: Named Frameworks as Anchors (R1)
Blueprints that reference named frameworks (Luhmann's Zettelkasten, McKinsey SCQA, MEDDPICC, Nielsen's 10 heuristics) tend to have stronger identities. The framework gives the agent a methodology-based personality rather than just a domain-based one.

### E3: Platform-Native Language (R1)
The xiaohongshu-specialist and feishu-integration-developer demonstrate that writing in the platform's native language and terminology (种草, 拔草, tenant_access_token vs user_access_token) produces more authentic, distinctive voices than generic translations.
