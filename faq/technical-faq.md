# Technical FAQ

## Smart Contract Questions


### Custom Records
**Q: How do I add custom record types?**

**A:** Extend the PublicResolver:
```solidity
contract CustomResolver is PublicResolver {
    mapping(bytes32 => string) customRecords;
    
    function setCustomRecord(bytes32 node, string calldata value) 
        external 
        authorised(node) 
    {
        customRecords[node] = value;
    }
}
```
