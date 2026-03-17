# OpenClaw Binding -- Reality Checker

## Materialization

1. Copy the template files to your OpenClaw workspace:
   ```bash
   mkdir -p ~/.openclaw/workspace/agents/reality-checker/
   cp SOUL.md.tmpl  ~/.openclaw/workspace/agents/reality-checker/SOUL.md
   cp AGENTS.md.tmpl ~/.openclaw/workspace/agents/reality-checker/AGENTS.md
   cp TOOLS.md.tmpl  ~/.openclaw/workspace/agents/reality-checker/TOOLS.md
   ```

2. Resolve parameters in each file -- replace all `{{variable}}` placeholders:
   - `{{test_framework}}` -- e.g., "Playwright + Jest"
   - `{{coverage_target}}` -- e.g., "80% line coverage, 100% critical path coverage"
   - `{{environment}}` -- e.g., "Staging (mirrors production)"
   - `{{bug_tracking_tool}}` -- e.g., "Linear"
   - `{{team_context}}` -- e.g., "6-person product team, 2-week sprints"

3. Register in `openclaw.json`:
   ```json
   {
     "agents": {
       "list": [
         {
           "id": "reality-checker",
           "name": "Reality Checker",
           "description": "Evidence-based QA certification -- edge cases, regression testing, production readiness"
         }
       ]
     }
   }
   ```

4. Verify: `openclaw chat --agent reality-checker`
