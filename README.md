# Crosodo MCP Server: cottage food law by state and county for AI agents

[![npm](https://img.shields.io/npm/v/crosodo-mcp.svg)](https://www.npmjs.com/package/crosodo-mcp)
[![MCP Registry](https://img.shields.io/badge/MCP%20Registry-listed-green)](https://registry.modelcontextprotocol.io/v0.1/servers?search=com.crosodo%2Fmcp)
[![License: MIT](https://img.shields.io/badge/license-MIT-blue.svg)](LICENSE)


[Model Context Protocol](https://modelcontextprotocol.io) (MCP) server for [Crosodo](https://crosodo.com). Ask Claude, Cursor or any MCP client about cottage food and home bakery laws in every US state, county permit checklists, which foods you can sell, compliant labels, and Crosodo Certified credentials.

**Website:** [crosodo.com](https://crosodo.com) · **Developer docs:** [crosodo.com/developers](https://crosodo.com/developers)

| | |
|---|---|
| Endpoint | `https://crosodo.com/api/mcp` |
| Transport | Streamable HTTP |
| npm (stdio proxy) | [`crosodo-mcp`](https://www.npmjs.com/package/crosodo-mcp) |
| Registry name | `com.crosodo/mcp` (see [`server.json`](server.json)) |
| Auth | None for public tools; OAuth (`crosodo:read` / `crosodo:write`) for account tools |

## Tools

As of server version 1.1.0.

**Public (no sign-in)**

| Tool | What it does |
|---|---|
| `lookup_state_law` | Cottage food and home bakery rules for a US state: sales cap, registration, allowed products, statute and agency links |
| `lookup_county` | County-level cottage food requirements for a state and county: contacts, verification status and local links |
| `get_four_box_checklist` | Any county's or independent city's 4-Box permit checklist: Food/Health, Zoning, Business License and Sales Tax, with fees, official .gov links and filing order |
| `check_food_legality` | "Can I sell this?" verdict for a food in a state (43 foods across 51 jurisdictions), with the statute and whether an inspected kitchen is needed |
| `generate_compliant_label` | State-compliant label preview: ingredients by weight, FDA Big-9 allergen detection and the state's required disclaimer. Pass `save: true` when signed in to save it |
| `list_products` | The Crosodo product catalog, including the free state-law report |
| `start_checkout` | Creates a Stripe Checkout link and returns the URL. It never charges; payment only happens if the user completes Stripe's hosted page |
| `verify_certification` | Public lookup of a Crosodo Certified credential (format `CC-{ST}-{YY}-{XXXX}`; `CC-VA-26-1042` only illustrates the format and is not a real credential) |

**Account (OAuth sign-in; `crosodo:read` for reads, `crosodo:write` for writes)**

| Tool | What it does |
|---|---|
| `get_my_dashboard` | The signed-in baker's dashboard summary |
| `get_permit_checklist` | The baker's county permit checklist and which steps are done |
| `set_permit_step` | Check or uncheck one permit step |
| `setup_bakery_business` | Save county, ladder rung (Hobby, Cottage Food, Inspected Kitchen, Commercial) and business name |
| `configure_storefront_profile` | Claim or update a public storefront at `crosodo.com/p/{handle}` |
| `log_sale` / `log_expense` | Add a sale or an expense to the Financials tab |
| `save_recipe` | Save or update a recipe |

## Prompts

| Prompt | What it does |
|---|---|
| `launch_home_bakery` | Set county and ladder rung, walk the 4 permit boxes, check the menu and outline next filing steps |
| `explain_four_box_permits` | Break down Food/Health, Zoning, Business License and Sales Tax for a county or city |
| `audit_recipe_and_label` | Sort ingredients, detect Big-9 allergens and draft a compliant state label |
| `weekly_market_closeout` | Log a week's sales and expenses and check progress against the state sales cap |

The tool and prompt lists come from the live server, so they can grow without a new release here.

## Install

### Remote (Claude custom connector, Cursor, any Streamable HTTP client)

```json
{
  "mcpServers": {
    "crosodo": { "url": "https://crosodo.com/api/mcp" }
  }
}
```

### Stdio (Claude Desktop and other stdio clients)

Requires Node.js 18+.

```json
{
  "mcpServers": {
    "crosodo": { "command": "npx", "args": ["-y", "crosodo-mcp"] }
  }
}
```

### Muse

```json
{
  "mcpServers": {
    "crosodo": { "transport": "streamable_http", "url": "https://crosodo.com/api/mcp" }
  }
}
```

## Example prompts

- "Can I sell cookies from my home kitchen in Virginia? What's the sales cap?"
- "What does Fairfax County require for a cottage food business?"
- "Compare cottage food rules in Texas and California."
- "Can I sell salsa from home in Texas?"
- "Make a compliant label for my banana bread in Virginia."
- "Is this Crosodo Certified credential valid?"

## Disclaimer

Cottage food laws change. Crosodo summaries come from a hand-maintained dataset and are **not legal advice**. Check with your state and county before you sell.

## Links

- [crosodo.com](https://crosodo.com) · [Developers](https://crosodo.com/developers)
- [npm package](https://www.npmjs.com/package/crosodo-mcp) · [Issues](../../issues)

## License

[MIT](LICENSE) © Terahertz, Inc.
