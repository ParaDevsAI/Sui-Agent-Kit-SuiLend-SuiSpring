# Sui Agent Kit: SuiSpring & SuiLend Edition 🚀

**Unlock the power of AI on the Sui Blockchain. Your agent's intelligent gateway to DeFi.**

[![Sui Overflow 2025 Submission - Infrastructure & Tooling Track](https://img.shields.io/badge/Sui_Overflow_2025-Infra_&_Tooling-blue?style=for-the-badge)](https://overflowportal.sui.io/)

---

## Sui Overflow 2025 Hackathon Submission

**Track:** Infrastructure and Tooling

**Project Name:** Sui Agent Kit SuiSpring SuiLend

---

## The Story: From Complex Chains to Intelligent Agents 🧠💻🔗

The world of Decentralized Finance (DeFi) on the Sui blockchain is a universe of exploding opportunity – from innovative lending markets like **Suilend** to groundbreaking liquid staking solutions like **SuiSpring**. Yet, for developers venturing into this space, especially those aiming to integrate the power of Artificial Intelligence, the journey can be a labyrinth of SDKs, protocol-specific nuances, and direct blockchain complexities.

We asked ourselves: *How can we make Sui DeFi truly programmable and accessible for AI? How can we empower AI agents to not just observe, but to act, to strategize, and to automate within this vibrant ecosystem?*

Our answer is the **Sui Agent Kit**.

We are submitting this project to the **Infrastructure and Tooling** track of the Sui Overflow 2025 Hackathon because we believe it provides a critical piece of foundational infrastructure. It's a robust, developer-friendly toolkit designed to significantly lower the barrier to entry for building AI-powered applications on Sui. It's not just about connecting to one protocol; it's about creating a unified, intelligent interface to the rich tapestry of Sui DeFi.

This kit is born from a desire to see AI agents seamlessly navigate and utilize the sophisticated financial instruments offered by protocols like SuiSpring and Suilend, turning complex on-chain operations into simple, manageable tasks for intelligent systems. We aim to empower developers to build the next generation of DeFi applications – ones that are smarter, more autonomous, and more intuitive, all powered by AI on Sui.

## What is the Sui Agent Kit?

The **Sui Agent Kit: SuiSpring & SuiLend Edition** is a comprehensive backend server, built with TypeScript and Node.js, that leverages the **Model Context Protocol (MCP)**. It acts as an intelligent intermediary, exposing the rich functionalities of core Sui protocols – specifically **MystenSui (base layer)**, **SuiSpring (Liquid Staking)**, and **Suilend (Lending/Borrowing)** – as a set of well-defined, easy-to-use "tools" for AI agents.

**Core Components:**

*   **MCP Server (`src/mcp/server.ts`):** The heart of the kit, implementing an MCP server using `@modelcontextprotocol/sdk`. It defines and registers all available tools.
*   **Protocol SDK Integrations (`src/protocols/`):** Dedicated modules for each supported protocol, handling SDK client initialization, configuration, and the core logic for each action.
    *   `mystenSui/`: For base Sui blockchain interactions.
    *   `springSui/`: For liquid staking with SuiSpring.
    *   `suilend/`: For lending and borrowing with Suilend.
*   **Secure Wallet Management (`src/mcp/internalSdkClientManager.ts` & `.env`):** Manages an active Sui wallet (derived from a private key in your `.env` file) for signing and executing transactions.
*   **Robust Input Validation (`src/mcp/zodSchemas/`):** Utilizes Zod schemas to define and validate the input parameters for every tool, ensuring type safety and clear contracts for AI interaction.
*   **Configuration (`.env`, `src/protocols/**/config.ts`):** Manages environment variables (RPC URL, private key) and protocol-specific constants (contract addresses, market IDs).
*   **Common Utilities (`src/common/`):** Shared helper functions for tasks like token amount formatting and address manipulation.

## Use Cases: Igniting AI-Powered DeFi on Sui

The Sui Agent Kit is designed to be a versatile foundation for a wide array of applications:

*   **🤖 Autonomous DeFi Portfolio Managers:** AI agents that monitor Suilend obligations, assess market conditions, and automatically rebalance collateral, borrow, or repay debt to optimize health factors and manage risk.
*   💧 **Intelligent Liquid Staking Agents:** Agents that analyze SuiSpring LST (e.g., ParaSUI) yields and exchange rates, automatically staking SUI or redeeming LSTs to maximize returns based on AI-driven strategies.
*   💹 **Automated Yield Farming Bots:** Sophisticated agents that can combine operations across SuiSpring and Suilend – for example, staking SUI for an LST via SuiSpring, then depositing that LST as collateral in Suilend to borrow other assets for further yield generation.
*   🗣️ **Conversational DeFi Interfaces:** Build chatbots or voice assistants that use the Sui Agent Kit to translate natural language commands (e.g., "Deposit 50 SUI into my Suilend account and show me my new health factor") into on-chain actions.
*   📊 **Enhanced DeFi Dashboards & Analytics Platforms:** Power frontends that not only display rich data from Sui protocols but also allow users to execute complex actions with a single click, orchestrated by the Agent Kit in the backend.
*   🔧 **Custom Tooling & Automation Scripts:** Developers can extend the kit with more specialized tools or build complex automation scripts that chain multiple DeFi operations together for advanced users or DAO treasuries.
*   💡 **Rapid Prototyping for New DeFi Strategies:** Quickly test and validate new AI-driven DeFi strategies on Sui without getting bogged down in direct SDK integration for each protocol.

By abstracting the underlying complexity, the Sui Agent Kit empowers developers to focus on the *intelligence* and *strategy* of their AI applications, rather than the intricacies of blockchain interaction.

## Key Features & Capabilities

The Sui Agent Kit provides a rich set of tools, categorized by protocol:

### ☯️ MystenSui (Core Sui Functionality)

*   `mystenSui_getSuiBalance`: Fetch the SUI balance for the active agent wallet.
*   `mystenSui_getTokenMetadata`: Retrieve detailed metadata for any fungible token.
*   `mystenSui_getUserTokenBalance`: Get the balance of a specific fungible token for the active agent.
*   `mystenSui_transferSui`: Execute SUI transfers.
*   `mystenSui_transferSuiToMany`: Transfer SUI to multiple recipients in a single transaction.
*   `mystenSui_transferFungibleTokensToMany`: Transfer a specific fungible token to multiple recipients.
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
    cd sui-agent-kit-suispring-suilend
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
    "sui-agent-kit": { // You can name this server alias anything you like
      "command": "node",
      "args": [
        "YOUR_ABSOLUTE_PATH_TO/sui-agent-kit-suispring-suilend/dist/main.js" // Path to the compiled JS entry point
      ],
      "cwd": "YOUR_ABSOLUTE_PATH_TO/sui-agent-kit-suispring-suilend", // Path to the project's root directory
      "env": {
        // Optional: Override or set environment variables here.
        // If SUI_MAINNET_PRIVATE_KEY is in your project's .env, you might not need it here.
        // "SUI_MAINNET_PRIVATE_KEY": "suiprivkey1...from_mcp_json_override", 
        // "SUI_RPC_URL": "https://fullnode.testnet.sui.io:443" // Example to force testnet via mcp.json
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
      "command": "npm", // Or "yarn" if you use yarn
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
*   🐍 **Python Client Library:** Develop a dedicated Python client library to make integration even simpler for the Python-centric AI/ML community.
*   🌐 **Community-Driven Expansion:** Foster a community around the kit to contribute new tools and protocol integrations.

## Contributing

This project was initiated for the Sui Overflow 2025 Hackathon, and we believe in the power of open collaboration! We enthusiastically welcome contributions. Whether it's reporting bugs, suggesting features, improving documentation, or submitting pull requests for new tools or protocol integrations, your input is valuable.

*(Please create a `CONTRIBUTING.md` file with guidelines if you formalize this process).*

## Meet the Team

*   **[Your Name / Team Name Here]** - Innovators @ Sui Overflow 2025!
    *   Passionate about the intersection of AI and Decentralized Finance on the Sui Blockchain.

## License

This project is licensed under the MIT License. (You should create a `LICENSE` file in your repository, typically with the MIT License text if that's your choice. For example, you can copy one from [choosealicense.com](https://choosealicense.com/licenses/mit/)).

---

Let's build the future of intelligent DeFi on Sui, together! 
