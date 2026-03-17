# OpenClaw Binding — Sprint Prioritizer

## Materialization

1. Copy the template files to your OpenClaw workspace:
   ```bash
   mkdir -p ~/.openclaw/workspace/agents/sprint-prioritizer/
   cp SOUL.md.tmpl  ~/.openclaw/workspace/agents/sprint-prioritizer/SOUL.md
   cp AGENTS.md.tmpl ~/.openclaw/workspace/agents/sprint-prioritizer/AGENTS.md
   cp TOOLS.md.tmpl  ~/.openclaw/workspace/agents/sprint-prioritizer/TOOLS.md
   ```

2. Resolve parameters in each file — replace all `{{variable}}` placeholders:
   - `{{prioritization_framework}}` — e.g., "RICE"
   - `{{sprint_duration}}` — e.g., "2 weeks"
   - `{{team_size}}` — e.g., "6 engineers + 1 designer"
   - `{{agile_methodology}}` — e.g., "Scrum"
   - `{{tracking_tool}}` — e.g., "Linear"
   - `{{team_context}}` — e.g., "B2B SaaS product team, biweekly sprints"

3. Register in `openclaw.json`:
   ```json
   {
     "agents": {
       "list": [
         {
           "id": "sprint-prioritizer",
           "name": "Sprint Prioritizer",
           "description": "Data-driven sprint planning and backlog prioritization using RICE/MoSCoW frameworks"
         }
       ]
     }
   }
   ```

4. Verify: `openclaw chat --agent sprint-prioritizer`
