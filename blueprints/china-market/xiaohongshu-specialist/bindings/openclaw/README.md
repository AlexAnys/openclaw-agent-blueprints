# OpenClaw Binding

For complete materialization and registration instructions, see [`ops-interface/INSTRUCTIONS.md`](../../../../ops-interface/INSTRUCTIONS.md).

## Quick Reference

1. Copy `*.md.tmpl` from the blueprint root to your workspace (`~/.openclaw/workspace-{agentId}/`)
2. Rename `.tmpl` → `.md` and resolve all `{{variable}}` placeholders
3. Register in `openclaw.json` (`agents.list` + `bindings`)
4. Restart Gateway and test

Parameters and onboarding questions are defined in `definition.json`.
