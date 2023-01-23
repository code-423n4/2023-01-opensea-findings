### Gas Optimizations Report
| No. | Issue |
| --- | --- |
| 1 | [Using `uint256` instead of `bool` in mappings is more gas efficient [146 gas per instance]](#G-01-using-uint256-instead-of-bool-in-mappings-is-more-gas-efficient-146-gas-per-instance)|
| 2 | [Usage of uint/int smaller than 32 bytes (256 bits) incurs overhead](#G-02-usage-of-uintint-smaller-than-32-bytes-256-bits-incurs-overhead)|
---
### [G-01] Using `uint256` instead of `bool` in mappings is more gas efficient [146 gas per instance]

---
**Description:**

OpenZeppelin uint256 and bool comparison: 

Booleans are more expensive than uint256 or any type that takes up a full word because each write operation emits an extra SLOAD to first read the slot's contents, replace the bits taken up by the boolean, and then write back. This is the compiler's defense against contract upgrades and pointer aliasing, and it cannot be disabled. The values being non-zero value makes deployment a bit more expensive.

Use uint256(1) and uint256(2) for true/false to avoid a Gwarmaccess (100 gas) for the extra SLOAD, and to avoid Gsset (20000 gas) when changing from ‘false’ to ‘true’, after having been ‘true’ in the past.

**Recommendation:**

Use uint256(1) and uint256(2) instead of bool.

**Lines of Code:** 

- [Conduit.sol#L34](https://github.com/ProjectOpenSea/seaport/tree/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/conduit/Conduit.sol#L34)
- [ReferenceConduit.sol#L30](https://github.com/ProjectOpenSea/seaport/tree/5de7302bc773d9821ba4759e47fc981680911ea0/reference/conduit/ReferenceConduit.sol#L30)

---
### [G-02] Usage of uint/int smaller than 32 bytes (256 bits) incurs overhead

---
**Description:**

When using elements that are smaller than 32 bytes, your contract’s gas usage may be higher. This is because the EVM operates on 32 bytes at a time. Therefore, if the element is smaller than that, the EVM must use more operations in order to reduce the size of the element from 32 bytes to the desired size. Each operation involving a uint8 costs an extra 22-28 gas (depending on whether the other operand is also a variable of type uint8) as compared to ones involving uint256, due to the compiler having to clear the higher bits of the memory word before operating on the uint8, as well as the associated stack operations of doing so.

**Recommendation:**

Use a larger size then downcast where needed

**Lines of Code:** 

- [PointerLibraries.sol#L614](https://github.com/ProjectOpenSea/seaport/tree/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/helpers/PointerLibraries.sol#L614)
- [PointerLibraries.sol#L1539](https://github.com/ProjectOpenSea/seaport/tree/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/helpers/PointerLibraries.sol#L1539)
- [PointerLibraries.sol#L2499](https://github.com/ProjectOpenSea/seaport/tree/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/helpers/PointerLibraries.sol#L2499)
- [SignatureVerificationErrors.sol#L17](https://github.com/ProjectOpenSea/seaport/tree/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/interfaces/SignatureVerificationErrors.sol#L17)
- [ReferenceSignatureVerification.sol#L45](https://github.com/ProjectOpenSea/seaport/tree/5de7302bc773d9821ba4759e47fc981680911ea0/reference/lib/ReferenceSignatureVerification.sol#L45)