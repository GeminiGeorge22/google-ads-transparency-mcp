# Changelog

All notable changes to this project.

## [python 0.1.0 on PyPI] - 2026-11-03

- Python package renamed to `google-ads-transparency-mcp-server` for PyPI (the `google-ads-transparency-mcp` name on PyPI belongs to an unrelated project). Install with `uvx google-ads-transparency-mcp-server` or `pip install google-ads-transparency-mcp-server`; the `google-ads-transparency-mcp` command stays as an alias.
- Python README carries the `mcp-name` line for MCP Registry verification; `server.json` 1.0.1 adds the PyPI package (stdio) next to the hosted remote.

## [0.1.0]

- Open-source stdio MCP server (Node.js, plus a matching Python package in `python/`) for the Google Ads Transparency Scraper Actor.
- `initialize` and `tools/list` work without a token: the tool is served from a checked-in `tools.json` built from the Actor's public input schema (`npm run build:tools`).
- `tools/call` goes to Apify's hosted MCP gateway with your own `APIFY_TOKEN`; without a token it returns a clear error.
- Tests run with no token (an env guard fails the suite if `APIFY_TOKEN` is set); CI and a daily workflow fail on drift between `tools.json` and the live public input schema.
- Dockerfile, glama.json, SECURITY.md and Dependabot config.

## Registry listing 1.0.0

- `server.json` for the official MCP Registry as a Streamable HTTP remote.
