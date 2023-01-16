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
sea/contracts/Seaport.sol::2 => pragma solidity ^0.8.17;
sea/contracts/conduit/Conduit.sol::2 => pragma solidity ^0.8.13;
sea/contracts/conduit/ConduitController.sol::2 => pragma solidity ^0.8.13;
sea/contracts/conduit/lib/ConduitConstants.sol::2 => pragma solidity ^0.8.13;
sea/contracts/conduit/lib/ConduitEnums.sol::2 => pragma solidity ^0.8.13;
sea/contracts/conduit/lib/ConduitStructs.sol::2 => pragma solidity ^0.8.13;
sea/contracts/helpers/PointerLibraries.sol::2 => pragma solidity ^0.8.13;
sea/contracts/interfaces/AbridgedTokenInterfaces.sol::2 => pragma solidity ^0.8.13;
sea/contracts/interfaces/AmountDerivationErrors.sol::2 => pragma solidity ^0.8.13;
sea/contracts/interfaces/ConduitControllerInterface.sol::2 => pragma solidity ^0.8.13;
sea/contracts/interfaces/ConduitInterface.sol::2 => pragma solidity ^0.8.13;
sea/contracts/interfaces/ConsiderationEventsAndErrors.sol::2 => pragma solidity ^0.8.13;
sea/contracts/interfaces/ConsiderationInterface.sol::2 => pragma solidity ^0.8.13;
sea/contracts/interfaces/ContractOffererInterface.sol::2 => pragma solidity ^0.8.13;
sea/contracts/interfaces/CriteriaResolutionErrors.sol::2 => pragma solidity ^0.8.13;
sea/contracts/interfaces/EIP1271Interface.sol::2 => pragma solidity ^0.8.13;
sea/contracts/interfaces/FulfillmentApplicationErrors.sol::2 => pragma solidity ^0.8.13;
sea/contracts/interfaces/IERC721Receiver.sol::2 => pragma solidity ^0.8.13;
sea/contracts/interfaces/ImmutableCreate2FactoryInterface.sol::2 => pragma solidity ^0.8.13;
sea/contracts/interfaces/ReentrancyErrors.sol::2 => pragma solidity ^0.8.13;
sea/contracts/interfaces/SeaportInterface.sol::2 => pragma solidity ^0.8.13;
sea/contracts/interfaces/SignatureVerificationErrors.sol::2 => pragma solidity ^0.8.13;
sea/contracts/interfaces/TokenTransferrerErrors.sol::2 => pragma solidity ^0.8.13;
sea/contracts/interfaces/TransferHelperErrors.sol::2 => pragma solidity ^0.8.13;
sea/contracts/interfaces/TransferHelperInterface.sol::2 => pragma solidity ^0.8.13;
sea/contracts/interfaces/ZoneInteractionErrors.sol::2 => pragma solidity ^0.8.13;
sea/contracts/interfaces/ZoneInterface.sol::2 => pragma solidity ^0.8.13;
sea/contracts/lib/AmountDeriver.sol::2 => pragma solidity ^0.8.17;
sea/contracts/lib/Assertions.sol::2 => pragma solidity ^0.8.17;
sea/contracts/lib/BasicOrderFulfiller.sol::2 => pragma solidity ^0.8.17;
sea/contracts/lib/Consideration.sol::2 => pragma solidity ^0.8.17;
sea/contracts/lib/ConsiderationBase.sol::2 => pragma solidity ^0.8.17;
sea/contracts/lib/ConsiderationConstants.sol::2 => pragma solidity ^0.8.13;
sea/contracts/lib/ConsiderationDecoder.sol::2 => pragma solidity ^0.8.17;
sea/contracts/lib/ConsiderationEncoder.sol::2 => pragma solidity ^0.8.13;
sea/contracts/lib/ConsiderationEnums.sol::2 => pragma solidity ^0.8.13;
sea/contracts/lib/ConsiderationErrors.sol::2 => pragma solidity ^0.8.17;
sea/contracts/lib/ConsiderationStructs.sol::2 => pragma solidity ^0.8.13;
sea/contracts/lib/CounterManager.sol::2 => pragma solidity ^0.8.17;
sea/contracts/lib/CriteriaResolution.sol::2 => pragma solidity ^0.8.17;
sea/contracts/lib/Executor.sol::2 => pragma solidity ^0.8.17;
sea/contracts/lib/FulfillmentApplier.sol::2 => pragma solidity ^0.8.17;
sea/contracts/lib/GettersAndDerivers.sol::2 => pragma solidity ^0.8.17;
sea/contracts/lib/LowLevelHelpers.sol::2 => pragma solidity ^0.8.17;
sea/contracts/lib/OrderCombiner.sol::2 => pragma solidity ^0.8.17;
sea/contracts/lib/OrderFulfiller.sol::2 => pragma solidity ^0.8.17;
sea/contracts/lib/OrderValidator.sol::2 => pragma solidity ^0.8.17;
sea/contracts/lib/ReentrancyGuard.sol::2 => pragma solidity ^0.8.17;
sea/contracts/lib/SignatureVerification.sol::2 => pragma solidity ^0.8.17;
sea/contracts/lib/TokenTransferrer.sol::2 => pragma solidity ^0.8.13;
sea/contracts/lib/TokenTransferrerConstants.sol::2 => pragma solidity ^0.8.13;
sea/contracts/lib/TypehashDirectory.sol::2 => pragma solidity ^0.8.17;
sea/contracts/lib/Verifiers.sol::2 => pragma solidity ^0.8.17;
sea/contracts/lib/ZoneInteraction.sol::2 => pragma solidity ^0.8.17;
```
#### Tools used
Manual VS Code review