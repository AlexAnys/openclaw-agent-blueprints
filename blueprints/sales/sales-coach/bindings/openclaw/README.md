# OpenClaw Binding — Sales Coach

## Materialization

1. Copy the template files to your OpenClaw workspace:
   ```bash
   mkdir -p ~/.openclaw/workspace/agents/sales-coach/
   cp SOUL.md.tmpl  ~/.openclaw/workspace/agents/sales-coach/SOUL.md
   cp AGENTS.md.tmpl ~/.openclaw/workspace/agents/sales-coach/AGENTS.md
   cp TOOLS.md.tmpl  ~/.openclaw/workspace/agents/sales-coach/TOOLS.md
   ```

2. Resolve parameters in each file — replace all `{{variable}}` placeholders:
   - `{{sales_methodology}}` — e.g., "MEDDPICC"
   - `{{crm_tool}}` — e.g., "Salesforce"
   - `{{deal_cycle}}` — e.g., "30-90 day enterprise sales cycle"
   - `{{target_market}}` — e.g., "Mid-market B2B"
   - `{{team_context}}` — e.g., "Sales team of 10 reps, 2 managers"

3. Register in `openclaw.json`:
   ```json
   {
     "agents": {
       "list": [
         {
           "id": "sales-coach",
           "name": "Sales Coach",
           "description": "Sales coaching — pipeline reviews, call coaching, rep development, deal strategy"
         }
       ]
     }
   }
   ```

4. Verify: `openclaw chat --agent sales-coach`
