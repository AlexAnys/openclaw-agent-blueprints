# OpenClaw Binding — Frontend Developer

## Materialization

1. Copy the template files to your OpenClaw workspace:
   ```bash
   mkdir -p ~/.openclaw/workspace/agents/frontend-developer/
   cp SOUL.md.tmpl  ~/.openclaw/workspace/agents/frontend-developer/SOUL.md
   cp AGENTS.md.tmpl ~/.openclaw/workspace/agents/frontend-developer/AGENTS.md
   cp TOOLS.md.tmpl  ~/.openclaw/workspace/agents/frontend-developer/TOOLS.md
   ```

2. Resolve parameters in each file — replace all `{{variable}}` placeholders:
   - `{{tech_stack}}` — e.g., "React, TypeScript, Tailwind CSS"
   - `{{design_tool}}` — e.g., "Figma"
   - `{{state_management}}` — e.g., "Zustand"
   - `{{build_tool}}` — e.g., "Vite"
   - `{{team_context}}` — e.g., "5-person startup, async-first"
   - `{{target_browsers}}` — e.g., "Chrome, Firefox, Safari latest 2 versions"

3. Register in `openclaw.json`:
   ```json
   {
     "agents": {
       "list": [
         {
           "id": "frontend-developer",
           "name": "Frontend Developer",
           "description": "React/TypeScript frontend development — UI components, performance, accessibility"
         }
       ]
     }
   }
   ```

4. Verify: `openclaw chat --agent frontend-developer`
