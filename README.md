# Estates data quality dashboard

A working data quality assessment for an Estates team, built as a single static page with no build step and no dependencies. It runs 13 rules across two systems (an IWMS asset register and a Common Data Environment) and ranks the failures so a data owner knows what to fix first.

All data is synthetic and generated in the browser from a fixed seed. It is not UCL data.

## What it shows

| Role requirement | Where it appears |
|---|---|
| Identify and analyse data quality issues across systems | 13 rules, 5 dimensions, 2 systems, ranked worst first |
| Root causes and improvement plans | Each rule has a likely cause, a recommended fix and a named data owner |
| Governance and stakeholder reporting | Severity ratings and plain-language labels for non-technical readers |
| CDE and ISO 19650 | File naming regex (Project-Originator-Volume-Level-Type-Role-Number), status, revision and metadata consistency checks |
| IWMS, FM operations and SFG20 | Asset completeness, PPM schedule codes, service timeliness |
| Excel | Failing records export to CSV for owners to work through |

## Method

- Pass rate = records passing / records assessed for that rule.
- Overall score = mean of rule pass rates. Dimension score = mean of its rules.
- Severity: High at 10% failing or more, Medium at 5% or more, otherwise Low.

## Run locally

Open `index.html` in a browser, or run `python -m http.server` and visit `localhost:8000`.

## Publish and push

```bash
git init
git add .
git commit -m "Add estates data quality dashboard"
git branch -M main
git remote add origin https://github.com/<your-username>/ucl-estates-dq-dashboard.git
git push -u origin main
```

Then in the repository go to Settings, Pages, and deploy from branch `main`, folder `/ (root)`. Add the live link to this README.

## Make it yours

1. Replace the `assets` and `docs` arrays with real exports (CSV parsed with fetch) to run the same rules on live data.
2. Set `NAME_RE` to your project's naming convention. The `S20-` codes are placeholders for your licensed SFG20 mapping.
3. Add or edit rules in the `rules` array. Each is one line.
