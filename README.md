<p align="center">
  <img src="assets/evm_sniper_bot_logo.png" alt="EVM Sniper Bot Logo" width="600">
</p>

# 🎯 EVM Mempool Sniper Bot

[![Python 3.10+](https://img.shields.io/badge/python-3.10+-blue.svg)](https://www.python.org/downloads/)
[![Web3.py](https://img.shields.io/badge/web3.py-7.14.0-orange.svg)](https://web3py.readthedocs.io/)
[![License: MIT](https://img.shields.io/badge/License-MIT-green.svg)](LICENSE)

A high-performance liquidity sniping bot for **Uniswap V4** and compatible DEXs, featuring async mempool monitoring, Flashbots integration, and honeypot detection.

![Demo](https://img.shields.io/badge/Status-Portfolio%20Demo-purple)

## 📸 Demo

![Sniper Bot Demo](assets/demo.png)

---

## ⚡ Features

![Features Map](assets/features_map.png)

---

## 🏗️ Architecture

![Architecture Diagram](assets/architecture_diagram.png)

---

## 🚀 Quick Start

### Prerequisites

- Python 3.10+
- Alchemy or Infura WebSocket RPC
- (Optional) Flashbots reputation key

### Installation

```bash
# Clone the repository
git clone https://github.com/yourusername/evm-mempool-sniper.git
cd evm-mempool-sniper

# Create virtual environment
python -m venv .venv
.venv\Scripts\activate  # Windows
# source .venv/bin/activate  # Linux/Mac

# Install dependencies
pip install -r requirements.txt

# Configure environment
cp .env.example .env
# Edit .env with your RPC URLs and private key
```

### Run Demo

```bash
python sniper.py
```

**Expected Output:**

```
=================================================================
  UNISWAP SNIPER BOT v1.0.0
  Mempool Monitor | Flashbots Protect | Multi-Chain
=================================================================

[2024-05-22 14:30:15] INFO: Starting Ethereum mempool monitor...
[2024-05-22 14:30:17] INFO: Connected to Sepolia Testnet via Infura.
[2024-05-22 14:31:02] EVENT: PairCreated detected on Uniswap V2!
[2024-05-22 14:31:02] EVENT: PairCreated detected on Uniswap V2! Token: 0x....8f2a (TEST/ETH)
[2024-05-22 14:31:02] ACTION: Initiating buy transaction...  Gas: 150 gwei
[2024-05-22 14:31:03] SUCCESS: Buy transaction confirmed in block 5678901.
[2024-05-22 14:31:05] INFO: Calculating arbitrage opportunity...
[2024-05-22 14:31:06] ACTION: Executing sell on Sushiswap...
[2024-05-22 14:31:08] SUCCESS: Sell transaction confirmed. Simulated Profit: +0.045 ETH
[2024-05-22 14:31:10] INFO: Continuing mempool scan...
```

---

## 🔧 Configuration

Edit `.env` with your settings:

```env
# RPC Endpoints (WebSocket required)
ETH_WSS=wss://eth-mainnet.g.alchemy.com/v2/YOUR_KEY

# Wallet (use dedicated wallet!)
PRIVATE_KEY=your_private_key

# Flashbots
FLASHBOTS_RELAY=https://relay.flashbots.net
```

Trading parameters in `sniper.py`:

```python
SNIPE_AMOUNT_ETH = 0.5      # ETH per snipe
SLIPPAGE_PERCENT = 5.0      # Max slippage
PRIORITY_FEE_GWEI = 2.5     # Miner tip
MAX_BUY_TAX = 10.0          # Max acceptable tax
```

---

## 🔐 Security Features

- **Honeypot Detection**: Checks tokens via `honeypot.is` API before buying
- **Tax Limits**: Configurable max buy/sell tax thresholds
- **Flashbots Protect**: Private mempool to prevent sandwich attacks
- **Environment Variables**: Secrets never hardcoded

---

## 🛠️ Technical Stack

![Technical Stack](assets/technical_stack_table.png)

---

## 📚 Key Concepts

### Uniswap V4 (Jan 2025)

- **Singleton Pattern**: Single `PoolManager` contract manages all pools
- **Hooks**: Custom logic via `beforeSwap`/`afterSwap`
- **Address**: `0x000000000004444c5dc75cB358380D2e3dE08A90`

### MEV & Flashbots

- **MEV**: Maximal Extractable Value from transaction ordering
- **Flashbots Protect**: Private tx submission to avoid frontrunning
- **EIP-1559**: Priority fees for faster inclusion

---

## ⚠️ Disclaimer

![Disclaimer](assets/disclaimer.png)

---

## 📄 License

MIT License - see [LICENSE](License) for details.

<p align="center">
  Built with ❤️ for the Web3 community
</p>
