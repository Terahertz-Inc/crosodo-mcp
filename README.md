# Crosodo MCP Server: cottage food law by state and county for AI agents

[Model Context Protocol](https://modelcontextprotocol.io) (MCP) server for [Crosodo](https://crosodo.com). Ask Claude, Cursor or any MCP client about cottage food and home bakery laws in every US state, county requirements, and Crosodo Certified credentials.

**Website:** [crosodo.com](https://crosodo.com) · **Developer docs:** [crosodo.com/developers](https://crosodo.com/developers)

| | |
|---|---|
| Endpoint | `https://crosodo.com/api/mcp` |
| Transport | Streamable HTTP |
| npm (stdio proxy) | [`crosodo-mcp`](https://www.npmjs.com/package/crosodo-mcp) |
| Registry name | `com.crosodo/mcp` (see [`server.json`](server.json)) |
| Auth | None needed for lookups |

## Tools

| Tool | What it does |
|---|---|
| `lookup_state_law` | Cottage food and home bakery rules for a US state: sales cap, registration, allowed products, statute and agency links |
| `lookup_county` | County-level cottage food requirements for a state and county: contacts, verification status and local links |
| `list_products` | The Crosodo product catalog, including the free state-law report |
| `start_checkout` | Creates a Stripe Checkout link and returns the URL. It never charges; payment only happens if the user completes Stripe's hosted page |
| `verify_certification` | Public lookup of a Crosodo Certified credential (format `CC-{ST}-{YY}-{XXXX}`; `CC-VA-26-1042` only illustrates the format and is not a real credential) |

The tool list comes from the live server, so it can grow without a new release here.

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
- "Is this Crosodo Certified credential valid?"

## Disclaimer

Cottage food laws change. Crosodo summaries come from a hand-maintained dataset and are **not legal advice**. Check with your state and county before you sell.

## Links

- [crosodo.com](https://crosodo.com) · [Developers](https://crosodo.com/developers)
- [npm package](https://www.npmjs.com/package/crosodo-mcp) · [Issues](../../issues)

## License

[MIT](LICENSE) © Terahertz, Inc.
