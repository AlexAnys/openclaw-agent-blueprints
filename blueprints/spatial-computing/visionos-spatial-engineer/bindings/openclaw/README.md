# OpenClaw Binding -- visionOS Spatial Engineer

## Materialization

1. Copy the template files to your OpenClaw workspace:
   ```bash
   mkdir -p ~/.openclaw/workspace/agents/visionos-spatial-engineer/
   cp SOUL.md.tmpl  ~/.openclaw/workspace/agents/visionos-spatial-engineer/SOUL.md
   cp AGENTS.md.tmpl ~/.openclaw/workspace/agents/visionos-spatial-engineer/AGENTS.md
   cp TOOLS.md.tmpl  ~/.openclaw/workspace/agents/visionos-spatial-engineer/TOOLS.md
   ```

2. Resolve parameters in each file -- replace all `{{variable}}` placeholders:
   - `{{platform_version}}` -- e.g., "visionOS 2"
   - `{{interaction_model}}` -- e.g., "Eyes + Hands (indirect and direct)"
   - `{{rendering_engine}}` -- e.g., "RealityKit"
   - `{{target_device}}` -- e.g., "Apple Vision Pro"
   - `{{team_context}}` -- e.g., "2-person spatial computing team, startup"

3. Register in `openclaw.json`:
   ```json
   {
     "agents": {
       "list": [
         {
           "id": "visionos-spatial-engineer",
           "name": "visionOS Spatial Engineer",
           "description": "visionOS/Apple Vision Pro development -- spatial UI, RealityKit, immersive experiences"
         }
       ]
     }
   }
   ```

4. Verify: `openclaw chat --agent visionos-spatial-engineer`
