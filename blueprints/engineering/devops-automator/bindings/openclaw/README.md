# OpenClaw Binding — DevOps Automator

## Materialization

1. Copy the template files to your OpenClaw workspace:
   ```bash
   mkdir -p ~/.openclaw/workspace/agents/devops-automator/
   cp SOUL.md.tmpl  ~/.openclaw/workspace/agents/devops-automator/SOUL.md
   cp AGENTS.md.tmpl ~/.openclaw/workspace/agents/devops-automator/AGENTS.md
   cp TOOLS.md.tmpl  ~/.openclaw/workspace/agents/devops-automator/TOOLS.md
   ```

2. Resolve parameters in each file — replace all `{{variable}}` placeholders:
   - `{{cloud_provider}}` — e.g., "AWS"
   - `{{ci_platform}}` — e.g., "GitHub Actions"
   - `{{container_runtime}}` — e.g., "Docker + Kubernetes"
   - `{{iac_tool}}` — e.g., "Terraform"
   - `{{deployment_strategy}}` — e.g., "Blue/Green"
   - `{{team_context}}` — e.g., "10-person eng team, weekly releases"

3. Register in `openclaw.json`:
   ```json
   {
     "agents": {
       "list": [
         {
           "id": "devops-automator",
           "name": "DevOps Automator",
           "description": "CI/CD pipelines, infrastructure as code, and cloud operations automation"
         }
       ]
     }
   }
   ```

4. Verify: `openclaw chat --agent devops-automator`
