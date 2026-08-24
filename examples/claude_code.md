# Claude Code setup

PaidSync is a hosted MCP server, so there is nothing to clone, build, or run locally. You add one remote URL.

## 1. Get an API key

Create a free account at https://paidsync.ai/signup?plan=free, open https://paidsync.ai/dashboard, and copy your MCP URL. It looks like this.

```
https://mcp.paidsync.ai/mcp?key=YOUR_API_KEY
```

## 2. Add the server

```bash
claude mcp add --transport http paidsync "https://mcp.paidsync.ai/mcp?key=YOUR_API_KEY"
```

Keep the quotes. In zsh the `?` in the URL is a glob character and an unquoted URL fails with "no matches found".

Add it for every project on this machine instead of just the current one.

```bash
claude mcp add --transport http --scope user paidsync "https://mcp.paidsync.ai/mcp?key=YOUR_API_KEY"
```

## 3. Verify it connected

```bash
claude mcp list
```

You want to see `paidsync` with a connected status. Inside a Claude Code session, `/mcp` shows the same thing plus the tools the server exposed.

Then make the first real call and confirm LinkedIn is actually connected, not just the server.

```
paidsync_context({ include_tools: ['linkedin_ads'] })
```

That returns your active account, the connected platforms, and the live LinkedIn tool catalog. Run any tool from it through `paidsync_exec`.

```
paidsync_exec({ tool: 'get_linkedin_performance', args: { date_range: 'last_30_days' } })
```

If `paidsync_context` returns LinkedIn as not connected, connect it once via OAuth at https://paidsync.ai/dashboard, or ask your assistant to run `connect_linkedin_ads` and follow the link it returns.

## 4. Remove it

```bash
claude mcp remove paidsync
```

## Troubleshooting

- **No tools listed.** The key in the URL is wrong or expired. Copy it again from https://paidsync.ai/dashboard.
- **Tools listed but LinkedIn missing.** The server is connected, the LinkedIn account is not. Run `connect_linkedin_ads`.
- **Writes do nothing.** They are approval gated by design. Every write comes back as a proposal you confirm in chat before it applies.
- **Out of tasks.** The free plan is 15 tasks a month. Plans are at https://paidsync.ai/pricing.
