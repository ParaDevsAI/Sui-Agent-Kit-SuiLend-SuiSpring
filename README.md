# Sui Agent Kit 🤖🌊 — Your Gateway to Automated DeFi on SuiLend Protocol

[![Sui Overflow 2025 Submission - Infrastructure & Tooling Track](https://img.shields.io/badge/Sui_Overflow_2025-Infra_&_Tooling-blue?style=for-the-badge)](https://overflowportal.sui.io/)

<img src="/public/banner.png" />

**The Sui Agent Kit was created to simplify DeFi development on the Sui blockchain and empower builders for the Sui Overflow 2025 Hackathon!**

We believe that accessing powerful DeFi protocols like SuiLend should be seamless and programmable. This toolkit abstracts away the complexities of the SuiLend SDK, exposing its features as intuitive "tools" through the Model-Context Protocol (MCP).

Our mission is to provide foundational infrastructure for developers to rapidly prototype, build, and deploy advanced DeFi apps, automation scripts, and AI-powered agents on Sui—especially those leveraging SuiLend’s lending and borrowing capabilities.

---

## What is the Sui Agent Kit?

Sui Agent Kit is a Node.js server application built with TypeScript. It bridges simple MCP tool calls to direct SuiLend protocol actions on the Sui blockchain.

---

## Use Cases

- **Automated Health Factor Manager:** Agents that monitor your SuiLend health factor and automatically deposit, withdraw, borrow, or repay to maintain safe collateralization.
- **Yield Farming Bots:** Agents that optimize asset allocation by monitoring SuiLend rates and opportunities.
- **DeFi Dashboards:** Web interfaces that offer one-click management of lending actions.
- **AI-Powered Advisors:** AI agents that analyze user portfolios and SuiLend markets, suggesting and executing optimal strategies.
- **Custom SuiLend Tooling:** Extend the kit with new or specialized tools for advanced users.

---

## Core Components

- **MCP Server (`src/mcp/server.ts`)** — Implements the MCP server and registers all SuiLend tools.
- **SuiLend SDK Integration (`src/protocols/suilend/`)** — Manages SDK connections and wallet initialization.
- **Configuration (`src/protocols/suilend/config.ts`)** — Loads environment variables (RPC URL, wallet credentials, contract addresses).
- **Input Validation (`src/mcp/zodSchemas/`)** — Zod schemas define and validate input for every tool.
- **Tool-Based API** — All interactions are exposed as MCP tools, compatible with any MCP client or agent.

---

## Key Features & Capabilities

- **📊 Portfolio Management**
  - `suilend_getUserObligationInfo`: View your lending/borrowing status.
  - `suilend_getObligationDetails`: See all positions, collateral, borrows, and health factor.
  - `suilend_getSuilendMarketAssets`: List available assets and market rates.
  - `suilend_getObligationHistory`: Review all lending/borrowing actions.

- **🌊 Lending Pool Operations**
  - `suilend_depositToSuilend`: Deposit SUI or supported assets as collateral.
  - `suilend_withdrawFromSuilend`: Withdraw your collateral.
  - `suilend_borrowFromSuilend`: Borrow assets against collateral.
  - `suilend_repayToSuilend`: Repay borrowed assets.

- **💧 Liquid Staking Integration (with SuiSpring)**
  - `springSui_stakeSuiForParaSui`: Stake SUI for liquid staked tokens.
  - `springSui_redeemSpringSuiLstForSui`: Redeem LSTs for SUI.

- **💱 Utilities**
  - `common_getCoinTypeBySymbol`: Get coin type and metadata by symbol.
  - `common_formatTokenAmount` / `common_parseTokenAmount`: Human-friendly token formatting.

- **📈 Market Data**
  - `suilend_getSuilendMarketAssets`: Live data for all SuiLend assets.
  - `springSui_getSpringSuiPoolApys`: APYs for liquid staking pools.

- **✅ Utility**
  - `ping`: Health check for the Sui Agent Kit server.

*See schemas in `src/mcp/zodSchemas/` for detailed tool contracts.*

---

<details>
<summary><h1>All Functions </h1></summary>

<ul>
  <li>
    <strong>bigNumberReplacer</strong> (<code>src/mcp/mcpUtils.ts</code>)<br>
    Converts BigNumber and bigint instances to strings for JSON serialization in outputs.
  </li>
  <li>
    <strong>createTextOutput</strong> (<code>src/mcp/mcpUtils.ts</code>)<br>
    Wraps data in an MCP-friendly text output structure for consistent responses.
  </li>
  <li>
    <strong>createErrorOutput</strong> (<code>src/mcp/mcpUtils.ts</code>)<br>
    Creates a standard error output for MCP tools, including error details.
  </li>
  <li>
    <strong>handleFormatTokenAmount</strong> (<code>src/mcp/toolHandlers/commonHandlers.ts</code>)<br>
    Formats a raw token amount to a human-readable string using token decimals.
  </li>
  <li>
    <strong>handleParseTokenAmount</strong> (<code>src/mcp/toolHandlers/commonHandlers.ts</code>)<br>
    Converts a formatted token amount back to its raw value for contracts.
  </li>
  <li>
    <strong>handleShortenAddress</strong> (<code>src/mcp/toolHandlers/commonHandlers.ts</code>)<br>
    Shortens a Sui address or object ID for concise display (e.g., <code>0x123...abc</code>).
  </li>
  <li>
    <strong>handleGetCoinTypeBySymbol</strong> (<code>src/mcp/toolHandlers/commonHandlers.ts</code>)<br>
    Fetches the technical <code>coinType</code> and metadata for a given token symbol and network.
  </li>
  <li>
    <strong>handleGetSuiBalance</strong> (<code>src/mcp/toolHandlers/mystenSuiHandlers.ts</code>)<br>
    Gets the SUI token balance for the active wallet on a chosen network.
  </li>
  <li>
    <strong>handleGetTokenMetadata</strong> (<code>src/mcp/toolHandlers/mystenSuiHandlers.ts</code>)<br>
    Fetches metadata (name, symbol, decimals, etc.) for a specified Sui token.
  </li>
  <li>
    <strong>handleGetUserTokenBalance</strong> (<code>src/mcp/toolHandlers/mystenSuiHandlers.ts</code>)<br>
    Gets the balance of a specific token for the active user wallet.
  </li>
  <li>
    <strong>handleRepayToSuilend</strong> (<code>src/mcp/toolHandlers/suilendHandlers.ts</code>)<br>
    Handles repayment transactions to the Suilend protocol, ensuring wallet and parameter checks.
  </li>
  <li>
    <strong>main</strong> (<code>src/mcp/server.ts</code>)<br>
    Entry point for the MCP server: initializes wallet, client manager, and registers tools.
  </li>
  <li>
    <strong>registerMcpTools</strong> (<code>src/mcp/server.ts</code>)<br>
    Registers all MCP tools (functions) with the server for external calls.
  </li>
  <li>
    <strong>InternalSdkClientManager</strong> (<code>src/mcp/internalSdkClientManager.ts</code>)<br>
    Class managing SDK client instances and tracks the active user wallet for protocol calls.<br>
    <ul>
      <li><code>setActiveUserWallet</code> – Sets the active wallet.</li>
      <li><code>getActiveUserWallet</code> – Gets the current wallet.</li>
      <li><code>getActiveUserAddress</code> – Returns the address of the active wallet.</li>
      <li><code>getSuiClientInstance</code> – Returns a SuiClient for the specified network.</li>
      <li><code>getSpringSuiLstClientInstance</code> – Gets a Spring SUI LST client instance.</li>
      <li><code>getSteammSdkInstance</code> – Gets a Steamm SDK instance for a network.</li>
      <li><code>getSuilendSdkInstance</code> – Gets a Suilend SDK instance for a market/network.</li>
    </ul>
  </li>
</ul>

<p><em>Note: Only the first 10-15 results are shown. For a complete list, review the code in <code>src/mcp/</code> and related handler directories.</em></p>
</details>

## Getting Started

### Prerequisites

1. **Node.js** (v18+ recommended)
2. **Sui Wallet** (mnemonic or Bech32-format private key, funded with SUI and any test assets)
3. **Git** (for cloning the repository)

### Installation

```bash
git clone https://github.com/ParaDevsAI/Sui-Agent-Kit-SuiLend-SuiSpring.git
cd Sui-Agent-Kit-SuiLend-SuiSpring
npm install
