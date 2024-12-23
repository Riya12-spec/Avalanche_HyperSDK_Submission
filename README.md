# HyperSDK Metacrafters Avalanche Module 2

## Overview
TokenVM is an application that showcases the usage of the HyperSDK for creating, minting, and trading user-generated tokens on-chain. The platform includes a built-in exchange for creating and filling trade orders, allowing seamless token interactions. TokenVM also provides a powerful CLI tool and serves RPC requests for trades using an in-memory order book.

**Status:** TokenVM is in ALPHA and is not safe for production. It is under active development, and its modules are subject to optimization and auditing.

---

## Features

### 1. Arbitrary Token Minting
- Create, mint, transfer, and manage user-generated tokens with ease.
- Assign "admin control" to asset owners, allowing them to:
  - Mint additional tokens.
  - Update asset metadata.
  - Transfer/revoke ownership.
- Optimized storage for assets requiring minimal state.
- Supports parallel execution for transfers.

### 2. On-Chain Token Trading
- Create and fill trade orders for any token pair.
- Maintains an in-memory order book for efficient interaction.
- Optimized storage for orders requiring minimal state.
- Supports parallel execution of trade fills.

### 3. In-Memory Order Book
- Efficiently listens for and manages on-chain orders.
- Implements a simple max heap per token pair for best rates.

### 4. Sandwich-Resistant Design
- Explicit order targeting prevents front-running by bots.
- Ensures fair execution rates for all trades.

### 5. Partial Fills and Refunds
- Orders can be partially filled, and unused pledged tokens are refunded.
- Guarantees secure and fair token handling in a blockchain context.

### 6. Expiring Fills
- Scoped transaction validity ensures efficient order management.

### 7. Avalanche Warp Support
- Enables cross-chain asset transfers between tokenvms without trusted intermediaries.
- Ensures secure and transparent asset tracking.
- Limits export to natively minted assets to prevent contagion.

---

## Getting Started

### Prerequisites
- **Operating System:** Compatible with Linux/Unix.
- **Dependencies:** Installed HyperSDK and Avalanche Network Runner.

### Running TokenVM
1. Launch a TokenVM Subnet:
   ```bash
   ./scripts/run.sh
   ```
   - Allocates all funds to the demo key located at `demo.pk`.
   - For single Subnet testing:
     ```bash
     MODE="run-single" ./scripts/run.sh
     ```

2. Build the TokenVM CLI:
   ```bash
   ./scripts/build.sh
   ```
   - The compiled CLI is located at `./build/token-cli`.

3. Import Keys and Chains:
   ```bash
   ./build/token-cli key import demo.pk
   ./build/token-cli chain import-anr
   ```

### Minting and Trading
#### Step 1: Create an Asset
```bash
./build/token-cli action create-asset
```
- Provide asset metadata (e.g., name, description).
- Confirm creation to receive a transaction ID.

#### Step 2: Mint Tokens
```bash
./build/token-cli action mint-asset --amount=<number>
```

#### Step 3: Trade Tokens
- Create a trade offer:
  ```bash
  ./build/token-cli action create-order --in-asset=<asset_id> --out-asset=<asset_id> --rate=<rate>
  ```
- Fill an order:
  ```bash
  ./build/token-cli action fill-order --order-id=<order_id> --amount=<amount>
  ```

---

## Demos
Run end-to-end tests to explore TokenVM functionalities:
```bash
./scripts/test.sh
```
- Demonstrates minting, trading, and Avalanche Warp Messaging workflows.

---

## License
TokenVM is licensed under the BSD-3-Clause. See the LICENSE file for details.

---

## Contributing
Contributions are welcome! Please open issues or pull requests in this repository. For major changes, please discuss them in advance to ensure alignment.

---

## Acknowledgments
TokenVM is built using the HyperSDK and leverages Avalanche Warp Messaging for advanced interoperability. Special thanks to the contributors and maintainers of these tools for enabling such a robust implementation.

---
