# OpenClaw Binding — Pipeline Analyst

## Materialization

1. Copy the template files to your OpenClaw workspace:
   ```bash
   mkdir -p ~/.openclaw/workspace/agents/pipeline-analyst/
   cp SOUL.md.tmpl  ~/.openclaw/workspace/agents/pipeline-analyst/SOUL.md
   cp AGENTS.md.tmpl ~/.openclaw/workspace/agents/pipeline-analyst/AGENTS.md
   cp TOOLS.md.tmpl  ~/.openclaw/workspace/agents/pipeline-analyst/TOOLS.md
   ```

2. Resolve parameters in each file — replace all `{{variable}}` placeholders:
   - `{{crm_tool}}` — e.g., "Salesforce"
   - `{{pipeline_stages}}` — e.g., "Discovery, Qualification, Evaluation, Proposal, Negotiation, Closed"
   - `{{forecast_model}}` — e.g., "Velocity-adjusted weighted pipeline"
   - `{{reporting_cadence}}` — e.g., "Weekly pipeline review, monthly forecast"
   - `{{team_context}}` — e.g., "RevOps team supporting 15 AEs"

3. Register in `openclaw.json`:
   ```json
   {
     "agents": {
       "list": [
         {
           "id": "pipeline-analyst",
           "name": "Pipeline Analyst",
           "description": "Pipeline analytics — health diagnostics, deal scoring, revenue forecasting, conversion analysis"
         }
       ]
     }
   }
   ```

4. Verify: `openclaw chat --agent pipeline-analyst`
