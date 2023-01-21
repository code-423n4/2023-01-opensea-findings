ConsiderationDecoder.sol
PROBLEM
Explicitly initializing a variable with it's default value costs unnecessary gas.
Uninitialised variables are assigned with the types default value.
PROOF OF CONCEPT
https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/lib/ConsiderationDecoder.sol#L399
399  for (uint256 offset = 0; offset < tailOffset; offset += OneWord) {/* .... */}
https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/lib/ConsiderationDecoder.sol#L498
498  for (uint256 offset = 0; offset < tailOffset; offset += OneWord) {/* .... */}
https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/lib/ConsiderationDecoder.sol#L538
538  for (uint256 offset = 0; offset < tailOffset; offset += OneWord) {/* .... */}
https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/lib/ConsiderationDecoder.sol#L630
630  for (uint256 offset = 0; offset < tailOffset; offset += OneWord) {/* .... */}
https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/lib/ConsiderationDecoder.sol#L673
673  for (uint256 offset = 0; offset < tailOffset; offset += OneWord) {/* .... */}
https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/lib/ConsiderationDecoder.sol#L744
744  for (uint256 offset = 0; offset < tailOffset; offset += OneWord) {/* .... */}
MITIGATION
Remove explicit initialization for default values.



OrderValidator.sol
PROBLEM
Explicitly initializing a variable with it's default value costs unnecessary gas.
Uninitialised variables are assigned with the types default value.
PROOF OF CONCEPT
https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/lib/OrderValidator.sol#L549
549  for (uint256 i = 0; i < originalOfferLength; ) {/* .... */}
https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/lib/OrderValidator.sol#L591
591  for (uint256 i = 0; i < newConsiderationLength; ) {/* .... */}
https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/lib/OrderValidator.sol#L667
667  for (uint256 i = 0; i < totalOrders; ) {/* .... */}
https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/lib/OrderValidator.sol#L753
753  for (uint256 i = 0; i < totalOrders; ++i) {/* .... */}
MITIGATION
Remove explicit initialization for default values.

ConsiderationConstants.sol
PROBLEM
Explicitly initializing a variable with it's default value costs unnecessary gas.
Uninitialised variables are assigned with the types default value.
PROOF OF CONCEPT
https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/lib/ConsiderationConstants.sol#L44
44  uint256 constant information_version_offset = 0;
MITIGATION
Remove explicit initialization for default values.


OrderFulfiller.sol
PROBLEM
Explicitly initializing a variable with it's default value costs unnecessary gas.
Uninitialised variables are assigned with the types default value.
PROOF OF CONCEPT
https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/lib/OrderFulfiller.sol#L207
207 for (uint256 i = 0; i < totalOfferItems; ++i) {/* .... */}
https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/lib/OrderFulfiller.sol#L301
301  for (uint256 i = 0; i < totalConsiderationItems; ++i) {/* .... */}
MITIGATION
Remove explicit initialization for default values.


ConduitController.sol
PROBLEM
Use assembly to check for address(0)
You can save about 6 gas per instance if using assembly to check for address (0)
PROOF OF CONCEPT
https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/conduit/ConduitController.sol#L61
61  if (initialOwner == address(0)) {/* .... */}
https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/conduit/ConduitController.sol#L210
210  if (newPotentialOwner == address(0)) {/* .... */}
https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/conduit/ConduitController.sol#L237
237  if (_conduits[conduit].potentialOwner == address(0)) {/* .... */}
https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/conduit/ConduitController.sol#L315
315  if (conduitKey == bytes32(0)) {/* .... */}
https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/conduit/ConduitController.sol#L499
499  if (_conduits[conduit].key == bytes32(0)) {/* .... */}
MITIGATION


ZoneInteraction.sol
PROBLEM
Use calldata instead of memory for function arguments that do not get mutated.
If a reference type function parameter is read-only, it is cheaper in gas to use calldata 
instead of memory. 
Calldata is a non-modifiable, non-persistent area where function arguments are stored, 
and behaves mostly like memory.
Try to use calldata as a data location because it will avoid copies and also makes sure that 
the data cannot be modified.
PROOF OF CONCEPT
https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/lib/ZoneInteraction.sol#L78
78  AdvancedOrder memory advancedOrder,
MITIGATION
Replace memory with calldata


TypehashDirectory.sol
PROBLEM
Explicitly initializing a variable with it's default value costs unnecessary gas.
Uninitialised variables are assigned with the types default value.
PROOF OF CONCEPT
https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/lib/TypehashDirectory.sol#L48
48   for (uint256 i = 0; i < MaxTreeHeight; ) {/* .... */}
MITIGATION
Remove explicit initialization for default values.
