# RPG MCP Server

A Model Context Protocol (MCP) server for running tabletop RPG campaigns with AI assistance.

## Features

- **Campaign Management**: Create and manage RPG campaigns
- **NPC Creation**: Generate and manage non-player characters with customizable stats
- **Bestiary System**: Create creature templates with threat levels (none → certain_death)
- **Dynamic Combat**: Team-based combat with hit chances based on threat levels
- **Resource Readers**: 6 tools to query campaign data (campaigns, NPCs, bestiary, combat status)
- **Repository Pattern**: Clean abstraction for swapping JSON files → database

## Installation

```bash
uv venv
source .venv/bin/activate  # or `.venv\Scripts\activate` on Windows
uv pip install -e .
```

## Usage

Run the server using stdio transport:

```bash
uv run python src/server.py
```

## Project Structure

```
src/
├── server.py              # Main MCP server
├── resources.py           # Resource handlers
├── utils.py               # Utility functions
├── repository.py          # Abstract repository interfaces
├── repository_json.py     # JSON file implementation
├── repository_db_example.py  # Example DB implementation
└── tools/                 # Tool implementations
    ├── campaign.py        # Campaign creation
    ├── npc.py             # NPC management (with hit_chance)
    ├── bestiary.py        # Creature templates (with threat_level)
    ├── combat.py          # Combat system (dynamic hit chance)
    └── readers.py         # Resource reader tools
```

## Tools Available

### Core Tools
- `begin_campaign` - Start a new RPG campaign with player character
- `create_npc` - Create NPC with optional `hit_chance` (default 50%)
- `create_bestiary_entry` - Add creatures with mandatory `threat_level`
- `attack` - Execute combat with dynamic hit chance based on attacker
- `remove_from_combat` - Remove entities from combat (death/flee/surrender)

### Resource Reader Tools
- `list_campaigns` - List all campaigns
- `get_campaign` - Get campaign details
- `list_npcs` - List NPCs in campaign
- `get_npc` - Get NPC details with stats
- `get_combat_status` - View active combat with hit chances
- `get_bestiary` - View all creature templates

## Threat Levels

Bestiary entries require a `threat_level` that determines hit chance:

| Threat Level | Hit Chance | Example |
|-------------|-----------|---------|
| `none` | 10% | Fly (needs lucky eye bite) |
| `negligible` | 25% | Dog (untrained) |
| `low` | 35% | Wolf (natural hunter) |
| `moderate` | 50% | Bandit (trained fighter) |
| `high` | 65% | Mercenary (professional) |
| `deadly` | 80% | Dragon (apex predator) |
| `certain_death` | 95% | Eldritch horror |

## Resources

- `campaign://list` - List all campaigns
- `campaign://{id}` - Access specific campaign data
- `npc://{campaign_id}` - Access NPC information

## Repository Pattern

The server uses a repository pattern for data persistence:

```python
# Current: JSON files
from repository_json import JsonNPCRepository
_npc_repo = JsonNPCRepository()

# Future: Swap to database
from repository_db import DbNPCRepository
_npc_repo = DbNPCRepository()
```

See `repository_db_example.py` for database implementation template.

## License

MIT
