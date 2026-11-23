# Google Ads Transparency MCP: Competitor Ads

An MCP server that tells your AI assistant which Google ads a competitor is running. Give it a website domain (`nike.com`), a Google advertiser ID, an Ads Transparency Center link or an exact advertiser name, and it returns the ads Google lists for that advertiser: which are **new**, **still running** or **stopped** in your look-back window, with first and last shown dates, days shown and links to each ad. Filter by country, or leave it on "anywhere". No Google login and no proxy setup.

Built on the public [Google Ads Transparency Center](https://adstransparency.google.com/) data, via the Apify Actor [Google Ads Transparency Scraper](https://apify.com/publicrecords/google-ads-transparency-scraper).

- Apify Store: https://apify.com/publicrecords/google-ads-transparency-scraper
- MCP server: https://mcp.apify.com?tools=publicrecords/google-ads-transparency-scraper

## Example prompts

- "Which Google ads did nike.com start running in the last 7 days in the US?"
- "Compare the ads running right now for hubspot.com and salesforce.com."
- "List the ads my competitor stopped this month, with first and last shown dates."

## Tool

| Tool | Input | Output |
| --- | --- | --- |
| `publicrecords--google-ads-transparency-scraper` | `targets` (domains, advertiser IDs, Transparency Center links or names), `sinceDays`, `region`, `statuses` | One row per ad: advertiser, ad ID, format (text, image, video), status, first and last shown dates, days shown, target domain and the ad link |

The full input schema is in [`tools.json`](tools.json), generated from the Actor's public input schema and checked for drift daily.

<!-- one-click-install:start -->
## One-click install

[![Install in VS Code](https://img.shields.io/badge/VS_Code-Install_MCP-0098FF?logo=visualstudiocode&logoColor=white)](https://insiders.vscode.dev/redirect/mcp/install?name=google-ads-transparency-mcp&config=%7B%22type%22%3A%22http%22%2C%22url%22%3A%22https%3A%2F%2Fmcp.apify.com%3Ftools%3Dpublicrecords%2Fgoogle-ads-transparency-scraper%22%7D) [![Install in VS Code Insiders](https://img.shields.io/badge/VS_Code_Insiders-Install_MCP-24bfa5?logo=visualstudiocode&logoColor=white)](https://insiders.vscode.dev/redirect/mcp/install?name=google-ads-transparency-mcp&config=%7B%22type%22%3A%22http%22%2C%22url%22%3A%22https%3A%2F%2Fmcp.apify.com%3Ftools%3Dpublicrecords%2Fgoogle-ads-transparency-scraper%22%7D&quality=insiders) [![Add to Cursor](https://img.shields.io/badge/Cursor-Add_MCP-000000?logo=cursor&logoColor=white)](https://cursor.com/en/install-mcp?name=google-ads-transparency-mcp&config=eyJ1cmwiOiJodHRwczovL21jcC5hcGlmeS5jb20%2FdG9vbHM9cHVibGljcmVjb3Jkcy9nb29nbGUtYWRzLXRyYW5zcGFyZW5jeS1zY3JhcGVyIn0%3D)

Other clients (all use the same Streamable HTTP endpoint; sign in with Apify OAuth or send `Authorization: Bearer <APIFY_TOKEN>` with your own token):

| Client | Setup |
| --- | --- |
| Claude Code | `claude mcp add --transport http google-ads-transparency-mcp "https://mcp.apify.com?tools=publicrecords/google-ads-transparency-scraper"` |
| Gemini CLI | `gemini mcp add --transport http google-ads-transparency-mcp "https://mcp.apify.com?tools=publicrecords/google-ads-transparency-scraper"` |
| Codex CLI | `~/.codex/config.toml`: `[mcp_servers.google_ads_transparency_mcp]` then `url = "https://mcp.apify.com?tools=publicrecords/google-ads-transparency-scraper"` |
| Zed | `settings.json`: `"context_servers": { "google-ads-transparency-mcp": { "url": "https://mcp.apify.com?tools=publicrecords/google-ads-transparency-scraper" } }` |
| JetBrains AI Assistant | Settings, Tools, AI Assistant, Model Context Protocol, Add: `{"mcpServers": {"google-ads-transparency-mcp": {"url": "https://mcp.apify.com?tools=publicrecords/google-ads-transparency-scraper"}}}` |
| Windsurf / Devin Desktop, Cline, Roo Code, Kiro, Goose, LibreChat, Cherry Studio | Add a remote (Streamable HTTP) server with the URL above |

Also listed in the [Official MCP Registry](https://registry.modelcontextprotocol.io/v0.1/servers?search=GeminiGeorge22), which Zed and VS Code read from.
<!-- one-click-install:end -->

## MCP endpoint

```
https://mcp.apify.com?tools=publicrecords/google-ads-transparency-scraper
```

Transport: Streamable HTTP (hosted by Apify, see https://docs.apify.com/mcp).

## Auth

Sign in with Apify OAuth when your client prompts you, or send the header
`Authorization: Bearer <APIFY_TOKEN>` where `<APIFY_TOKEN>` is your own Apify API token.
Never commit a real token.

## Client setup

### Claude

Claude Code:

```
claude mcp add --transport http google-ads-transparency "https://mcp.apify.com?tools=publicrecords/google-ads-transparency-scraper"
```

Claude Desktop / claude.ai: Settings → Connectors → Add custom connector, and paste the MCP endpoint URL above.

### Cursor

`~/.cursor/mcp.json`:

```json
{
  "mcpServers": {
    "google-ads-transparency": {
      "url": "https://mcp.apify.com?tools=publicrecords/google-ads-transparency-scraper"
    }
  }
}
```

### VS Code

`.vscode/mcp.json`:

```json
{
  "servers": {
    "google-ads-transparency": {
      "type": "http",
      "url": "https://mcp.apify.com?tools=publicrecords/google-ads-transparency-scraper"
    }
  }
}
```

To use a token instead of OAuth, add `"headers": { "Authorization": "Bearer <APIFY_TOKEN>" }` next to `"url"`.

---

Disclosure: I maintain this Actor.

## Local stdio server (open source)

This repo also ships a small MCP server in [`src/`](src/) for clients that only run local stdio servers. It answers `initialize` and `tools/list` locally from [`tools.json`](tools.json), which is generated from each Actor's public input schema and checked for drift in CI and weekly, so any client or directory can inspect the tools with no token. `tools/call` is forwarded to the hosted Apify MCP endpoint above with **your own** `APIFY_TOKEN`; without a token a call returns a clear error instead of running anything. The token is only sent in the `Authorization` header and is never logged.

```json
{
  "mcpServers": {
    "google-ads-transparency": {
      "command": "npx",
      "args": ["-y", "github:GeminiGeorge22/google-ads-transparency-mcp"],
      "env": { "APIFY_TOKEN": "YOUR_APIFY_TOKEN" }
    }
  }
}
```

Or from a clone:

```bash
git clone https://github.com/GeminiGeorge22/google-ads-transparency-mcp.git
cd google-ads-transparency-mcp && npm install
APIFY_TOKEN=YOUR_APIFY_TOKEN node src/server.js
```

Optional env: `APIFY_ACTORS` (comma-separated subset of the Actors above) and `APIFY_MCP_URL` (full endpoint override).

Tests run against an in-memory mock server, with no network and no token: `npm test`. Requires Node.js 18+.

### Python (uvx/pip)

A matching Python version of this server lives in [`python/`](python/), built on the official `mcp` Python SDK: same tools, same `APIFY_TOKEN`, same hosted endpoint. Requires Python 3.10+.

```json
{
  "mcpServers": {
    "google-ads-transparency": {
      "command": "uvx",
      "args": ["google-ads-transparency-mcp-server"],
      "env": { "APIFY_TOKEN": "YOUR_APIFY_TOKEN" }
    }
  }
}
```

Or with pip: `pip install google-ads-transparency-mcp-server`, then run `google-ads-transparency-mcp-server`. Python tests: `cd python && pip install -e ".[test]" && env -u APIFY_TOKEN python -m pytest`.

## See also

- [Awesome Ad Intelligence MCP](https://github.com/GeminiGeorge22/awesome-ad-intelligence-mcp): a curated list of MCP servers and tools for competitor ads, ad libraries and ad intelligence, from many providers.
- [ecommerce-search-rankings-mcp](https://github.com/GeminiGeorge22/ecommerce-search-rankings-mcp): E-commerce search results and product rankings across Amazon, eBay, Walmart, Google Shopping, AliExpress, Shopify and Etsy.
- [ecommerce-sales-mcp](https://github.com/GeminiGeorge22/ecommerce-sales-mcp): E-commerce sales signals: Amazon bestsellers and reviews, eBay sold prices, TikTok Shop and Etsy shop sales.
- [forecast-accuracy-mcp](https://github.com/GeminiGeorge22/forecast-accuracy-mcp): Forecast accuracy and track records: forecasts vs actuals, earnings beats, prediction markets, archived pages and news.
- [ats-jobs-mcp](https://github.com/GeminiGeorge22/ats-jobs-mcp): New job postings from Greenhouse, Lever, Ashby and SmartRecruiters.
- [gov-tenders-mcp](https://github.com/GeminiGeorge22/gov-tenders-mcp): Government tenders, grants, awards and council meetings.
