# RPG MCP Server

A Model Context Protocol (MCP) server for running tabletop RPG campaigns with AI assistance.

## Features

- **Campaign Management**: Create and manage RPG campaigns
- **NPC Creation**: Generate and manage non-player characters
- **Bestiary**: Create and manage creature entries
- **Combat System**: Handle attacks and combat tracking
- **Resource System**: Access campaign and NPC data via MCP resources

## Installation

```bash
cd mcp
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
mcp/
├── src/
│   ├── server.py          # Main MCP server
│   ├── resources.py       # Resource handlers
│   ├── utils.py           # Utility functions
│   └── tools/             # Tool implementations
│       ├── campaign.py
│       ├── npc.py
│       ├── bestiary.py
│       └── combat.py
├── campaigns/             # Campaign data storage (gitignored)
└── pyproject.toml
```

## Tools Available

- `begin_campaign` - Start a new RPG campaign
- `create_npc` - Create a non-player character
- `create_bestiary_entry` - Add creatures to the bestiary
- `attack` - Execute combat attacks
- `remove_from_combat` - Remove entities from combat

## Resources

- `campaign://` - Access campaign data
- `npc://` - Access NPC information

## License

MIT
