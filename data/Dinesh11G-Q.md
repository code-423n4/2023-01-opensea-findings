### Unspecific Compiler Version Pragma

#### Impact
Issue Information: 
Avoid floating pragmas for non-library contracts.

While floating pragmas make sense for libraries to allow them to be included with multiple different versions of applications, it may be a security risk for application implementations.

A known vulnerable compiler version may accidentally be selected or security tools might fall-back to an older compiler version ending up checking a different EVM compilation that is ultimately deployed on the blockchain.

It is recommended to pin to a concrete compiler version.

Example
🤦 Bad:

pragma solidity ^0.8.0;
🚀 Good:

pragma solidity 0.8.4;

#### Findings:
```
seaport/contracts/Seaport.sol::2 => pragma solidity ^0.8.13;
seaport/contracts/conduit/Conduit.sol::2 => pragma solidity ^0.8.7;
seaport/contracts/conduit/ConduitController.sol::2 => pragma solidity ^0.8.7;
seaport/contracts/conduit/lib/ConduitConstants.sol::2 => pragma solidity ^0.8.7;
seaport/contracts/conduit/lib/ConduitEnums.sol::2 => pragma solidity ^0.8.7;
seaport/contracts/conduit/lib/ConduitStructs.sol::2 => pragma solidity ^0.8.7;
seaport/contracts/interfaces/AbridgedTokenInterfaces.sol::2 => pragma solidity ^0.8.7;
seaport/contracts/interfaces/AmountDerivationErrors.sol::2 => pragma solidity ^0.8.7;
seaport/contracts/interfaces/ConduitControllerInterface.sol::2 => pragma solidity ^0.8.7;
seaport/contracts/interfaces/ConduitInterface.sol::2 => pragma solidity ^0.8.7;
seaport/contracts/interfaces/ConsiderationEventsAndErrors.sol::2 => pragma solidity ^0.8.7;
seaport/contracts/interfaces/ConsiderationInterface.sol::2 => pragma solidity ^0.8.7;
seaport/contracts/interfaces/CriteriaResolutionErrors.sol::2 => pragma solidity ^0.8.7;
seaport/contracts/interfaces/EIP1271Interface.sol::2 => pragma solidity ^0.8.7;
seaport/contracts/interfaces/FulfillmentApplicationErrors.sol::2 => pragma solidity ^0.8.7;
seaport/contracts/interfaces/IERC721Receiver.sol::2 => pragma solidity ^0.8.7;
seaport/contracts/interfaces/ImmutableCreate2FactoryInterface.sol::2 => pragma solidity ^0.8.7;
seaport/contracts/interfaces/ReentrancyErrors.sol::2 => pragma solidity ^0.8.7;
seaport/contracts/interfaces/SeaportInterface.sol::2 => pragma solidity ^0.8.7;
seaport/contracts/interfaces/SignatureVerificationErrors.sol::2 => pragma solidity ^0.8.7;
seaport/contracts/interfaces/TokenTransferrerErrors.sol::2 => pragma solidity ^0.8.7;
seaport/contracts/interfaces/TransferHelperErrors.sol::2 => pragma solidity ^0.8.7;
seaport/contracts/interfaces/TransferHelperInterface.sol::2 => pragma solidity ^0.8.7;
seaport/contracts/interfaces/ZoneInteractionErrors.sol::2 => pragma solidity ^0.8.7;
seaport/contracts/interfaces/ZoneInterface.sol::2 => pragma solidity ^0.8.7;
seaport/contracts/lib/AmountDeriver.sol::2 => pragma solidity ^0.8.13;
seaport/contracts/lib/Assertions.sol::2 => pragma solidity ^0.8.13;
seaport/contracts/lib/BasicOrderFulfiller.sol::2 => pragma solidity ^0.8.13;
seaport/contracts/lib/Consideration.sol::2 => pragma solidity ^0.8.13;
seaport/contracts/lib/ConsiderationBase.sol::2 => pragma solidity ^0.8.13;
seaport/contracts/lib/ConsiderationConstants.sol::2 => pragma solidity ^0.8.7;
seaport/contracts/lib/ConsiderationEnums.sol::2 => pragma solidity ^0.8.7;
seaport/contracts/lib/ConsiderationStructs.sol::2 => pragma solidity ^0.8.7;
seaport/contracts/lib/CounterManager.sol::2 => pragma solidity ^0.8.13;
seaport/contracts/lib/CriteriaResolution.sol::2 => pragma solidity ^0.8.13;
seaport/contracts/lib/Executor.sol::2 => pragma solidity ^0.8.13;
seaport/contracts/lib/FulfillmentApplier.sol::2 => pragma solidity ^0.8.13;
seaport/contracts/lib/GettersAndDerivers.sol::2 => pragma solidity ^0.8.13;
seaport/contracts/lib/LowLevelHelpers.sol::2 => pragma solidity ^0.8.13;
seaport/contracts/lib/OrderCombiner.sol::2 => pragma solidity ^0.8.13;
seaport/contracts/lib/OrderFulfiller.sol::2 => pragma solidity ^0.8.13;
seaport/contracts/lib/OrderValidator.sol::2 => pragma solidity ^0.8.13;
seaport/contracts/lib/ReentrancyGuard.sol::2 => pragma solidity ^0.8.13;
seaport/contracts/lib/SignatureVerification.sol::2 => pragma solidity ^0.8.13;
seaport/contracts/lib/TokenTransferrer.sol::2 => pragma solidity ^0.8.7;
seaport/contracts/lib/TokenTransferrerConstants.sol::2 => pragma solidity ^0.8.7;
seaport/contracts/lib/Verifiers.sol::2 => pragma solidity ^0.8.13;
seaport/contracts/lib/ZoneInteraction.sol::2 => pragma solidity ^0.8.13;
```
#### Tools used
Manual VS Code review