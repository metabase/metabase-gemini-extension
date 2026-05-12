# Metabase

This Gemini extension connects to your Metabase instance via the built-in MCP server (Metabase 60+).

When the user asks about tables, metrics, dashboards, saved questions, or wants to run a query, use the `metabase` MCP server's tools.

## When to use the Metabase MCP server

- Searching for tables, metrics, models, or saved questions.
- Inspecting table schemas, field stats, or metric definitions.
- Constructing MBQL queries against the semantic layer.
- Executing queries and reading results.
- Saving results back to Metabase as questions or dashboards.

## When NOT to use it

- Do not read or query Metabase's underlying H2/Postgres application database directly.
- Do not call Metabase REST endpoints (`/api/card`, `/api/dashboard`, etc.) to "shortcut" around the MCP server.

The MCP server is the only allowed channel to read Metabase data — it scopes everything to the authenticated user's Metabase permissions via OAuth.

## First-time auth

Gemini CLI does **not** auto-discover OAuth on streamable HTTP MCP servers. The user must run this once in their chat:

```
/mcp auth metabase
```

That opens the browser for the Metabase OAuth handshake. After approval, the token is cached and subsequent tool calls work transparently.

If the user reports that `gemini mcp list` shows the `metabase` server as `Disconnected`, the most likely cause is that `/mcp auth metabase` has not been run yet. Tell them to run that command first.

If OAuth lands on a Metabase login form rather than an authorize page, the Metabase instance has not completed its first-run setup yet. Tell the user to open `$METABASE_URL` in their browser, finish the wizard, then retry `/mcp auth metabase`.
