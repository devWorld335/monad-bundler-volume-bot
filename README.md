# Monad Bundler Volume Bot

An automated monitoring bot that tracks, analyzes, and reports trading volume data for assets bundled via the Monad blockchain. Provides real-time insights into volume fluctuations, detects anomalies, and sends alerts to help traders, liquidity providers, and project teams track market activity effectively.

### Key Capabilities

- **Real-time Volume Tracking**: Continuously monitors trading volume for selected bundles or assets on the Monad blockchain
- **Anomaly Detection**: Automatically flags sudden spikes, drops, or unusual patterns in volume activity
- **Multi-channel Alerts**: Sends notifications via Discord, Telegram, email, or other configured channels when volume thresholds are exceeded
- **Historical Analytics**: Aggregates and stores volume data over customizable time intervals (hourly, daily, weekly) for trend analysis
- **Configurable Watchlists**: Monitor specific assets, bundles, or trading pairs based on your requirements
- **Dashboard Interface**: Web-based dashboard built with Next.js for visualizing volume trends and bot status

The bot integrates with Monad's blockchain infrastructure to fetch real-time transaction data, calculate volume metrics, and maintain a historical database for comprehensive market analysis. It's designed to be lightweight, modular, and easily extensible for custom monitoring requirements.

## Features

- 📊 **Volume Monitoring**: Real-time tracking of bundler volume across configured assets
- 🔔 **Smart Alerts**: Threshold-based notifications for volume changes, spikes, or anomalies
- 📈 **Analytics Dashboard**: Web interface for viewing volume trends and statistics
- 🔍 **Anomaly Detection**: Automatic identification of unusual volume patterns
- 📝 **Historical Data**: Persistent storage of volume history for trend analysis
- ⚙️ **Configurable**: Easy setup with configurable watchlists, thresholds, and intervals
- 🔐 **Web3 Integration**: Direct blockchain interaction via Ethers.js and Hardhat
- 🚀 **Production Ready**: Built with Next.js for scalable deployment

## Tech Stack

- **Frontend**: Next.js 11, React 17, Tailwind CSS
- **Blockchain**: Solidity, Hardhat, Ethers.js
- **Data Storage**: IPFS for metadata, local/cloud database for volume history
- **Notifications**: Discord/Telegram bot integration (configurable)
- **Monitoring**: Real-time RPC polling and event listening
- **Deployment**: Docker support, cloud-ready architecture

## Prerequisites

- Node.js (v14 or higher)
- npm or yarn
- Access to Monad blockchain RPC endpoint
- (Optional) Discord/Telegram bot tokens for notifications
- (Optional) Database for historical data storage

## Installation

1. Clone the repository:
```bash
git clone <repository-url>
cd monad-bundler-volume-bot
```

2. Install dependencies:
```bash
npm install
# or
yarn install
```

3. Set up configuration:
```bash
cp config.example.js config.js
```

4. Configure your settings in `config.js`:
   - Monad RPC endpoint
   - Assets/bundles to monitor
   - Volume thresholds
   - Notification channels
   - Polling intervals

## Configuration

### Environment Variables

Create a `.env` file or update `config.js` with the following:

```javascript
// RPC Configuration
export const RPC_URL = "https://your-monad-rpc-endpoint.com"
export const CHAIN_ID = 1337 // Monad chain ID

// Monitoring Configuration
export const POLLING_INTERVAL = 60000 // 1 minute in milliseconds
export const VOLUME_THRESHOLD = 1000 // Minimum volume to trigger alerts
export const PERCENTAGE_CHANGE_THRESHOLD = 50 // % change to trigger alerts

// Watchlist
export const WATCH_LIST = [
  "0x...", // Asset addresses or bundle identifiers
]

// Notification Settings
export const DISCORD_WEBHOOK_URL = "your-discord-webhook-url"
export const TELEGRAM_BOT_TOKEN = "your-telegram-bot-token"
export const TELEGRAM_CHAT_ID = "your-telegram-chat-id"

// Database (optional)
export const DATABASE_URL = "your-database-connection-string"
```

### Network Configuration

Edit `hardhat.config.js` to configure Monad network:

```javascript
networks: {
  monad: {
    url: process.env.RPC_URL || "https://monad-rpc-endpoint.com",
    chainId: 1337, // Update with actual Monad chain ID
    accounts: process.env.PRIVATE_KEY ? [process.env.PRIVATE_KEY] : []
  }
}
```

## Development

### Running the Bot

Start the monitoring bot:
```bash
npm run dev
# or
yarn dev
```

The bot will:
1. Connect to the Monad blockchain via RPC
2. Start monitoring configured assets/bundles
3. Begin tracking volume data
4. Send alerts when thresholds are exceeded

### Running the Dashboard

Start the Next.js dashboard:
```bash
npm run dev
```

Open [http://localhost:3000](http://localhost:3000) to view the dashboard.

### Compiling Smart Contracts

If using smart contracts for data aggregation:
```bash
npx hardhat compile
```

### Running Tests

Run the test suite:
```bash
npx hardhat test
```

## Usage

### Basic Monitoring

1. **Configure Watchlist**: Add asset addresses or bundle identifiers to monitor in `config.js`
2. **Set Thresholds**: Configure volume and percentage change thresholds
3. **Start Bot**: Run `npm run dev` to begin monitoring
4. **View Dashboard**: Access the web dashboard at `http://localhost:3000`

### Alert Configuration

The bot can send alerts when:
- Volume exceeds a specified threshold
- Volume changes by a certain percentage
- Anomalies are detected in volume patterns
- Custom conditions are met

### Dashboard Features

- **Real-time Volume Display**: See current volume for all monitored assets
- **Historical Charts**: View volume trends over time
- **Alert History**: Review past alerts and notifications
- **Configuration Panel**: Update monitoring settings from the UI

## Project Structure

```
monad-bundler-volume-bot/
├── contracts/           # Solidity smart contracts (if needed)
│   └── NFTMarketplace.sol
├── pages/              # Next.js dashboard pages
│   ├── index.js        # Main dashboard
│   ├── dashboard.js    # Volume analytics dashboard
│   ├── create-nft.js   # Asset configuration (if applicable)
│   ├── my-nfts.js      # Monitored assets view
│   └── resell-nft.js   # Alert configuration
├── scripts/            # Bot scripts and utilities
│   └── deploy.js       # Deployment scripts
├── services/           # Core bot services
│   ├── volume-tracker.js    # Volume monitoring logic
│   ├── anomaly-detector.js  # Anomaly detection
│   └── notifier.js          # Alert sending
├── styles/            # CSS styles
├── public/            # Static assets
├── config.example.js  # Example configuration
├── hardhat.config.js  # Hardhat configuration
└── package.json       # Dependencies
```

## Monitoring Logic

The bot operates on the following principles:

1. **Data Collection**: Polls Monad blockchain RPC endpoints at configured intervals
2. **Volume Calculation**: Aggregates transaction volumes for monitored assets
3. **Pattern Analysis**: Compares current volume against historical baselines
4. **Alert Triggering**: Sends notifications when configured conditions are met
5. **Data Storage**: Persists volume data for historical analysis

## Deployment

### Local Deployment

1. Configure your settings in `config.js`
2. Start the bot: `npm run dev`
3. Access dashboard at `http://localhost:3000`

### Production Deployment

1. Build the application:
```bash
npm run build
```

2. Start production server:
```bash
npm start
```

3. Use process managers like PM2 for long-running operation:
```bash
pm2 start npm --name "monad-volume-bot" -- start
```

### Docker Deployment

```bash
docker build -t monad-volume-bot .
docker run -d --env-file .env monad-volume-bot
```

## Configuration Examples

### Monitoring Specific Assets

```javascript
export const WATCH_LIST = [
  "0x1234...", // Token A
  "0x5678...", // Token B
  "0x9abc...", // Bundle contract
]
```

### Alert Thresholds

```javascript
export const VOLUME_THRESHOLD = 10000 // Alert if volume > 10,000
export const PERCENTAGE_CHANGE_THRESHOLD = 25 // Alert if volume changes > 25%
export const SPIKE_DETECTION = true // Enable anomaly detection
```

## Building for Production

Build the Next.js application:

```bash
npm run build
# or
yarn build
```

Start the production server:

```bash
npm start
# or
yarn start
```

## Troubleshooting

### Bot Not Connecting

- Verify RPC endpoint is accessible
- Check network configuration in `hardhat.config.js`
- Ensure chain ID matches Monad network

### Alerts Not Sending

- Verify notification credentials (Discord webhook, Telegram token)
- Check bot permissions
- Review alert threshold settings

### Volume Data Not Updating

- Verify polling interval configuration
- Check RPC endpoint rate limits
- Review asset addresses in watchlist

## License

See [LICENSE.txt](LICENSE.txt) for details.

## Contributing

Contributions are welcome! Please feel free to submit a Pull Request.

## Support

For issues and questions, please open an issue on the repository.
