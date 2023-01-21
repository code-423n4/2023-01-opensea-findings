
Bug Description:
The function "_validateOrderAndUpdateStatus" uses "revert" at multiple location which can cause unexpected behavior and make it hard to debug.

Steps to Reproduce:

1. Deploy the smart contract to the blockchain
2. Call the function "_validateOrderAndUpdateStatus"
3. Observe the unexpected behavior caused by the "revert" statements

Expected Result:
The function should provide clear and informative error messages when it fails.

Actual Result:
The function uses "revert" statements, which do not provide any information about the reason for the failure, making it difficult to debug.

Impact:
This bug can make it difficult to diagnose and fix issues with the smart contract, potentially leading to further bugs and vulnerabilities.

Recommendation:
Use "require" statement instead of "revert" statement in the function "_validateOrderAndUpdateStatus" to provide clear and informative error messages when the function fails.

```
function _validateOrderAndUpdateStatus(...) internal {
    ...
    require(denominator != 0, "Supplied denominator cannot be zero.");
    ...
}
```

Severity: Medium

Notes: The severity can be considered as medium as it makes it hard to debug the smart contract but the remediation effort is low as it's just need to replace revert statement with require statement.

