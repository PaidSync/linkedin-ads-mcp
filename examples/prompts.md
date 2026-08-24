# LinkedIn Ads prompts

15 prompts you can paste straight into Claude, ChatGPT, Gemini, Cursor, or any MCP client once PaidSync is connected. Each one names the tools it lands on, so you can check the call in `paidsync_context({ include_tools: ['linkedin_ads'] })` before you run it.

Every write comes back as a proposal you approve in chat. Nothing changes in the ad account until you confirm.

## Setup and account selection

**1. Connect and pick the right ad account**

```
Connect my LinkedIn Ads account. List every ad account I have access to with
its name, ID, and currency, then set the one called "Acme B2B" as active.
```

Tools: `connect_linkedin_ads`, `list_linkedin_ad_accounts`, `set_linkedin_ad_account`

**2. Map the account before touching anything**

```
Show me how this LinkedIn account is structured. List every campaign group,
then the campaigns inside each one with status, objective, and daily budget.
Flag any campaign that is active with no spend in the last 7 days.
```

Tools: `list_linkedin_campaign_groups`, `list_linkedin_campaigns`, `get_linkedin_performance`

## Reporting

**3. Last 30 days, plain numbers**

```
Pull my LinkedIn performance for the last 30 days. Spend, impressions, clicks,
CTR, leads, and cost per lead by campaign. Sort by spend, highest first.
```

Tools: `get_linkedin_performance`

**4. Who is actually converting, by job function**

```
Break my LinkedIn performance for the last 90 days down by job function.
Show spend, leads, and cost per lead for each. Tell me which three job
functions I should stop paying for.
```

Tools: `get_linkedin_performance_by_dimension`

**5. Company size and seniority split**

```
Break last quarter's LinkedIn spend down by company size, then by seniority.
I sell to companies with 200 or more employees. Tell me what percentage of
my spend went to companies smaller than that.
```

Tools: `get_linkedin_performance_by_dimension`

**6. Geography check before a budget move**

```
Show LinkedIn spend and cost per lead by geography for the last 60 days.
List any country taking more than 5% of spend with a cost per lead above
the account average.
```

Tools: `get_linkedin_performance_by_dimension`, `get_linkedin_performance`

**7. Creative performance with the actual assets**

```
List my live LinkedIn creatives with their media so I can see the images and
copy. Pair each one with its impressions, CTR, and cost per lead for the last
30 days. Which three creatives are carrying the account?
```

Tools: `list_linkedin_creatives_with_media`, `list_linkedin_creatives`, `get_linkedin_performance_by_dimension`

**8. Quarterly rollup for the board**

```
Build a Q3 LinkedIn summary by campaign group. Spend, leads, cost per lead,
and quarter over quarter change for each group. Keep it to one table.
```

Tools: `list_linkedin_campaign_groups`, `get_linkedin_performance`

## Optimization and budget

**9. Cut the campaigns that are not working**

```
Find every LinkedIn campaign with more than $1,000 spent in the last 30 days
and a cost per lead above $250. Show me the list with the numbers, then pause
them. Tell me the monthly spend that frees up.
```

Tools: `get_linkedin_performance`, `list_linkedin_campaigns`, `pause_linkedin_campaign`

**10. Move budget to the winner**

```
Compare my two best LinkedIn campaigns by cost per lead over the last 14 days.
Raise the daily budget on the cheaper one by 40% and lower the other by the
same dollar amount so total daily spend stays flat.
```

Tools: `get_linkedin_performance`, `update_linkedin_campaign`

**11. Restart what worked last season**

```
List every paused LinkedIn campaign that had a cost per lead under $150 the
last time it ran. Re-enable the top two and set their daily budget to $300 each.
```

Tools: `list_linkedin_campaigns`, `get_linkedin_performance`, `enable_linkedin_campaign`, `update_linkedin_campaign`

## Targeting

**12. Read the targeting before you argue about it**

```
Show me the current targeting on the "Demo Request Q3" LinkedIn campaign.
Job functions, seniorities, industries, company sizes, and member skills,
exactly as they are set right now.
```

Tools: `list_linkedin_campaigns`, `get_linkedin_campaign_targeting`

**13. Tighten seniority on a live campaign**

```
On my "Demo Request Q3" LinkedIn campaign, remove Entry and Senior from the
seniority targeting and keep Director, VP, and CXO. Leave everything else
untouched. Show me the before and after before you apply it.
```

Tools: `get_linkedin_campaign_targeting`, `update_linkedin_campaign_targeting`

## Build and track

**14. Launch a new group and campaign from scratch**

```
Build a LinkedIn campaign group called "Enterprise Demo Q4" with a $30,000
budget. Inside it, create a lead generation campaign targeting Director and
above in IT and Engineering job functions, at software companies with 200 or
more employees in the US and UK, at $400 a day. Leave it paused so I can
review it first.
```

Tools: `create_linkedin_campaign_group`, `create_linkedin_campaign`, `update_linkedin_campaign_targeting`

**15. Fix conversion tracking, then attach the new creative**

```
List the conversions on this LinkedIn ad account and tell me which campaigns
are not attached to one. Create a conversion called "Demo Request" for the
form on my /book-demo page, then build a new single image creative for the
"Enterprise Demo Q4" campaign using my strongest performing headline and
launch it as an ad.
```

Tools: `list_linkedin_conversions`, `create_linkedin_conversion`, `create_linkedin_creative`, `create_linkedin_ad`, `update_linkedin_creative`

## Notes

- Dollar amounts, campaign names, dates, and page paths in these prompts are placeholders. Swap in your own.
- If a prompt returns nothing, run `paidsync_context({ include_tools: ['linkedin_ads'] })` first. It confirms which account is active and what is connected.
- LinkedIn's Marketing API is rate limited more tightly than Google or Meta on some account classes. Large reporting pulls may come back in pages.
- Have a prompt that earns its place, open a PR. See [CONTRIBUTING.md](../CONTRIBUTING.md).
