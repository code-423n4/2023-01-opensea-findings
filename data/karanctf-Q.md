## On line `584` ConsiderationConstants.sol use `error` insted of `err` to match same pattern used with other constants
```solidity
- uint256 constant ConsiderationCriteriaResolverOutOfRange_err_selector = 0x6088d7de;
+ uint256 constant ConsiderationCriteriaResolverOutOfRange_error_selector = 0x6088d7de;

```

## Use more recent version of solidity
When deploying contracts, you should use the latest released version of Solidity. This is because **breaking changes, as well as new features and bug fixes are introduced regularly**.


