### Table of contents
- [FINDINGS](#findings)
- [Internal/Private functions only called once can be inlined to save gas](#internalprivate-functions-only-called-once-can-be-inlined-to-save-gas)
- [Multiple accesses of a mapping/array should use a local variable cache](#multiple-accesses-of-a-mappingarray-should-use-a-local-variable-cache)
  - [Conduit.sol.updateChannel(): \_channels\[channel\] should be cached in local storage](#conduitsolupdatechannel-_channelschannel-should-be-cached-in-local-storage)
- [Pack structs by variables that can fit together next to each other.](#pack-structs-by-variables-that-can-fit-together-next-to-each-other)
  - [We can save 2 SLOTS here: 4k gas\*\*](#we-can-save-2-slots-here-4k-gas)
  - [Save 2 slots here(4k gas)](#save-2-slots-here4k-gas)
  - [Save 2 SLOTS here: 4k gas](#save-2-slots-here-4k-gas)
  - [save 2 SLOTS here: 4k Gas](#save-2-slots-here-4k-gas-1)
- [Using storage instead of memory for structs/arrays saves gas](#using-storage-instead-of-memory-for-structsarrays-saves-gas)
- [`keccak256()` should only need to be called on a specific string literal once](#keccak256-should-only-need-to-be-called-on-a-specific-string-literal-once)
- [y++ costs more gas than ++y for state variables](#y-costs-more-gas-than-y-for-state-variables)

## FINDINGS
NB: Some functions have been truncated where necessary to just show affected parts of the code
Through out the report some places might be denoted with audit tags to show the actual place affected.

## Internal/Private functions only called once can be inlined to save gas

Not inlining costs 20 to 40 gas because of two extra JUMP instructions and additional stack operations needed for function calls.

Affected code:

https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/lib/BasicOrderFulfiller.sol#L304-L311
```solidity
File: /contracts/lib/BasicOrderFulfiller.sol
304:    function _prepareBasicFulfillmentFromCalldata(
305:        BasicOrderParameters calldata parameters,
306:        OrderType orderType,
307:        ItemType receivedItemType,
308:        ItemType additionalRecipientsItemType,
309:        address additionalRecipientsToken,
310:        ItemType offeredItemType
311:    ) internal returns (bytes32 orderHash) {
```
The above function is only called once on [Line 150](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/lib/BasicOrderFulfiller.sol#L150)

https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/lib/BasicOrderFulfiller.sol#L916-L919
```solidity
File: /contracts/lib/BasicOrderFulfiller.sol
916:    function _transferNativeTokensAndFinalize(
917:        uint256 amount,
918:        address payable to
919:    ) internal {
```
The above function is only called once on [Line 196](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/lib/BasicOrderFulfiller.sol#L196)

https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/lib/BasicOrderFulfiller.sol#L1006-L1011
```solidity
File: /contracts/lib/BasicOrderFulfiller.sol
1006:    function _transferERC20AndFinalize(
1007:        address offerer,
1008:        BasicOrderParameters calldata parameters,
1009:        bool fromOfferer,
1010:        bytes memory accumulator
1011:    ) internal {
```
The above function is only called once on [Line 258](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/lib/BasicOrderFulfiller.sol#L258)

https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/lib/OrderValidator.sol#L439-L442
```solidity
File: /contracts/lib/OrderValidator.sol
439:    function _checkRecipients(
440:        address originalRecipient,
441:        address newRecipient
442:    ) internal pure returns (uint256 isInvalid) {
```
The above function is only called once on [Line 609](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/lib/OrderValidator.sol#L609)

https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/lib/OrderValidator.sol#L472-L477
```solidity
File: /contracts/lib/OrderValidator.sol
472:    function _getGeneratedOrder(
473:        OrderParameters memory orderParameters,
474:        bytes memory context,
475:        bool revertOnInvalid
476:    )
477:        internal
```
The above function is only called once on [Line 169](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/lib/OrderValidator.sol#L169)

https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/lib/OrderValidator.sol#L890-L894
```solidity
File: /contracts/lib/OrderValidator.sol
890:    function _doesNotSupportPartialFills(
891:        OrderType orderType,
892:        uint256 numerator,
893:        uint256 denominator
894:    ) internal pure returns (bool isFullOrder) {
```
The above function is only called once on [Line 188](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/lib/OrderValidator.sol#L188)

https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/lib/OrderCombiner.sol#L537-L545
```solidity
File: /contracts/lib/OrderCombiner.sol
537:    function _executeAvailableFulfillments(
538:        AdvancedOrder[] memory advancedOrders,
539:        FulfillmentComponent[][] memory offerFulfillments,
540:        FulfillmentComponent[][] memory considerationFulfillments,
541:        bytes32 fulfillerConduitKey,
542:        address recipient,
543:        bytes32[] memory orderHashes
544:    )
545:        internal
```
The above function is only called once on [Line 132](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/lib/OrderCombiner.sol#L132)

https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/lib/OrderCombiner.sol#L867
```solidity
File: /contracts/lib/OrderCombiner.sol
867:    function _emitOrdersMatched(bytes32[] memory orderHashes) internal {
```
The above function is only called once on [Line 948](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/lib/OrderCombiner.sol#L948)

https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/lib/OrderCombiner.sol#L981-L986
```solidity
File: /contracts/lib/OrderCombiner.sol
981:    function _fulfillAdvancedOrders(
982:        AdvancedOrder[] memory advancedOrders,
983:        Fulfillment[] memory fulfillments,
984:        bytes32[] memory orderHashes,
985:        address recipient
986:    ) internal returns (Execution[] memory executions) {
```
The above function is only called once on [Line 952](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/lib/OrderCombiner.sol#L952)

https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/lib/Executor.sol#L479
```solidity
File: /contracts/lib/Executor.sol
479:    function _trigger(bytes32 conduitKey, bytes memory accumulator) internal {
```
The above function is only called once on [Line 464](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/lib/Executor.sol#L464)

https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/lib/OrderFulfiller.sol#L158-L164
```solidity
File: /contracts/lib/OrderFulfiller.sol
158:    function _applyFractionsAndTransferEach(
159:        OrderParameters memory orderParameters,
160:        uint256 numerator,
161:        uint256 denominator,
162:        bytes32 fulfillerConduitKey,
163:        address recipient
164:    ) internal {
```
The above is only called once on [Line 107](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/lib/OrderFulfiller.sol#L107)

https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/lib/CriteriaResolution.sol#L193-L197
```solidity
File: /contracts/lib/CriteriaResolution.sol
193:    function _updateCriteriaItem(
194:        OfferItem[] memory offer,
195:        uint256 componentIndex,
196:        CriteriaResolver memory criteriaResolver
197:    ) internal pure {
```
The above function is only called once on [Line 132](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/lib/CriteriaResolution.sol#L132)

https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/lib/CriteriaResolution.sol#L265-L269
```solidity
File: /contracts/lib/CriteriaResolution.sol
265:    function _verifyProof(
266:        uint256 leaf,
267:        uint256 root,
268:        bytes32[] memory proof
269:    ) internal pure {
```
The above function is only called once on [Line 214](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/lib/CriteriaResolution.sol#L214)

https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/lib/Verifiers.sol#L117-L119
```solidity
File: /contracts/lib/Verifiers.sol
117:    function _isValidBulkOrderSize(
118:        uint256 signatureLength
119:    ) internal pure returns (bool validLength) {
```
The above is only called once on [Line 92](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/lib/Verifiers.sol#L92)

https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/lib/Verifiers.sol#L150-L153
```solidity
File: /contracts/lib/Verifiers.sol
150:    function _computeBulkOrderProof(
151:        bytes memory proofAndSignature,
152:        bytes32 leaf
153:    ) internal view returns (bytes32 bulkOrderHash) {
```
The above is only called once on [Line 94](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/lib/Verifiers.sol#L94)

https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/lib/TypehashDirectory.sol#L99-L101
```solidity
File: /contracts/lib/TypehashDirectory.sol
99:    function getMaxTreeBrackets(
100:        uint256 maxHeight
101:    ) internal pure returns (bytes memory) {
```
The above is only called once on [Line 35](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/lib/TypehashDirectory.sol#L35)

https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/lib/TypehashDirectory.sol#L131
```solidity
File: /contracts/lib/TypehashDirectory.sol
131:    function getTreeSubTypes() internal pure returns (bytes memory) {
```
The above is only called once on [Line 38](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/lib/TypehashDirectory.sol#L38)

## Multiple accesses of a mapping/array should use a local variable cache

Caching a mapping's value in a local storage or calldata variable when the value is accessed multiple times saves ~42 gas per access due to not having to perform the same offset calculation every time.
**Help the Optimizer by saving a storage variable's reference instead of repeatedly fetching it**

To help the optimizer,declare a storage type variable and use it instead of repeatedly fetching the reference in a map or an array. 
As an example, instead of repeatedly calling ```someMap[someIndex]```, save its reference like this: ```SomeStruct storage someStruct = someMap[someIndex]``` and use it.

https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/conduit/Conduit.sol#L187-L203
### Conduit.sol.updateChannel(): \_channels\[channel] should be cached in local storage
```solidity
File: /contracts/conduit/Conduit.sol
187:    function updateChannel(address channel, bool isOpen) external override {

195:        if (_channels[channel] == isOpen) { //@audit: Initial access
196:            revert ChannelStatusAlreadySet(channel, isOpen);
197:        }

198:        // Update the status of the channel.
199:        _channels[channel] = isOpen;//@audit: 2nd access
```


## Pack structs by variables that can fit together next to each other.
**Note: The following optimizations requires we use uint64 for variables that reference time, using uint64 should be safe for 532 years**

As the solidity EVM works with 32 bytes, variables less than 32 bytes should be packed inside a struct so that they can be stored in the same slot, this saves gas when writing to storage ~20000 gas

### We can save 2 SLOTS here: 4k gas**
https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/lib/ConsiderationStructs.sol#L26-L38
**startTime and endTime can be declared as uint64 which would still be safe for 
```solidity
File: /contracts/lib/ConsiderationStructs.sol
26: struct OrderComponents {
27:    address offerer;
28:    address zone;
29:    OfferItem[] offer;
30:    ConsiderationItem[] consideration;
31:    OrderType orderType;
32:    uint256 startTime;
33:    uint256 endTime;
34:    bytes32 zoneHash;
35:    uint256 salt;
36:    bytes32 conduitKey;
37:    uint256 counter;
38: }
```

```diff
diff --git a/contracts/lib/ConsiderationStructs.sol b/contracts/lib/ConsiderationStructs.sol
index fbea9f53..be9f0799 100644
--- a/contracts/lib/ConsiderationStructs.sol
+++ b/contracts/lib/ConsiderationStructs.sol
@@ -24,13 +24,13 @@ import {
  *      be received by their respective recipient.
  */
 struct OrderComponents {
+    uint64 startTime;
     address offerer;
+    uint64 endTime;
     address zone;
     OfferItem[] offer;
     ConsiderationItem[] consideration;
     OrderType orderType;
-    uint256 startTime;
-    uint256 endTime;
     bytes32 zoneHash;
     uint256 salt;
     bytes32 conduitKey;
```

### Save 2 slots here(4k gas)
https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/lib/ConsiderationStructs.sol#L104-L125
**Same case as the above, we can use uint64 for startTime and endTime**
```solidity
File: /contracts/lib/ConsiderationStructs.sol
104: struct BasicOrderParameters {
105:    // calldata offset
106:    address considerationToken; // 0x24
107:    uint256 considerationIdentifier; // 0x44
108:    uint256 considerationAmount; // 0x64
109:    address payable offerer; // 0x84
110:    address zone; // 0xa4
111:    address offerToken; // 0xc4
112:    uint256 offerIdentifier; // 0xe4
113:    uint256 offerAmount; // 0x104
114:    BasicOrderType basicOrderType; // 0x124
115:    uint256 startTime; // 0x144
116:    uint256 endTime; // 0x164
117:    bytes32 zoneHash; // 0x184
118:    uint256 salt; // 0x1a4
119:    bytes32 offererConduitKey; // 0x1c4
120:    bytes32 fulfillerConduitKey; // 0x1e4
121:    uint256 totalOriginalAdditionalRecipients; // 0x204
122:    AdditionalRecipient[] additionalRecipients; // 0x224
123:    bytes signature; // 0x244
124:    // Total length, excluding dynamic array data: 0x264 (580)
125: }
```

```diff
diff --git a/contracts/lib/ConsiderationStructs.sol b/contracts/lib/ConsiderationStructs.sol
index fbea9f53..90883e30 100644
--- a/contracts/lib/ConsiderationStructs.sol
+++ b/contracts/lib/ConsiderationStructs.sol
@@ -102,18 +102,17 @@ struct ReceivedItem {
  *      type is `basicOrderType = orderType + (4 * basicOrderRoute)`.)
  */
 struct BasicOrderParameters {
-    // calldata offset
+    uint64 startTime; // 0x144
     address considerationToken; // 0x24
     uint256 considerationIdentifier; // 0x44
     uint256 considerationAmount; // 0x64
+    uint64 endTime; // 0x164
     address payable offerer; // 0x84
     address zone; // 0xa4
     address offerToken; // 0xc4
     uint256 offerIdentifier; // 0xe4
     uint256 offerAmount; // 0x104
     BasicOrderType basicOrderType; // 0x124
-    uint256 startTime; // 0x144
-    uint256 endTime; // 0x164
     bytes32 zoneHash; // 0x184
     uint256 salt; // 0x1a4
     bytes32 offererConduitKey; // 0x1c4
```

### Save 2 SLOTS here: 4k gas
https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/lib/ConsiderationStructs.sol#L143-L156
**Same case as the above, we can use uint64 for startTime and endTime**
```solidity
File: /contracts/lib/ConsiderationStructs.sol
143: struct OrderParameters {
144:    address offerer; // 0x00
145:    address zone; // 0x20
146:    OfferItem[] offer; // 0x40
147:    ConsiderationItem[] consideration; // 0x60
148:    OrderType orderType; // 0x80
149:    uint256 startTime; // 0xa0
150:    uint256 endTime; // 0xc0
151:    bytes32 zoneHash; // 0xe0
152:    uint256 salt; // 0x100
153:    bytes32 conduitKey; // 0x120
154:    uint256 totalOriginalConsiderationItems; // 0x140
155:    // offer.length                          // 0x160
156: }
```

```diff
diff --git a/contracts/lib/ConsiderationStructs.sol b/contracts/lib/ConsiderationStructs.sol
index fbea9f53..01420929 100644
--- a/contracts/lib/ConsiderationStructs.sol
+++ b/contracts/lib/ConsiderationStructs.sol
@@ -141,13 +141,13 @@ struct AdditionalRecipient {
  *      supplied, as the caller may specify additional consideration items.
  */
 struct OrderParameters {
+    uint64 startTime; // 0xa0
     address offerer; // 0x00
+    uint64 endTime; // 0xc0
     address zone; // 0x20
     OfferItem[] offer; // 0x40
     ConsiderationItem[] consideration; // 0x60
     OrderType orderType; // 0x80
-    uint256 startTime; // 0xa0
-    uint256 endTime; // 0xc0
     bytes32 zoneHash; // 0xe0
     uint256 salt; // 0x100
     bytes32 conduitKey; // 0x120
```

### save 2 SLOTS here: 4k Gas
https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/lib/ConsiderationStructs.sol#L256-L267
**Same case as the above, we can use uint64 for startTime and endTime**
```solidity
File: /contracts/lib/ConsiderationStructs.sol
256: struct ZoneParameters {
257:    bytes32 orderHash;
258:    address fulfiller;
259:    address offerer;
260:    SpentItem[] offer;
261:    ReceivedItem[] consideration;
262:    bytes extraData;
263:    bytes32[] orderHashes;
264:    uint256 startTime;
265:    uint256 endTime;
266:    bytes32 zoneHash;
267: }
```

```diff
diff --git a/contracts/lib/ConsiderationStructs.sol b/contracts/lib/ConsiderationStructs.sol
index fbea9f53..0387ff7f 100644
--- a/contracts/lib/ConsiderationStructs.sol
+++ b/contracts/lib/ConsiderationStructs.sol
@@ -255,14 +255,14 @@ struct Execution {
  */
 struct ZoneParameters {
     bytes32 orderHash;
+    uint64 startTime;
     address fulfiller;
+    uint64 endTime;
     address offerer;
     SpentItem[] offer;
     ReceivedItem[] consideration;
     bytes extraData;
     bytes32[] orderHashes;
-    uint256 startTime;
-    uint256 endTime;
     bytes32 zoneHash;
 }
```


## Using storage instead of memory for structs/arrays saves gas

When fetching data from a storage location, assigning the data to a memory variable causes all fields of the struct/array to be read from storage, which incurs a Gcoldsload (2100 gas) for each field of the struct/array. If the fields are read from the new memory variable, they incur an additional MLOAD rather than a cheap stack read. Instead of declearing the variable with the memory keyword, declaring the variable with the storage keyword and caching any fields that need to be re-read in stack variables, will be much cheaper, only incuring the Gcoldsload for the fields actually read. The only time it makes sense to read the whole struct/array into a memory variable, is if the full struct/array is being returned by the function, is being passed to a function that requires memory, or if the array/struct is being read from another memory array/struct

https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/lib/FulfillmentApplier.sol#L122
```solidity
File: /contracts/lib/FulfillmentApplier.sol
122:            FulfillmentComponent memory targetComponent = offerComponents[0];
```

https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/lib/CriteriaResolution.sol#L199
```solidity
File: /contracts/lib/CriteriaResolution.sol
199:        OfferItem memory offerItem = offer[componentIndex];
```

https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/lib/OrderFulfiller.sol#L104
```solidity
File: /contracts/lib/CriteriaResolution.sol
104:        OrderParameters memory orderParameters = advancedOrders[0].parameters;
```

## `keccak256()` should only need to be called on a specific string literal once

It should be saved to an immutable variable, and the variable used instead. If the hash is being used as a part of a function selector, the cast to `bytes4` should also only be done once

https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/lib/ConsiderationBase.sol#L196
```solidity
File: /contracts/lib/ConsiderationBase.sol
196:        versionHash = keccak256(bytes("1.2"));
```

https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/lib/ConsiderationBase.sol#L243-L252
```solidity
File: /contracts/lib/ConsiderationBase.sol
243:        eip712DomainTypehash = keccak256(
244:            bytes(
245:                "EIP712Domain("
246:                    "string name,"
247:                    "string version,"
248:                    "uint256 chainId,"
249:                    "address verifyingContract"
250:                ")"
251:            )
252:        );
```

##  y++ costs more gas than ++y for state variables
https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/lib/OrderValidator.sol#L508
```solidity
File: /contracts/lib/OrderValidator.sol
508:                    contractNonce = _contractNonces[offerer]++;
```

```diff
diff --git a/contracts/lib/OrderValidator.sol b/contracts/lib/OrderValidator.sol
index e679e467..a413c152 100644
--- a/contracts/lib/OrderValidator.sol
+++ b/contracts/lib/OrderValidator.sol
@@ -505,7 +505,7 @@ contract OrderValidator is Executor, ZoneInteraction {
                     // and  even if generateOrder's return data does not satisfy
                     // all the constraints. This is the case when errorBuffer
                     // !=0 and revertOnInvalid == false.
-                    contractNonce = _contractNonces[offerer]++;
+                    contractNonce = ++_contractNonces[offerer];
                 }
```