# Starter prompt: build a personal investment dashboard with real data

Use this prompt in a ChatGPT conversation **after connecting Monarch MCP to ChatGPT** and authorizing the financial accounts you want included. Monarch MCP should be the primary aggregation source for the household dashboard. You may add other institution-specific MCP connections or carefully prepared manual data to fill gaps in Monarch's coverage.

## Before you run this prompt: connect Monarch MCP

1. In ChatGPT, open the available apps/connectors and connect **Monarch MCP** (the Monarch connection).
2. Complete Monarch's authorization flow and select/authorize the accounts you want the dashboard to include.
3. Start or continue a ChatGPT conversation in which the Monarch MCP tools are available.
4. Ask ChatGPT to verify that it can see the Monarch MCP connection and inspect its available read operations before beginning the data pull.
5. Do not paste Monarch credentials, passwords, one-time codes, or access tokens into chat.

If Monarch MCP is not connected or its tools are not available in the current conversation, stop and tell me that the connection is missing. Do not pretend to have retrieved Monarch data, and do not substitute invented or guessed account information.

The public `index.html` demo in this repository is separate: it is a static interface example that uses fictional data only. Connecting Monarch MCP is for building your own private dashboard with your own authorized data; it does not connect or change the public demo.

---

Act as a careful portfolio-data engineer and dashboard developer. Help me build a consolidated investment dashboard using **my real financial data from the authorized connectors and files I provide in this conversation**.

## 1. Data access and operating boundaries

- First verify that **Monarch MCP is connected and available in this ChatGPT conversation**. Treat it as the primary household aggregation source. If it is unavailable, stop and ask me to connect it rather than proceeding as though data was retrieved.
- Inventory Monarch MCP's available read tools and schemas before calling them. Determine whether they expose account inventory, current account balances, holdings/positions, and transaction or historical data; use only operations that actually exist.
- Retrieve the account inventory and current balances through Monarch MCP first. Retrieve holdings and transaction/history details through Monarch MCP wherever those read operations are available. Record any coverage gaps explicitly.
- Use only sources I have explicitly connected or files I provide. Do not assume an institution is connected merely because it is named.
- Prefer read-only retrieval. Do not initiate transfers, trades, bill payments, account changes, or any other financial write action.
- Never ask me to provide passwords, one-time codes, private keys, or API tokens in chat.
- Do not fabricate missing accounts, balances, holdings, prices, dates, or returns. Mark unavailable information as missing and explain the gap.
- Before using manually supplied data, record the source, date, currency, account/asset represented, and whether the value is current or stale.

## 2. Build a complete source inventory

Identify all relevant sources and accounts, including where applicable:
- Cash, checking, savings, money-market and sweep balances
- Taxable brokerage and managed/direct-indexing accounts
- Workplace retirement plans, IRAs and other retirement accounts
- Education savings accounts
- Private investments, private-equity funds and capital-account statements
- Physical bullion and other manually valued assets
- Liabilities, if I request a net-worth view

For each account, preserve the institution, account name, account type, owner/registration where provided, currency, source connector, retrieval timestamp, and source as-of date. Do not expose full account numbers in dashboard labels.

## 3. Combine connectors carefully

Use **Monarch MCP as the default primary source** for household accounts and balances. A single aggregator may not expose all account details. Where Monarch MCP is incomplete:
- Identify the specific missing fields.
- Check whether another already-authorized institution-specific MCP connector can supply them; use it to supplement Monarch MCP, not to duplicate the same underlying account.
- Use a manual statement/export only when I provide it or explicitly authorize its use.
- Preserve provenance for every value so I can distinguish institution-reported, aggregator-reported, manually entered, and calculated data.
- Detect overlapping accounts across sources and prevent duplicates. Do not add two feeds for the same underlying account.

## 4. Normalize and reconcile

Create a canonical data model for accounts, holdings, cash balances, prices, currencies, and snapshots. Retain source identifiers internally when useful, but mask sensitive identifiers in display output.

Reconcile account balances and holding market values. Explicitly handle:
- Cash held inside brokerage accounts versus cash accounts shown separately
- Sweep funds and money-market positions
- Accrued interest, unsettled trades, and pending transactions when available
- Multiple currencies and the exchange rates/as-of dates used
- Holdings duplicated across account-level and security-level feeds
- Stale, partial, or conflicting data
- Private assets and manually entered valuations, including their valuation dates and uncertainty

Show reconciliation differences rather than forcing totals to match. Explain every adjustment.

## 5. Holdings and look-through allocation

Build a position-level holdings table with, when available: security/fund name, ticker or identifier, account, quantity, price, price date/source, market value, cost basis, unrealized gain/loss, and asset-class classification.

Classify underlying holdings for look-through allocation (for example equities, fixed income, cash, real assets, and alternatives). Do not classify from account names alone where position data is available. For funds with incomplete transparency, identify the classification method and confidence; keep an explicit unknown/unclassified category rather than inventing exposure.

Treat private investments, bullion, real estate, and other non-public assets separately where their valuation methods differ. Do not imply that a stale manual valuation is a live market quote.

## 6. Dashboard and outputs

Create a responsive dashboard with:
- Total assets and, when liabilities are included, net worth shown distinctly
- Cash and equivalents, public investments, retirement, private investments, and manual/physical assets
- Account-level balances and account groups
- Searchable account inventory
- Holdings and look-through asset allocation
- Gains/losses only when reliable cost-basis data is present
- Historical snapshots and performance only when dated history exists
- Data freshness, source coverage, missing fields, reconciliation status, and methodology notes
- CSV exports that preserve source/as-of metadata and do not silently omit unknown values

Clearly distinguish current balances from historical values, contributions, withdrawals, and investment performance. Do not calculate performance from balance changes without accounting for external cash flows.

## 7. Validation before presenting results

Before calling a refresh complete:
- Reconcile displayed subtotals to the canonical account and holdings records.
- Check for duplicates, missing accounts, stale values, currency mismatches, and arithmetic errors.
- Confirm that cash is not double-counted.
- Verify the displayed snapshot date and source timestamps.
- State which sources were successfully refreshed and which failed or returned partial data.
- List assumptions and unresolved discrepancies.

Do not claim a source was refreshed unless you actually retrieved new data from it in this run.

## 8. Privacy and publication

Treat all retrieved financial information as sensitive. Keep real-data files, dashboard outputs, logs, and exports in a private workspace. Never publish, commit, or deploy actual account data to a public repository or public website. The public Portfolio Studio demo in this repository is fictional and must remain separate from my real-data dashboard.

## 9. Delivery

Start by auditing the connected sources and proposing the canonical data model. Then build the dashboard from verified data. Make assumptions explicit, keep a clear audit trail, and prefer a transparent partial result over fabricated completeness.

Remember: this is a tracking and analysis workflow, not investment advice or permission to execute transactions.
