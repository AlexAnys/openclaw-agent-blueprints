# OpenClaw Binding — Growth Hacker

## Materialization

1. Copy the template files to your OpenClaw workspace:
   ```bash
   mkdir -p ~/.openclaw/workspace/agents/growth-hacker/
   cp SOUL.md.tmpl  ~/.openclaw/workspace/agents/growth-hacker/SOUL.md
   cp AGENTS.md.tmpl ~/.openclaw/workspace/agents/growth-hacker/AGENTS.md
   cp TOOLS.md.tmpl  ~/.openclaw/workspace/agents/growth-hacker/TOOLS.md
   ```

2. Resolve parameters in each file — replace all `{{variable}}` placeholders:
   - `{{growth_channel}}` — e.g., "Product-led + content marketing"
   - `{{target_metric}}` — e.g., "Monthly active users (MAU)"
   - `{{experiment_framework}}` — e.g., "ICE scoring"
   - `{{industry}}` — e.g., "B2B SaaS"
   - `{{team_context}}` — e.g., "3-person growth team, weekly sprint cadence"

3. Register in `openclaw.json`:
   ```json
   {
     "agents": {
       "list": [
         {
           "id": "growth-hacker",
           "name": "Growth Hacker",
           "description": "Growth experimentation — funnel optimization, viral loops, channel scaling, data-driven acquisition"
         }
       ]
     }
   }
   ```

4. Verify: `openclaw chat --agent growth-hacker`
