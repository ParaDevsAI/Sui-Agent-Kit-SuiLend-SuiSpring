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

The Sui Agent Kit provides a rich set of tools, categorized by protocol:

### ☯️ MystenSui (Core Sui Functionality)

*   `mystenSui_getSuiBalance`: Fetch the SUI balance for the active agent wallet.
*   `mystenSui_getTokenMetadata`: Retrieve detailed metadata for any fungible token.
*   `mystenSui_getUserTokenBalance`: Get the balance of a specific fungible token for the active agent.
*   `mystenSui_transferSui`: Execute SUI transfers.
*   `mystenSui_transferSuiToMany`: Transfer SUI to multiple recipients in a single transaction.
*   `mystenSui_transferFungTokensToMany`: Transfer a specific fungible token to multiple recipients.
*   `mystenSui_getUserRecentTxs`: Fetch recent transaction history for the active agent.

### 🌱 SuiSpring (Liquid Staking)

*   `springSui_discoverLstPools`: Discover available Liquid Staking Token (LST) pools.
*   `springSui_getLstSuiExchangeRate`: Get the current exchange rate between an LST and SUI.
*   `springSui_getUserLstDetails`: Fetch details about the agent's position in a specific LST (balance, APY, SUI equivalent).
*   `springSui_getSpringSuiPoolApys`: Get APYs for specific LST pools.
*   `springSui_stakeSuiForSpringSuiLst`: Stake SUI to mint a generic SpringSui LST.
*   `springSui_stakeSuiForParaSui`: Specifically stake SUI to obtain ParaSUI.
*   `springSui_redeemSpringSuiLstForSui`: Redeem an LST back into SUI.

### 🏦 Suilend (Lending & Borrowing)

*   `suilend_getSuilendMarketAssets`: List supported assets and their current metrics (interest rates, APYs).
*   `suilend_ensureSuilendObligation`: Check for or create a Suilend obligation (loan account) for the active agent.
*   `suilend_getUserObligationInfo`: Get the `obligationId` and `ownerCapId` for the active agent's obligation, crucial for most other Suilend actions.
*   `suilend_depositToSuilend`: Deposit assets as collateral into the agent's obligation.
*   `suilend_getObligationDetails`: Retrieve a comprehensive report of a specific obligation (collateral, borrows, health factor).
*   `suilend_withdrawFromSuilend`: Withdraw collateral from an obligation.
*   `suilend_borrowFromSuilend`: Borrow assets against deposited collateral.
*   `suilend_repayToSuilend`: Repay a borrowed asset.
*   `suilend_getObligationHistory`: Fetch the transaction history for an obligation.

### 🛠️ Common Utilities

*   `common_formatTokenAmount`: Convert raw token amounts to human-readable strings.
*   `common_parseTokenAmount`: Convert human-readable strings to raw token amounts for transactions.
*   `common_shortenAddress`: Shorten Sui addresses for display.
*   `common_getCoinTypeBySymbol`: Get the full `coinType` and metadata for a token from its symbol.

*(Refer to the Zod schema definitions in `src/mcp/zodSchemas/` for detailed input/output structures for each tool).*

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

Follow these steps to get the Sui Agent Kit up and running on your local machine.

### Prerequisites

1.  **Node.js:** Version 18.x or later is highly recommended (as per `tsx` and modern dependencies).
2.  **npm or yarn:** Package manager for Node.js.
3.  **Sui Wallet Private Key:** You'll need a Sui private key in **Bech32 format** (starting with `suiprivkey1...`). This key corresponds to the wallet the Agent Kit will use to sign transactions.
    *   **IMPORTANT:** This wallet must be funded with SUI for gas fees and any assets you intend to interact with (e.g., SUI for deposits in Suilend or staking in SuiSpring).
4.  **Git:** For cloning the repository.

### Installation

1.  **Clone the Repository:**
    ```bash
    git clone https://github.com/ParaDevsAI/Sui-Agent-Kit-SuiLend-SuiSpring
    cd Sui-Agent-Kit-SuiLend-SuiSpring
    ```

2.  **Install Dependencies:**
    ```bash
    npm install
    # OR if you prefer yarn
    # yarn install 
    ```

### Configuration

1.  **Create `.env` File:**
    In the root directory of the project (`sui-agent-kit-suispring-suilend`), create a file named `.env`.

2.  **Add Environment Variables:**
    Open the `.env` file and add your Sui private key. You can also specify the RPC URL if you want to override the default (which is typically Mainnet if not specified otherwise in protocol configs).

    ```env
    # Your Agent's Sui Wallet Private Key (Bech32 format)
    SUI_MAINNET_PRIVATE_KEY="suiprivkey1yourlongprivatekeystringgoeshere..."

    # Optional: Sui RPC URL (defaults to Mainnet if not set, or if protocol configs specify it)
    # SUI_RPC_URL="https://fullnode.mainnet.sui.io:443"
    ```

    **⚠️ CRITICAL SECURITY WARNING ⚠️**
    *   The `SUI_MAINNET_PRIVATE_KEY` grants full control over the associated Sui wallet.
    *   **NEVER commit your `.env` file containing a real private key to any Git repository, especially a public one.** The provided `.gitignore` file should already exclude `.env`.
    *   For development and testing, it is strongly recommended to use a dedicated **devnet or testnet wallet** with only test funds.
    *   Ensure this wallet is adequately funded for gas and any DeFi operations you intend the agent to perform.

### Build the Kit

To compile the TypeScript code into JavaScript (output to `dist/` directory):

```bash
npm run build
```

### Running the Sui Agent Kit Server

*   **For Development (with hot-reloading via `tsx`):**
    ```bash
    npm run dev
    ```
    This command uses `tsx` to run `src/main.ts` directly, recompiling on changes.

*   **For Production (after building with `npm run build`):**
    ```bash
    npm start
    # This typically runs: node dist/main.js
    ```

Upon successful startup, you should see log messages indicating the MCP server has started and is ready to accept connections and tool calls via stdio. The active wallet address derived from your private key will also be logged.

## Connecting an MCP Client (e.g., MCP Inspector)

The Sui Agent Kit server communicates via **stdio (standard input/output)** using JSON-RPC 2.0 messages, as per the Model Context Protocol. To interact with it, you'll need an MCP client. The `@modelcontextprotocol/inspector` is an excellent tool for this.

You can configure the MCP Inspector (or other MCP clients that support JSON configuration) using an `mcp.json` (or similar) file. This file tells the client how to launch and manage your Sui Agent Kit server process.

**Example `mcp.json` Configuration:**

Create an `mcp.json` file (e.g., in your user home directory, or wherever your MCP client expects it). **You MUST replace `YOUR_ABSOLUTE_PATH_TO` placeholders with the correct absolute paths on your system.**

```json
{
  "mcpServers": {
    "sui-agent-kit": {
      "command": "node",
      "args": [
        "YOUR_ABSOLUTE_PATH_TO/sui-agent-kit-suispring-suilend/dist/main.js"
      ],
      "cwd": "YOUR_ABSOLUTE_PATH_TO/sui-agent-kit-suispring-suilend",
      "env": {
        // Optional: Override or set environment variables here.
        // If SUI_MAINNET_PRIVATE_KEY is in your project's .env, you might not need it here.
        // "SUI_MAINNET_PRIVATE_KEY": "suiprivkey1...from_mcp_json_override", 
        // "SUI_RPC_URL": "https://fullnode.testnet.sui.io:443"
      }
    }
  }
}
```

**Key Parts to Customize in `mcp.json`:**

*   **`"args"`**: The most critical part is the path to your server's entry point.
    *   Ensure `YOUR_ABSOLUTE_PATH_TO/sui-agent-kit-suispring-suilend/dist/main.js` correctly points to the compiled `main.js` file within your project structure.
    *   **Windows Users:** Remember to use double backslashes for paths (e.g., `"C:\\Users\\YourUser\\Projects\\sui-agent-kit-suispring-suilend\\dist\\main.js"`).
    *   **macOS/Linux Users:** Standard forward slashes (e.g., `"/Users/YourUser/Projects/sui-agent-kit-suispring-suilend/dist/main.js"`).

*   **`"cwd"`** (Current Working Directory):
    *   Set this to the **absolute path of your project's root directory** (`sui-agent-kit-suispring-suilend`). This helps the server correctly locate its `.env` file (if used) and any other relative path dependencies.

*   **`"env"`**:
    *   Use this section to pass environment variables directly from the MCP client configuration. These can override variables set in the project's `.env` file.
    *   For instance, you could use this to quickly switch networks (`SUI_RPC_URL`) or test with a different private key without modifying the project's `.env` file.
    *   **Security Note:** Avoid hardcoding highly sensitive private keys directly in `mcp.json` if this file is shared. Prefer using the project's `.env` file for the primary private key.

**Using `npm run dev` with `mcp.json` (Alternative for Development):**

If you prefer to have the MCP Inspector launch your server in development mode (using `tsx` for hot-reloading), you could modify the `mcp.json` like this:

```json
{
  "mcpServers": {
    "sui-agent-kit-dev": {
      "command": "npm",
      "args": [
        "run",
        "dev"
      ],
      "cwd": "YOUR_ABSOLUTE_PATH_TO/sui-agent-kit-suispring-suilend",
      "env": {}
    }
  }
}
```
In this case, `npm run dev` (which executes `tsx src/main.ts`) becomes the command. Ensure `npm` is in your system PATH.

### Interacting with the Kit (MCP Inspector CLI Examples)

Once your MCP client (like MCP Inspector) is configured with the `mcp.json` pointing to your server (e.g., aliased as `sui-agent-kit`):

1.  **You do not need to manually start the server (`npm run dev` or `npm start`) if the MCP client is configured to launch it.** The client will manage the server process.
2.  Open your terminal and use the `mcp-inspector` CLI:

    ```bash
    # Ensure your mcp.json is discoverable by mcp-inspector (e.g., in ~/.config/mcp/mcp.json or by setting MCP_CONFIG_PATH)

    # Example: Get SUI Balance for the active wallet on mainnet
    mcp-inspector --server sui-agent-kit --method tools/call --tool-name mystenSui_getSuiBalance --tool-arg network=mainnet

    # Example: List available assets in Suilend's default market on mainnet
    mcp-inspector --server sui-agent-kit --method tools/call --tool-name suilend_getSuilendMarketAssets --tool-arg network=mainnet

    # Example: Stake 0.05 SUI for ParaSUI on mainnet (ensure active wallet has SUI)
    mcp-inspector --server sui-agent-kit --method tools/call --tool-name springSui_stakeSuiForParaSui --tool-arg amountSuiToStake=0.05 --tool-arg network=mainnet

    # Example: Get User Obligation Info from Suilend on mainnet (prerequisite for many Suilend actions)
    mcp-inspector --server sui-agent-kit --method tools/call --tool-name suilend_getUserObligationInfo --tool-arg network=mainnet
    
    # Example: Get coin type for "USDC" on mainnet
    mcp-inspector --server sui-agent-kit --method tools/call --tool-name common_getCoinTypeBySymbol --tool-arg symbol=USDC --tool-arg network=mainnet
    ```

    *   Replace `sui-agent-kit` with the server alias you defined in your `mcp.json`.
    *   Consult the tool definitions in `src/mcp/zodSchemas/` for the exact names and required/optional arguments for each tool.
    *   The output will be JSON responses from the server.

## Technical Deep Dive (Recap)

*   **MCP Server (`src/mcp/server.ts`):** Orchestrates tool registration and request handling.
*   **Zod Schemas (`src/mcp/zodSchemas/`):** Provide data validation and clear API contracts for AI.
*   **Tool Handlers (`src/mcp/toolHandlers/`):** Bridge MCP calls to protocol-specific actions.
*   **Internal SDK Client Manager (`src/mcp/internalSdkClientManager.ts`):** Centralizes SDK client instances and active wallet access.
*   **Protocol Actions (`src/protocols/**/actions.ts`):** Encapsulate the core business logic using protocol SDKs.
*   **Protocol Clients & Configs (`src/protocols/**/client.ts`, `src/protocols/**/config.ts`):** Manage SDK initialization and static configurations.
*   **Common Utilities (`src/common/`):** Reusable functions for data transformation and common tasks.

## Project Status (Sui Overflow 2025 MVP)

*   ✅ **Core Infrastructure:** MCP server, wallet management, Zod validation, and tool handling framework are stable and robust.
*   ✅ **MystenSui Integration:** Comprehensive set of tools for core Sui operations.
*   ✅ **SpringSui Integration:** Full support for discovering LSTs, staking, redeeming, and fetching user/market data.
*   ✅ **Suilend Integration:** Extensive capabilities for managing obligations, deposits, borrows, and market data retrieval.
*   ⚠️ **Steamm (DEX) Integration:** Initial scaffolding and some actions exist but are **currently disabled/paused** in the MCP server for this MVP due to complexities encountered during initial development. Planned for future robust implementation.
*   🧪 **Testing:** Basic Jest test structure is in place (`tests/`). Focus has been on action-level tests. Further unit and integration test coverage is a priority for post-hackathon development.

## Future Roadmap: Expanding the Agent Horizon

The Sui Agent Kit is a living project with a bright future:

*   🌟 **Activate Steamm DEX Integration:** Fully implement and enable robust tools for token swaps, liquidity provision, and route finding via Steamm.
*   ➕ **Broader Protocol Support:** Integrate with other key Sui DeFi protocols (e.g., other AMMs/DEXs, perpetuals platforms, yield aggregators, NFT marketplaces).
*   🤖 **Advanced AI Agent Showcases:** Develop and open-source example AI agents (e.g., in Python) that demonstrate sophisticated DeFi strategies using the kit.
*   🔐 **Enhanced Security & Permissioning:** Explore options for more granular control, potentially integrating with wallet standards for delegated execution or multi-sig setups for production agents.
*   📡 **Real-time Event Streaming:** Enable agents to subscribe to on-chain events for reactive decision-making.
*   📈 **Comprehensive Test Suite:** Implement extensive unit, integration, and end-to-end tests.
*   🌐 **Community-Driven Expansion:** Foster a community around the kit to contribute new tools and protocol integrations.

## Contributing

This project was initiated for the Sui Overflow 2025 Hackathon, and we believe in the power of open collaboration! We enthusiastically welcome contributions. Whether it's reporting bugs, suggesting features, improving documentation, or submitting pull requests for new tools or protocol integrations, your input is valuable.

<div align="center">

## 💝 Support Us

Support our work by using **ParaSui** liquid staking on SUI: [springsui.com/SUI-ParaSui](https://springsui.com/SUI-ParaSui)

**Built with ❤️ for the Sui Overflow 2025 Hackathon**

*Let's build the future of decentralized finance on Sui, together!*

**🌊 [Navi Kit Repository](https://github.com/ParaDevsAI/Sui-Agent-Kit-Navi) | 🏦 [SuiLend+SuiSpring Kit Repository](https://github.com/ParaDevsAI/Sui-Agent-Kit-SuiLend-SuiSpring)**

</div>
