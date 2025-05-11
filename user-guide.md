# PNS User Guide

## Introduction

Welcome to the Polkadot Naming Service (PNS) user guide. This guide will help you understand how to use PNS to manage your blockchain identities and addresses.

## Getting Started

### Prerequisites

1. A Web3 wallet (like MetaMask)
2. Some test tokens (WND) on the Westend Asset Hub testnet
3. Basic understanding of blockchain concepts

### Connecting Your Wallet

1. Visit the PNS website
2. Click the "Connect Wallet" button
3. Select your preferred wallet
4. Approve the connection request

## Managing Your Names

### Registering a Name

1. Navigate to the "Register" page
2. Enter your desired name (e.g., "myname.pns")
3. Check name availability
4. Click "Register"
5. Approve the transaction in your wallet
6. Wait for confirmation

### Domain Name Rules

When creating a domain name, please follow the guidelines below to ensure your name is valid and accepted by the system.

#### ✅ Allowed Characters

- **Latin alphabet letters** (A–Z, a–z)
- **Numbers** (0–9)

#### ❌ Not Allowed

- **Spaces** (e.g., `helena boing` is invalid)
- **Emojis** (e.g., `🌟helena` is invalid)
- **Dots between words** (e.g., `helena.boing` is invalid)

#### ✅ Valid Examples

- `helena`
- `helena123`
- `helena.dot`
- `helena.jam`

Only single names or names with **approved suffixes** like `.dot` and `.jam` are accepted.

### Viewing Your Names

1. Go to the "My Names" section
2. View all names registered to your address
3. See registration date and expiration
4. Check current resolver settings

### Updating Name Records

#### Setting an Address

1. Select your name from "My Names"
2. Go to the "Records" tab
3. Enter the address you want to associate
4. Click "Update"
5. Approve the transaction

#### Setting Other Records

1. Navigate to the "Records" tab
2. Choose the record type
3. Enter the record value
4. Save changes
5. Approve the transaction

### Transferring Names

1. Select the name you want to transfer
2. Click "Transfer"
3. Enter the recipient's address
4. Confirm the transfer
5. Approve the transaction

## Name Resolution

### Resolving Names to Addresses

1. Go to the "Resolve" page
2. Enter the PNS name
3. View the associated address
4. Copy the address if needed

### Reverse Resolution

1. Enter an address in the search bar
2. View any associated PNS names
3. See primary name if set

## Security

### Best Practices

1. **Keep Your Private Keys Safe**
   - Never share your private keys
   - Use hardware wallets for large holdings
   - Enable 2FA where available

2. **Verify Transactions**
   - Always check transaction details
   - Verify recipient addresses
   - Review gas fees

3. **Regular Maintenance**
   - Monitor name expiration
   - Update records when needed
   - Keep resolver information current

### Common Scams

1. **Phishing Attempts**
   - Be wary of fake PNS websites
   - Verify website URLs
   - Don't share private keys

2. **Fake Support**
   - Official support won't ask for private keys
   - Use official channels only
   - Verify support staff identity

## Troubleshooting

### Common Issues

1. **Transaction Failures**
   - Check gas fees
   - Verify network connection
   - Ensure sufficient balance

2. **Name Registration Issues**
   - Verify name availability
   - Check name format
   - Ensure sufficient funds

3. **Resolution Problems**
   - Verify name spelling
   - Check resolver settings
   - Ensure proper network

### Getting Help

1. **Documentation**
   - Check the [PNS documentation](https://github.com/helenaboing/pns-docs)
   - Review [troubleshooting guides](https://docs.pns/troubleshooting)

2. **Community Support**
   - Join the [Discord community](https://discord.gg/pns)
   - Check [GitHub discussions](https://github.com/mokita-j/pns/discussions)

3. **Technical Support**
   - Submit issues on [GitHub](https://github.com/mokita-j/pns/issues)
   - Contact support team
   - Check status page for outages

## Advanced Features

### Subdomains

1. **Creating Subdomains**
   - Select parent name
   - Click "Create Subdomain"
   - Enter subdomain name
   - Set permissions

2. **Managing Subdomains**
   - View subdomain list
   - Update records
   - Transfer ownership

### Custom Resolvers

1. **Setting Custom Resolvers**
   - Choose resolver type
   - Enter resolver address
   - Configure settings

2. **Resolver Management**
   - Update resolver settings
   - Change resolver type
   - Remove resolver

## Frequently Asked Questions

### General Questions

1. **What is PNS?**
   - PNS is a naming service for the Polkadot ecosystem
   - It maps human-readable names to blockchain addresses
   - It supports various record types

2. **How much does it cost?**
   - Registration fees vary by name length
   - Gas fees apply for transactions
   - No recurring fees

3. **Can I transfer my name?**
   - Yes, names are transferable
   - Use the transfer function
   - Verify recipient address

### Technical Questions

1. **What networks are supported?**
   - Currently on Westend Asset Hub testnet
   - More networks coming soon
   - Check network status

2. **How do resolvers work?**
   - Resolvers store record data
   - Different types available
   - Can be customized

3. **What record types are supported?**
   - Address records
   - Content hashes
   - Custom records
   - More coming soon
