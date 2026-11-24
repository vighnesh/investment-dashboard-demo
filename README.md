# Portfolio Studio — Build a Personal Investment Dashboard

Portfolio Studio is a project blueprint for building a consolidated investment dashboard from **your own financial data**. The intended workflow uses ChatGPT with connected data tools (such as Monarch MCP and, where needed, other institution-specific MCP integrations or carefully prepared manual data). The goal is to bring accounts and holdings from multiple providers into one consistent view.

This repository also hosts a **public, static demonstration** of the interface. That demonstration is deliberately separate from anyone's personal portfolio and contains only fictional data totaling exactly **$10,000**.

## Two distinct things

### 1. Build your own real-data dashboard

Use the project prompt in [PROMPT.md](PROMPT.md) as a starting point. Connect only the financial data services you choose and authorize in your ChatGPT environment. A real build can combine sources when one provider does not return all the account balances, holdings, or asset details you need.

The intended workflow is:

1. Inventory your institutions and accounts, and decide which sources you want to authorize.
2. Retrieve balances and positions through supported, permissioned, preferably read-only connectors.
3. Supplement genuine gaps with another authorized integration or a manually supplied statement/export. Label each source and its as-of date.
4. Normalize account names, ownership, account types, currencies, security identifiers, quantities, prices, and market values.
5. Reconcile totals across source accounts and avoid double-counting cash, sweep funds, money-market holdings, or assets shown in more than one system.
6. Classify holdings for look-through asset allocation, preserving unknown or uncertain classifications rather than guessing.
7. Generate a dashboard and verify balances, freshness, missing data, and calculations before relying on it.

Connector availability and data coverage vary by institution, aggregator, account type, and the permissions granted. A balance feed may not include complete positions or transaction history. Treat missing fields as missing; do not silently infer them.

### 2. Explore the public fictional demo

The live/static demo is a front-end illustration only. It uses invented institutions, account names, holdings, values, and dates, with a sample total of $10,000. It does not connect to Monarch, MCP, brokerages, or any financial account and makes no network requests.

Open [index.html](index.html) locally, or visit the public GitHub Pages site once deployment is enabled:

https://vighnesh.github.io/investment-dashboard-demo/

The demo is not a real-data application and does not become connected simply by entering credentials or publishing it.

## Privacy and security

- Never commit personal financial data, account identifiers, statements, tokens, or credentials to this public repository.
- Do not paste passwords, API keys, one-time codes, or full account numbers into prompts or source code.
- Review connector permissions and use read-only access for portfolio reporting wherever possible.
- Keep any real-data outputs in a private, access-controlled workspace. Do not host real portfolio data on this public GitHub Pages site.
- Treat any downloaded dashboard or CSV export containing your data as sensitive.
- Keep refreshing and exporting separate from financial actions. This project is for tracking and analysis, not trade execution or money movement.

## Repository contents

- `index.html` — static fictional-data demo; no build step or external dependency
- `PROMPT.md` — starter prompt for building a personal dashboard with authorized real-data sources
- `LICENSE` — project license

## Local use

Download or clone the repository and open `index.html` in a modern browser. The page and its CSV exports use fictional sample values only.

## GitHub Pages

In repository **Settings → Pages**, choose **GitHub Actions** as the deployment source. The workflow deploys the static repository root on pushes to `main`.

## Disclaimer

This is an educational project blueprint, not financial, investment, tax, or legal advice. A custom dashboard is only as accurate as its data sources, mappings, prices, assumptions, and reconciliation checks. Verify important figures against the original institutions.
