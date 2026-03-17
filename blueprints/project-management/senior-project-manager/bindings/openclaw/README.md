# OpenClaw Binding — Senior Project Manager

## Materialization

1. Copy the template files to your OpenClaw workspace:
   ```bash
   mkdir -p ~/.openclaw/workspace/agents/senior-project-manager/
   cp SOUL.md.tmpl  ~/.openclaw/workspace/agents/senior-project-manager/SOUL.md
   cp AGENTS.md.tmpl ~/.openclaw/workspace/agents/senior-project-manager/AGENTS.md
   cp TOOLS.md.tmpl  ~/.openclaw/workspace/agents/senior-project-manager/TOOLS.md
   ```

2. Resolve parameters in each file — replace all `{{variable}}` placeholders:
   - `{{methodology}}` — e.g., "Agile (2-week sprints)"
   - `{{project_tool}}` — e.g., "Linear"
   - `{{team_size}}` — e.g., "5-person cross-functional team"
   - `{{reporting_cadence}}` — e.g., "Weekly stakeholder update, daily standup"
   - `{{team_context}}` — e.g., "Product development team, hybrid remote"

3. Register in `openclaw.json`:
   ```json
   {
     "agents": {
       "list": [
         {
           "id": "senior-project-manager",
           "name": "Senior Project Manager",
           "description": "Project management — spec-to-task conversion, scope management, risk mitigation, stakeholder communication"
         }
       ]
     }
   }
   ```

4. Verify: `openclaw chat --agent senior-project-manager`
