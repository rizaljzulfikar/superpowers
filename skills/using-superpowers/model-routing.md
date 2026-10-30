# Model Routing

Every Superpowers subagent dispatch must specify a model explicitly. An omitted
model inherits the session model and silently defeats this routing.

Resolve the concrete `provider/model` from the **Model routing by role** table
in `~/.config/opencode/AGENTS.md`. This table maps the tiers used by
Superpowers to the roles in that global table.

| Superpowers dispatch | Global role |
| --- | --- |
| Mechanical implementer (1-2 files, complete spec) | `oneshot.implement` |
| Standard implementer (multi-file, integration) | `sub_agents.code` |
| Architecture, design, ambiguous decisions | `advisor` |
| Plan authoring or spec/plan review | `oneshot.plan` |
| Final whole-branch review | `oneshot.review` |
| Scoped re-review or small fix review | `sub_agents.review` |
| Fix-loop escalation (rounds 4-5) | `sub_agents.code`, then `advisor` |
| Codebase exploration | `sub_agents.explore` |
| Research and documentation | `sub_agents.research` |
| Quick verification / sanity check | `sub_agents.sanity_check` |
| Visual, screenshot, or image check | `sub_agents.vision` |
| Option or quality evaluation | `sub_agents.evaluate` |

Rules:

- Pass the selected model as `model: "<provider>/<model>"` on every `subagent`
  call.
- When a skill does not name a model (for example `requesting-code-review` or
  `dispatching-parallel-agents`), infer the role from the task and use the
  matching row.
- If a skill's generic tier conflicts with the global table, the global table
  wins.
- If a mapped model is unavailable, report it and use the fallback from the
  global table. Do not silently inherit the session model.
