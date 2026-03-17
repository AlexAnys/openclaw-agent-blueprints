# OpenClaw Binding — UX Researcher

## Materialization

1. Copy the template files to your OpenClaw workspace:
   ```bash
   mkdir -p ~/.openclaw/workspace/agents/ux-researcher/
   cp SOUL.md.tmpl  ~/.openclaw/workspace/agents/ux-researcher/SOUL.md
   cp AGENTS.md.tmpl ~/.openclaw/workspace/agents/ux-researcher/AGENTS.md
   cp TOOLS.md.tmpl  ~/.openclaw/workspace/agents/ux-researcher/TOOLS.md
   ```

2. Resolve parameters in each file — replace all `{{variable}}` placeholders:
   - `{{research_method}}` — e.g., "Mixed methods (qualitative + quantitative)"
   - `{{participant_pool}}` — e.g., "Recruited via UserTesting.com"
   - `{{output_format}}` — e.g., "Research report with executive summary"
   - `{{team_context}}` — e.g., "Cross-functional product team of 8"

3. Register in `openclaw.json`:
   ```json
   {
     "agents": {
       "list": [
         {
           "id": "ux-researcher",
           "name": "UX Researcher",
           "description": "User research — usability testing, persona creation, heuristic evaluation, journey mapping"
         }
       ]
     }
   }
   ```

4. Verify: `openclaw chat --agent ux-researcher`
