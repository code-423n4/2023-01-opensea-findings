
## Summary

### Gas Optimizations
| |Issue|Instances|Total Gas Saved|
|-|:-|:-:|:-:|
| [G&#x2011;01] | Structs can be packed into fewer storage slots | 3 |  - |
| [G&#x2011;02] | Using `storage` instead of `memory` for structs/arrays saves gas | 9 |  37800 |
| [G&#x2011;03] | `internal` functions only called once can be inlined to save gas | 26 |  520 |
| [G&#x2011;04] | Add `unchecked {}` for subtractions where the operands cannot underflow because of a previous `require()` or `if`-statement | 1 |  85 |
| [G&#x2011;05] | Optimize names to save gas | 5 |  110 |
| [G&#x2011;06] | `internal` functions not called by the contract should be removed to save deployment gas | 8 |  - |
| [G&#x2011;07] | `++i` costs less gas than `i++`, especially when it's used in `for`-loops (`--i`/`i--` too) | 1 |  5 |
| [G&#x2011;08] | Functions guaranteed to revert when called by normal users can be marked `payable` | 3 |  63 |

Total: 56 instances over 8 issues with **38583 gas** saved

Gas totals use lower bounds of ranges and count two iterations of each `for`-loop. All values above are runtime, not deployment, values; deployment values are listed in the individual issue descriptions. The table above as well as its gas numbers do not include any of the excluded findings.





## Gas Optimizations

### [G&#x2011;01]  Structs can be packed into fewer storage slots
Each slot saved can avoid an extra Gsset (**20000 gas**) for the first setting of the struct. Subsequent reads as well as writes have smaller gas savings

*There are 3 instances of this issue:*

```solidity
File: contracts/lib/ConsiderationStructs.sol

/// @audit Variable ordering with 10 slots instead of the current 11:
///           user-defined[](32):offer, user-defined[](32):consideration, uint256(32):startTime, uint256(32):endTime, bytes32(32):zoneHash, uint256(32):salt, bytes32(32):conduitKey, uint256(32):counter, address(20):offerer, uint8(1):orderType, address(20):zone
26    struct OrderComponents {
27        address offerer;
28        address zone;
29        OfferItem[] offer;
30        ConsiderationItem[] consideration;
31        OrderType orderType;
32        uint256 startTime;
33        uint256 endTime;
34        bytes32 zoneHash;
35        uint256 salt;
36        bytes32 conduitKey;
37        uint256 counter;
38:   }

/// @audit Variable ordering with 17 slots instead of the current 18:
///           uint256(32):considerationIdentifier, uint256(32):considerationAmount, uint256(32):offerIdentifier, uint256(32):offerAmount, uint256(32):startTime, uint256(32):endTime, bytes32(32):zoneHash, uint256(32):salt, bytes32(32):offererConduitKey, bytes32(32):fulfillerConduitKey, uint256(32):totalOriginalAdditionalRecipients, user-defined[](32):additionalRecipients, bytes(32):signature, address(20):considerationToken, uint8(1):basicOrderType, address(20):offerer, address(20):zone, address(20):offerToken
104   struct BasicOrderParameters {
105       // calldata offset
106       address considerationToken; // 0x24
107       uint256 considerationIdentifier; // 0x44
108       uint256 considerationAmount; // 0x64
109       address payable offerer; // 0x84
110       address zone; // 0xa4
111       address offerToken; // 0xc4
112       uint256 offerIdentifier; // 0xe4
113       uint256 offerAmount; // 0x104
114       BasicOrderType basicOrderType; // 0x124
115       uint256 startTime; // 0x144
116       uint256 endTime; // 0x164
117       bytes32 zoneHash; // 0x184
118       uint256 salt; // 0x1a4
119       bytes32 offererConduitKey; // 0x1c4
120       bytes32 fulfillerConduitKey; // 0x1e4
121       uint256 totalOriginalAdditionalRecipients; // 0x204
122       AdditionalRecipient[] additionalRecipients; // 0x224
123       bytes signature; // 0x244
124       // Total length, excluding dynamic array data: 0x264 (580)
125:  }

/// @audit Variable ordering with 10 slots instead of the current 11:
///           user-defined[](32):offer, user-defined[](32):consideration, uint256(32):startTime, uint256(32):endTime, bytes32(32):zoneHash, uint256(32):salt, bytes32(32):conduitKey, uint256(32):totalOriginalConsiderationItems, address(20):offerer, uint8(1):orderType, address(20):zone
143   struct OrderParameters {
144       address offerer; // 0x00
145       address zone; // 0x20
146       OfferItem[] offer; // 0x40
147       ConsiderationItem[] consideration; // 0x60
148       OrderType orderType; // 0x80
149       uint256 startTime; // 0xa0
150       uint256 endTime; // 0xc0
151       bytes32 zoneHash; // 0xe0
152       uint256 salt; // 0x100
153       bytes32 conduitKey; // 0x120
154       uint256 totalOriginalConsiderationItems; // 0x140
155       // offer.length                          // 0x160
156:  }

```
https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/lib/ConsiderationStructs.sol#L26-L38

### [G&#x2011;02]  Using `storage` instead of `memory` for structs/arrays saves gas
When fetching data from a storage location, assigning the data to a `memory` variable causes all fields of the struct/array to be read from storage, which incurs a Gcoldsload (**2100 gas**) for *each* field of the struct/array. If the fields are read from the new memory variable, they incur an additional `MLOAD` rather than a cheap stack read. Instead of declearing the variable with the `memory` keyword, declaring the variable with the `storage` keyword and caching any fields that need to be re-read in stack variables, will be much cheaper, only incuring the Gcoldsload for the fields actually read. The only time it makes sense to read the whole struct/array into a `memory` variable, is if the full struct/array is being returned by the function, is being passed to a function that requires `memory`, or if the array/struct is being read from another `memory` array/struct

*There are 9 instances of this issue:*

```solidity
File: contracts/lib/CriteriaResolution.sol

91:                       OfferItem[] memory items = orderParameters.offer;

```
https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/lib/CriteriaResolution.sol#L91

```solidity
File: contracts/lib/FulfillmentApplier.sol

72:           ReceivedItem memory considerationItem = considerationExecution.item;

```
https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/lib/FulfillmentApplier.sol#L72

```solidity
File: contracts/lib/OrderCombiner.sol

300:                      OfferItem memory offerItem = offer[j];

701:              ReceivedItem memory item = execution.item;

752:                  OrderParameters memory parameters = advancedOrder.parameters;

756:                      OfferItem[] memory offer = parameters.offer;

763:                          OfferItem memory offerItem = offer[j];

```
https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/lib/OrderCombiner.sol#L300

```solidity
File: contracts/lib/OrderFulfiller.sol

104:          OrderParameters memory orderParameters = advancedOrders[0].parameters;

```
https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/lib/OrderFulfiller.sol#L104

```solidity
File: contracts/lib/OrderValidator.sol

758:                  OrderParameters memory orderParameters = order.parameters;

```
https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/lib/OrderValidator.sol#L758

### [G&#x2011;03]  `internal` functions only called once can be inlined to save gas
Not inlining costs **20 to 40 gas** because of two extra `JUMP` instructions and additional stack operations needed for function calls.

*There are 26 instances of this issue:*

```solidity
File: contracts/lib/BasicOrderFulfiller.sol

304       function _prepareBasicFulfillmentFromCalldata(
305           BasicOrderParameters calldata parameters,
306           OrderType orderType,
307           ItemType receivedItemType,
308           ItemType additionalRecipientsItemType,
309           address additionalRecipientsToken,
310           ItemType offeredItemType
311:      ) internal returns (bytes32 orderHash) {

916       function _transferNativeTokensAndFinalize(
917           uint256 amount,
918:          address payable to

1006      function _transferERC20AndFinalize(
1007          address offerer,
1008          BasicOrderParameters calldata parameters,
1009          bool fromOfferer,
1010:         bytes memory accumulator

```
https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/lib/BasicOrderFulfiller.sol#L304-L311

```solidity
File: contracts/lib/ConsiderationBase.sol

180       function _deriveTypehashes()
181           internal
182           pure
183           returns (
184               bytes32 nameHash,
185               bytes32 versionHash,
186               bytes32 eip712DomainTypehash,
187               bytes32 offerItemTypehash,
188               bytes32 considerationItemTypehash,
189:              bytes32 orderTypehash

```
https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/lib/ConsiderationBase.sol#L180-L189

```solidity
File: contracts/lib/ConsiderationDecoder.sol

233       function _decodeOrderParameters(
234           CalldataPointer cdPtr
235:      ) internal pure returns (MemoryPointer mPtr) {

252       function _decodeOrder(
253           CalldataPointer cdPtr
254:      ) internal pure returns (MemoryPointer mPtr) {

278       function _decodeAdvancedOrder(
279           CalldataPointer cdPtr
280:      ) internal pure returns (MemoryPointer mPtr) {

319       function _getEmptyBytesOrArray()
320           internal
321           pure
322:          returns (MemoryPointer mPtr)

336       function _decodeOrderAsAdvancedOrder(
337           CalldataPointer cdPtr
338:      ) internal pure returns (MemoryPointer mPtr) {

419       function _decodeCriteriaProof(
420           CalldataPointer cdPtrLength
421:      ) internal pure returns (MemoryPointer mPtrLength) {

445       function _decodeCriteriaResolver(
446           CalldataPointer cdPtr
447:      ) internal pure returns (MemoryPointer mPtr) {

691       function _decodeFulfillment(
692           CalldataPointer cdPtr
693:      ) internal pure returns (MemoryPointer mPtr) {

```
https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/lib/ConsiderationDecoder.sol#L233-L235

```solidity
File: contracts/lib/CriteriaResolution.sol

193       function _updateCriteriaItem(
194           OfferItem[] memory offer,
195           uint256 componentIndex,
196:          CriteriaResolver memory criteriaResolver

265       function _verifyProof(
266           uint256 leaf,
267           uint256 root,
268:          bytes32[] memory proof

```
https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/lib/CriteriaResolution.sol#L193-L196

```solidity
File: contracts/lib/Executor.sol

479:      function _trigger(bytes32 conduitKey, bytes memory accumulator) internal {

```
https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/lib/Executor.sol#L479

```solidity
File: contracts/lib/OrderCombiner.sol

537       function _executeAvailableFulfillments(
538           AdvancedOrder[] memory advancedOrders,
539           FulfillmentComponent[][] memory offerFulfillments,
540           FulfillmentComponent[][] memory considerationFulfillments,
541           bytes32 fulfillerConduitKey,
542           address recipient,
543           bytes32[] memory orderHashes
544       )
545           internal
546:          returns (bool[] memory availableOrders, Execution[] memory executions)

867:      function _emitOrdersMatched(bytes32[] memory orderHashes) internal {

981       function _fulfillAdvancedOrders(
982           AdvancedOrder[] memory advancedOrders,
983           Fulfillment[] memory fulfillments,
984           bytes32[] memory orderHashes,
985           address recipient
986:      ) internal returns (Execution[] memory executions) {

```
https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/lib/OrderCombiner.sol#L537-L546

```solidity
File: contracts/lib/OrderFulfiller.sol

158       function _applyFractionsAndTransferEach(
159           OrderParameters memory orderParameters,
160           uint256 numerator,
161           uint256 denominator,
162           bytes32 fulfillerConduitKey,
163:          address recipient

```
https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/lib/OrderFulfiller.sol#L158-L163

```solidity
File: contracts/lib/OrderValidator.sol

439       function _checkRecipients(
440           address originalRecipient,
441           address newRecipient
442:      ) internal pure returns (uint256 isInvalid) {

472       function _getGeneratedOrder(
473           OrderParameters memory orderParameters,
474           bytes memory context,
475           bool revertOnInvalid
476       )
477           internal
478:          returns (bytes32 orderHash, uint256 numerator, uint256 denominator)

890       function _doesNotSupportPartialFills(
891           OrderType orderType,
892           uint256 numerator,
893           uint256 denominator
894:      ) internal pure returns (bool isFullOrder) {

```
https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/lib/OrderValidator.sol#L439-L442

```solidity
File: contracts/lib/TypehashDirectory.sol

99        function getMaxTreeBrackets(
100           uint256 maxHeight
101:      ) internal pure returns (bytes memory) {

131:      function getTreeSubTypes() internal pure returns (bytes memory) {

```
https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/lib/TypehashDirectory.sol#L99-L101

```solidity
File: contracts/lib/Verifiers.sol

117       function _isValidBulkOrderSize(
118           uint256 signatureLength
119:      ) internal pure returns (bool validLength) {

150       function _computeBulkOrderProof(
151           bytes memory proofAndSignature,
152           bytes32 leaf
153:      ) internal view returns (bytes32 bulkOrderHash) {

```
https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/lib/Verifiers.sol#L117-L119

### [G&#x2011;04]  Add `unchecked {}` for subtractions where the operands cannot underflow because of a previous `require()` or `if`-statement
`require(a <= b); x = b - a` => `require(a <= b); unchecked { x = b - a }`

*There is 1 instance of this issue:*

```solidity
File: contracts/lib/BasicOrderFulfiller.sol

/// @audit if-condition on line 981
987:                      nativeTokensRemaining - amount

```
https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/lib/BasicOrderFulfiller.sol#L987

### [G&#x2011;05]  Optimize names to save gas
`public`/`external` function names and `public` member variable names can be optimized to save gas. See [this](https://gist.github.com/IllIllI000/a5d8b486a8259f9f77891a919febd1a9) link for an example of how it works. Below are the interfaces/abstract contracts that can be optimized so that the most frequently-called functions use the least amount of gas possible during method lookup. Method IDs that have two leading zero bytes can save **128 gas** each during deployment, and renaming functions to have lower method IDs will save **22 gas** per call, [per sorted position shifted](https://medium.com/joyso/solidity-how-does-function-name-affect-gas-consumption-in-smart-contract-47d270d8ac92)

*There are 5 instances of this issue:*

```solidity
File: contracts/interfaces/ConduitInterface.sol

/// @audit execute(), executeBatch1155(), executeWithBatch1155(), updateChannel()
15:   interface ConduitInterface {

```
https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/interfaces/ConduitInterface.sol#L15

```solidity
File: contracts/interfaces/ConsiderationInterface.sol

/// @audit fulfillBasicOrder(), fulfillOrder(), fulfillAdvancedOrder(), fulfillAvailableOrders(), fulfillAvailableAdvancedOrders(), matchOrders(), matchAdvancedOrders(), cancel(), validate(), incrementCounter(), getOrderHash(), getOrderStatus(), getCounter(), information(), getContractOffererNonce()
27:   interface ConsiderationInterface {

```
https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/interfaces/ConsiderationInterface.sol#L27

```solidity
File: contracts/interfaces/ContractOffererInterface.sol

/// @audit generateOrder(), ratifyOrder(), previewOrder(), getMetadata()
6:    interface ContractOffererInterface {

```
https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/interfaces/ContractOffererInterface.sol#L6

```solidity
File: contracts/interfaces/ImmutableCreate2FactoryInterface.sol

/// @audit safeCreate2(), findCreate2Address(), findCreate2AddressViaHash(), hasBeenDeployed()
18:   interface ImmutableCreate2FactoryInterface {

```
https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/interfaces/ImmutableCreate2FactoryInterface.sol#L18

```solidity
File: contracts/interfaces/SeaportInterface.sol

/// @audit fulfillBasicOrder(), fulfillOrder(), fulfillAdvancedOrder(), fulfillAvailableOrders(), fulfillAvailableAdvancedOrders(), matchOrders(), matchAdvancedOrders(), cancel(), validate(), incrementCounter(), getOrderHash(), getOrderStatus(), getCounter(), information(), getContractOffererNonce()
26:   interface SeaportInterface {

```
https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/interfaces/SeaportInterface.sol#L26

### [G&#x2011;06]  `internal` functions not called by the contract should be removed to save deployment gas
If the functions are required by an interface, the contract should inherit from that interface and use the `override` keyword

*There are 8 instances of this issue:*

```solidity
File: contracts/lib/ConsiderationDecoder.sol

378       function _decodeOrdersAsAdvancedOrders(
379           CalldataPointer cdPtrLength
380:      ) internal pure returns (MemoryPointer mPtrLength) {

477       function _decodeCriteriaResolvers(
478           CalldataPointer cdPtrLength
479:      ) internal pure returns (MemoryPointer mPtrLength) {

517       function _decodeOrders(
518           CalldataPointer cdPtrLength
519:      ) internal pure returns (MemoryPointer mPtrLength) {

609       function _decodeNestedFulfillmentComponents(
610           CalldataPointer cdPtrLength
611:      ) internal pure returns (MemoryPointer mPtrLength) {

652       function _decodeAdvancedOrders(
653           CalldataPointer cdPtrLength
654:      ) internal pure returns (MemoryPointer mPtrLength) {

723       function _decodeFulfillments(
724           CalldataPointer cdPtrLength
725:      ) internal pure returns (MemoryPointer mPtrLength) {

764       function _decodeOrderComponentsAsOrderParameters(
765           CalldataPointer cdPtr
766:      ) internal pure returns (MemoryPointer mPtr) {

804       function _decodeGenerateOrderReturndata()
805           internal
806           pure
807           returns (
808               uint256 invalidEncoding,
809               MemoryPointer offer,
810:              MemoryPointer consideration

```
https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/lib/ConsiderationDecoder.sol#L378-L380

### [G&#x2011;07]  `++i` costs less gas than `i++`, especially when it's used in `for`-loops (`--i`/`i--` too)
Saves **5 gas per loop**

*There is 1 instance of this issue:*

```solidity
File: contracts/lib/OrderCombiner.sol

272:                  maximumFulfilled--;

```
https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/lib/OrderCombiner.sol#L272

### [G&#x2011;08]  Functions guaranteed to revert when called by normal users can be marked `payable`
If a function modifier such as `onlyOwner` is used, the function will revert if a normal user tries to pay the function. Marking the function as `payable` will lower the gas cost for legitimate callers because the compiler will not include checks for whether a payment was provided. The extra opcodes avoided are 
`CALLVALUE`(2),`DUP1`(3),`ISZERO`(3),`PUSH2`(3),`JUMPI`(10),`PUSH1`(3),`DUP1`(3),`REVERT`(0),`JUMPDEST`(1),`POP`(2), which costs an average of about **21 gas per call** to the function, in addition to the extra deployment cost

*There are 3 instances of this issue:*

```solidity
File: contracts/conduit/Conduit.sol

92        function execute(
93            ConduitTransfer[] calldata transfers
94:       ) external override onlyOpenChannel returns (bytes4 magicValue) {

127       function executeBatch1155(
128           ConduitBatch1155Transfer[] calldata batchTransfers
129:      ) external override onlyOpenChannel returns (bytes4 magicValue) {

154       function executeWithBatch1155(
155           ConduitTransfer[] calldata standardTransfers,
156           ConduitBatch1155Transfer[] calldata batchTransfers
157:      ) external override onlyOpenChannel returns (bytes4 magicValue) {

```
https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/conduit/Conduit.sol#L92-L94


___

## Excluded findings
These findings are excluded from awards calculations because there are publicly-available automated tools that find them. The valid ones appear here for completeness

## Summary

### Gas Optimizations
| |Issue|Instances|Total Gas Saved|
|-|:-|:-:|:-:|
| [G&#x2011;01] | Using `bool`s for storage incurs overhead | 1 |  17100 |

Total: 1 instances over 1 issues with **17100 gas** saved

Gas totals use lower bounds of ranges and count two iterations of each `for`-loop. All values above are runtime, not deployment, values; deployment values are listed in the individual issue descriptions. The table above as well as its gas numbers do not include any of the excluded findings.





## Gas Optimizations

### [G&#x2011;01]  Using `bool`s for storage incurs overhead
```solidity
    // Booleans are more expensive than uint256 or any type that takes up a full
    // word because each write operation emits an extra SLOAD to first read the
    // slot's contents, replace the bits taken up by the boolean, and then write
    // back. This is the compiler's defense against contract upgrades and
    // pointer aliasing, and it cannot be disabled.
```
https://github.com/OpenZeppelin/openzeppelin-contracts/blob/58f635312aa21f947cae5f8578638a85aa2519f5/contracts/security/ReentrancyGuard.sol#L23-L27
Use `uint256(1)` and `uint256(2)` for true/false to avoid a Gwarmaccess (**[100 gas](https://gist.github.com/IllIllI000/1b70014db712f8572a72378321250058)**) for the extra SLOAD, and to avoid Gsset (**20000 gas**) when changing from `false` to `true`, after having been `true` in the past

*There is 1 instance of this issue:*

```solidity
File: contracts/conduit/Conduit.sol

/// @audit (valid but excluded finding)
34:       mapping(address => bool) private _channels;

```
https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/conduit/Conduit.sol#L34


