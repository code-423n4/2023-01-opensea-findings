

## [L-01] Unspecific Compiler Version Pragma

Avoid floating pragmas for non-library contracts.

While floating pragmas make sense for libraries to allow them to be included with multiple different versions of applications, it may be a security risk for application implementations.

A known vulnerable compiler version may accidentally be selected or security tools might fall-back to an older compiler version ending up checking a different EVM compilation that is ultimately deployed on the blockchain.

It is recommended to pin to a concrete compiler version.

```
seaport/contracts/Seaport.sol::2 => pragma solidity ^0.8.17;
seaport/contracts/conduit/Conduit.sol::2 => pragma solidity ^0.8.13;
seaport/contracts/conduit/ConduitController.sol::2 => pragma solidity ^0.8.13;
seaport/contracts/conduit/lib/ConduitConstants.sol::2 => pragma solidity ^0.8.13;
seaport/contracts/conduit/lib/ConduitEnums.sol::2 => pragma solidity ^0.8.13;
seaport/contracts/conduit/lib/ConduitStructs.sol::2 => pragma solidity ^0.8.13;
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
seaport/contracts/zones/PausableZone.sol::2 => pragma solidity ^0.8.13;
seaport/contracts/zones/PausableZoneController.sol::2 => pragma solidity ^0.8.13;
seaport/contracts/zones/interfaces/PausableZoneControllerInterface.sol::2 => pragma solidity ^0.8.13;
seaport/contracts/zones/interfaces/PausableZoneEventsAndErrors.sol::2 => pragma solidity ^0.8.13;
seaport/contracts/zones/interfaces/PausableZoneInterface.sol::2 => pragma solidity ^0.8.13;
```

## [L-02] Use of Block.timestamp

Block timestamps have historically been used for a variety of applications, such as entropy for random numbers (see the Entropy Illusion for further details), locking funds for periods of time, and various state-changing conditional statements that are time-dependent. Miners have the ability to adjust timestamps slightly, which can prove to be dangerous if block timestamps are used incorrectly in smart contracts.

```
seaport/contracts/lib/AmountDeriver.sol::58 => elapsed = block.timestamp - startTime;
```

## [L-03] abi.encodePacked() should not be used with dynamic types when passing the result to a hash function such as keccak256()

Use abi.encode() instead which will pad items to 32 bytes, which will prevent hash collisions (e.g. abi.encodePacked(0x123,0x456) => 0x123456 => abi.encodePacked(0x1,0x23456), but abi.encode(0x123,0x456) => 0x0...1230...456). Unless there is a compelling reason, abi.encode should be preferred. If there is only one argument to abi.encodePacked() it can often be cast to bytes() or bytes32() instead.

```
seaport/contracts/lib/BasicOrderFulfiller.sol::572 => *   `keccak256(abi.encodePacked(receivedItemHashes))`
seaport/contracts/lib/BasicOrderFulfiller.sol::699 => *   `keccak256(abi.encodePacked(offerItemHashes))`
seaport/contracts/lib/BasicOrderFulfiller.sol::741 => *   - 0xe0:   keccak256(abi.encodePacked(offerHashes))
seaport/contracts/lib/BasicOrderFulfiller.sol::742 => *   - 0x100:  keccak256(abi.encodePacked(considerationHashes))
seaport/contracts/lib/ConsiderationConstants.sol::326 => *   - 0xe0:   keccak256(abi.encodePacked(offerHashes))
seaport/contracts/lib/ConsiderationConstants.sol::327 => *   - 0x100:  keccak256(abi.encodePacked(considerationHashes))
```

## [L-04] Events not emitted for important state changes

When changing state variables events are not emitted. Emitting events allows monitoring activities with off-chain monitoring tools.

```
seaport/contracts/interfaces/AbridgedTokenInterfaces.sol::13 => function setApprovalForAll(address, bool) external;
seaport/contracts/interfaces/AbridgedTokenInterfaces.sol::35 => function setApprovalForAll(address, bool) external;
```

## [N-01] Event is missing indexed fields

Each event should use three indexed fields if there are three or more fields

```
seaport/contracts/interfaces/ConduitControllerInterface.sol::29 => event NewConduit(address conduit, bytes32 conduitKey);
seaport/contracts/interfaces/ConsiderationEventsAndErrors.sol::61 => event OrderValidated(bytes32 orderHash, OrderParameters orderParameters);
seaport/contracts/interfaces/ConsiderationEventsAndErrors.sol::69 => event OrdersMatched(bytes32[] orderHashes);
seaport/contracts/zones/interfaces/PausableZoneEventsAndErrors.sol::25 => event PotentialOwnerUpdated(address newPotentialOwner);
seaport/contracts/zones/interfaces/PausableZoneEventsAndErrors.sol::33 => event OwnershipTransferred(address previousOwner, address newOwner);
seaport/contracts/zones/interfaces/PausableZoneEventsAndErrors.sol::41 => event ZoneCreated(address zone, bytes32 salt);
seaport/contracts/zones/interfaces/PausableZoneEventsAndErrors.sol::48 => event PauserUpdated(address newPauser);
seaport/contracts/zones/interfaces/PausableZoneEventsAndErrors.sol::55 => event OperatorUpdated(address newOperator);
```

## [N-02] Missing NatSpec

Code should include NatSpec

```
seaport/contracts/conduit/lib/ConduitConstants.sol::1 => // SPDX-License-Identifier: MIT
seaport/contracts/conduit/lib/ConduitEnums.sol::1 => // SPDX-License-Identifier: MIT
seaport/contracts/conduit/lib/ConduitStructs.sol::1 => // SPDX-License-Identifier: MIT
seaport/contracts/interfaces/AbridgedTokenInterfaces.sol::1 => // SPDX-License-Identifier: MIT
seaport/contracts/interfaces/ContractOffererInterface.sol::1 => // SPDX-License-Identifier: MIT
seaport/contracts/interfaces/EIP1271Interface.sol::1 => // SPDX-License-Identifier: MIT
seaport/contracts/interfaces/IERC721Receiver.sol::1 => // SPDX-License-Identifier: MIT
seaport/contracts/interfaces/ZoneInterface.sol::1 => // SPDX-License-Identifier: MIT
seaport/contracts/lib/ConsiderationEnums.sol::1 => // SPDX-License-Identifier: MIT
seaport/contracts/lib/TokenTransferrerConstants.sol::1 => // SPDX-License-Identifier: MIT
```

## [N-03] Missing event for critical parameter change

Emitting events after sensitive changes take place, to facilitate tracking and notify off-chain clients following changes to the contract.

```
seaport/contracts/interfaces/AbridgedTokenInterfaces.sol::13 => function setApprovalForAll(address, bool) external;
seaport/contracts/interfaces/AbridgedTokenInterfaces.sol::35 => function setApprovalForAll(address, bool) external;
```
