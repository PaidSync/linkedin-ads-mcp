# Contributing

The LinkedIn Ads MCP server itself is hosted at `https://mcp.paidsync.ai/mcp` and its source is closed. This repository is the developer entry point: the tool reference, the client configs in [`examples/`](./examples), the prompt library, and the agent install guide. All of that is open to contributions.

## Report a tool bug

A tool bug is a LinkedIn tool that errors, returns the wrong numbers, or silently does nothing. Open a GitHub issue on this repo, or email support@paidsync.ai if the report contains account data you do not want public.

Include:

1. The tool name, for example `update_linkedin_campaign_targeting`.
2. The exact `paidsync_exec` call you ran, with the args. Redact the API key.
3. What you expected and what came back, error text included.
4. The LinkedIn ad account ID and the approximate timestamp in UTC. That is what lets us find the request in the logs.
5. Your MCP client and version, for example Claude Desktop or Claude Code.

Do not paste your API key, an access token, or a refresh token into an issue. If one has already been posted, email support@paidsync.ai and we will rotate it.

## Request a tool

LinkedIn Ads currently exposes 25 tools here. If the operation you need is missing, open an issue titled `Tool request: <what it does>` or email support@paidsync.ai.

Include:

1. The LinkedIn Marketing API endpoint or object it maps to, if you know it.
2. Read or write, and whether a write on it is reversible.
3. The workflow it unblocks. One real scenario beats a feature list.

Tool requests are triaged against the live registry. If the LinkedIn API does not expose the operation, we will say so in the issue rather than leave it open.

## Contribute to this repo directly

- A client config for an MCP client `examples/` does not cover yet.
- A prompt for `examples/prompts.md`. It must use tool names that exist in the README, and it must be paste ready.
- A documentation fix. Wrong number, dead link, unclear wording.
- A row in the comparison table. If you maintain a competing LinkedIn Ads MCP and the table is wrong about you, open a PR with your data.

How: fork, branch (`git checkout -b prompt-abm-targeting`), one topic per PR, and say in the description what you added and the real scenario it applies to. We review weekly.

## Out of scope

- Server source code. It is a hosted managed service.
- Pricing and plan changes. Those are set by the PaidSync team.
- Numbers that are not in the live registry. Tool counts in this repo have to match what `paidsync_context` returns.

## Style rules

- Plain English. No "supercharge", no "unleash".
- No em dashes. Use commas, periods, or restructure.
- Specific beats vague. "Pause campaigns above $250 cost per lead" beats "optimize underperformers".
- Never invent a tool name. Check it against `paidsync_context({ include_tools: ['linkedin_ads'] })` first.

## License

By contributing you agree your contribution is licensed under MIT, the same as this repo.
