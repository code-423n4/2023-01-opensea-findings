### 1st BUG
Don't Initialize Variables with Default Value

#### Impact
Issue Information: 
Uninitialized variables are assigned with the types default value.

Explicitly initializing a variable with it's default value costs unnecessary gas.

Example
🤦 Bad:

uint256 x = 0;
bool y = false;
🚀 Good:

uint256 x;
bool y;

#### Findings:
```
sea/contracts/lib/BasicOrderFulfiller.sol::939 => uint256 i = 0;
sea/contracts/lib/BasicOrderFulfiller.sol::1079 => for (uint256 i = 0; i < totalAdditionalRecipientsDataSize; ) {
sea/contracts/lib/ConsiderationDecoder.sol::399 => for (uint256 offset = 0; offset < tailOffset; offset += OneWord) {
sea/contracts/lib/ConsiderationDecoder.sol::498 => for (uint256 offset = 0; offset < tailOffset; offset += OneWord) {
sea/contracts/lib/ConsiderationDecoder.sol::538 => for (uint256 offset = 0; offset < tailOffset; offset += OneWord) {
sea/contracts/lib/ConsiderationDecoder.sol::630 => for (uint256 offset = 0; offset < tailOffset; offset += OneWord) {
sea/contracts/lib/ConsiderationDecoder.sol::673 => for (uint256 offset = 0; offset < tailOffset; offset += OneWord) {
sea/contracts/lib/ConsiderationDecoder.sol::744 => for (uint256 offset = 0; offset < tailOffset; offset += OneWord) {
sea/contracts/lib/OrderCombiner.sol::298 => for (uint256 j = 0; j < totalOfferItems; ++j) {
sea/contracts/lib/OrderCombiner.sol::356 => for (uint256 j = 0; j < totalConsiderationItems; ++j) {
sea/contracts/lib/OrderCombiner.sol::567 => for (uint256 i = 0; i < totalOfferFulfillments; ) {
sea/contracts/lib/OrderCombiner.sol::698 => for (uint256 i = 0; i < totalExecutions; ) {
sea/contracts/lib/OrderCombiner.sol::762 => for (uint256 j = 0; j < totalOfferItems; ++j) {
sea/contracts/lib/OrderCombiner.sol::799 => for (uint256 j = 0; j < totalConsiderationItems; ++j) {
sea/contracts/lib/OrderFulfiller.sol::207 => for (uint256 i = 0; i < totalOfferItems; ++i) {
sea/contracts/lib/OrderFulfiller.sol::301 => for (uint256 i = 0; i < totalConsiderationItems; ++i) {
sea/contracts/lib/OrderValidator.sol::549 => for (uint256 i = 0; i < originalOfferLength; ) {
sea/contracts/lib/OrderValidator.sol::591 => for (uint256 i = 0; i < newConsiderationLength; ) {
sea/contracts/lib/TypehashDirectory.sol::48 => for (uint256 i = 0; i < MaxTreeHeight; ) {
```
#### Tools used
Manual VS Code review

### 2nd BUG
Cache Array Length Outside of Loop

#### Impact
Issue Information: 
Caching the array length outside a loop saves reading it on each iteration, as long as the array's length is not changed during the loop.

Example
🤦 Bad:

for (uint256 i = 0; i < array.length; i++) {
    // invariant: array's length is not changed
}
🚀 Good:

uint256 len = array.length
for (uint256 i = 0; i < len; i++) {
    // invariant: array's length is not changed
}

#### Findings:
```
sea/contracts/conduit/Conduit.sol::96 => uint256 totalStandardTransfers = transfers.length;
sea/contracts/conduit/Conduit.sol::159 => uint256 totalStandardTransfers = standardTransfers.length;
sea/contracts/conduit/ConduitController.sol::153 => conduitProperties.channels.length
sea/contracts/conduit/ConduitController.sol::167 => uint256 finalChannelIndex = conduitProperties.channels.length - 1;
sea/contracts/conduit/ConduitController.sol::408 => totalChannels = _conduits[conduit].channels.length;
sea/contracts/conduit/ConduitController.sol::429 => uint256 totalChannels = _conduits[conduit].channels.length;
sea/contracts/conduit/lib/ConduitConstants.sol::10 => uint256 constant ChannelClosed_error_length = 0x24;
sea/contracts/conduit/lib/ConduitConstants.sol::18 => uint256 constant ChannelKey_length = 0x40;
sea/contracts/lib/ConsiderationEncoder.sol::432 => size = ZoneParameters_selectorAndPointer_length + tailOffset;
sea/contracts/lib/ConsiderationEncoder.sol::498 => uint256 offerDataOffset = OrderFulfilled_offer_length_baseOffset +
sea/contracts/lib/ConsiderationEncoder.sol::539 => size = ZoneParameters_basicOrderFixedElements_length + tailOffset;
sea/contracts/lib/ConsiderationEncoder.sol::562 => uint256 length = srcLength.readUint256();
sea/contracts/lib/ConsiderationEncoder.sol::563 => dstLength.write(length);
sea/contracts/lib/ConsiderationEncoder.sol::567 => uint256 headAndTailSize = length * OneWord;
sea/contracts/lib/ConsiderationEncoder.sol::670 => uint256 length = srcLength.readUint256();
sea/contracts/lib/ConsiderationEncoder.sol::671 => dstLength.write(length);
sea/contracts/lib/ConsiderationEncoder.sol::678 => MemoryPointer srcHeadEnd = srcHead.offset(length * OneWord);
sea/contracts/lib/ConsiderationEncoder.sol::692 => size = OneWord + (length * ReceivedItem_size);
sea/contracts/lib/CriteriaResolution.sol::51 => uint256 totalCriteriaResolvers = 
sea/contracts/lib/CriteriaResolution.sol::54 => uint256 totalAdvancedOrders = advancedOrders.length;
sea/contracts/lib/CriteriaResolution.sol::124 => if (componentIndex >= items.length) {
sea/contracts/lib/CriteriaResolution.sol::156 => uint256 totalItems = orderParameters.consideration.length;
sea/contracts/lib/CriteriaResolution.sol::171 => totalItems = orderParameters.offer.length;
sea/contracts/lib/CriteriaResolution.sol::219 => } else if (criteriaResolver.criteriaProof.length != 0) {
sea/contracts/lib/FulfillmentApplier.sol::56 => offerComponents.length == 0 || considerationComponents.length == 0
sea/contracts/lib/FulfillmentApplier.sol::177 => if (fulfillmentComponents.length == 0) {
sea/contracts/lib/GettersAndDerivers.sol::331 => return(information_version_offset, information_length)
sea/contracts/lib/OrderCombiner.sol::214 => uint256 totalOrders = advancedOrders.length;
sea/contracts/lib/OrderCombiner.sol::284 => uint256 totalOfferItems = offer.length;
sea/contracts/lib/OrderCombiner.sol::353 => uint256 totalConsiderationItems = consideration.length;
sea/contracts/lib/OrderCombiner.sol::549 => uint256 totalOfferFulfillments = offerFulfillments.length;
sea/contracts/lib/OrderCombiner.sol::553 => considerationFulfillments.length
sea/contracts/lib/OrderCombiner.sol::639 => if (executions.length == 0) {
sea/contracts/lib/OrderCombiner.sol::682 => uint256 totalOrders = advancedOrders.length;
sea/contracts/lib/OrderCombiner.sol::695 => uint256 totalExecutions = executions.length;
sea/contracts/lib/OrderCombiner.sol::759 => uint256 totalOfferItems = offer.length;
sea/contracts/lib/OrderCombiner.sol::988 => uint256 totalFulfillments = fulfillments.length;
sea/contracts/lib/OrderFulfiller.sol::199 => uint256 totalOfferItems = orderParameters.offer.length;
sea/contracts/lib/OrderValidator.sol::343 => revert(Error_selector_offset, Panic_error_length)
sea/contracts/lib/OrderValidator.sol::483 => orderParameters.consideration.length !=
sea/contracts/lib/OrderValidator.sol::540 => uint256 originalOfferLength = orderParameters.offer.length;
sea/contracts/lib/OrderValidator.sol::541 => uint256 newOfferLength = offer.length;
sea/contracts/lib/OrderValidator.sol::583 => uint256 newConsiderationLength = consideration.length;
sea/contracts/lib/OrderValidator.sol::586 => if (newConsiderationLength > originalConsiderationArray.length) {
sea/contracts/lib/OrderValidator.sol::664 => uint256 totalOrders = orders.length;
sea/contracts/lib/OrderValidator.sol::750 => uint256 totalOrders = orders.length;
sea/contracts/lib/OrderValidator.sol::789 => orderParameters.consideration.length !=
sea/contracts/lib/TokenTransferrer.sol::718 => add(elementPtr, ConduitBatch1155Transfer_ids_length_offset),
sea/contracts/lib/TokenTransferrerConstants.sol::62 => uint256 constant ERC20_transferFrom_length = 0x64; // 4 + 32 * 3 == 100
sea/contracts/lib/TokenTransferrerConstants.sol::76 => uint256 constant ERC1155_safeTransferFrom_data_length_ptr = 0xa4;
sea/contracts/lib/TokenTransferrerConstants.sol::77 => uint256 constant ERC1155_safeTransferFrom_length = 0xc4; // 4 + 32 * 6 == 196
sea/contracts/lib/TokenTransferrerConstants.sol::78 => uint256 constant ERC1155_safeTransferFrom_data_length_offset = 0xa0;
sea/contracts/lib/TokenTransferrerConstants.sol::96 => uint256 constant ERC721_transferFrom_length = 0x64; // 4 + 32 * 3 == 100
sea/contracts/lib/TokenTransferrerConstants.sol::108 => uint256 constant NoContract_error_length = 0x24;
sea/contracts/lib/TokenTransferrerConstants.sol::129 => uint256 constant TokenTransferGenericFailure_error_length = 0xa4;
sea/contracts/lib/TokenTransferrerConstants.sol::141 => uint256 constant BatchTransfer1155Params_data_length_basePtr = 0xc4;
sea/contracts/lib/TokenTransferrerConstants.sol::144 => uint256 constant BatchTransfer1155Params_ids_length_ptr = 0xc4;
sea/contracts/lib/TokenTransferrerConstants.sol::146 => uint256 constant BatchTransfer1155Params_ids_length_offset = 0xa0;
sea/contracts/lib/TokenTransferrerConstants.sol::147 => uint256 constant BatchTransfer1155Params_amounts_length_baseOffset = 0xc0;
sea/contracts/lib/TokenTransferrerConstants.sol::148 => uint256 constant BatchTransfer1155Params_data_length_baseOffset = 0xe0;
sea/contracts/lib/TokenTransferrerConstants.sol::155 => uint256 constant ConduitBatch1155Transfer_ids_length_offset = 0xa0;
sea/contracts/lib/TokenTransferrerConstants.sol::156 => uint256 constant ConduitBatch1155Transfer_amounts_length_baseOffset = 0xc0;
sea/contracts/lib/TokenTransferrerConstants.sol::163 => uint256 constant Invalid1155BatchTransferEncoding_length = 0x04;
sea/contracts/lib/TokenTransferrerConstants.sol::190 => uint256 constant BadReturnValueFromERC20OnTransfer_error_length = 0x84;
```
#### Tools used
Manual VS Code review

### 3rd BUG
Use immutable for OpenZeppelin AccessControl's Roles Declarations

#### Impact
Issue Information: 
⚡️ Only valid for solidity versions <0.6.12 ⚡️

Access roles marked as constant results in computing the keccak256 operation each time the variable is used because assigned operations for constant variables are re-evaluated every time.

Changing the variables to immutable results in computing the hash only once on deployment, leading to gas savings.

Example
🤦 Bad:

bytes32 public constant GOVERNOR_ROLE = keccak256("GOVERNOR_ROLE");
🚀 Good:

bytes32 public immutable GOVERNOR_ROLE = keccak256("GOVERNOR_ROLE");

#### Findings:
```
sea/contracts/conduit/Conduit.sol::52 => sload(keccak256(ChannelKey_channel_ptr, ChannelKey_length))
sea/contracts/conduit/ConduitController.sol::33 => _CONDUIT_CREATION_CODE_HASH = keccak256(type(Conduit).creationCode);
sea/contracts/lib/BasicOrderFulfiller.sol::701 => mstore(BasicOrder_order_offerHashes_ptr, keccak256(0, OneWord))
sea/contracts/lib/BasicOrderFulfiller.sol::797 => orderHash := keccak256(
sea/contracts/lib/ConsiderationBase.sol::116 => domainSeparator := keccak256(0, EIP712_domainData_size)
sea/contracts/lib/ConsiderationBase.sol::193 => nameHash = keccak256(bytes(_nameString()));
sea/contracts/lib/ConsiderationBase.sol::196 => versionHash = keccak256(bytes("1.2"));
sea/contracts/lib/ConsiderationBase.sol::243 => eip712DomainTypehash = keccak256(
sea/contracts/lib/ConsiderationBase.sol::255 => offerItemTypehash = keccak256(offerItemTypeString);
sea/contracts/lib/ConsiderationBase.sol::258 => considerationItemTypehash = keccak256(considerationItemTypeString);
sea/contracts/lib/ConsiderationBase.sol::267 => orderTypehash = keccak256(orderTypeString);
sea/contracts/lib/CounterManager.sol::53 => let storagePointer := keccak256(0, TwoWords)
sea/contracts/lib/CriteriaResolution.sol::279 => let computedHash := keccak256(0, OneWord)
sea/contracts/lib/CriteriaResolution.sol::306 => computedHash := keccak256(0, TwoWords)
sea/contracts/lib/FulfillmentApplier.sol::375 => dataHash := keccak256(
sea/contracts/lib/FulfillmentApplier.sol::419 => keccak256(
sea/contracts/lib/FulfillmentApplier.sol::655 => dataHash := keccak256(
sea/contracts/lib/FulfillmentApplier.sol::684 => keccak256(considerationItemPtr, ReceivedItem_size)
sea/contracts/lib/GettersAndDerivers.sol::94 => mstore(hashArrPtr, keccak256(ptr, EIP712_OfferItem_size))
sea/contracts/lib/GettersAndDerivers.sol::105 => offerHash := keccak256(
sea/contracts/lib/GettersAndDerivers.sol::151 => keccak256(ptr, EIP712_ConsiderationItem_size)
sea/contracts/lib/GettersAndDerivers.sol::163 => considerationHash := keccak256(
sea/contracts/lib/GettersAndDerivers.sol::217 => orderHash := keccak256(typeHashPtr, EIP712_Order_size)
sea/contracts/lib/GettersAndDerivers.sol::272 => keccak256(
sea/contracts/lib/GettersAndDerivers.sol::363 => value := keccak256(0, EIP712_DigestPayload_size)
sea/contracts/lib/TypehashDirectory.sol::66 => bytes32 typeHash = keccak256(bulkOrderTypeString);
sea/contracts/lib/Verifiers.sol::196 => mstore(scratchPtr, keccak256(0, TwoWords))
sea/contracts/lib/Verifiers.sol::201 => root := keccak256(0, TwoWords)
sea/contracts/lib/Verifiers.sol::211 => bulkOrderHash := keccak256(0, TwoWords)
```
#### Tools used
Manual VS Code review

### 4th BUG
Use Shift Right/Left instead of Division/Multiplication if possible

#### Impact
Issue Information: 
A division/multiplication by any number x being a power of 2 can be calculated by shifting log2(x) to the right/left.

While the DIV opcode uses 5 gas, the SHR opcode only uses 3 gas. Furthermore, Solidity's division operation also includes a division-by-0 prevention which is bypassed using shifting.

Example
🤦 Bad:

uint256 b = a / 2;
uint256 c = a / 4;
uint256 d = a * 8;
🚀 Good:

uint256 b = a >> 1;
uint256 c = a >> 2;
uint256 d = a << 3;

#### Findings:
```
sea/contracts/lib/Consideration.sol::278 => bool[] memory /* availableOrders */,
sea/contracts/lib/Consideration.sol::412 => bool[] memory /* availableOrders */,
sea/contracts/lib/ConsiderationConstants.sol::282 => uint256 constant BasicOrder_basicOrderType_range = 0x18; // 24 values
sea/contracts/lib/ConsiderationConstants.sol::462 => uint256 constant IsValidOrder_length = 0x84; // 4 + 32 * 4 == 132
sea/contracts/lib/OrderCombiner.sol::117 => bool[] memory /* availableOrders */,
sea/contracts/lib/TokenTransferrerConstants.sol::62 => uint256 constant ERC20_transferFrom_length = 0x64; // 4 + 32 * 3 == 100
sea/contracts/lib/TokenTransferrerConstants.sol::77 => uint256 constant ERC1155_safeTransferFrom_length = 0xc4; // 4 + 32 * 6 == 196
sea/contracts/lib/TokenTransferrerConstants.sol::96 => uint256 constant ERC721_transferFrom_length = 0x64; // 4 + 32 * 3 == 100
```
#### Tools used
Manual VS Code review