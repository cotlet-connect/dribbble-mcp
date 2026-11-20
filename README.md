# Dribbble API and MCP server for ChatGPT and Claude

Dribbble offers a publishing API for shots and projects. The Cotlet.dev page reports no official Dribbble MCP server, checked 27 October 2026. Cotlet.dev connects ChatGPT, Claude and other AI agents to Dribbble leads, Messages, Pro Analytics, shots and comments.

## What you can ask

> Find Project Requests I have not answered.

> Read unread client conversations and draft replies for my approval.

> Prepare a weekly Pro Analytics report.

> Rank my shots by saves per view.

> Draft replies to comments on my shots.

> Update the title, description or tags of one of my shots.

## Connect in 2 minutes

Get your API key at https://cotlet.dev/app and export it as `COTLET_API_KEY`.

### ChatGPT

Settings → Apps & Connectors → Create, use `https://cotlet.dev/mcp/v1/connect` with OAuth, then sign in with Cotlet.dev. No API key needed.

### Claude Code

```bash
claude mcp add --transport http cotlet https://cotlet.dev/mcp/v1 --header "Authorization: Bearer $COTLET_API_KEY"
```

### Cursor

Copy `.cursor/mcp.json` from this repo into your project:

```json
{
  "mcpServers": {
    "cotlet": {
      "url": "https://cotlet.dev/mcp/v1",
      "headers": {
        "Authorization": "Bearer ${COTLET_API_KEY}"
      }
    }
  }
}
```

## Run it locally (stdio)

This repo is a real MCP server. It speaks MCP over stdio, lists its Dribbble tools without any key, and forwards every tool call to the hosted Cotlet.dev server. The hosted URL above stays the recommended way. Use this when your client only starts local servers.

```json
{"mcpServers":{"dribbble":{"command":"uvx","args":["dribbble-mcp"],"env":{"COTLET_API_KEY":"your-key"}}}}
```

Or with Docker:

```bash
docker build -t dribbble-mcp .
docker run -i --rm -e COTLET_API_KEY dribbble-mcp
```

Tools: `dribbble_guide`, `dribbble_status`, `dribbble_open`, `dribbble_read`, `dribbble_click`, `dribbble_type`, `dribbble_close`. Without `COTLET_API_KEY` a tool call answers: "Set COTLET_API_KEY. Get a key at https://cotlet.dev/app".

## Command line

Python 3.10+, nothing else to install. From PyPI:

```bash
pip install dribbble-mcp        # or run it once: uvx dribbble-mcp connect
dribbble-mcp connect
```

Or straight from this repo:

```bash
export COTLET_API_KEY="your-key"
python3 dribbble_agent.py connect   # ready config for Claude Code, Cursor, ChatGPT
python3 dribbble_agent.py status    # is Dribbble ready in your Cotlet.dev account
python3 dribbble_agent.py guide     # Dribbble screens and sign-in link
python3 dribbble_agent.py read      # open Dribbble, read the page, close the browser
python3 dribbble_agent.py tools     # list Cotlet.dev tools
python3 dribbble_agent.py serve     # start the stdio MCP server (same as no argument)
```

## Questions from Dribbble users

**Does Dribbble have an official MCP server?**

The live Cotlet.dev page reports no official Dribbble MCP server, checked 27 October 2026. Its API v2 covers publishing shots and projects.

**What can I do with Dribbble through Cotlet.dev?**

Work with leads, client messages, Pro Analytics, shots, shot statistics and comments. The live page describes 11 hosted operations. This repository provides a local MCP adapter to Cotlet.dev browser tools.

**Do I need Dribbble Pro?**

Pro Analytics needs a Pro account. The page describes shots, comments and Messages tools for your own account.

**Is Cotlet.dev affiliated with Dribbble?**

No. Cotlet.dev is independent and is not affiliated with Dribbble.

## Find it on

- [Dribbble on Cotlet.dev](https://cotlet.dev/integrations/dribbble-api-mcp-server?utm_source=github&utm_medium=readme&utm_campaign=dribbble&utm_content=find)
- [PyPI package dribbble-mcp](https://pypi.org/project/dribbble-mcp/)
- [Odel](https://odel.app/modules/cotlet/dribbble)
- [mcpbeat](https://mcpbeat.com/mcp-servers/cotlet/dribbble/)
- [Step-by-step guide (PDF) on Internet Archive](https://archive.org/details/cotlet-connect-dribbble-to-ai-agents-guide)

## Also works with


- [All apps connected through Cotlet.dev](https://github.com/cotlet-connect)

---

More: https://cotlet.dev/integrations/dribbble-api-mcp-server?utm_source=github&utm_medium=readme&utm_campaign=dribbble

Start free: https://cotlet.dev/signup?app=dribbble&utm_source=github&utm_medium=readme&utm_campaign=dribbble
