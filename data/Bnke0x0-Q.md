

### [N01] `require()`/`revert()` statements should have descriptive reason strings


#### Findings:
```
seaport/contracts/helpers/PointerLibraries.sol::225 => revert(0, 0)
seaport/contracts/lib/LowLevelHelpers.sol::66 => revert(0, returndatasize())
seaport/contracts/lib/TokenTransferrer.sol::152 => revert(0, returndatasize())
seaport/contracts/lib/TokenTransferrer.sol::356 => revert(0, returndatasize())
seaport/contracts/lib/TokenTransferrer.sol::508 => revert(0, returndatasize())
seaport/contracts/lib/TokenTransferrer.sol::791 => revert(0, returndatasize())
seaport/contracts/lib/TokenTransferrer.sol::821 => revert(0, transferDataSize)
```



### [N02] Unused file



#### Findings:
```
seaport/contracts/conduit/Conduit.sol::1 => // SPDX-License-Identifier: MIT
seaport/contracts/conduit/ConduitController.sol::1 => // SPDX-License-Identifier: MIT
seaport/contracts/conduit/lib/ConduitConstants.sol::1 => // SPDX-License-Identifier: MIT
seaport/contracts/conduit/lib/ConduitEnums.sol::1 => // SPDX-License-Identifier: MIT
seaport/contracts/conduit/lib/ConduitStructs.sol::1 => // SPDX-License-Identifier: MIT
seaport/contracts/helpers/PointerLibraries.sol::1 => // SPDX-License-Identifier: MIT
seaport/contracts/interfaces/AbridgedTokenInterfaces.sol::1 => // SPDX-License-Identifier: MIT
seaport/contracts/interfaces/AmountDerivationErrors.sol::1 => // SPDX-License-Identifier: MIT
seaport/contracts/interfaces/ConduitControllerInterface.sol::1 => // SPDX-License-Identifier: MIT
seaport/contracts/interfaces/ConduitInterface.sol::1 => // SPDX-License-Identifier: MIT
seaport/contracts/interfaces/ConsiderationEventsAndErrors.sol::1 => // SPDX-License-Identifier: MIT
seaport/contracts/interfaces/ConsiderationInterface.sol::1 => // SPDX-License-Identifier: MIT
seaport/contracts/interfaces/ContractOffererInterface.sol::1 => // SPDX-License-Identifier: MIT
seaport/contracts/interfaces/CriteriaResolutionErrors.sol::1 => // SPDX-License-Identifier: MIT
seaport/contracts/interfaces/EIP1271Interface.sol::1 => // SPDX-License-Identifier: MIT
seaport/contracts/interfaces/FulfillmentApplicationErrors.sol::1 => // SPDX-License-Identifier: MIT
seaport/contracts/interfaces/IERC721Receiver.sol::1 => // SPDX-License-Identifier: MIT
seaport/contracts/interfaces/ImmutableCreate2FactoryInterface.sol::1 => // SPDX-License-Identifier: MIT
seaport/contracts/interfaces/ReentrancyErrors.sol::1 => // SPDX-License-Identifier: MIT
seaport/contracts/interfaces/SeaportInterface.sol::1 => // SPDX-License-Identifier: MIT
seaport/contracts/interfaces/SignatureVerificationErrors.sol::1 => // SPDX-License-Identifier: MIT
seaport/contracts/interfaces/TokenTransferrerErrors.sol::1 => // SPDX-License-Identifier: MIT
seaport/contracts/interfaces/TransferHelperErrors.sol::1 => // SPDX-License-Identifier: MIT
seaport/contracts/interfaces/TransferHelperInterface.sol::1 => // SPDX-License-Identifier: MIT
seaport/contracts/interfaces/ZoneInteractionErrors.sol::1 => // SPDX-License-Identifier: MIT
seaport/contracts/interfaces/ZoneInterface.sol::1 => // SPDX-License-Identifier: MIT
seaport/contracts/lib/AmountDeriver.sol::1 => // SPDX-License-Identifier: MIT
seaport/contracts/lib/Assertions.sol::1 => // SPDX-License-Identifier: MIT
seaport/contracts/lib/BasicOrderFulfiller.sol::1 => // SPDX-License-Identifier: MIT
seaport/contracts/lib/Consideration.sol::1 => // SPDX-License-Identifier: MIT
seaport/contracts/lib/ConsiderationBase.sol::1 => // SPDX-License-Identifier: MIT
seaport/contracts/lib/ConsiderationConstants.sol::1 => // SPDX-License-Identifier: MIT
seaport/contracts/lib/ConsiderationDecoder.sol::1 => // SPDX-License-Identifier: MIT
seaport/contracts/lib/ConsiderationEncoder.sol::1 => // SPDX-License-Identifier: MIT
seaport/contracts/lib/ConsiderationEnums.sol::1 => // SPDX-License-Identifier: MIT
seaport/contracts/lib/ConsiderationErrors.sol::1 => // SPDX-License-Identifier: MIT
seaport/contracts/lib/ConsiderationStructs.sol::1 => // SPDX-License-Identifier: MIT
seaport/contracts/lib/CounterManager.sol::1 => // SPDX-License-Identifier: MIT
seaport/contracts/lib/CriteriaResolution.sol::1 => // SPDX-License-Identifier: MIT
seaport/contracts/lib/Executor.sol::1 => // SPDX-License-Identifier: MIT
seaport/contracts/lib/FulfillmentApplier.sol::1 => // SPDX-License-Identifier: MIT
seaport/contracts/lib/GettersAndDerivers.sol::1 => // SPDX-License-Identifier: MIT
seaport/contracts/lib/LowLevelHelpers.sol::1 => // SPDX-License-Identifier: MIT
seaport/contracts/lib/OrderCombiner.sol::1 => // SPDX-License-Identifier: MIT
seaport/contracts/lib/OrderFulfiller.sol::1 => // SPDX-License-Identifier: MIT
seaport/contracts/lib/OrderValidator.sol::1 => // SPDX-License-Identifier: MIT
seaport/contracts/lib/ReentrancyGuard.sol::1 => // SPDX-License-Identifier: MIT
seaport/contracts/lib/SignatureVerification.sol::1 => // SPDX-License-Identifier: MIT
seaport/contracts/lib/TokenTransferrer.sol::1 => // SPDX-License-Identifier: MIT
seaport/contracts/lib/TokenTransferrerConstants.sol::1 => // SPDX-License-Identifier: MIT
seaport/contracts/lib/TypehashDirectory.sol::1 => // SPDX-License-Identifier: MIT
seaport/contracts/lib/Verifiers.sol::1 => // SPDX-License-Identifier: MIT
seaport/contracts/lib/ZoneInteraction.sol::1 => // SPDX-License-Identifier: MIT
```



### [N03] NC-library/interface files should use fixed compiler versions, not floating ones


#### Findings:
```
seaport/contracts/conduit/Conduit.sol::2 => pragma solidity ^0.8.13;
seaport/contracts/conduit/ConduitController.sol::2 => pragma solidity ^0.8.13;
seaport/contracts/conduit/lib/ConduitConstants.sol::2 => pragma solidity ^0.8.13;
seaport/contracts/conduit/lib/ConduitEnums.sol::2 => pragma solidity ^0.8.13;
seaport/contracts/conduit/lib/ConduitStructs.sol::2 => pragma solidity ^0.8.13;
seaport/contracts/helpers/PointerLibraries.sol::2 => pragma solidity ^0.8.13;
seaport/contracts/interfaces/AbridgedTokenInterfaces.sol::2 => pragma solidity ^0.8.13;
seaport/contracts/interfaces/AmountDerivationErrors.sol::2 => pragma solidity ^0.8.13;
seaport/contracts/interfaces/ConduitControllerInterface.sol::2 => pragma solidity ^0.8.13;
seaport/contracts/interfaces/ConduitInterface.sol::2 => pragma solidity ^0.8.13;
seaport/contracts/interfaces/ConsiderationEventsAndErrors.sol::2 => pragma solidity ^0.8.13;
seaport/contracts/interfaces/ConsiderationInterface.sol::2 => pragma solidity ^0.8.13;
seaport/contracts/interfaces/ContractOffererInterface.sol::2 => pragma solidity ^0.8.13;
seaport/contracts/interfaces/CriteriaResolutionErrors.sol::2 => pragma solidity ^0.8.13;
seaport/contracts/interfaces/EIP1271Interface.sol::2 => pragma solidity ^0.8.13;
seaport/contracts/interfaces/FulfillmentApplicationErrors.sol::2 => pragma solidity ^0.8.13;
seaport/contracts/interfaces/IERC721Receiver.sol::2 => pragma solidity ^0.8.13;
seaport/contracts/interfaces/ImmutableCreate2FactoryInterface.sol::2 => pragma solidity ^0.8.13;
seaport/contracts/interfaces/ReentrancyErrors.sol::2 => pragma solidity ^0.8.13;
seaport/contracts/interfaces/SeaportInterface.sol::2 => pragma solidity ^0.8.13;
seaport/contracts/interfaces/SignatureVerificationErrors.sol::2 => pragma solidity ^0.8.13;
seaport/contracts/interfaces/TokenTransferrerErrors.sol::2 => pragma solidity ^0.8.13;
seaport/contracts/interfaces/TransferHelperErrors.sol::2 => pragma solidity ^0.8.13;
seaport/contracts/interfaces/TransferHelperInterface.sol::2 => pragma solidity ^0.8.13;
seaport/contracts/interfaces/ZoneInteractionErrors.sol::2 => pragma solidity ^0.8.13;
seaport/contracts/interfaces/ZoneInterface.sol::2 => pragma solidity ^0.8.13;
seaport/contracts/lib/AmountDeriver.sol::2 => pragma solidity ^0.8.17;
seaport/contracts/lib/Assertions.sol::2 => pragma solidity ^0.8.17;
seaport/contracts/lib/BasicOrderFulfiller.sol::2 => pragma solidity ^0.8.17;
seaport/contracts/lib/Consideration.sol::2 => pragma solidity ^0.8.17;
seaport/contracts/lib/ConsiderationBase.sol::2 => pragma solidity ^0.8.17;
seaport/contracts/lib/ConsiderationConstants.sol::2 => pragma solidity ^0.8.13;
seaport/contracts/lib/ConsiderationDecoder.sol::2 => pragma solidity ^0.8.17;
seaport/contracts/lib/ConsiderationEncoder.sol::2 => pragma solidity ^0.8.13;
seaport/contracts/lib/ConsiderationEnums.sol::2 => pragma solidity ^0.8.13;
seaport/contracts/lib/ConsiderationErrors.sol::2 => pragma solidity ^0.8.17;
seaport/contracts/lib/ConsiderationStructs.sol::2 => pragma solidity ^0.8.13;
seaport/contracts/lib/CounterManager.sol::2 => pragma solidity ^0.8.17;
seaport/contracts/lib/CriteriaResolution.sol::2 => pragma solidity ^0.8.17;
seaport/contracts/lib/Executor.sol::2 => pragma solidity ^0.8.17;
seaport/contracts/lib/FulfillmentApplier.sol::2 => pragma solidity ^0.8.17;
seaport/contracts/lib/GettersAndDerivers.sol::2 => pragma solidity ^0.8.17;
seaport/contracts/lib/LowLevelHelpers.sol::2 => pragma solidity ^0.8.17;
seaport/contracts/lib/OrderCombiner.sol::2 => pragma solidity ^0.8.17;
seaport/contracts/lib/OrderFulfiller.sol::2 => pragma solidity ^0.8.17;
seaport/contracts/lib/OrderValidator.sol::2 => pragma solidity ^0.8.17;
seaport/contracts/lib/ReentrancyGuard.sol::2 => pragma solidity ^0.8.17;
seaport/contracts/lib/SignatureVerification.sol::2 => pragma solidity ^0.8.17;
seaport/contracts/lib/TokenTransferrer.sol::2 => pragma solidity ^0.8.13;
seaport/contracts/lib/TokenTransferrerConstants.sol::2 => pragma solidity ^0.8.13;
seaport/contracts/lib/TypehashDirectory.sol::2 => pragma solidity ^0.8.17;
seaport/contracts/lib/Verifiers.sol::2 => pragma solidity ^0.8.17;
seaport/contracts/lib/ZoneInteraction.sol::2 => pragma solidity ^0.8.17;
```


### [N04] USE A MORE RECENT VERSION OF SOLIDITY

#### Impact

Code contains empty block


#### Findings:
```
seaport/contracts/conduit/Conduit.sol::2 => pragma solidity ^0.8.13;
seaport/contracts/conduit/ConduitController.sol::2 => pragma solidity ^0.8.13;
seaport/contracts/conduit/lib/ConduitConstants.sol::2 => pragma solidity ^0.8.13;
seaport/contracts/conduit/lib/ConduitEnums.sol::2 => pragma solidity ^0.8.13;
seaport/contracts/conduit/lib/ConduitStructs.sol::2 => pragma solidity ^0.8.13;
seaport/contracts/helpers/PointerLibraries.sol::2 => pragma solidity ^0.8.13;
seaport/contracts/interfaces/AbridgedTokenInterfaces.sol::2 => pragma solidity ^0.8.13;
seaport/contracts/interfaces/AmountDerivationErrors.sol::2 => pragma solidity ^0.8.13;
seaport/contracts/interfaces/ConduitControllerInterface.sol::2 => pragma solidity ^0.8.13;
seaport/contracts/interfaces/ConduitInterface.sol::2 => pragma solidity ^0.8.13;
seaport/contracts/interfaces/ConsiderationEventsAndErrors.sol::2 => pragma solidity ^0.8.13;
seaport/contracts/interfaces/ConsiderationInterface.sol::2 => pragma solidity ^0.8.13;
seaport/contracts/interfaces/ContractOffererInterface.sol::2 => pragma solidity ^0.8.13;
seaport/contracts/interfaces/CriteriaResolutionErrors.sol::2 => pragma solidity ^0.8.13;
seaport/contracts/interfaces/EIP1271Interface.sol::2 => pragma solidity ^0.8.13;
seaport/contracts/interfaces/FulfillmentApplicationErrors.sol::2 => pragma solidity ^0.8.13;
seaport/contracts/interfaces/IERC721Receiver.sol::2 => pragma solidity ^0.8.13;
seaport/contracts/interfaces/ImmutableCreate2FactoryInterface.sol::2 => pragma solidity ^0.8.13;
seaport/contracts/interfaces/ReentrancyErrors.sol::2 => pragma solidity ^0.8.13;
seaport/contracts/interfaces/SeaportInterface.sol::2 => pragma solidity ^0.8.13;
seaport/contracts/interfaces/SignatureVerificationErrors.sol::2 => pragma solidity ^0.8.13;
seaport/contracts/interfaces/TokenTransferrerErrors.sol::2 => pragma solidity ^0.8.13;
seaport/contracts/interfaces/TransferHelperErrors.sol::2 => pragma solidity ^0.8.13;
seaport/contracts/interfaces/TransferHelperInterface.sol::2 => pragma solidity ^0.8.13;
seaport/contracts/interfaces/ZoneInteractionErrors.sol::2 => pragma solidity ^0.8.13;
seaport/contracts/interfaces/ZoneInterface.sol::2 => pragma solidity ^0.8.13;
seaport/contracts/lib/ConsiderationConstants.sol::2 => pragma solidity ^0.8.13;
seaport/contracts/lib/ConsiderationEncoder.sol::2 => pragma solidity ^0.8.13;
seaport/contracts/lib/ConsiderationEnums.sol::2 => pragma solidity ^0.8.13;
seaport/contracts/lib/ConsiderationStructs.sol::2 => pragma solidity ^0.8.13;
seaport/contracts/lib/TokenTransferrer.sol::2 => pragma solidity ^0.8.13;
seaport/contracts/lib/TokenTransferrerConstants.sol::2 => pragma solidity ^0.8.13;
```
####  Recommendation:
Old version of Solidity is used `(^0.8.13)`, newer version can be used `(0.8.17)`







### [N05] EMPTY BLOCKS SHOULD BE REMOVED OR EMIT SOMETHING

#### Impact
The code should be refactored such that they no longer exist, or the 
block should do something useful, such as emitting an event or 
reverting. If the contract is meant to be extended, the contract should 
be abstract and the function signatures be added without 
any default implementation. If the block is an empty if-statement block 
to avoid doing subsequent checks in the else-if/else conditions, the 
else-if/else conditions should be nested under the negation of the 
if-statement, because they involve different classes of checks, which 
may lead to the introduction of errors when the code is later modified (if(x){}else if(y){...}else{...} => if(!x){if(y){...}else{...}})


#### Findings:
```
seaport/contracts/lib/Assertions.sol::37 => ) GettersAndDerivers(conduitController) {}
seaport/contracts/lib/BasicOrderFulfiller.sol::41 => constructor(address conduitController) OrderValidator(conduitController) {}
seaport/contracts/lib/BasicOrderFulfiller.sol::488 => for {} lt(i, totalAdditionalRecipients) {
seaport/contracts/lib/BasicOrderFulfiller.sol::597 => for {} lt(i, totalAdditionalRecipients) {
seaport/contracts/lib/Consideration.sol::50 => constructor(address conduitController) OrderCombiner(conduitController) {}
seaport/contracts/lib/Executor.sol::35 => constructor(address conduitController) Verifiers(conduitController) {}
seaport/contracts/lib/GettersAndDerivers.sol::27 => ) ConsiderationBase(conduitController) {}
seaport/contracts/lib/OrderCombiner.sol::41 => constructor(address conduitController) OrderFulfiller(conduitController) {}
seaport/contracts/lib/OrderFulfiller.sol::47 => ) BasicOrderFulfiller(conduitController) {}
seaport/contracts/lib/OrderValidator.sol::55 => constructor(address conduitController) Executor(conduitController) {}
seaport/contracts/lib/Verifiers.sol::26 => constructor(address conduitController) Assertions(conduitController) {}
```

####  Recommendation:
The code should be refactored such that they no longer exist, or the block should do something useful, such as emitting an event or reverting.