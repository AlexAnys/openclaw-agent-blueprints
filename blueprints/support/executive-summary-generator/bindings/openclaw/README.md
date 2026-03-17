# OpenClaw Binding -- Executive Summary Generator

## Materialization

1. Copy the template files to your OpenClaw workspace:
   ```bash
   mkdir -p ~/.openclaw/workspace/agents/executive-summary-generator/
   cp SOUL.md.tmpl  ~/.openclaw/workspace/agents/executive-summary-generator/SOUL.md
   cp AGENTS.md.tmpl ~/.openclaw/workspace/agents/executive-summary-generator/AGENTS.md
   cp TOOLS.md.tmpl  ~/.openclaw/workspace/agents/executive-summary-generator/TOOLS.md
   ```

2. Resolve parameters in each file -- replace all `{{variable}}` placeholders:
   - `{{reporting_frequency}}` -- e.g., "Weekly"
   - `{{audience_level}}` -- e.g., "C-suite executives"
   - `{{kpi_framework}}` -- e.g., "OKRs"
   - `{{output_format}}` -- e.g., "Markdown document"
   - `{{team_context}}` -- e.g., "Cross-functional leadership team, 50-person company"

3. Register in `openclaw.json`:
   ```json
   {
     "agents": {
       "list": [
         {
           "id": "executive-summary-generator",
           "name": "Executive Summary Generator",
           "description": "Leadership reporting -- executive summaries, KPI dashboards, risk highlights, board decks"
         }
       ]
     }
   }
   ```

4. Verify: `openclaw chat --agent executive-summary-generator`
