# Blockchain Project

A Python-based blockchain implementation created as a practice project to learn the fundamentals of Python programming and blockchain technology.

## Overview

This project implements a complete blockchain system with cryptocurrency functionality, including:

- **Blockchain Core**: Chain of blocks with proof-of-work consensus
- **Cryptocurrency**: Transaction system with digital signatures
- **Wallet System**: RSA-based key generation and transaction signing
- **Peer-to-Peer Network**: Multi-node blockchain network with conflict resolution
- **Web Interface**: Flask-based REST API and web UI

## Features

### Core Blockchain
- **Block Structure**: Each block contains transactions, previous hash, proof of work, and timestamp
- **Proof of Work**: Mining algorithm requiring hash with two leading zeros
- **Chain Validation**: Automatic verification of blockchain integrity
- **Persistence**: Save and load blockchain data from files

### Cryptocurrency
- **Transactions**: Send and receive coins between wallets
- **Digital Signatures**: RSA-based transaction signing and verification
- **Balance Tracking**: Calculate balances from transaction history
- **Mining Rewards**: Miners receive rewards for creating new blocks

### Network Features
- **Peer Nodes**: Connect multiple nodes to form a network
- **Transaction Broadcasting**: Automatically share transactions across the network
- **Block Broadcasting**: Share newly mined blocks with peers
- **Conflict Resolution**: Automatically resolve chain conflicts using longest valid chain

### Web Interface
- **REST API**: Full API for interacting with the blockchain
- **Web UI**: HTML interfaces for node and network management

## Project Structure

```
.
├── blockchain.py      # Main blockchain class
├── block.py          # Block data structure
├── transaction.py    # Transaction data structure
├── wallet.py         # Wallet and cryptographic functions
├── node.py           # Flask web server and API endpoints
├── pyproject.toml    # Project metadata and dependencies
├── uv.lock           # Dependency lock file (auto-generated)
├── ui/               # Web interface files
│   ├── node.html
│   └── network.html
└── utility/          # Helper modules
    ├── hash_util.py   # Hashing functions
    ├── verification.py # Validation and verification logic
    └── printable.py  # Base class for object representation
```

## Requirements

- Python 3.8+
- [uv](https://github.com/astral-sh/uv) - Fast Python package installer and resolver

## Installation

This project uses [uv](https://github.com/astral-sh/uv) for dependency management and virtual environment handling.

### Installing uv

If you haven't installed uv yet, you can install it using:

```bash
# macOS and Linux
curl -LsSf https://astral.sh/uv/install.sh | sh

# Windows (PowerShell)
powershell -ExecutionPolicy ByPass -c "irm https://astral.sh/uv/install.ps1 | iex"

# Or via pip
pip install uv
```

### Setting up the Project

1. Clone or navigate to the project directory:
```bash
cd next-steps-01-finished
```

2. Install dependencies and create a virtual environment:
```bash
uv sync
```

This will:
- Create a virtual environment in `.venv/`
- Install all project dependencies from `pyproject.toml`
- Install development dependencies (mypy, type stubs, etc.)

3. Activate the virtual environment (optional - uv commands work without activation):
```bash
# macOS/Linux
source .venv/bin/activate

# Windows
.venv\Scripts\activate
```

### Installing Development Dependencies

To install dependencies including development tools:

```bash
uv sync --all-groups
```

### Common uv Commands

- **Install dependencies**: `uv sync`
- **Add a new dependency**: `uv add package-name`
- **Add a development dependency**: `uv add --dev package-name`
- **Remove a dependency**: `uv remove package-name`
- **Run a command in the virtual environment**: `uv run python script.py`
- **Show installed packages**: `uv pip list`
- **Update dependencies**: `uv lock --upgrade`

## Usage

### Starting a Node

Run a blockchain node using uv:

```bash
# Using uv run (recommended - automatically uses virtual environment)
uv run python node.py -p 8000

# Or activate the virtual environment first
source .venv/bin/activate  # macOS/Linux
python node.py -p 8000
```

Or use the default port (8000):

```bash
uv run python node.py
```

### Accessing the Web Interface

Once the node is running, open your browser and navigate to:

- **Node Interface**: `http://localhost:8000/` (or your specified port)
- **Network Interface**: `http://localhost:8000/network`

### API Endpoints

#### Wallet Management
- `POST /wallet` - Create new wallet keys
- `GET /wallet` - Load existing wallet keys
- `GET /balance` - Get wallet balance

#### Transactions
- `POST /transaction` - Create a new transaction
- `GET /transactions` - Get all open transactions
- `POST /broadcast-transaction` - Broadcast transaction to network

#### Mining
- `POST /mine` - Mine a new block

#### Blockchain
- `GET /chain` - Get the full blockchain
- `POST /broadcast-block` - Broadcast a block to network
- `POST /resolve-conflicts` - Resolve blockchain conflicts

#### Network
- `POST /node` - Add a peer node
- `DELETE /node/<node_url>` - Remove a peer node
- `GET /nodes` - Get all peer nodes

## How It Works

### Creating a Wallet

1. Start a node
2. Use the web interface or API to create wallet keys
3. Keys are saved to `wallet-{node_id}.txt`

### Making Transactions

1. Ensure you have a wallet with sufficient balance
2. Create a transaction specifying recipient and amount
3. Transaction is signed with your private key
4. Transaction is broadcast to all peer nodes

### Mining Blocks

1. Open transactions are collected
2. Proof of work is calculated (finding a hash with two leading zeros)
3. Block is created with transactions and proof
4. Miner receives a mining reward
5. Block is broadcast to all peer nodes

### Network Consensus

- When multiple nodes exist, they share transactions and blocks
- If chains diverge, the longest valid chain is accepted
- Conflict resolution ensures all nodes converge to the same chain

## Learning Objectives

This project demonstrates:

- **Object-Oriented Programming**: Classes, inheritance, properties
- **Data Structures**: Lists, dictionaries, sets
- **File I/O**: Reading and writing data to files
- **Cryptography**: RSA encryption, digital signatures, hashing
- **Networking**: HTTP requests, REST APIs
- **Web Development**: Flask framework, JSON APIs
- **Blockchain Concepts**: Proof of work, consensus, distributed systems

## File Persistence

The blockchain stores data in files:

- `blockchain-{node_id}.txt` - Blockchain and transaction data
- `wallet-{node_id}.txt` - Wallet keys (private and public)

**Note**: Keep your wallet files secure! Losing your private key means losing access to your funds.

## Limitations

This is an educational project and has several limitations:

- Simple proof of work (not suitable for production)
- No protection against double-spending attacks in all scenarios
- No transaction fees beyond mining rewards
- Basic conflict resolution (longest chain wins)
- No encryption of stored data
- Limited scalability

## Future Enhancements

Potential improvements for learning:

- Implement Merkle trees for transaction verification
- Add transaction fees
- Implement UTXO (Unspent Transaction Output) model
- Add smart contract functionality
- Improve network security and validation
- Add database persistence instead of text files
- Implement more sophisticated consensus algorithms

## License

This is an educational project created for learning purposes.
