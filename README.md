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

| Feature                | Description                                       |
| ---------------------- | ------------------------------------------------- |
| **Uniswap V4**         | Supports latest PoolManager singleton pattern     |
| **Async WebSocket**    | Real-time mempool monitoring with `eth_subscribe` |
| **Flashbots Protect**  | Private transactions to prevent frontrunning      |
| **Honeypot Detection** | API-based scam token filtering                    |
| **EIP-1559 Gas**       | Dynamic priority fee optimization                 |
| **Multi-Chain**        | ETH Mainnet, Base, Arbitrum ready                 |

---

## 🏗️ Architecture

```
┌─────────────────┐     ┌──────────────────┐     ┌─────────────────┐
│  WebSocket RPC  │────▶│  Mempool Scanner │────▶│ Event Detection │
└─────────────────┘     └──────────────────┘     └────────┬────────┘
                                                          │
                                                          ▼
┌─────────────────┐     ┌──────────────────┐     ┌─────────────────┐
│   Flashbots     │◀────│  TX Builder      │◀────│ Honeypot Check  │
│   Protect RPC   │     │  (EIP-1559)      │     │ (honeypot.is)   │
└─────────────────┘     └──────────────────┘     └─────────────────┘
```

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
============================================================
  EVM MEMPOOL SNIPER BOT v1.0.0
  Uniswap V4 | Flashbots Protect | Multi-Chain
============================================================

[15:42:01] 🔗 Connected: Ethereum Mainnet [Block #19842103]
[15:42:01] 📡 Subscribed: newPendingTransactions
[15:42:01] 🔍 Monitoring Uniswap V4 PoolManager...
[15:42:02] 🔍 Scanning Block #19842103...
[15:42:03] 🔍 Scanning Block #19842104...
[15:42:04] ⚡ NEW PAIR: WETH/0x6B17547...
[15:42:04] 🔒 Honeypot Check: ✅ SAFE (Buy: 0.0%, Sell: 0.0%)
[15:42:04] 💰 Preparing snipe: 0.5 ETH → 0x6B17547...
[15:42:04] ⛽ Gas: 42.0 Gwei | Priority: 2.5 Gwei
[15:42:04] 🚀 Submitting via Flashbots Protect...
[15:42:05] ✅ Private TX Sent: 0x3b8a7c9d...a7b
[15:42:05] 🛡️ MEV Protection: ACTIVE
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

| Component      | Technology             |
| -------------- | ---------------------- |
| Runtime        | Python 3.10+ / asyncio |
| Web3           | web3.py 7.14.0         |
| HTTP           | aiohttp (async)        |
| WebSocket      | websockets 12.0        |
| MEV Protection | Flashbots Protect RPC  |

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

**This software is for educational and portfolio demonstration purposes only.**

- Cryptocurrency trading carries significant financial risk
- Past performance does not guarantee future results
- Never invest more than you can afford to lose
- This code is NOT financial advice

---

## 📄 License

MIT License - see [LICENSE](LICENSE) for details.

---

## 🤝 Contributing

Contributions welcome! Please read the contributing guidelines first.

---

<p align="center">
  Built with ❤️ for the Web3 community
</p>
