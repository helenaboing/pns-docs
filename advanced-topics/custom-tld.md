# Custom Top-Level Domain (TLD) Registration

## Overview
You can create your own TLD (e.g., `.custom`) or sublevel domains by deploying a BaseRegistrar contract and configuring it with the PNS Registry.

## Step-by-Step Process

1. **Calculate Node Hash**
```javascript
const labelHash = keccak256('custom');
const rootNode = '0x0000000000000000000000000000000000000000000000000000000000000000';
const nodeHash = keccak256(rootNode + labelHash);
```

2. **Deploy BaseRegistrar**
```solidity
// Deploy new registrar for your TLD
const baseRegistrar = await BaseRegistrar.deploy(
    PNS_REGISTRY_ADDRESS,
    nodeHash
);
```

3. **Set Registrar as Owner**
```solidity
// Through PNS Registry
await pnsRegistry.setSubnodeOwner(
    rootNode,
    labelHash,
    baseRegistrar.address
);
```

4. **Configure Registrar**
```solidity
// Set resolver
await baseRegistrar.setResolver(PUBLIC_RESOLVER_ADDRESS);
```

## Example Configuration
```javascript
const PNS_REGISTRY = "0x123..."; // PNS Registry address
const PUBLIC_RESOLVER = "0x456..."; // Default resolver

// Deploy TLD Registrar
const customRegistrar = await BaseRegistrar.deploy(
    PNS_REGISTRY,
    namehash("custom")
);

// Set as owner in registry
await pnsRegistry.setSubnodeOwner(
    "0x0",
    keccak256("custom"),
    customRegistrar.address
);
```