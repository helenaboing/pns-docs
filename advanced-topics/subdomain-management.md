# Subdomain Management

## Overview
You can deploy BaseRegistrar for any node, not just TLDs. This allows for managed subdomain registration.

## Creating a Subdomain Registrar

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