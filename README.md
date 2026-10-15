<!-- mcp-name: io.github.clearline-labs/public-data-mcp -->
# Public Data MCP

Remote MCP server that gives Claude, Cursor, VS Code, ChatGPT, n8n and any streamable-HTTP MCP client live access to official US public datasets, so your agent cites real numbers instead of guessing.

Hosted on Apify. Pay per successful call, no subscription.

- **Endpoint:** `https://intuitive-ytterbium--public-data-mcp.apify.actor/mcp` (streamable HTTP)
- **Auth:** `Authorization: Bearer <APIFY_TOKEN>` (free token at [apify.com](https://console.apify.com/settings/integrations))
- **Store page:** https://apify.com/intuitive_ytterbium/public-data-mcp
- **Website:** https://payoffpath-wv2.pages.dev/public-data-mcp-server/

## Tools

| Tool | What it does | Price |
|---|---|---|
| `search_recalls` | Recent CPSC, FDA (food/drug/device) and USDA FSIS recalls matching brands, products, UPCs or keywords | $0.01 |
| `vehicle_recalls` | NHTSA recalls for a make/model/year | $0.01 |
| `federal_contract_winners` | Top federal contract recipients by NAICS code and state (USAspending.gov) | $0.03 |
| `zip_income` | IRS Statistics of Income figures for up to 50 ZIP codes | $0.03 |
| `texas_new_businesses` | Newly issued Texas sales-tax permits by county, city, ZIP or NAICS | $0.03 |
| `domain_lookup` | Registrar, age, expiry, DNS, email provider, SPF/DMARC, SSL expiry | $0.01 |
| `website_tech_stack` | CMS, ecommerce, analytics, pixels, payments and CDN for up to 25 sites | $0.01 |

Charges are billed through your Apify account (Apify's free plan includes monthly credit).

## Setup

### Claude Desktop / Claude Code
```json
{
  "mcpServers": {
    "public-data": {
      "command": "npx",
      "args": ["-y", "mcp-remote", "https://intuitive-ytterbium--public-data-mcp.apify.actor/mcp", "--header", "Authorization: Bearer ${APIFY_TOKEN}"],
      "env": {"APIFY_TOKEN": "your-apify-token"}
    }
  }
}
```
Claude Code: `claude mcp add --transport http public-data https://intuitive-ytterbium--public-data-mcp.apify.actor/mcp --header "Authorization: Bearer YOUR_APIFY_TOKEN"`

### Cursor (`~/.cursor/mcp.json`)
```json
{
  "mcpServers": {
    "public-data": {
      "url": "https://intuitive-ytterbium--public-data-mcp.apify.actor/mcp",
      "headers": {"Authorization": "Bearer YOUR_APIFY_TOKEN"}
    }
  }
}
```

### VS Code (`.vscode/mcp.json`)
```json
{
  "inputs": [{"type": "promptString", "id": "apify-token", "description": "Apify API token", "password": true}],
  "servers": {
    "public-data": {
      "type": "http",
      "url": "https://intuitive-ytterbium--public-data-mcp.apify.actor/mcp",
      "headers": {"Authorization": "Bearer ${input:apify-token}"}
    }
  }
}
```

## Example prompts
- "Any FDA or USDA recalls mentioning listeria in the last 30 days?"
- "Who won the most NAICS 541511 contracts performed in Texas this year?"
- "Compare average income for ZIPs 77459, 77479 and 77489."
- "List new restaurants that got Texas sales-tax permits in Harris County this week."

## Data sources
CPSC, openFDA, USDA FSIS, NHTSA, USAspending.gov, IRS SOI, Texas Comptroller open data, public WHOIS/RDAP/DNS. Data is provided as-is from these public sources.

## License
MIT. This repo holds docs and registry metadata only; the server is hosted.
