# 1: Floating Pragma

Vulnerability details

## Impact

Contracts should be deployed using the same compiler version/flags with which they have been tested. Locking the floating pragma, i.e. by not using ^ in pragma solidity ^0.8.9, ensures that contracts do not accidentally get deployed using an older compiler version with unfixed bugs.

For reference, see https://swcregistry.io/docs/SWC-103

## Proof of Concept

https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/Seaport.sol#L2 

All contracts found in Lib
https://github.com/ProjectOpenSea/seaport/tree/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/lib 

All contracts found in Interface
https://github.com/ProjectOpenSea/seaport/tree/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/interfaces 

## Tools Used

Manual Analysis

### Recommended Mitigation Steps

Remove ^ in “pragma solidity ^0.8.9” and change it to “pragma solidity 0.8.9” to be consistent with the rest of the contracts.


# 2: USE CONSTANTS FOR NUMBERS

Vulnerability details

### Impact

In several locations in the code, numbers like 0x20, 0x47, 0x60 are used. It is quite easy to make a mistake somewhere when comparing values.

## Proof of Concept

https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/Seaport.sol#L104 

https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/Seaport.sol#L105 

https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/Seaport.sol#L106 

## Tools Used

Manual Analysis

### Recommended Mitigation Steps

Recommend defining constants for the numbers used throughout the code.


# 3: USE OF BYTES.CONCAT() INSTEAD OF ABI.ENCODEPACKED(,)

Vulnerability details

### Impact

Rather than using abi.encodePacked for appending bytes, since version 0.8.4, bytes.concat() is enabled

## Proof of Concept

https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/conduit/ConduitController.sol#L76 

https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/conduit/ConduitController.sol#L339 

## Tools Used

Manual Analysis

## Recommended Mitigation Steps

Since version 0.8.4 for appending bytes, bytes.concat() can be used instead of abi.encodePacked(,).
