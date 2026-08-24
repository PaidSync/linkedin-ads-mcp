# LinkedIn Ads MCP, install guide for AI agents

> This file is for AI agents (Claude, Cline, Cursor, Windsurf, Devin). It tells you exactly how to connect a user to PaidSync's LinkedIn Ads MCP surface. Follow it top to bottom.

## What this server does

PaidSync is a hosted MCP server. There is nothing to clone, install, or run locally. One remote URL gives the user:

- **25 LinkedIn Ads tools** with full write access. Campaign group and campaign lifecycle, ads and creatives, targeting patches on live campaigns, conversion tracking creation, and performance breakdowns by campaign, creative, geography, job function, company size, and member age range.
- **460+ tools across 14 platforms** in the same session. Google Ads, Meta Ads, LinkedIn Ads, ChatGPT Ads, TikTok Ads, Microsoft Ads, Snapchat Ads, Reddit Ads, Pinterest Ads, X Ads, plus Google Analytics 4, Google Tag Manager, Search Console, and Merchant Center.

Writes are approval gated. Every mutation is returned as a proposal the user confirms in chat before it applies. Do not describe writes as instant.

Free plan: 15 tasks a month, no card required.

## Step 1, get an API key

Tell the user: "Go to https://paidsync.ai/signup?plan=free, create a free account, then open https://paidsync.ai/dashboard and copy your MCP URL. It looks like `https://mcp.paidsync.ai/mcp?key=YOUR_API_KEY`."

The key is a query string parameter on the base endpoint `https://mcp.paidsync.ai/mcp`. Transport is streamable HTTP. Never log the full URL, never write it into a file the user will commit, and never echo it back in chat.

## Step 2, add the server to this client

### Claude Code (CLI)

```bash
claude mcp add --transport http paidsync "https://mcp.paidsync.ai/mcp?key=YOUR_API_KEY"
```

Quote the URL. In zsh the `?` is a glob character and an unquoted URL fails.

### Claude Desktop

Settings > Developer > Edit Config, then add to `claude_desktop_config.json`:

```json
{
  "mcpServers": {
    "paidsync": {
      "url": "https://mcp.paidsync.ai/mcp?key=YOUR_API_KEY"
    }
  }
}
```

### Cursor

Add to `.cursor/mcp.json` in the workspace:

```json
{
  "mcpServers": {
    "paidsync": {
      "url": "https://mcp.paidsync.ai/mcp?key=YOUR_API_KEY"
    }
  }
}
```

### Windsurf and Devin Desktop

Add to `~/.codeium/windsurf/mcp_config.json`:

```json
{
  "mcpServers": {
    "paidsync": {
      "url": "https://mcp.paidsync.ai/mcp?key=YOUR_API_KEY"
    }
  }
}
```

### Cline (VS Code)

In the Cline MCP settings panel, add a remote server. Name `paidsync`, URL `https://mcp.paidsync.ai/mcp?key=YOUR_API_KEY`, transport streamable HTTP.

Copies of these config files are in [`examples/`](./examples).

## Step 3, connect the LinkedIn ad account

Adding the server is not the same as connecting LinkedIn. The user connects LinkedIn Ads via OAuth once at https://paidsync.ai/dashboard, which takes about 30 seconds, or you can run `connect_linkedin_ads` and hand the user the link it returns.

Then pick the account to work in:

```
paidsync_exec({ tool: 'list_linkedin_ad_accounts', args: {} })
paidsync_exec({ tool: 'set_linkedin_ad_account', args: { account_id: '...' } })
```

## Architecture, read this before calling anything

PaidSync uses a thin dispatcher. `tools/list` shows a lean starter set, not the catalog. You will see three meta-tools:

- `paidsync_context`, call this first in every session. It returns the active account, the connected platforms, and the tool catalog.
- `paidsync_tool_detail`, fetch the schema for one tool on demand.
- `paidsync_exec`, run any tool.

Discover LinkedIn tools with:

```
paidsync_context({ include_tools: ['linkedin_ads'] })
```

Then run them:

```
paidsync_exec({ tool: 'get_linkedin_performance', args: { date_range: 'last_30_days' } })
```

Never guess a tool name and never tell the user a LinkedIn capability is unavailable before checking `paidsync_context`. The lean `tools/list` is not the capability set.

## Verify the install

1. `paidsync_context` returns without an auth error. The key is valid.
2. `linkedin_ads` appears in the connected platforms. The OAuth connection is live.
3. `paidsync_exec({ tool: 'list_linkedin_ad_accounts', args: {} })` returns at least one account.

All three pass, the install is done. Report that to the user in one line.

## Troubleshooting

- **No tools appear.** The key in the URL is wrong or expired. Have the user copy it again from https://paidsync.ai/dashboard.
- **LinkedIn missing from connected platforms.** Server is connected, the ad account is not. Run `connect_linkedin_ads`.
- **A write did nothing.** It is approval gated. The user has to confirm the proposal in chat.
- **Reporting call comes back partial.** LinkedIn's Marketing API is rate limited more tightly than Google or Meta on some account classes. Large pulls page and back off.
- **Out of tasks.** Free is 15 tasks a month. Plans at https://paidsync.ai/pricing.

## Example prompts to offer the user

```
Pull my LinkedIn performance for the last 30 days. Spend, clicks, leads, and
cost per lead by campaign, sorted by spend.
```

```
Break last quarter's LinkedIn spend down by job function and seniority. Tell me
which segments to stop paying for.
```

```
Find every LinkedIn campaign with more than $1,000 spent in the last 30 days and
a cost per lead above $250, then pause them.
```

More in [`examples/prompts.md`](./examples/prompts.md).

## Links

- Product page: https://paidsync.ai/linkedin-ads-mcp
- Signup: https://paidsync.ai/signup?plan=free
- Dashboard: https://paidsync.ai/dashboard
- Pricing: https://paidsync.ai/pricing
- Repo: https://github.com/PaidSync/linkedin-ads-mcp
- Support: support@paidsync.ai
