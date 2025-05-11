# PNS Advanced Topics

## Deployed Contracts

### Contract Addresses

| Contract | Address | Description |
|----------|---------|-------------|
| PNS Registry | `0xBE10c808B7ea10542b9F91418Ad3A696a132358d` | Core registry managing the naming system |
| Public Resolver | `0x1Ee165d0F70d6672A8a6C954Bc993e9c4Ef7bB17` | Default resolver for address resolution |
| DOT BaseRegistrar | `0x56fdDF0Eb0567371715997E43106bBE4667990C5` | Registrar for .dot domains |
| JAM BaseRegistrar | `0xcBc1C5f7A095e5947d987eB41369327e775998fe` | Registrar for .jam domains |
| MetadataResolver | `0xa19f97DBcDF7E456774F6DFF5324AC10d82E00Ce` | Resolver for metadata storage |
| PNSDOT BaseRegistrar | `0x3056862E15e18469971fc15f75BD84268f4a66aD` | Registrar for pns.dot domains |


## Custom Top-Level Domain (TLD) Registration

### Overview
You can create your own TLD (e.g., `.custom`) or sublevel domains by deploying a BaseRegistrar contract and configuring it with the PNS Registry.

### Step-by-Step Process

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

### Example Configuration
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

## Custom Resolvers

### Overview
Custom resolvers allow you to implement specialized resolution logic and store additional data for domains.

### Implementation Example

```solidity
// Custom resolver with social media handles
contract SocialMediaResolver {
    PNS pns;
    mapping(bytes32 => string) twitter;
    mapping(bytes32 => string) github;
    
    constructor(PNS _pns) {
        pns = _pns;
    }
    
    modifier onlyOwner(bytes32 node) {
        require(pns.owner(node) == msg.sender);
        _;
    }
    
    function setTwitter(bytes32 node, string calldata handle) 
        external 
        onlyOwner(node) 
    {
        twitter[node] = handle;
    }
    
    function setGithub(bytes32 node, string calldata profile)
        external
        onlyOwner(node)
    {
        github[node] = profile;
    }
}
```

### Deployment and Setup

1. **Deploy Custom Resolver**
```javascript
const customResolver = await SocialMediaResolver.deploy(
    PNS_REGISTRY_ADDRESS
);
```

2. **Set Resolver for Domain**
```javascript
// Through PNS Registry
await pnsRegistry.setResolver(
    namehash("domain.dot"), 
    customResolver.address
);
```

3. **Configure Records**
```javascript
await customResolver.setTwitter(
    namehash("domain.dot"),
    "@handle"
);
```

## Subdomain Registrars

### Overview
You can deploy BaseRegistrar for any node, not just TLDs. This allows for managed subdomain registration.

### Example: Creating a Subdomain Registrar

1. **Calculate Subdomain Node**
```javascript
const node = namehash("service.dot");
```

2. **Deploy Registrar**
```javascript
const subRegistrar = await BaseRegistrar.deploy(
    PNS_REGISTRY_ADDRESS,
    node
);
```

3. **Transfer Ownership**
```javascript
// Current owner must approve
await pnsRegistry.setSubnodeOwner(
    node,
    namehash("service"),
    subRegistrar.address
);
```
