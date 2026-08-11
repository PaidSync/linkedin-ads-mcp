# LinkedIn Ads MCP

A Model Context Protocol (MCP) server that lets AI assistants (Claude, ChatGPT, Gemini, Cursor, Perplexity, or any MCP client) run LinkedIn Ads end to end. 25 typed tools with full write access, verified LinkedIn Marketing Partner, approval-gated writes, and 12 more ad and measurement platforms in the same session.

**Hosted at [paidsync.ai](https://paidsync.ai). Free plan: 15 tasks a month, no card required.**

[![MCP](https://img.shields.io/badge/MCP-server-black?logo=anthropic&logoColor=white)](https://modelcontextprotocol.io)
[![Hosted](https://img.shields.io/badge/hosted-paidsync.ai-0077B6)](https://paidsync.ai/linkedin-ads-mcp)
[![Free plan](https://img.shields.io/badge/free%20plan-15%20tasks%2Fmo-7CB518)](https://paidsync.ai/signup?plan=free)
[![LinkedIn Marketing Partner](https://img.shields.io/badge/LinkedIn-Marketing%20Partner-0A66C2?logo=linkedin)](https://paidsync.ai/linkedin-ads-mcp)
[![License](https://img.shields.io/badge/license-MIT-green)](./LICENSE)

## What this is

PaidSync's LinkedIn Ads MCP surface, exposed to any AI assistant that speaks the Model Context Protocol. The full product page lives at [paidsync.ai/linkedin-ads-mcp](https://paidsync.ai/linkedin-ads-mcp). This repository is the developer entry point.

Three properties that set this LinkedIn Ads MCP apart from every current option:

1. **25 LinkedIn tools with full write access.** Campaign group and campaign lifecycle, ad and creative management including `list_linkedin_creatives_with_media`, targeting patches on live campaigns (job function, seniority, industry, company size, member skills), conversion tracking creation, and performance breakdowns by campaign, creative, geography, job function, company size, and member age range.
2. **Verified LinkedIn Marketing Partner.** Adzviser is read-only. Adkit added LinkedIn write access in July 2026 but without approval gates. PaidSync is the only LinkedIn Ads MCP that combines write access, approval gates, and verified Marketing Partner status.
3. **12 more platforms in the same session.** Google Ads (136 tools), Meta Ads (69), TikTok (13), GA4 (28), GTM (37), Search Console (6), Merchant Center (15), plus Microsoft, Snapchat, Reddit, Pinterest, and ChatGPT Ads. For B2B teams running LinkedIn alongside Google Ads and GA4, cross-platform attribution lands in one conversation.

## Getting started (hosted, recommended)

### Claude Desktop

```json
{
  "mcpServers": {
    "paidsync": {
      "url": "https://mcp.paidsync.ai/mcp?key=YOUR_API_KEY"
    }
  }
}
```

Get your API key at [paidsync.ai/signup](https://paidsync.ai/signup?plan=free).

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
| Free | $0/mo | 15 | No card required, all 13 platforms |
| Pro | From $99/mo | 600 to 4,000 | Solo operators and small teams |
| Team | From $249/mo | 6,000 shared | 5 seats included |
| Done For You | Custom | Managed | PaidSync runs the accounts |

## Safety model

- Approval-gated. Every write is a proposal shown in chat before it applies.
- Dry-run previews on most mutations.
- Destructive-write second confirmation required.
- Revocable sessions.
- Rate-limit aware. LinkedIn's Marketing API is tighter than Google or Meta for some account classes; PaidSync's polling loops build in back-off.

## Compared with other LinkedIn Ads MCP options

| | PaidSync | Adkit | Adzviser |
|---|---|---|---|
| LinkedIn tools | 25 native | Subset of 23 total | Reporting connector |
| Write access | Full, gated | Yes, ungated | Read-only |
| Approval gates on writes | Yes | No, applies immediately | Not applicable |
| Platform scope in same session | 13 platforms | Google, Meta, LinkedIn | 45+ sources, reporting only |
| LinkedIn Marketing Partner | Yes, company-verified | Not listed | Not listed |
| Conversion tracking creation | Yes, `create_linkedin_conversion` | Not listed | No |
| Price | Free $0 (15 tasks), Pro from $99/mo | $29 to $49/year | $48.99 to $148.99/month |

Full comparison at [paidsync.ai/linkedin-ads-mcp](https://paidsync.ai/linkedin-ads-mcp).

## License

MIT. See [LICENSE](./LICENSE).

## Links

- Product page: [paidsync.ai/linkedin-ads-mcp](https://paidsync.ai/linkedin-ads-mcp)
- MCP server overview: [paidsync.ai/mcp-server](https://paidsync.ai/mcp-server)
- Category guide: [Best MCP for LinkedIn Ads in 2026](https://paidsync.ai/blog/best-mcp-for-linkedin-ads)
- LinkedIn prompts for Claude: [15 LinkedIn Ads prompts for Claude](https://paidsync.ai/blog/15-linkedin-ads-prompts-for-claude)
- Support: support@paidsync.ai

Built by [Ahmed Ashraf](https://paidsync.ai/about/ahmed-ashraf), $500M+ in managed ad spend.
