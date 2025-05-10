# PNS Developer Guide

## Introduction

This guide provides detailed information for developers who want to integrate with the Polkadot Naming Service (PNS). It covers both smart contract integration and frontend development.

## Smart Contract Integration

### Contract Addresses

The PNS contracts are deployed on the Westend Asset Hub testnet:

```javascript
const PNS_REGISTRY_ADDRESS = "0x..."; // Add actual address
const PUBLIC_RESOLVER_ADDRESS = "0x..."; // Add actual address
```

### Basic Integration

#### 1. Installing Dependencies

```bash
npm install @pns/contracts
# or
yarn add @pns/contracts
# or
pnpm add @pns/contracts
```

#### 2. Contract Interaction Example

```typescript
import { PNSRegistry, PublicResolver } from "@pns/contracts";
import { ethers } from "ethers";

async function resolveName(name: string) {
  const provider = new ethers.providers.Web3Provider(window.ethereum);
  const registry = new ethers.Contract(PNS_REGISTRY_ADDRESS, PNSRegistry.abi, provider);
  
  const node = ethers.utils.namehash(name);
  const resolverAddress = await registry.resolver(node);
  
  if (resolverAddress === ethers.constants.AddressZero) {
    throw new Error("No resolver found for this name");
  }
  
  const resolver = new ethers.Contract(resolverAddress, PublicResolver.abi, provider);
  const address = await resolver.addr(node);
  
  return address;
}
```

### Common Operations

#### 1. Registering a Name

```typescript
async function registerName(name: string) {
  const provider = new ethers.providers.Web3Provider(window.ethereum);
  const signer = provider.getSigner();
  const registry = new ethers.Contract(PNS_REGISTRY_ADDRESS, PNSRegistry.abi, signer);
  
  const tx = await registry.register(name);
  await tx.wait();
}
```

#### 2. Setting a Resolver

```typescript
async function setResolver(name: string, resolverAddress: string) {
  const provider = new ethers.providers.Web3Provider(window.ethereum);
  const signer = provider.getSigner();
  const registry = new ethers.Contract(PNS_REGISTRY_ADDRESS, PNSRegistry.abi, signer);
  
  const node = ethers.utils.namehash(name);
  const tx = await registry.setResolver(node, resolverAddress);
  await tx.wait();
}
```

#### 3. Setting an Address

```typescript
async function setAddress(name: string, address: string) {
  const provider = new ethers.providers.Web3Provider(window.ethereum);
  const signer = provider.getSigner();
  const registry = new ethers.Contract(PNS_REGISTRY_ADDRESS, PNSRegistry.abi, signer);
  
  const node = ethers.utils.namehash(name);
  const resolverAddress = await registry.resolver(node);
  const resolver = new ethers.Contract(resolverAddress, PublicResolver.abi, signer);
  
  const tx = await resolver.setAddr(node, address);
  await tx.wait();
}
```

## Frontend Integration

### Using the PNS React Components

#### 1. Installation

```bash
npm install @pns/react
# or
yarn add @pns/react
# or
pnpm add @pns/react
```

#### 2. Basic Usage

```typescript
import { PNSProvider, usePNS } from "@pns/react";

function App() {
  return (
    <PNSProvider>
      <YourApp />
    </PNSProvider>
  );
}

function YourApp() {
  const { resolveName, registerName } = usePNS();
  
  // Use the hooks and components
}
```

### Available Hooks

#### 1. usePNSName

```typescript
function NameComponent({ address }: { address: string }) {
  const { name, isLoading, error } = usePNSName(address);
  
  if (isLoading) return <div>Loading...</div>;
  if (error) return <div>Error: {error.message}</div>;
  
  return <div>Name: {name}</div>;
}
```

#### 2. usePNSAddress

```typescript
function AddressComponent({ name }: { name: string }) {
  const { address, isLoading, error } = usePNSAddress(name);
  
  if (isLoading) return <div>Loading...</div>;
  if (error) return <div>Error: {error.message}</div>;
  
  return <div>Address: {address}</div>;
}
```

## Best Practices

### 1. Error Handling

Always implement proper error handling for contract interactions:

```typescript
try {
  const address = await resolveName("example.pns");
} catch (error) {
  if (error.code === "INSUFFICIENT_FUNDS") {
    // Handle insufficient funds
  } else if (error.code === "UNPREDICTABLE_GAS_LIMIT") {
    // Handle gas estimation failure
  } else {
    // Handle other errors
  }
}
```

### 2. Loading States

Implement loading states for better user experience:

```typescript
function NameResolver({ name }: { name: string }) {
  const [isLoading, setIsLoading] = useState(false);
  const [address, setAddress] = useState<string | null>(null);
  
  const resolve = async () => {
    setIsLoading(true);
    try {
      const result = await resolveName(name);
      setAddress(result);
    } finally {
      setIsLoading(false);
    }
  };
  
  return (
    <div>
      {isLoading ? (
        <div>Resolving...</div>
      ) : (
        <div>Address: {address}</div>
      )}
    </div>
  );
}
```

### 3. Gas Optimization

Optimize gas usage by:

- Batching transactions when possible
- Using appropriate gas limits
- Implementing proper error handling
- Using events for tracking state changes

## Testing

### 1. Unit Testing

```typescript
import { ethers } from "ethers";
import { PNSRegistry, PublicResolver } from "@pns/contracts";

describe("PNS Integration", () => {
  it("should resolve a name to an address", async () => {
    // Test implementation
  });
  
  it("should register a new name", async () => {
    // Test implementation
  });
});
```

### 2. Integration Testing

```typescript
describe("PNS Frontend Integration", () => {
  it("should display name resolution", async () => {
    // Test implementation
  });
  
  it("should handle registration flow", async () => {
    // Test implementation
  });
});
```

## Troubleshooting

### Common Issues

1. **Transaction Failures**
   - Check gas limits
   - Verify account balance
   - Ensure proper permissions

2. **Resolution Errors**
   - Verify name format
   - Check resolver configuration
   - Ensure proper network connection

3. **Frontend Issues**
   - Check Web3 provider connection
   - Verify contract addresses
   - Ensure proper error handling

## Support

For additional support:

- Join our [Discord community](https://discord.gg/pns)
- Check our [GitHub repository](https://github.com/mokita-j/pns)
- Read our [documentation](https://docs.pns) 