# Facebook Reels Scraper MCP Server

[![Glama score](https://glama.ai/mcp/servers/mambalabsdev/mcp-facebook-reels-scraper/badges/score.svg)](https://glama.ai/mcp/servers/mambalabsdev/mcp-facebook-reels-scraper) [![MCP Registry](https://img.shields.io/badge/dynamic/json?url=https%3A%2F%2Fregistry.modelcontextprotocol.io%2Fv0%2Fservers%3Fsearch%3Dcom.mambabuilt%252Fmcp-facebook-reels-scraper%26limit%3D1&query=%24.servers%5B0%5D._meta%5B%22io.modelcontextprotocol.registry%2Fofficial%22%5D.status&label=mcp%20registry&color=blue)](https://registry.modelcontextprotocol.io/v0/servers?search=com.mambabuilt/mcp-facebook-reels-scraper&limit=1) [![npm version](https://img.shields.io/npm/v/@mambalabsdev/mcp-facebook-reels-scraper)](https://www.npmjs.com/package/@mambalabsdev/mcp-facebook-reels-scraper) [![npm downloads](https://img.shields.io/npm/dm/@mambalabsdev/mcp-facebook-reels-scraper)](https://www.npmjs.com/package/@mambalabsdev/mcp-facebook-reels-scraper) [![license](https://img.shields.io/github/license/mambalabsdev/mcp-facebook-reels-scraper)](https://github.com/mambalabsdev/mcp-facebook-reels-scraper/blob/main/LICENSE)

An MCP server for the Mamba Labs Facebook Reels Scraper actor on Apify. Public Facebook Page reels with plays, as rows.

## What's Inside

- [What it does](#what-it-does)
- [Quick start](#quick-start)
- [Prerequisites](#prerequisites)
- [Example prompts](#example-prompts)
- [Tool](#tool)
- [Inputs](#inputs)
- [Pricing](#pricing)
- [Full actor documentation](#full-actor-documentation)
- [License](#license)

## What it does

Takes public Facebook Page names or addresses and returns one row per reel with plays, reactions, comments, shares, caption, date, length, and link.

All of the work runs on Apify. This package is a thin client that starts the actor run, waits for it, and hands back the dataset rows.

## Quick start

You need Node.js 18 or newer and an Apify account with an API token.

Add this to your Claude Desktop config (`claude_desktop_config.json`), Cursor, or any MCP client:

```json
{
  "mcpServers": {
    "mamba-facebook-reels-scraper": {
      "command": "npx",
      "args": [
        "-y",
        "@mambalabsdev/mcp-facebook-reels-scraper"
      ],
      "env": {
        "APIFY_TOKEN": "your-apify-token"
      }
    }
  }
}
```

Restart the client. The `get_facebook_page_reels` tool appears.

## Prerequisites

- Node.js 18 or newer.
- An Apify API token from [console.apify.com/account/integrations](https://console.apify.com/account/integrations), set as `APIFY_TOKEN`. The server lists its tool without a token; a call needs one.

## Example prompts

- "Get the last 20 reels from the National Geographic Facebook Page with their plays."
- "Which of these Facebook Pages' reels since 2026-10-01 got the most plays?"

## Tool

`get_facebook_page_reels`. One tool. Example arguments:

```json
{
  "pages": [
    "natgeo"
  ],
  "max_reels_per_page": 5
}
```

## Inputs

Every buyer facing input of the actor. Omitted inputs take the actor's own defaults.

| Input | Type | Required | Description |
|---|---|---|---|
| `pages` | array | no | Public Page names or facebook.com addresses, for example natgeo or https://www.facebook.com/natgeo/reels/. Groups and personal profiles are not read. In Clay, put the column inside a one item list. |
| `max_reels_per_page` | number | no | Text number from 1 to 300. Default 20. Newest reels first. |
| `since_date` | string | no | Optional date like 2026-01-31. Reading stops at the first reel older than this. |
| `max_charge_usd` | number | no | Optional. The run stops before a charge that would pass this amount. Summary rows are always returned. |

## Pricing

Pay per event on Apify, billed to your Apify account. Prices in USD.

| Event | Free plan | Bronze | Silver | Gold |
|---|---|---|---|---|
| `reel-row`, one reel | $0.005 | $0.00475 | $0.0045 | $0.00425 |
| `apify-actor-start`, per run start | $0.007 | $0.007 | $0.007 | $0.007 |

Page status rows and refused input are free. Mamba Labs pays the platform costs of the run, Apify proxy traffic included.

## Full actor documentation

[apify.com/mambalabs/facebook-reels-scraper](https://apify.com/mambalabs/facebook-reels-scraper)

## License

MIT. See [LICENSE](LICENSE).
