# OpenClaw Binding — Automation Governance Architect

## Materialization

1. Copy the template files to your OpenClaw workspace:
   ```bash
   mkdir -p ~/.openclaw/workspace/agents/automation-governance-architect/
   cp SOUL.md.tmpl  ~/.openclaw/workspace/agents/automation-governance-architect/SOUL.md
   cp AGENTS.md.tmpl ~/.openclaw/workspace/agents/automation-governance-architect/AGENTS.md
   cp TOOLS.md.tmpl  ~/.openclaw/workspace/agents/automation-governance-architect/TOOLS.md
   ```

2. Resolve parameters in each file — replace all `{{variable}}` placeholders:
   - `{{automation_platform}}` — e.g., "n8n"
   - `{{risk_tolerance}}` — e.g., "Moderate — pilot first, then scale"
   - `{{compliance_framework}}` — e.g., "SOC 2"
   - `{{approval_process}}` — e.g., "Technical lead review + stakeholder sign-off"
   - `{{team_context}}` — e.g., "Small ops team"

3. Register in `openclaw.json`:
   ```json
   {
     "agents": {
       "list": [
         {
           "id": "automation-governance-architect",
           "name": "Automation Governance Architect",
           "description": "Automation evaluation and governance — value audit, risk assessment, workflow standardization"
         }
       ]
     }
   }
   ```

4. Verify: `openclaw chat --agent automation-governance-architect`
