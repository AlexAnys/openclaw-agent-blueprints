# OpenClaw Binding — Content Creator

## Materialization

1. Copy the template files to your OpenClaw workspace:
   ```bash
   mkdir -p ~/.openclaw/workspace/agents/content-creator/
   cp SOUL.md.tmpl  ~/.openclaw/workspace/agents/content-creator/SOUL.md
   cp AGENTS.md.tmpl ~/.openclaw/workspace/agents/content-creator/AGENTS.md
   cp TOOLS.md.tmpl  ~/.openclaw/workspace/agents/content-creator/TOOLS.md
   ```

2. Resolve parameters in each file — replace all `{{variable}}` placeholders:
   - `{{brand_voice}}` — e.g., "Witty, conversational, data-backed"
   - `{{target_audience}}` — e.g., "Developer team leads, 28-40, US/EU"
   - `{{content_platforms}}` — e.g., "Blog, LinkedIn, Twitter/X, YouTube"
   - `{{industry}}` — e.g., "Developer Tools"
   - `{{content_pillars}}` — e.g., "Engineering culture, Product deep-dives, Industry trends"
   - `{{team_context}}` — e.g., "Solo content marketer, biweekly publishing cadence"

3. Register in `openclaw.json`:
   ```json
   {
     "agents": {
       "list": [
         {
           "id": "content-creator",
           "name": "Content Creator",
           "description": "Multi-platform content strategy and creation aligned with brand voice"
         }
       ]
     }
   }
   ```

4. Verify: `openclaw chat --agent content-creator`
