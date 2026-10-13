# RiskModels for Gemini CLI

US equity and portfolio risk analytics in [Gemini CLI](https://geminicli.com). Break any US stock or portfolio into market, sector, subsector and stock-specific risk, get the ETF hedge ratio for each layer, and pull point-in-time quarterly fundamentals. Data comes from the hosted [RiskModels](https://riskmodels.app) MCP server.

The extension contains no code and no credentials. It configures one remote MCP server (`https://riskmodels.app/api/mcp/openai`, Streamable HTTP) plus a `GEMINI.md` context file.

## Requirements

- **Gemini CLI 0.63.0 or later.** Earlier versions are untested.
- **A RiskModels account.** New accounts start with $20 of prepaid credit. A payment method is collected at signup for verification and is not charged until you top up.
- **Usage is metered per tool call**, even though every tool is read-only. Most single-stock calls cost $0.005, fundamentals cost $0.02, and a full portfolio exposure report costs $0.25. See [riskmodels.app/pricing](https://riskmodels.app/pricing).

## Install

```
gemini extensions install https://github.com/BlueWaterCorp/riskmodels-gemini-extension
```

Start Gemini CLI in a folder you trust. MCP servers stay disabled in untrusted folders.

## Sign in

At the Gemini prompt:

```
/mcp auth riskmodels
```

Gemini registers itself with RiskModels and opens your browser at riskmodels.app. Sign in, check that the consent screen shows the account you expect (use **Use a different account** if not), and click **Allow**. Then `/mcp` should list `riskmodels` as connected.

The browser must run on the same machine as Gemini CLI, because the sign-in returns to a `http://localhost:<port>/oauth/callback` address. Gemini waits only a few minutes for it.

## Try it

- `Break down NVDA's risk into market, sector, subsector and stock-specific parts. Include the data date.`
- `Which ETFs would hedge a long NVDA position, and how much of each per dollar?`
- `Analyze a hypothetical portfolio of 40% AAPL, 35% MSFT and 25% NVDA. Show aggregate risk exposures.`
- `Retrieve AAPL's quarterly fundamentals available as of June 30, 2025. Include filing dates and exclude later filings.`
- With a brokerage account linked in [riskmodels.net](https://riskmodels.net) settings: `Show my linked brokerage positions, including longs and shorts.`

Tools return structured data with chart specifications. Gemini CLI shows the results as text and tables; it does not draw charts.

## What it does not do

RiskModels does not place orders, move money or give personalized investment advice. Hedge ratios are model exposures, not executed trades. Historical analytics describe observed behavior and do not predict returns.

## Links

- Website: https://riskmodels.app
- Agent integration docs: https://riskmodels.app/docs/agent-integration
- Support: https://riskmodels.net/support
- Privacy: https://riskmodels.net/privacy
- API terms: https://riskmodels.net/terms/api

## License

Apache-2.0 for the files in this repository. Use of the RiskModels service is governed by the [API terms](https://riskmodels.net/terms/api).
