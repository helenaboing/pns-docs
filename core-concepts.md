# 🐡 PNS (Polkadot Name Service) - Core Concepts

## Overview
PNS (Polkadot Name Service) is a distributed, open, and extensible naming system built on the Polkadot ecosystem. Similar to ENS (Ethereum Name Service), PNS allows human-readable names to be mapped to Polkadot addresses and other resources.

## Core Components

### 1. Registry 📋
The [registry](https://github.com/mokita-j/pns/blob/main/pns-v2/contracts/registry/PNSRegistry.sol) is the core contract of PNS. It keeps track of all domains and subdomains, storing three critical pieces of information:
- The owner of the domain
- The resolver for the domain
- The time-to-live (TTL) for all records under the domain

### 2. Registrars
Registrars are contracts that own a domain and specify rules for the allocation of their subdomains. The primary registrar in PNS is the `.dot` registrar, which allows users to register second-level domains. [BaseRegistrar](https://github.com/mokita-j/pns/blob/main/pns-v2/contracts/registrar/BaseRegistrar.sol) is simple implemmentation of a registrar and be extended to include additional business logic.

### 3. Resolvers 🔍
Resolvers are responsible for the process of translating names into addresses. A resolver can implement any number of public resolution interfaces that other smart contracts or external clients can query.

> **Key resolver features:**
> - Address Resolution: Maps domain names to Polkadot addresses. ([PublicResolver](https://github.com/mokita-j/pns/blob/main/pns-v2/contracts/resolver/PublicResolver.sol))
> - Metadata Storage: Stores additional information about domains. ([MetadataResolver](https://github.com/mokita-j/pns/blob/main/pns-v2/contracts/resolver/MetadataResolver.sol))

## Name Structure and Hashing

### Name Syntax
Names in PNS follow a hierarchical dot-separated format:
```
<domain> ::= <label> | <domain> "." <label>
```
Example: "wallet.dot" or "sub.wallet.dot"

**Important Rules:**
- Labels must be normalized according to UTS46 rules
- Case-insensitive (folded during normalization)
- Recommended length: max 64 chars per label, 255 chars total name

### 🔐 Namehash Algorithm
Names are processed using the namehash algorithm to create unique fixed-length identifiers:

```javascript
function namehash(name) {
    if (name === '') {
        return '0x' + '0'.repeat(64)
    }
    const [label, ...remainder] = name.split('.')
    const remainderHash = namehash(remainder.join('.'))
    return keccak256(remainderHash + keccak256(label))
}
```

> **Example hashes:**
```
namehash('') = 0x0000...0000
namehash('dot') = 0x93cdeb...c4ae
namehash('wallet.dot') = 0xde9b09...f84f
```

## System Architecture

### Smart Contract Architecture 🏗️

#### Core Components:
1. **PNSRegistry.sol**
- Central registry contract
- Maintains ownership and resolver mapping
- Controls domain and subdomain creation

2. **BaseRegistrar.sol**
- Manages the registration of second-level domains
- Implements domain expiration and renewal logic
- Can be extended to implement controls pricing and registration rules

3. **Resolvers**
- PublicResolver.sol: Basic name resolution
- MetadataResolver.sol: Additional metadata storage

#### Contract Interactions
```
+----------------+      +-----------------+
|  PNS Registry  |<---->| Base Registrar |
+----------------+      +-----------------+
        ^               
        |               
        v             
+----------------+     
|   Resolvers    |     
+----------------+ 
```

### Frontend Architecture 🖥️

The frontend application is built using Next.js and provides:
- Domain search and registration interface
- Domain management dashboard
- Resolver configuration
- Integration with Polkadot wallets

## Key Features

1. **Human-Readable Names**
   - Transform complex Polkadot addresses into memorable names
   - Support for multiple name formats

2. **Decentralized Operation** ⛓️
   - Fully on-chain resolution
   - No central authority
   - Community-driven governance

3. **Extensibility**
   - Custom resolvers can be implemented
   - Support for various record types
   - Upgradeable architecture

4. **Security** 🔒
   - Based on proven ENS architecture
   - Secure ownership model
   - Protected against common attack vectors

## Technical Workflow

1. **Registration Process**
   ```
   User -> Registrar -> Registry -> Resolver
   ```

2. **Resolution Process**
   ```
   Query -> Registry -> Resolver -> Address/Content
   ```

3. **Update Process**
   ```
   Owner -> Registry -> Resolver -> New Records
   ```
