# Privacy-First AI Service Marketplace 🤖🪙

A decentralized platform for privacy-preserving AI services, integrating HTTP privacy APIs (from [AI-Robotic-Labs/http-privacy](https://github.com/AI-Robotic-Labs/http-privacy)), Nostr for secure communication, and Bitcoin UTXOs for private payments. Users can access AI models (e.g., Grok, Stable Diffusion) anonymously, communicate with providers via Nostr, and pay using Bitcoin with privacy techniques like CoinJoin.

**Status: Proof-of-concept (PoC). The http-privacy project is in beta, so use with caution.**

## Features

- **Anonymous AI Access**: Query AI APIs via HTTP with a SOCKS5 proxy for IP anonymity, leveraging http-privacy Python bindings.
- **Decentralized Communication**: Use Nostr for pseudonymous, encrypted messaging between users and AI service providers.
- **Private Payments**: Pay for services using Bitcoin UTXOs, with support for CoinJoin to obscure transaction origins.
- **Modular Design**: Built with Python, extensible to other languages (Rust, C++, JavaScript) supported by http-privacy.
- **Future-Ready**: Planned support for Lightning Network and additional AI models (e.g., Claude, Llama) per the http-privacy roadmap.

## Architecture

The platform integrates three layers:

### Access Layer (HTTP Privacy)
- Uses http-privacy APIs to interact with AI services (e.g., Grok).
- Routes requests through a SOCKS5 proxy (e.g., Tor or http-privacy’s proxy) to hide IP addresses.
- Encrypts payloads for data privacy.

### Communication Layer (Nostr)
- Nostr relays handle service discovery, negotiation, and result delivery.
- Encrypted direct messages ensure secure coordination (e.g., sharing Bitcoin addresses).

### Payment Layer (UTXOs)
- Bitcoin UTXOs enable pseudonymous payments.
- Privacy is enhanced with CoinJoin or Lightning Network (future).

## Workflow

1. A user browses AI service listings on Nostr relays via a Tor browser.
2. They send an encrypted Nostr message to a provider with a query (e.g., "Generate a summary").
3. The provider responds with a Bitcoin address and price (e.g., 0.001 BTC).
4. The user sends a CoinJoin-mixed payment and queries the AI API via http-privacy.
5. The provider delivers the result (e.g., generated text) via Nostr.

## Installation

### Prerequisites
- Python 3.8+
- A running SOCKS5 proxy (e.g., Tor at `127.0.0.1:9050` or http-privacy’s proxy, once available).
- A Bitcoin wallet supporting CoinJoin (e.g., Wasabi Wallet, not yet integrated).
- Nostr keypair for user and provider.

### Setup

1. **Clone the Repository**:
   ```bash
   git clone https://github.com/AI-Robotic-Labs/privacy-ai-marketplace.git
   cd privacy-ai-marketplace
   ```

2. **Install Dependencies**:
   ```bash
   pip install requests pysocks nostr
   ```

3. **Configure the Client**:
   - Edit `ai_privacy_client.py` to set:
     - `SOCKS5_PROXY`: Your proxy address (e.g., `127.0.0.1:9050`).
     - `AI_API_ENDPOINT`: The http-privacy API URL (placeholder: `http://example.com/api/grok`).
     - `NOSTR_RELAYS`: List of Nostr relays (e.g., `wss://relay.damus.io`).
     - `USER_PRIVATE_KEY`: Your Nostr private key.
     - `PROVIDER_PUBKEY`: The AI provider’s Nostr public key.

4. **Run the Client**:
   ```bash
   python ai_privacy_client.py
   ```

## Usage

1. Ensure your SOCKS5 proxy is running.
2. Run the client to:
   - Send a Nostr request to an AI provider (e.g., for text generation).
   - Receive a Bitcoin address and price via Nostr.
   - Simulate a Bitcoin payment (UTXO-based, placeholder).
   - Query the AI API via http-privacy and display the result.
3. Check console output for the AI response or errors.

**Example**:
```bash
$ python ai_privacy_client.py
Sent Nostr request with ID: 123e4567-...
Received provider response: {"bitcoin_address": "bc1...", "price_btc": 0.001}
Initiating payment of 0.001 BTC to bc1...
AI Result: Decentralized systems enhance privacy by...
```

## Roadmap

- **Bitcoin Integration**: Add full Bitcoin wallet support (e.g., `bitcoinlib` or Wasabi) for UTXO payments with CoinJoin.
- **Lightning Network**: Enable fast, low-cost payments via Lightning, using Nostr for invoice exchange.
- **http-privacy Updates**: Incorporate new AI model bindings (e.g., Claude, Llama) and the MCP server from the http-privacy roadmap.
- **GUI Client**: Develop a user-friendly interface (e.g., with `tkinter` or web-based).
- **Reputation System**: Use Nostr events for decentralized provider ratings.
- **Monero Support**: Add Monero for stronger payment privacy.

## Limitations

- **Beta Dependency**: The http-privacy project is in beta, so API bindings and SOCKS5 proxy may be unstable.
- **Placeholder Payment**: Bitcoin payment logic is simulated; real wallet integration is pending.
- **Nostr Relay Trust**: Relays could log metadata. Use multiple relays or run your own for privacy.
- **Complexity**: Users must manage Nostr keys and Bitcoin wallets manually.
