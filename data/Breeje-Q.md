## QA Report

| |Issue|Instances|
|-|:-|:-:|
| [L-1](#L-1) | LOCK PRAGMAS TO SPECIFIC COMPILER VERSION | 50 |
| [NC-1](#NC-1) | USE BYTES.CONCAT() INSTEAD OF ABI.ENCODEPACKED(,) | 1 |
| [NC-2](#NC-2) | FOR MODERN AND MORE READABLE CODE; UPDATE IMPORT USAGES | 27 |

### [L-1] LOCK PRAGMAS TO SPECIFIC COMPILER VERSION

Pragma statements can be allowed to float when a contract is intended for consumption by other developers, as in the case with contracts in a library or EthPM package. Otherwise, the developer would need to manually update the pragma in order to compile locally.

Impact: [swcregistry](https://swcregistry.io/docs/SWC-103)

#### Recommendation:
Ethereum Smart Contract Best Practices - Lock pragmas to specific compiler version.
[solidity-specific/locking-pragmas](https://consensys.github.io/smart-contract-best-practices/development-recommendations/solidity-specific/locking-pragmas/)

*Instances (50):*
All the files in scope uses Floating Pragma.

### [NC-1] USE BYTES.CONCAT() INSTEAD OF ABI.ENCODEPACKED(,)

Since version 0.8.4, `bytes.concat()` is enabled. Hence, Rather than using `abi.encodePacked` for appending bytes, `bytes.concat()` can be used.

[Similar NC Issue Reference](https://code4rena.com/reports/2022-12-pooltogether#n-04-use-of-bytesconcat-instead-of-abiencodepacked)

*Instance (1):*
```solidity
File: 

177:      abi.encodePacked(
178:            considerationItemTypeString,
179:            offerItemTypeString,
180:            orderComponentsPartialTypeString
181:       );

```
[Link to Code](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/lib/TypehashDirectory.sol#L177-L181)

### [NC-2] FOR MODERN AND MORE READABLE CODE; UPDATE IMPORT USAGES

The below instances breaks the rule of modularity and modular programming: `only import what you need` Specific imports with curly braces.

*Instances (27):*
* [`AmountDeriver.sol` Instance 1](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/lib/AmountDeriver.sol#L8)
* [`Assertions.sol` Instance 1](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/lib/Assertions.sol#L14)
* [`BasicOrderFulfiller.sol` Instance 1](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/lib/BasicOrderFulfiller.sol#L23)
* [`Consideration.sol` Instance 1](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/lib/Consideration.sol#L23)
* [`Consideration.sol` Instance 2](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/lib/Consideration.sol#L25)
* [`ConsiderationBase.sol` Instance 1](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/lib/ConsiderationBase.sol#L12)
* [`ConsiderationDecoder.sol` Instance 1](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/lib/ConsiderationDecoder.sol#L20)
* [`ConsiderationDecoder.sol` Instance 2](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/lib/ConsiderationDecoder.sol#L22)
* [`ConsiderationEncoder.sol` Instance 1](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/lib/ConsiderationEncoder.sol#L4)
* [`ConsiderationEncoder.sol` Instance 2](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/lib/ConsiderationEncoder.sol#L20)
* [`ConsiderationErrors.sol` Instance 1](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/lib/ConsiderationErrors.sol#L6)
* [`CounterManager.sol` Instance 1](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/lib/CounterManager.sol#L10)
* [`CriteriaResolution.sol` Instance 1](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/lib/CriteriaResolution.sol#L15)
* [`CriteriaResolution.sol` Instance 2](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/lib/CriteriaResolution.sol#L17)
* [`Executor.sol` Instance 1](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/lib/Executor.sol#L15)
* [`Executor.sol` Instance 2](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/lib/Executor.sol#L17)
* [`FulfillmentApplier.sol` Instance 1](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/lib/FulfillmentApplier.sol#L16)
* [`GettersAndDerivers.sol` Instance 1](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/lib/GettersAndDerivers.sol#L8)
* [`LowLevelHelpers.sol` Instance 1](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/lib/LowLevelHelpers.sol#L4)
* [`OrderCombiner.sol` Instance 1](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/lib/OrderCombiner.sol#L23)
* [`OrderFulfiller.sol` Instance 1](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/lib/OrderFulfiller.sol#L23)
* [`OrderValidator.sol` Instance 1](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/lib/OrderValidator.sol#L19)
* [`ReentrancyGuard.sol` Instance 1](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/lib/ReentrancyGuard.sol#L8)
* [`SignatureVerification.sol` Instance 1](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/lib/SignatureVerification.sol#L12)
* [`TokenTransferrer.sol` Instance 1](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/lib/TokenTransferrer.sol#L4)
* [`Verifiers.sol` Instance 1](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/lib/Verifiers.sol#L10)
* [`ZoneInteraction.sol` Instance 1](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/lib/ZoneInteraction.sol#L16)