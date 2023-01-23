# QA Report

## [NC-1] Unused imports are used
Its recommend to remove used imports for better readability of the code
here are the permalinks of them 
https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/lib/ConsiderationDecoder.sol#L5
https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/lib/ConsiderationDecoder.sol#L10
https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/lib/ConsiderationDecoder.sol#L20
https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/lib/ConsiderationDecoder.sol#L22
https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/lib/BasicOrderFulfiller.sol#L23
https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/lib/OrderValidator.sol#L15
https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/lib/OrderValidator.sol#L16
https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/lib/OrderValidator.sol#L19
https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/lib/OrderValidator.sol#L26
https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/lib/OrderValidator.sol#L31
https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/lib/OrderCombiner.sol#L23
https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/lib/TokenTransferrer.sol#L4
https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/lib/FulfillmentApplier.sol#L16
https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/lib/Executor.sol#L16
https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/lib/Executor.sol#L18
https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/lib/ConsiderationEncoder.sol#L4
https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/lib/ConsiderationEncoder.sol#L9
https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/lib/ConsiderationEncoder.sol#L10
https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/lib/ConsiderationEncoder.sol#L11
https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/lib/ConsiderationEncoder.sol#L12
https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/lib/ConsiderationEncoder.sol#L14
https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/lib/ConsiderationEncoder.sol#L20
https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/lib/Consideration.sol#L23
https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/lib/Consideration.sol#L25
https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/lib/ConsiderationErrors.sol#L6
https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/lib/OrderFulfiller.sol#L23
https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/lib/SignatureVerification.sol#L4
https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/lib/SignatureVerification.sol#L12
https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/lib/CriteriaResolution.sol#L8
https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/lib/CriteriaResolution.sol#L15
https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/lib/CriteriaResolution.sol#L17
https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/lib/GettersAndDerivers.sol#L8
https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/lib/ConsiderationBase.sol#L12

## [NC-2] Inconsistent solidity version
The source files have different solidity compiler ranges (some are at ^0.8.13 & ^0.8.17). This leads to potential security flaws between deployed contracts depending on the compiler version chosen for any particular file. It also greatly increases the cost of maintenance as different compiler versions have different semantics and behavior.