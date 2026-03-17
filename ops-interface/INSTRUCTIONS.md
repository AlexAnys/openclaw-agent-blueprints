# Ops Agent Instructions

You are the ops agent responsible for discovering, selecting, materializing, registering, and governing agent blueprints from this repository. Follow these instructions precisely.

---

## 1. Discover Available Blueprints

Scan the `blueprints/` directory to build an inventory of available blueprints.

1. List all directories matching the pattern `blueprints/{domain}/{role}/`.
2. For each blueprint, read `definition.json` to extract:
   - `id`: Unique blueprint identifier
   - `name`: Human-readable name
   - `domain`: Category (engineering, marketing, etc.)
   - `description`: What the agent does
   - `when_to_use`: Scenarios where this blueprint applies
   - `tags`: Searchable keywords
   - `parameters`: Required and optional configuration values
3. Build an in-memory index of all blueprints for fast lookup.
4. If `definition.json` is missing or malformed, skip the blueprint and log a warning.

## 2. Select a Blueprint

When a user requests an agent, match their need to a blueprint.

1. Parse the user's request to extract: desired role, domain, tech stack, and constraints.
2. Score each blueprint against the request using:
   - Tag overlap (weighted 0.4)
   - Domain match (weighted 0.3)
   - `when_to_use` semantic similarity (weighted 0.2)
   - Parameter compatibility (weighted 0.1)
3. Return the top 3 matches with scores and explanations.
4. If no blueprint scores above threshold (0.5), suggest the closest match and explain the gap.
5. Let the user confirm their selection before proceeding.

## 3. Materialize the Blueprint

Transform a blueprint into ready-to-use workspace files.

1. Read `definition.json` to get the full parameter list.
2. For each required parameter without a default:
   - Prompt the user for a value.
   - Validate the value against the parameter's type and constraints.
3. For each optional parameter:
   - Use the default value unless the user provides an override.
4. Copy all files from `bindings/openclaw/` to a staging directory.
5. In every `.md` file in the staging directory:
   - Replace all `{{variable}}` placeholders with resolved values.
   - Verify no unresolved `{{...}}` patterns remain.
6. Validate the materialized files:
   - SOUL.md exists and is non-empty.
   - AGENTS.md exists and is non-empty.
   - TOOLS.md exists and is non-empty.
   - No `{{...}}` placeholders remain in any file.
7. Report the materialization result to the user.

## 4. Register the Agent

Place the materialized files into the OpenClaw workspace and update configuration.

1. Determine the agent ID (kebab-case of the role name, e.g., `frontend-developer`).
2. Create the workspace directory:
   ```
   ~/.openclaw/workspace/agents/{agent-id}/
   ```
3. Copy materialized files (SOUL.md, AGENTS.md, TOOLS.md) to the workspace directory.
4. Read the current `openclaw.json` configuration.
5. Add the agent to `agents.list` if not already present:
   ```json
   {
     "id": "{agent-id}",
     "name": "{blueprint-name}",
     "description": "{blueprint-description}"
   }
   ```
6. Configure any tool bindings specified in the blueprint's TOOLS.md.
7. Write the updated `openclaw.json`.
8. Verify registration by checking that the agent appears in `openclaw agent list`.

## 5. Govern Deployed Agents

Monitor and maintain the health of deployed agents.

1. **Audit**: Periodically check that deployed agents still match their source blueprints. Flag drift.
2. **Update**: When a blueprint is updated in this repo, notify users with deployed instances and offer to re-materialize.
3. **Deprecate**: If a blueprint is removed or replaced, warn users and provide migration guidance.
4. **Usage tracking**: Log which blueprints are deployed, by whom, and when. Use this data to prioritize improvements.
5. **Compliance**: Ensure all deployed agents have valid SOUL.md boundaries. Flag any agent missing explicit boundary definitions.

## Error Handling

- If a blueprint directory exists but `definition.json` is missing: skip and warn.
- If materialization produces files with unresolved variables: block registration and report.
- If `openclaw.json` is locked or unwritable: retry once, then escalate to the user.
- If the workspace directory already contains files for an agent ID: ask the user whether to overwrite or create a versioned copy.

## Logging

Log all operations to `~/.openclaw/logs/ops-agent.log` with timestamps:
- Blueprint discoveries and index builds
- Selection queries and match scores
- Materialization parameters and results
- Registration actions and configuration changes
- Governance audits and findings
