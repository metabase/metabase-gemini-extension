# Metabase Gemini Extension

The official [Gemini CLI](https://geminicli.com/) extension for [Metabase](https://www.metabase.com/). Developed and maintained by the Metabase Team.

## What's included

- Extension manifest: `gemini-extension.json` (declares the `metabaseUrl` setting + the Metabase MCP server)
- Context file: `GEMINI.md` (tells Gemini when to use the Metabase MCP and what not to do)

Current scope: **manifest + MCP config + context file only** (no agent skills, commands, or hooks yet).

## Requirements

- Gemini CLI with extension support.
- A Metabase instance on version **60 or higher** with the MCP server enabled (it ships enabled by default in 60+).

## Install

```sh
gemini extensions install https://github.com/metabase/metabase-gemini-extension
```

Gemini will prompt for `metabaseUrl` during install — paste your Metabase base URL (e.g. `https://metabase.acme.com` or `http://localhost:3000`, no trailing slash).

## First use

After installing, open `gemini` and run this once to authorize:

```
/mcp auth metabase
```

This opens your browser for the Metabase OAuth handshake. Approve, and the token is cached for subsequent calls. After that you can ask things like "what tables do I have in Metabase?" and the agent will use the MCP tools.

> Note: Gemini CLI does not currently kick off OAuth automatically for streamable-HTTP MCP servers, so `gemini mcp list` will show `Disconnected` until you run `/mcp auth metabase` once. You only need to do this once; tokens are cached. Tracking issues: [google-gemini/gemini-cli#19068](https://github.com/google-gemini/gemini-cli/issues/19068), [#20017](https://github.com/google-gemini/gemini-cli/issues/20017), [#20990](https://github.com/google-gemini/gemini-cli/issues/20990), [#23296](https://github.com/google-gemini/gemini-cli/issues/23296), [#25473](https://github.com/google-gemini/gemini-cli/issues/25473).

## Changing the URL later

```sh
gemini extensions set metabase.metabaseUrl https://metabase.new-host.com
```

## How to test the extension locally

1. Clone this repo.
2. Link it into Gemini as a local development extension:

   ```sh
   gemini extensions link /path/to/metabase-gemini-extension
   ```

3. Gemini will prompt for the `metabaseUrl` setting (paste any reachable Metabase URL).
4. Start a Gemini chat and ask it to query something in Metabase — the first call triggers OAuth in your browser.

## Attribution

Sister projects from the Metabase Team:

- [`metabase-codex-plugin`](https://github.com/metabase/metabase-codex-plugin)
- [`metabase-cursor-plugin`](https://github.com/metabase/metabase-cursor-plugin)

## License

MIT
