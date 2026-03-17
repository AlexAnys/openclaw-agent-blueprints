# OpenClaw Binding -- PPC Campaign Strategist

## Materialization

1. Copy the template files to your OpenClaw workspace:
   ```bash
   mkdir -p ~/.openclaw/workspace/agents/ppc-campaign-strategist/
   cp SOUL.md.tmpl  ~/.openclaw/workspace/agents/ppc-campaign-strategist/SOUL.md
   cp AGENTS.md.tmpl ~/.openclaw/workspace/agents/ppc-campaign-strategist/AGENTS.md
   cp TOOLS.md.tmpl  ~/.openclaw/workspace/agents/ppc-campaign-strategist/TOOLS.md
   ```

2. Resolve parameters in each file -- replace all `{{variable}}` placeholders:
   - `{{ad_platform}}` -- e.g., "Google Ads"
   - `{{monthly_budget}}` -- e.g., "$50K"
   - `{{target_roas}}` -- e.g., "400%"
   - `{{industry}}` -- e.g., "E-commerce"
   - `{{team_context}}` -- e.g., "In-house marketing team, 3 people"

3. Register in `openclaw.json`:
   ```json
   {
     "agents": {
       "list": [
         {
           "id": "ppc-campaign-strategist",
           "name": "PPC Campaign Strategist",
           "description": "PPC campaigns -- keyword strategy, bid optimization, ad copy, ROAS analysis"
         }
       ]
     }
   }
   ```

4. Verify: `openclaw chat --agent ppc-campaign-strategist`
