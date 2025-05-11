# Contribution Guidelines

## Code Style

### Solidity
- Follow the [Solidity Style Guide](https://docs.soliditylang.org/en/latest/style-guide.html)
- Use 4 spaces for indentation
- Maximum line length: 120 characters
- Use `@notice` for public function documentation
- Use `@dev` for implementation details

```solidity
// Good
function transferOwnership(address newOwner) public {
    require(msg.sender == owner, "Not authorized");
    require(newOwner != address(0), "Invalid address");
    owner = newOwner;
}

// Bad
function transferOwnership(address newOwner) public{
require(msg.sender==owner);owner=newOwner;}
```

### TypeScript/JavaScript
- Use ESLint with provided configuration
- Use Prettier for formatting
- Use TypeScript for new code
- Write JSDoc comments for public APIs

```typescript
// Good
interface DomainInfo {
  name: string;
  owner: string;
  expires: number;
}

// Bad
interface domainInfo {
  n: string,
  o: string,
  e: number
}
```


## Documentation

1. **Code Documentation**
   - Document all public functions
   - Explain complex logic
   - Update relevant documentation files

2. **README Updates**
   - Keep installation instructions current
   - Document new features
   - Update examples when needed

## Review Process

1. **Before Submitting**
   - Run all tests locally
   - Ensure code is formatted
   - Update documentation
   - Check for breaking changes

2. **During Review**
   - Respond to comments promptly
   - Make requested changes
   - Rebase if needed
   - Keep PR scope focused