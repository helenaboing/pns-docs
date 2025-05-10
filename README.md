# PNS (Polkadot Naming Service) Documentation

## Introduction

PNS (Polkadot Naming Service) is a decentralized naming system built specifically for the Polkadot ecosystem. It provides human-readable names for blockchain addresses, making it easier to manage multiple addresses across different parachains and enhancing the overall wallet user experience.

### Key Features

- Human-readable names for blockchain addresses
- Cross-chain compatibility within the Polkadot ecosystem
- Simple registration and transfer system
- Enhanced wallet user experience
- Secure and decentralized architecture

## Architecture

### Smart Contracts

PNS consists of several key smart contracts:

1. **PNSRegistry**: The main registry contract that manages domain ownership and records
2. **PublicResolver**: Handles the resolution of names to addresses and other records
3. **Base Contracts**: Core functionality for managing domains and subdomains

### Frontend Application

The frontend is built with:
- Next.js
- TypeScript
- Tailwind CSS
- Modern React patterns and best practices

## Getting Started

### Prerequisites

- Node.js (v18 or higher)
- pnpm (for package management)
- A Web3 wallet (like MetaMask)

### Installation

1. Clone the repository:
```bash
git clone https://github.com/mokita-j/pns.git
cd pns
```

2. Install dependencies for the frontend:
```bash
cd pns-app
pnpm install
```

3. Set up your environment variables:
Create a `.env.local` file in the `pns-app` directory with:
```bash
NEXT_PUBLIC_WALLET_CONNECT_PROJECT_ID=your_project_id_here
```

### Development

To run the frontend application in development mode:
```bash
cd pns-app
pnpm dev
```

The application will be available at `http://localhost:3000`.

## Smart Contract Architecture

### PNSRegistry

The PNSRegistry contract is the core of the naming system, providing:

- Domain ownership management
- Subdomain creation and management
- Resolver management
- TTL (Time To Live) settings
- Operator approvals

### PublicResolver

The PublicResolver contract handles:
- Address resolution
- Content hash management
- Interface support verification

## API Reference

### Smart Contract Functions

#### PNSRegistry

- `setRecord(bytes32 node, address owner, address resolver, uint64 ttl)`
- `setSubnodeRecord(bytes32 node, bytes32 label, address owner, address resolver, uint64 ttl)`
- `setOwner(bytes32 node, address owner)`
- `setResolver(bytes32 node, address resolver)`
- `setTTL(bytes32 node, uint64 ttl)`
- `owner(bytes32 node)`
- `resolver(bytes32 node)`
- `ttl(bytes32 node)`

#### PublicResolver

- `addr(bytes32 node)`
- `setAddr(bytes32 node, address newAddr)`
- `supportsInterface(bytes4 interfaceID)`

## Deployment

### Frontend Deployment (Vercel)

1. Push your code to a GitHub repository
2. Go to [Vercel](https://vercel.com)
3. Sign up or log in with your GitHub account
4. Click "New Project"
5. Import your repository
6. Configure the project:
   - Root Directory: pns-app
7. Add your environment variables in the Vercel dashboard
8. Click "Deploy"

### Smart Contract Deployment

The smart contracts can be deployed using Hardhat. The deployment process is managed through the Ignition module system.

## Contributing

We welcome contributions to PNS! Please see our contributing guidelines for more information.

## License

This project is licensed under the MIT License - see the LICENSE file for details.
