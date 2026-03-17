# OpenClaw Binding — Xiaohongshu Specialist

## Materialization

1. Copy the template files to your OpenClaw workspace:
   ```bash
   mkdir -p ~/.openclaw/workspace/agents/xiaohongshu-specialist/
   cp SOUL.md.tmpl  ~/.openclaw/workspace/agents/xiaohongshu-specialist/SOUL.md
   cp AGENTS.md.tmpl ~/.openclaw/workspace/agents/xiaohongshu-specialist/AGENTS.md
   cp TOOLS.md.tmpl  ~/.openclaw/workspace/agents/xiaohongshu-specialist/TOOLS.md
   ```

2. Resolve parameters in each file — replace all `{{variable}}` placeholders:
   - `{{brand_category}}` — e.g., "Beauty / skincare"
   - `{{target_demographic}}` — e.g., "Gen Z women in tier 1-2 cities"
   - `{{content_style}}` — e.g., "Minimalist aesthetic with warm tones"
   - `{{posting_frequency}}` — e.g., "4 posts per week"
   - `{{team_context}}` — e.g., "3-person brand marketing team"

3. Register in `openclaw.json`:
   ```json
   {
     "agents": {
       "list": [
         {
           "id": "xiaohongshu-specialist",
           "name": "Xiaohongshu Specialist",
           "description": "小红书 content strategy — lifestyle content, trend analysis, KOL collaboration, community engagement"
         }
       ]
     }
   }
   ```

4. Verify: `openclaw chat --agent xiaohongshu-specialist`
