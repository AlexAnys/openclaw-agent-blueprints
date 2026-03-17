# OpenClaw Binding — Feishu Integration Developer

## Materialization

1. Copy the template files to your OpenClaw workspace:
   ```bash
   mkdir -p ~/.openclaw/workspace/agents/feishu-integration-developer/
   cp SOUL.md.tmpl  ~/.openclaw/workspace/agents/feishu-integration-developer/SOUL.md
   cp AGENTS.md.tmpl ~/.openclaw/workspace/agents/feishu-integration-developer/AGENTS.md
   cp TOOLS.md.tmpl  ~/.openclaw/workspace/agents/feishu-integration-developer/TOOLS.md
   ```

2. Resolve parameters in each file — replace all `{{variable}}` placeholders:
   - `{{feishu_app_type}}` — e.g., "Enterprise self-built app (企业自建应用)"
   - `{{integration_scope}}` — e.g., "Bot + Approval + Bitable"
   - `{{auth_method}}` — e.g., "tenant_access_token"
   - `{{target_features}}` — e.g., "Approval notification bot with Bitable data sync"
   - `{{team_context}}` — e.g., "Small engineering team"

3. Register in `openclaw.json`:
   ```json
   {
     "agents": {
       "list": [
         {
           "id": "feishu-integration-developer",
           "name": "Feishu Integration Developer",
           "description": "飞书/Lark integration — bots, message cards, approvals, Bitable, SSO, mini programs"
         }
       ]
     }
   }
   ```

4. Verify: `openclaw chat --agent feishu-integration-developer`
