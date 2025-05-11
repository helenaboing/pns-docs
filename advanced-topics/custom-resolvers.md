# Custom Resolvers

## Overview
Custom resolvers allow you to implement specialized resolution logic and store additional data for domains.

## Implementation Example

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

## Deployment and Setup

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