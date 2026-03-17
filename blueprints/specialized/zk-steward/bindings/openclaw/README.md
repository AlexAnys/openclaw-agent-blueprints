# OpenClaw Binding — ZK Steward

## Materialization

1. Copy the template files to your OpenClaw workspace:
   ```bash
   mkdir -p ~/.openclaw/workspace/agents/zk-steward/
   cp SOUL.md.tmpl  ~/.openclaw/workspace/agents/zk-steward/SOUL.md
   cp AGENTS.md.tmpl ~/.openclaw/workspace/agents/zk-steward/AGENTS.md
   cp TOOLS.md.tmpl  ~/.openclaw/workspace/agents/zk-steward/TOOLS.md
   ```

2. Resolve parameters in each file — replace all `{{variable}}` placeholders:
   - `{{note_tool}}` — e.g., "Obsidian"
   - `{{knowledge_domain}}` — e.g., "AI/ML engineering"
   - `{{linking_strategy}}` — e.g., "Bidirectional wiki-links with backlink sections"
   - `{{review_cadence}}` — e.g., "Daily log + weekly review"
   - `{{team_context}}` — e.g., "Solo knowledge worker"

3. Register in `openclaw.json`:
   ```json
   {
     "agents": {
       "list": [
         {
           "id": "zk-steward",
           "name": "ZK Steward",
           "description": "Zettelkasten knowledge management — atomic notes, linking, validation, expert perspectives"
         }
       ]
     }
   }
   ```

4. Verify: `openclaw chat --agent zk-steward`
