# OpenClaw Binding -- Support Responder

## Materialization

1. Copy the template files to your OpenClaw workspace:
   ```bash
   mkdir -p ~/.openclaw/workspace/agents/support-responder/
   cp SOUL.md.tmpl  ~/.openclaw/workspace/agents/support-responder/SOUL.md
   cp AGENTS.md.tmpl ~/.openclaw/workspace/agents/support-responder/AGENTS.md
   cp TOOLS.md.tmpl  ~/.openclaw/workspace/agents/support-responder/TOOLS.md
   ```

2. Resolve parameters in each file -- replace all `{{variable}}` placeholders:
   - `{{support_platform}}` -- e.g., "Zendesk"
   - `{{tone}}` -- e.g., "Professional and empathetic"
   - `{{sla_target}}` -- e.g., "First response < 2 hours, resolution < 24 hours"
   - `{{product_domain}}` -- e.g., "SaaS developer tools"
   - `{{team_context}}` -- e.g., "3-person support team, async-first"

3. Register in `openclaw.json`:
   ```json
   {
     "agents": {
       "list": [
         {
           "id": "support-responder",
           "name": "Support Responder",
           "description": "Customer support -- ticket triage, response drafting, escalation, knowledge base"
         }
       ]
     }
   }
   ```

4. Verify: `openclaw chat --agent support-responder`
