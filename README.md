# NFT Marketplace

A decentralized NFT marketplace built with Next.js and Hardhat, allowing users to create, buy, and resell NFTs on the blockchain.

## Features

- 🎨 **Create NFTs**: Mint and list your NFTs on the marketplace
- 💰 **Buy NFTs**: Purchase NFTs from other users
- 🔄 **Resell NFTs**: Resell your purchased NFTs
- 📊 **Dashboard**: View your owned NFTs and listed items
- 🔐 **Web3 Integration**: Connect your wallet using Web3Modal
- 📦 **IPFS Storage**: NFT metadata stored on IPFS

## Tech Stack

- **Frontend**: Next.js 11, React 17, Tailwind CSS
- **Blockchain**: Solidity, Hardhat, Ethers.js
- **Smart Contracts**: OpenZeppelin ERC721
- **Wallet**: Web3Modal
- **Storage**: IPFS (via ipfs-http-client)

## Prerequisites

- Node.js (v14 or higher)
- npm or yarn
- MetaMask or another Web3 wallet
- IPFS node (or use a public IPFS gateway)

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

4. Update `config.js` with your deployed contract addresses (after deployment).

## Development

### Running the Development Server

Start the Next.js development server:
```bash
npm run dev
# or
yarn dev
```

Open [http://localhost:3000](http://localhost:3000) in your browser.

### Compiling Smart Contracts

Compile the Solidity contracts:
```bash
npx hardhat compile
```

### Running Tests

Run the test suite:
```bash
npx hardhat test
```

### Deploying Smart Contracts

#### Local Deployment (Hardhat Network)

1. Start a local Hardhat node:
```bash
npx hardhat node
```

2. In a new terminal, deploy the contracts:
```bash
npx hardhat run scripts/deploy.js --network localhost
```

The deployment script will automatically update `config.js` with the deployed contract address.

#### Polygon Mumbai Testnet

1. Update `hardhat.config.js` to uncomment the Mumbai network configuration
2. Set your private key in environment variables:
```bash
export privateKey=your_private_key_here
```

3. Deploy to Mumbai:
```bash
npx hardhat run scripts/deploy.js --network mumbai
```

4. Update `config.js` with the deployed contract address.

#### Polygon Mainnet

1. Update `hardhat.config.js` to uncomment the Polygon mainnet configuration
2. Set your private key in environment variables
3. Deploy to mainnet:
```bash
npx hardhat run scripts/deploy.js --network matic
```

4. Update `config.js` with the deployed contract address.

## Project Structure

```
monad-bundler-volume-bot/
├── contracts/           # Solidity smart contracts
│   └── NFTMarketplace.sol
├── pages/              # Next.js pages
│   ├── index.js        # Home/Marketplace page
│   ├── create-nft.js   # Create NFT page
│   ├── my-nfts.js      # My NFTs page
│   ├── resell-nft.js   # Resell NFT page
│   └── dashboard.js    # Dashboard page
├── scripts/            # Deployment scripts
│   └── deploy.js
├── styles/            # CSS styles
├── public/            # Static assets
├── config.example.js  # Example configuration
├── hardhat.config.js  # Hardhat configuration
└── package.json       # Dependencies
```

## Smart Contract

The `NFTMarketplace` contract is an ERC721 token contract that includes marketplace functionality:

- **createToken**: Mint a new NFT and list it on the marketplace
- **createMarketSale**: Purchase an NFT from the marketplace
- **resellToken**: Resell a purchased NFT
- **fetchMarketItems**: Get all unsold items
- **fetchMyNFTs**: Get NFTs owned by the caller
- **fetchItemsListed**: Get items listed by the caller

The contract charges a listing fee (default: 0.025 ETH) for each listing.

## Usage

1. **Connect Wallet**: Click the connect button and select your wallet
2. **Create NFT**: 
   - Go to the "Create NFT" page
   - Upload your image (stored on IPFS)
   - Enter name, description, and price
   - Pay the listing fee and mint your NFT
3. **Buy NFT**: 
   - Browse available NFTs on the homepage
   - Click "Buy" on any NFT
   - Confirm the transaction in your wallet
4. **View Your NFTs**: 
   - Go to "My NFTs" to see your purchased NFTs
   - Go to "Dashboard" to see your listed items
5. **Resell NFT**: 
   - Select an NFT from "My NFTs"
   - Set a new price and pay the listing fee

## Configuration

### Network Configuration

Edit `hardhat.config.js` to configure networks:

- **Hardhat**: Local development network (chainId: 1337)
- **Mumbai**: Polygon Mumbai testnet
- **Matic**: Polygon mainnet

### Contract Addresses

After deployment, update `config.js` with your contract addresses:

```javascript
export const marketplaceAddress = "0x..."
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

## License

See [LICENSE.txt](LICENSE.txt) for details.

## Contributing

Contributions are welcome! Please feel free to submit a Pull Request.

## Support

For issues and questions, please open an issue on the repository.

