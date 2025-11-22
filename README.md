# RPG MCP Server

MCP server for D&D-style campaigns. Combat, NPCs, bestiary with threat levels.

## Install & Run

```bash
uv venv && source .venv/bin/activate
uv pip install -e .
uv run python src/server.py
```

## Connect to Claude Desktop

Add to `claude_desktop_config.json`:
```json
{
  "mcpServers": {
    "rpg": {
      "command": "uv",
      "args": ["run", "python", "/path/to/src/server.py"]
    }
  }
}
```

## Tools (11 total)

**Core:** `begin_campaign`, `create_npc`, `create_bestiary_entry`, `attack`, `remove_from_combat`

**Readers:** `list_campaigns`, `get_campaign`, `list_npcs`, `get_npc`, `get_combat_status`, `get_bestiary`

## Threat Levels

Bestiary creatures get a `threat_level` → determines hit chance:

`none` 10% | `negligible` 25% | `low` 35% | `moderate` 50% | `high` 65% | `deadly` 80% | `certain_death` 95%

NPCs can override with custom `hit_chance`.

## Swap to Database

```python
# tools/combat.py
from repository_json import JsonCombatRepository  # ← files
from repository_db import DbCombatRepository      # ← database
```

See `repository_db_example.py`.

## License

MIT
