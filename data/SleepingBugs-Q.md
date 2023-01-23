# Unused `receive()` function will lock ether in contract
## Summary

If the intention is for the Ether to be used, the function should call another function, otherwise it should `revert`

## Code Snippet

- [Consideration.sol#L58](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0//contracts/lib/Consideration.sol#L58)
`receive() external payable {`

## Recommendation

If the intention is for the Ether to be used, the function should call another function, otherwise it should `revert`.
