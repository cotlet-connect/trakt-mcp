# How to connect Trakt to Claude Code, ChatGPT and any AI agent

**Trakt watchlists, ratings, history and lists in your own account.** Cotlet.dev connects your signed-in Trakt Cloud Browser to Claude, ChatGPT and any AI agent over MCP, or to scripts through REST. Cotlet is independent and not affiliated with Trakt.

## What you can ask

> Add these 12 titles to my Trakt watchlist.

> Log Slow Horses season 4 as watched.

> Which episodes air this week?

> Rate everything I watched this month.

## Connect in 2 minutes

Get your Cotlet API key at https://cotlet.dev/app and export it as `COTLET_API_KEY`. Sign in to Trakt once in your own Cotlet Cloud Browser.

### Claude Code

```bash
claude mcp add --transport http cotlet https://cotlet.dev/mcp/v1 --header "Authorization: Bearer $COTLET_API_KEY"
```

### ChatGPT

Settings → Apps → add connector URL `https://cotlet.dev/mcp/v1`, then sign in with Cotlet.dev. No API key needed.

### Cursor

Copy `.cursor/mcp.json` from this repo into your project.

## Run it locally (stdio)

This repo is a small MCP server that forwards calls to hosted Cotlet.dev. Python 3.10+ and the standard library are enough.

```json
{"mcpServers":{"trakt":{"command":"uvx","args":["trakt-mcp"],"env":{"COTLET_API_KEY":"your-key"}}}}
```

Or run it directly:

```bash
export COTLET_API_KEY="your-key"
python3 trakt_agent.py connect
python3 trakt_agent.py status
python3 trakt_agent.py guide
python3 trakt_agent.py serve
```

Tools include search titles, watchlist, history, ratings, custom lists, calendar, account limits, adding and removing watchlist/history items, rating titles, creating lists and adding titles to lists.

## REST API

Each operation is also available under `https://cotlet.dev/api/v1/trakt` with the same bearer key. For example:

```bash
curl https://cotlet.dev/api/v1/trakt/watchlist \
  -H "Authorization: Bearer $COTLET_API_KEY"
```

## Questions from Trakt users

**Does Trakt have an API?** Trakt has a REST API for history, ratings, watchlist, lists and calendars. Cotlet provides the same operations through MCP and REST while working in your own account.

**Can my agent act without asking me?** Changes that can reach other people, such as public lists, wait for your approval by default.

**Is Cotlet affiliated with Trakt?** No. Cotlet is an independent service.

## Find it on

- [Trakt on Cotlet.dev](https://cotlet.dev/integrations/trakt-api-mcp-server?utm_source=github&utm_medium=readme&utm_campaign=trakt&utm_content=find)
- [All apps connected through Cotlet](https://github.com/cotlet-connect)

More: https://cotlet.dev/integrations/trakt-api-mcp-server?utm_source=github&utm_medium=readme&utm_campaign=trakt

Start free: https://cotlet.dev/signup?app=trakt&utm_source=github&utm_medium=readme&utm_campaign=trakt
