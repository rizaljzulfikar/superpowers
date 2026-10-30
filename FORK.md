# Personal fork: model routing for OpenCode

This fork is maintained by [rizaljzulfikar](https://github.com/rizaljzulfikar)
for the OpenCode setup on this machine. It is based on
[obra/superpowers](https://github.com/obra/superpowers) and is installed by
OpenCode directly from this repository.

## Changes from upstream

- OpenCode V1 and V2 subagent mappings now require an explicit `model`.
  Previously the V2 mapping told the agent to call `subagent` without a model,
  so every child silently inherited the parent session model.
- The session bootstrap injects
  [`skills/using-superpowers/model-routing.md`](skills/using-superpowers/model-routing.md).
  That file maps the tier names used by Superpowers to the roles in the global
  `~/.config/opencode/AGENTS.md` model table.
- `subagent-driven-development` resolves its Model Selection tiers through that
  mapping (`oneshot.implement`, `sub_agents.code`, `advisor`,
  `oneshot.review`, `sub_agents.review`, and so on).
- `tests/opencode/test-bootstrap-caching.mjs` covers the injected routing and
  the required `model` field.

The concrete model IDs stay in `~/.config/opencode/AGENTS.md`. This fork maps
Superpowers tiers to role names, so changing a model does not require editing
the plugin.

## Install

```json
{
  "plugins": [
    "superpowers@git+https://github.com/rizaljzulfikar/superpowers.git#<commit>"
  ]
}
```

Pin the commit. Do not use a moving branch, or the installed behavior can
change without an explicit update.

## Sync with upstream

```bash
git fetch upstream
git rebase upstream/main
# resolve conflicts in the files listed above
git push origin main
```

Then update the commit pin in the OpenCode configuration.

## Upstream

The fork keeps `upstream` pointed at `https://github.com/obra/superpowers.git`.
Only the model-routing changes above are local; everything else is upstream.
