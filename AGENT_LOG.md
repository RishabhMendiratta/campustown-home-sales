# Agent log

Add a dated entry each time you work with your AI coding agent, with the newest entry at the bottom. Each entry records what you asked the agent, what it produced, and what you checked or changed. Paste your key prompts in exactly as you typed them. Include at least one time the agent got something wrong, and how you caught it.

Copy this outline for each entry:

```markdown
## YYYY-MM-DD: What you worked on

- **Asked:** "Paste your prompt here."
- **Agent produced:** What it made or changed.
- **Checked or changed:** How you checked it, and what you fixed.
```

## 2026-11-20: First page built from the dataset (Part 1)

- **Agent:** Claude (Anthropic), Opus 5.5.
- **Agent produced:** It read AGENTS.md and docs/data_description_sheet.md, then replaced the placeholder index.html with one static page (plain HTML/CSS/JS, with Papa Parse and Chart.js loaded by script tag). The page reads data/college_town_home_sales.csv in the browser and shows summary tiles (sales analysed, number of cities, overall median price, median days on market, median price per sq ft), a bar chart of median sale price by city, a sortable city table, and a campus-area filter. It leaves out sales under $10,000 and states that rule on the page. Days on market is list_date to contract_date, using only rows that have both dates, and price per sq ft skips rows where living area is 0 or blank. No dataset files were changed.
- **Checked or changed:** The agent recomputed the figures separately in Python (pandas) and compared them with the page: 35,402 sales kept (40 under $10,000 dropped), 18 cities, an overall median of $410,000, and city medians that match the data description sheet (for example Champaign $240,000 and Urbana $229,900). One thing went wrong: its first browser test showed blank numbers, because its own sandbox blocked the CDN that hosts the chart and CSV libraries. It caught this from the console errors, served local copies of the same library versions, and reran the test, which then loaded with no errors. It also rounded all prices to whole dollars, so Pittsboro's median shows as $876,986 instead of $876,985.5. I checked the live site in an incognito window after publishing.
