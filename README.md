# LinkedIn Ads MCP

A Model Context Protocol (MCP) server that lets AI assistants (Claude, ChatGPT, Gemini, Cursor, Perplexity, or any MCP client) run LinkedIn Ads end to end. 34 typed tools with full write access, approval-gated writes, and 13 more ad and measurement platforms in the same session.

**Hosted at [paidsync.ai](https://paidsync.ai). Free plan: 100 tasks a month, no card required.**

[![MCP](https://img.shields.io/badge/MCP-server-black?logo=anthropic&logoColor=white)](https://modelcontextprotocol.io)
[![Hosted](https://img.shields.io/badge/hosted-paidsync.ai-0077B6)](https://paidsync.ai/linkedin-ads-mcp)
[![Free plan](https://img.shields.io/badge/free%20plan-100%20tasks%2Fmo-7CB518)](https://paidsync.ai/signup?plan=free)
[![License](https://img.shields.io/badge/license-MIT-green)](./LICENSE)

## What this is

PaidSync's LinkedIn Ads MCP surface, exposed to any AI assistant that speaks the Model Context Protocol. The full product page lives at [paidsync.ai/linkedin-ads-mcp](https://paidsync.ai/linkedin-ads-mcp). This repository is the developer entry point.

Three properties of this LinkedIn Ads MCP surface:

1. **34 LinkedIn tools with full write access.** Campaign group and campaign lifecycle, ad and creative management including `list_linkedin_creatives_with_media`, targeting patches on live campaigns (job function, seniority, industry, company size, member skills), conversion tracking creation, and performance breakdowns by campaign, creative, geography, job function, company size, and member age range.
2. **Every write is approval-gated.** Nothing reaches a live LinkedIn account until you approve the exact proposal in chat. Destructive writes need a second confirmation, most mutations have a dry-run preview, and sessions are revocable.
3. **13 more platforms in the same session.** Google Ads (158 tools), Microsoft Ads (156), Meta Ads (92), GTM (39), ChatGPT Ads (28), GA4 (26), TikTok Ads (24), Merchant Center (16), Snapchat Ads (15), Pinterest Ads (14), Reddit Ads (14), X Ads (14), Search Console (6). 630+ tools across 14 platforms in total. For B2B teams running LinkedIn alongside Google Ads and GA4, cross-platform attribution lands in one conversation.

## Getting started (hosted, recommended)

### Claude Desktop

```json
{
  "mcpServers": {
    "paidsync": {
      "url": "https://mcp.paidsync.ai/mcp"
    }
  }
}
```

No API key is needed: sign in when your client asks. Start free at [paidsync.ai/signup](https://paidsync.ai/signup?plan=free).

### claude.ai (web), ChatGPT, Gemini, Cursor, Windsurf, Perplexity

Setup guides:
- [Connect LinkedIn Ads to Claude](https://paidsync.ai/blog/connect-linkedin-ads-to-claude)
- [Connect LinkedIn Ads to ChatGPT](https://paidsync.ai/blog/connect-linkedin-ads-to-chatgpt)
- [Connect LinkedIn Ads to Gemini](https://paidsync.ai/blog/connect-linkedin-ads-to-gemini)
- [Connect LinkedIn Ads to Perplexity](https://paidsync.ai/blog/connect-linkedin-ads-to-perplexity)
- [Connect LinkedIn Ads to Copilot](https://paidsync.ai/blog/connect-linkedin-ads-to-copilot)

## First call

```
paidsync_context({ include_tools: ['linkedin_ads'] })
paidsync_exec({ tool: 'get_linkedin_performance', args: { date_range: 'last_30_days' } })
```

## Examples

Runnable configs and copy-paste prompts live in [`examples/`](./examples).

| File | What it is |
|---|---|
| [`examples/claude_desktop_config.json`](./examples/claude_desktop_config.json) | Claude Desktop config block |
| [`examples/claude_code.md`](./examples/claude_code.md) | The `claude mcp add` command and how to verify it connected |
| [`examples/cursor_mcp.json`](./examples/cursor_mcp.json) | Cursor `.cursor/mcp.json` |
| [`examples/windsurf_mcp_config.json`](./examples/windsurf_mcp_config.json) | Windsurf `mcp_config.json` |
| [`examples/prompts.md`](./examples/prompts.md) | 15 LinkedIn Ads prompts mapped to the tools below |

Installing this as an AI agent, read [llms-install.md](./llms-install.md). Filing a bug or a tool request, read [CONTRIBUTING.md](./CONTRIBUTING.md).

## Tools by category

| Category | Named tools |
|---|---|
| Account and identity | `connect_linkedin_ads`, `list_linkedin_ad_accounts`, `set_linkedin_ad_account` |
| Campaign groups | `list_linkedin_campaign_groups`, `create_linkedin_campaign_group`, `update_linkedin_campaign_group` |
| Campaigns | `list_linkedin_campaigns`, `create_linkedin_campaign`, `update_linkedin_campaign`, `pause_linkedin_campaign`, `enable_linkedin_campaign` |
| Ads and creatives | `create_linkedin_ad`, `list_linkedin_creatives`, `create_linkedin_creative`, `update_linkedin_creative`, `list_linkedin_creatives_with_media` |
| Audience and targeting | `get_linkedin_campaign_targeting`, `update_linkedin_campaign_targeting` |
| Conversions | `list_linkedin_conversions`, `create_linkedin_conversion` |
| Performance reporting | `get_linkedin_performance`, `get_linkedin_performance_by_dimension` |

Full live catalog at `paidsync_context({ include_tools: ['linkedin_ads'] })`.

## Pricing

| Plan | Price | Tasks | Notes |
|---|---|---|---|
| Free | $0/mo | 100 | No card required, all 14 platforms |
| Pro | From $99/mo | 1,000 to 6,000 | 1 seat, solo operators and small teams |
| Team | From $249/mo | 10,000 shared | Entry tier is up to 20 seats, larger tiers on paidsync.ai/pricing |
| Done For You | Custom | Managed | PaidSync runs the accounts |

## Safety model

- Approval-gated. Every write is a proposal shown in chat before it applies.
- Dry-run previews on most mutations.
- Destructive-write second confirmation required.
- Revocable sessions.
- Rate-limit aware. LinkedIn's Marketing API is tighter than Google or Meta for some account classes; PaidSync's polling loops build in back-off.

## What this surface gives you

| | PaidSync LinkedIn Ads MCP |
|---|---|
| LinkedIn tools | 34 native |
| Write access | Full, approval-gated |
| Approval gates on writes | Yes, on every write |
| Platform scope in same session | 14 platforms |
| Conversion tracking creation | Yes, `create_linkedin_conversion` |
| Price | Free $0 (100 tasks), Pro from $99/mo |

Vendor by vendor comparisons go stale as products ship, so they are kept dated and sourced on the product page rather than here. See [paidsync.ai/linkedin-ads-mcp](https://paidsync.ai/linkedin-ads-mcp).

## License

MIT. See [LICENSE](./LICENSE).

## Links

- Product page: [paidsync.ai/linkedin-ads-mcp](https://paidsync.ai/linkedin-ads-mcp)
- MCP server overview: [paidsync.ai/mcp-server](https://paidsync.ai/mcp-server)
- Category guide: [Best MCP for LinkedIn Ads in 2026](https://paidsync.ai/blog/best-mcp-for-linkedin-ads)
- LinkedIn prompts for Claude: [15 LinkedIn Ads prompts for Claude](https://paidsync.ai/blog/15-linkedin-ads-prompts-for-claude)
- Support: support@paidsync.ai

Built by [Ahmed Ashraf](https://paidsync.ai/about/ahmed-ashraf), $500M+ in managed ad spend.
