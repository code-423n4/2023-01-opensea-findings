
### [Low-01] abi.encodePacked()
 should not be used with dynamic types when passing the result to a hash function such as keccak256()

Use abi.encode()
 instead which will pad items to 32 bytes, which will prevent hash collisions
 (e.g. abi.encodePacked(0x123,0x456)
 => 0x123456
 => abi.encodePacked(0x1,0x23456)
, but abi.encode(0x123,0x456)
 => 0x0...1230...456
). "Unless there is a compelling reason, abi.encode
 should be preferred". If there is only one argument to abi.encodePacked()
 it can often be cast to bytes()
 or bytes32()
 instead
. If all arguments are strings and or bytes, bytes.concat()
 should be used instead

*instances(3)*
```solidity
File::  /helpers/TransferHelper.sol
https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/helpers/TransferHelper.sol#L107-L112
```
```solidity
File::  conduit/ConduitController.sol
https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/conduit/ConduitController.sol#L75-L82
https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/conduit/ConduitController.sol#L338-L345
```


### [Low-02] Different Solidity version used
^0.8.17 used by following
```solidity
File::  Seaport.sol

file::  contracts/lib/AmountDeriver.sol
file::  contracts/lib/Assertions.sol
file::  contracts/lib/BasicOrderFulfiller.sol
file::  contracts/lib/Consideration.sol
file::  contracts/lib/ConsiderationBase.sol
file::  contracts/lib/ConsiderationDecoder.sol
file::  contracts/lib/ConsiderationErrors.sol
file::  contracts/lib/CounterManager.sol
file::  contracts/lib/CriteriaResolution.sol
file::  contracts/lib/Executor.sol
file::  contracts/lib/FulfillmentApplier.sol
file::  contracts/lib/GettersAndDerivers.sol
file::  contracts/lib/LowLevelHelpers.sol
file::  contracts/lib/OrderCombiner.sol
file::  contracts/lib/OrderFulfiller.sol
file::  contracts/lib/OrderValidator.sol
file::  contracts/lib/ReentrancyGuard.sol
file::  contracts/lib/SignatureVerification.sol
file::  contracts/lib/TypehashDirectory.sol
file::  contracts/lib/Verifiers.sol
file::  contracts/lib/ZoneInteraction.sol

```

^0.8.13 used by following
```solidity
File::  /helpers/PointerLibraries.sol
File::  /helpers/TransferHelperStructs.sol

File::  conduit/Conduit.sol
File::  conduit/ConduitController.sol
File::  conduit/lib/ConduitConstants.sol
File::  conduit/lib/ConduitEnums.sol
File::  conduit/lib/ConduitStructs.sol

file::  contracts/lib/ConsiderationConstants.sol
file::  contracts/lib/ConsiderationEncoder.sol
file::  contracts/lib/ConsiderationEnums.sol
file::  contracts/lib/ConsiderationStructs.sol
file::  contracts/lib/TokenTransferrer.sol
file::  contracts/lib/TokenTransferrerConstants.sol


```


### [NC-01] Floating Pragma used

*instances()*
```solidity
File::  All contracts using floating pragma
```