# Common Issues

## Transaction Issues

### Transaction Failing
**Q: Why is my domain registration transaction failing?**

**A:** Common reasons include:
1. Insufficient funds for gas
2. Domain already taken
3. Invalid characters in name
4. Network congestion

**Solution:**
```bash
# Check domain availability first
await pns.available('mydomain.dot')

# Ensure proper gas estimation
const gasEstimate = await pns.estimateGas.register(
    'mydomain.dot',
    address,
    ONE_YEAR_IN_SECONDS
)
```

### Domain Not Showing Up
**Q: I registered a domain but can't see it in my wallet**

**A:** Try these steps:
1. Clear browser cache
2. Reconnect wallet
3. Check transaction status on explorer
4. Wait for network confirmation

## Resolver Issues

### Resolution Not Working
**Q: Why isn't my domain resolving to my address?**

**A:** Check these:
1. Resolver is set correctly
2. Address record exists
3. Domain hasn't expired

**Verification:**
```javascript
// Check resolver
const resolver = await pns.resolver('mydomain.dot')
console.log('Resolver:', resolver)

// Check address record
const address = await pns.getAddress('mydomain.dot')
console.log('Address:', address)
```

## Integration Issues

### Wallet Connection
**Q: Wallet won't connect to PNS dApp?**

**A:** Try:
1. Update wallet software
2. Clear browser cache
3. Use supported browser
4. Check network settings