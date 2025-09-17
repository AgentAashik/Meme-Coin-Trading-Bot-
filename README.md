# Meme Coin Trading Bot

A Solana-based trading bot designed to scan, filter, and trade new meme coins on the Solana blockchain. The bot uses **DEX Screener** for real-time market data, **Jupiter API** for swaps, and **PostgreSQL** for data storage.

---

## Features

- **Real-time Scanning**: Fetches new meme coins from DEX Screener.
- **Trading Filters**: Filters coins based on liquidity, volume, and contract age.
- **Automated Trading**: Executes buy/sell orders using Jupiter API.
- **Price Monitoring**: Tracks prices via WebSocket for profit/stop-loss conditions.
- **Data Storage**: Logs all trades and performance metrics in a PostgreSQL database.

---

## Prerequisites

Before running the bot, ensure you have the following:

1. **Python 3.8+**: Install Python from [python.org](https://www.python.org/).
2. **Solana CLI**: Install the Solana CLI for wallet management:
   ```bash
   sh -c "$(curl -sSfL https://release.solana.com/stable/install)"
   ```
3. **PostgreSQL**: Install PostgreSQL for data storage:
   ```bash
   sudo apt-get install postgresql postgresql-contrib
   ```
4. **API Keys**:
   - [DEX Screener API Key](https://dexscreener.com/)
   - [Jupiter API Key](https://jup.ag/)

---

## Setup

### 1. Clone the Repository
Clone the repository to your local machine:
```bash
git clone https://github.com/agentaashik/meme-coin-trading-bot.git
cd meme-coin-trading-bot
```

### 2. Install Dependencies
Install the required Python packages:
```bash
pip install -r requirements.txt
```

### 3. Set Up `.env` File
Create a `.env` file in the root directory and add the following configuration:

```plaintext
# API Keys and Secrets
DEX_SCREENER_API_KEY=your_dex_screener_api_key
JUPITER_API_KEY=your_jupiter_api_key
SOLANA_RPC_URL=https://api.testnet.solana.com  # Use Testnet for testing

# Wallet Configuration
PRIVATE_KEY=your_solana_wallet_private_key
WALLET_ADDRESS=your_solana_wallet_address

# Trading Parameters
MIN_LIQUIDITY=50e9  # 50 SOL
MIN_VOLUME=100e9    # 100 SOL
MAX_CONTRACT_AGE=300  # 5 minutes
PROFIT_TARGET=1.2    # 20% profit
STOP_LOSS=0.8        # 20% loss

# Database Configuration
DB_HOST=localhost
DB_PORT=5432
DB_NAME=meme_bot
DB_USER=postgres
DB_PASSWORD=your_db_password
```

### 4. Set Up PostgreSQL Database
Create a database and table for storing trade data:
```sql
CREATE DATABASE meme_bot;

\c meme_bot;

CREATE TABLE trades (
    id SERIAL PRIMARY KEY,
    pair_address TEXT NOT NULL,
    base_token TEXT NOT NULL,
    quote_token TEXT NOT NULL,
    amount NUMERIC NOT NULL,
    price NUMERIC NOT NULL,
    timestamp TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);
```

### 5. Fund Your Wallet
If using **Testnet**, airdrop Testnet SOL to your wallet:
```bash
solana airdrop 10
```

---

## Running the Bot

1. **Start the Bot**:
   Run the bot using Python:
   ```bash
   python main.py
   ```

2. **Monitor Logs**:
   The bot will log its actions to the console. Example logs:
   ```
   [INFO] New pair found: MEME
   [INFO] Executing buy order for MEME...
   [INFO] Buy order completed.
   [INFO] Monitoring price for MEME...
   [INFO] Sell order executed at 20% profit.
   ```

3. **Check Database**:
   Use a PostgreSQL client (e.g., `psql` or pgAdmin) to view trade data:
   ```sql
   SELECT * FROM trades;
   ```

---

## Bot Workflow

1. **Scan**:
   - Fetches new meme coin pairs from DEX Screener every minute.
2. **Filter**:
   - Filters pairs based on liquidity, volume, and contract age.
3. **Buy**:
   - Executes a buy order using Jupiter API if the pair meets the criteria.
4. **Monitor**:
   - Tracks the price via WebSocket and sells when the profit target or stop-loss is reached.
5. **Log**:
   - Stores all trade data in the PostgreSQL database for analysis.

---

## Configuration

### Trading Parameters
You can adjust the trading parameters in the `.env` file:
- `MIN_LIQUIDITY`: Minimum liquidity required (in lamports).
- `MIN_VOLUME`: Minimum 24-hour volume required (in lamports).
- `MAX_CONTRACT_AGE`: Maximum age of the token contract (in seconds).
- `PROFIT_TARGET`: Target profit percentage (e.g., `1.2` for 20% profit).
- `STOP_LOSS`: Stop-loss percentage (e.g., `0.8` for 20% loss).

---

## Testing on Solana Testnet

To test the bot on Solana Testnet:
1. Update `.env` to use Testnet RPC:
   ```plaintext
   SOLANA_RPC_URL=https://api.testnet.solana.com
   ```
2. Use a Testnet wallet and airdrop Testnet SOL:
   ```bash
   solana airdrop 10
   ```
3. Run the bot and monitor transactions on the [Solana Testnet Explorer](https://explorer.solana.com/?cluster=testnet).

---

## Contributing

Contributions are welcome! Follow these steps:
1. Fork the repository.
2. Create a new branch:
   ```bash
   git checkout -b feature/your-feature
   ```
3. Commit your changes:
   ```bash
   git commit -m "Add your feature"
   ```
4. Push to the branch:
   ```bash
   git push origin feature/your-feature
   ```
5. Open a pull request.

---

## License

This project is licensed under the MIT License. See the [LICENSE](LICENSE) file for details.

---

## Support

For questions or issues, please open an issue on the [GitHub repository](https://github.com/your-username/meme-coin-trading-bot/issues).

---

🚀 **Happy Trading!** 🚀
