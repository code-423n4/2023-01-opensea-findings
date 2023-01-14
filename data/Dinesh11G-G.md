
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
seaport/contracts/lib/BasicOrderFulfiller.sol::937 => for (uint256 i = 0; i < totalAdditionalRecipients; ++i) {
seaport/contracts/lib/OrderFulfiller.sol::214 => for (uint256 i = 0; i < totalOfferItems; ++i) {
seaport/contracts/lib/OrderFulfiller.sol::306 => for (uint256 i = 0; i < totalConsiderationItems; ++i) {
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
seaport/contracts/conduit/Conduit.sol::52 => sload(keccak256(ChannelKey_channel_ptr, ChannelKey_length))
seaport/contracts/conduit/Conduit.sol::62 => revert(ChannelClosed_error_ptr, ChannelClosed_error_length)
seaport/contracts/conduit/Conduit.sol::99 => uint256 totalStandardTransfers = transfers.length;
seaport/contracts/conduit/Conduit.sol::162 => uint256 totalStandardTransfers = standardTransfers.length;
seaport/contracts/conduit/ConduitController.sol::154 => conduitProperties.channels.length
seaport/contracts/conduit/ConduitController.sol::168 => uint256 finalChannelIndex = conduitProperties.channels.length - 1;
seaport/contracts/conduit/ConduitController.sol::426 => totalChannels = _conduits[conduit].channels.length;
seaport/contracts/conduit/ConduitController.sol::449 => uint256 totalChannels = _conduits[conduit].channels.length;
seaport/contracts/conduit/lib/ConduitConstants.sol::10 => uint256 constant ChannelClosed_error_length = 0x24;
seaport/contracts/lib/BasicOrderFulfiller.sol::334 => parameters.additionalRecipients.length,
seaport/contracts/lib/BasicOrderFulfiller.sol::433 => BasicOrder_additionalRecipients_length_cdPtr
seaport/contracts/lib/BasicOrderFulfiller.sol::599 => BasicOrder_additionalRecipients_length_cdPtr
seaport/contracts/lib/BasicOrderFulfiller.sol::712 => OrderFulfilled_offer_length_baseOffset,
seaport/contracts/lib/BasicOrderFulfiller.sol::715 => BasicOrder_additionalRecipients_length_cdPtr
seaport/contracts/lib/BasicOrderFulfiller.sol::843 => calldataload(BasicOrder_additionalRecipients_length_cdPtr),
seaport/contracts/lib/BasicOrderFulfiller.sol::872 => calldataload(BasicOrder_additionalRecipients_length_cdPtr),
seaport/contracts/lib/BasicOrderFulfiller.sol::932 => uint256 totalAdditionalRecipients = additionalRecipients.length;
seaport/contracts/lib/BasicOrderFulfiller.sol::1054 => parameters.additionalRecipients.length
seaport/contracts/lib/Consideration.sol::504 => order.consideration.length
seaport/contracts/lib/ConsiderationConstants.sol::45 => uint256 constant Version_length = 3;
seaport/contracts/lib/ConsiderationConstants.sol::81 => uint256 constant Panic_error_length = 0x24;
seaport/contracts/lib/ConsiderationConstants.sol::172 => uint256 constant OrderFulfilled_consideration_length_baseOffset = 0x2a0;
seaport/contracts/lib/ConsiderationConstants.sol::173 => uint256 constant OrderFulfilled_offer_length_baseOffset = 0x200;
seaport/contracts/lib/ConsiderationConstants.sol::202 => uint256 constant BasicOrder_additionalRecipients_length_cdPtr = 0x264;
seaport/contracts/lib/ConsiderationConstants.sol::303 => uint256 constant NoContract_error_length = 0x24; // 4 + 32 == 36
seaport/contracts/lib/ConsiderationConstants.sol::314 => uint256 constant Create2AddressDerivation_length = 0x55;
seaport/contracts/lib/ConsiderationConstants.sol::336 => uint256 constant Conduit_execute_ConduitTransfer_length = 0x01;
seaport/contracts/lib/ConsiderationConstants.sol::339 => uint256 constant Conduit_execute_ConduitTransfer_length_ptr = 0x24;
seaport/contracts/lib/ConsiderationConstants.sol::355 => uint256 constant Accumulator_array_length_ptr = 0x64;
seaport/contracts/lib/ConsiderationConstants.sol::384 => uint256 constant BadSignatureV_error_length = 0x24;
seaport/contracts/lib/ConsiderationConstants.sol::390 => uint256 constant InvalidSigner_error_length = 0x04;
seaport/contracts/lib/ConsiderationConstants.sol::396 => uint256 constant InvalidSignature_error_length = 0x04;
seaport/contracts/lib/ConsiderationConstants.sol::402 => uint256 constant BadContractSignature_error_length = 0x04;
seaport/contracts/lib/CriteriaResolution.sol::48 => uint256 totalCriteriaResolvers = criteriaResolvers.length;
seaport/contracts/lib/CriteriaResolution.sol::51 => uint256 totalAdvancedOrders = advancedOrders.length;
seaport/contracts/lib/CriteriaResolution.sol::91 => if (componentIndex >= offer.length) {
seaport/contracts/lib/CriteriaResolution.sol::121 => if (componentIndex >= consideration.length) {
seaport/contracts/lib/CriteriaResolution.sol::183 => uint256 totalItems = orderParameters.consideration.length;
seaport/contracts/lib/CriteriaResolution.sol::198 => totalItems = orderParameters.offer.length;
seaport/contracts/lib/Executor.sol::158 => Conduit_execute_ConduitTransfer_length_ptr
seaport/contracts/lib/Executor.sol::160 => Conduit_execute_ConduitTransfer_length
seaport/contracts/lib/Executor.sol::438 => if (accumulator.length != AccumulatorArmed) {
seaport/contracts/lib/Executor.sol::476 => mload(add(accumulator, Accumulator_array_length_ptr)),
seaport/contracts/lib/Executor.sol::603 => if (accumulator.length == AccumulatorDisarmed) {
seaport/contracts/lib/Executor.sol::614 => mstore(add(accumulator, Accumulator_array_length_ptr), elements)
seaport/contracts/lib/Executor.sol::620 => mload(add(accumulator, Accumulator_array_length_ptr)),
seaport/contracts/lib/Executor.sol::623 => mstore(add(accumulator, Accumulator_array_length_ptr), elements)
seaport/contracts/lib/FulfillmentApplier.sol::53 => offerComponents.length == 0 || considerationComponents.length == 0
seaport/contracts/lib/FulfillmentApplier.sol::166 => if (fulfillmentComponents.length == 0) {
seaport/contracts/lib/FulfillmentApplier.sol::242 => revert(0, Panic_error_length)
seaport/contracts/lib/FulfillmentApplier.sol::534 => revert(0, Panic_error_length)
seaport/contracts/lib/GettersAndDerivers.sol::278 => Create2AddressDerivation_length
seaport/contracts/lib/GettersAndDerivers.sol::328 => version = new string(Version_length);
seaport/contracts/lib/OrderCombiner.sol::172 => uint256 totalOrders = advancedOrders.length;
seaport/contracts/lib/OrderCombiner.sol::273 => uint256 totalOfferItems = offer.length;
seaport/contracts/lib/OrderCombiner.sol::328 => uint256 totalConsiderationItems = consideration.length;
seaport/contracts/lib/OrderCombiner.sol::496 => uint256 totalOfferFulfillments = offerFulfillments.length;
seaport/contracts/lib/OrderCombiner.sol::500 => considerationFulfillments.length
seaport/contracts/lib/OrderCombiner.sol::580 => if (executions.length == 0) {
seaport/contracts/lib/OrderCombiner.sol::612 => uint256 totalOrders = advancedOrders.length;
seaport/contracts/lib/OrderCombiner.sol::641 => uint256 totalConsiderationItems = consideration.length;
seaport/contracts/lib/OrderCombiner.sol::667 => uint256 totalExecutions = executions.length;
seaport/contracts/lib/OrderCombiner.sol::763 => advancedOrders.length,
seaport/contracts/lib/OrderCombiner.sol::793 => uint256 totalFulfillments = fulfillments.length;
seaport/contracts/lib/OrderFulfiller.sol::210 => uint256 totalOfferItems = orderParameters.offer.length;
seaport/contracts/lib/OrderFulfiller.sol::455 => uint256 totalOrders = orders.length;
seaport/contracts/lib/OrderValidator.sol::271 => revert(0, Panic_error_length)
seaport/contracts/lib/OrderValidator.sol::321 => uint256 totalOrders = orders.length;
seaport/contracts/lib/OrderValidator.sol::349 => order.consideration.length
seaport/contracts/lib/OrderValidator.sol::403 => uint256 totalOrders = orders.length;
seaport/contracts/lib/SignatureVerification.sol::207 => revert(0, BadContractSignature_error_length)
seaport/contracts/lib/SignatureVerification.sol::210 => // Check if signature length was invalid.
seaport/contracts/lib/SignatureVerification.sol::214 => revert(0, InvalidSignature_error_length)
seaport/contracts/lib/SignatureVerification.sol::224 => revert(0, BadSignatureV_error_length)
seaport/contracts/lib/SignatureVerification.sol::229 => revert(0, InvalidSigner_error_length)
seaport/contracts/lib/SignatureVerification.sol::249 => revert(0, BadContractSignature_error_length)
seaport/contracts/lib/TokenTransferrer.sol::64 => ERC20_transferFrom_length,
seaport/contracts/lib/TokenTransferrer.sol::177 => TokenTransferGenericFailure_error_length
seaport/contracts/lib/TokenTransferrer.sol::205 => BadReturnValueFromERC20OnTransfer_error_length
seaport/contracts/lib/TokenTransferrer.sol::212 => revert(NoContract_error_sig_ptr, NoContract_error_length)
seaport/contracts/lib/TokenTransferrer.sol::252 => revert(NoContract_error_sig_ptr, NoContract_error_length)
seaport/contracts/lib/TokenTransferrer.sol::271 => ERC721_transferFrom_length,
seaport/contracts/lib/TokenTransferrer.sol::342 => TokenTransferGenericFailure_error_length
seaport/contracts/lib/TokenTransferrer.sol::380 => revert(NoContract_error_sig_ptr, NoContract_error_length)
seaport/contracts/lib/TokenTransferrer.sol::401 => ERC1155_safeTransferFrom_data_length_offset
seaport/contracts/lib/TokenTransferrer.sol::403 => mstore(ERC1155_safeTransferFrom_data_length_ptr, 0)
seaport/contracts/lib/TokenTransferrer.sol::411 => ERC1155_safeTransferFrom_length,
seaport/contracts/lib/TokenTransferrer.sol::482 => TokenTransferGenericFailure_error_length
seaport/contracts/lib/TokenTransferrer.sol::518 => let len := batchTransfers.length
seaport/contracts/lib/TokenTransferrer.sol::557 => revert(NoContract_error_sig_ptr, NoContract_error_length)
seaport/contracts/lib/TokenTransferrer.sol::562 => add(elementPtr, ConduitBatch1155Transfer_ids_length_offset)
seaport/contracts/lib/TokenTransferrer.sol::567 => ConduitBatch1155Transfer_amounts_length_baseOffset,
seaport/contracts/lib/TokenTransferrer.sol::588 => ConduitBatch1155Transfer_ids_length_offset
seaport/contracts/lib/TokenTransferrer.sol::612 => Invalid1155BatchTransferEncoding_length
seaport/contracts/lib/TokenTransferrer.sol::634 => BatchTransfer1155Params_ids_length_offset,
seaport/contracts/lib/TokenTransferrer.sol::642 => BatchTransfer1155Params_data_length_basePtr,
seaport/contracts/lib/TokenTransferrer.sol::656 => BatchTransfer1155Params_ids_length_ptr,
seaport/contracts/lib/TokenTransferrer.sol::657 => add(elementPtr, ConduitBatch1155Transfer_ids_length_offset),
seaport/contracts/lib/TokenTransferrerConstants.sol::57 => uint256 constant ERC20_transferFrom_length = 0x64; // 4 + 32 * 3 == 100
seaport/contracts/lib/TokenTransferrerConstants.sol::71 => uint256 constant ERC1155_safeTransferFrom_data_length_ptr = 0xa4;
seaport/contracts/lib/TokenTransferrerConstants.sol::72 => uint256 constant ERC1155_safeTransferFrom_length = 0xc4; // 4 + 32 * 6 == 196
seaport/contracts/lib/TokenTransferrerConstants.sol::73 => uint256 constant ERC1155_safeTransferFrom_data_length_offset = 0xa0;
seaport/contracts/lib/TokenTransferrerConstants.sol::91 => uint256 constant ERC721_transferFrom_length = 0x64; // 4 + 32 * 3 == 100
seaport/contracts/lib/TokenTransferrerConstants.sol::99 => uint256 constant NoContract_error_length = 0x24; // 4 + 32 == 36
seaport/contracts/lib/TokenTransferrerConstants.sol::115 => uint256 constant TokenTransferGenericFailure_error_length = 0xa4;
seaport/contracts/lib/TokenTransferrerConstants.sol::130 => uint256 constant BadReturnValueFromERC20OnTransfer_error_length = 0x84;
seaport/contracts/lib/TokenTransferrerConstants.sol::142 => uint256 constant BatchTransfer1155Params_data_length_basePtr = 0xc4;
seaport/contracts/lib/TokenTransferrerConstants.sol::145 => uint256 constant BatchTransfer1155Params_ids_length_ptr = 0xc4;
seaport/contracts/lib/TokenTransferrerConstants.sol::147 => uint256 constant BatchTransfer1155Params_ids_length_offset = 0xa0;
seaport/contracts/lib/TokenTransferrerConstants.sol::148 => uint256 constant BatchTransfer1155Params_amounts_length_baseOffset = 0xc0;
seaport/contracts/lib/TokenTransferrerConstants.sol::149 => uint256 constant BatchTransfer1155Params_data_length_baseOffset = 0xe0;
seaport/contracts/lib/TokenTransferrerConstants.sol::156 => uint256 constant ConduitBatch1155Transfer_ids_length_offset = 0xa0;
seaport/contracts/lib/TokenTransferrerConstants.sol::157 => uint256 constant ConduitBatch1155Transfer_amounts_length_baseOffset = 0xc0;
seaport/contracts/lib/TokenTransferrerConstants.sol::164 => uint256 constant Invalid1155BatchTransferEncoding_length = 0x04;
seaport/contracts/lib/ZoneInteraction.sol::118 => advancedOrder.extraData.length == 0 &&
seaport/contracts/lib/ZoneInteraction.sol::119 => criteriaResolvers.length == 0
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
seaport/contracts/conduit/Conduit.sol::52 => sload(keccak256(ChannelKey_channel_ptr, ChannelKey_length))
seaport/contracts/conduit/ConduitController.sol::33 => _CONDUIT_CREATION_CODE_HASH = keccak256(type(Conduit).creationCode);
seaport/contracts/lib/BasicOrderFulfiller.sol::403 => keccak256(
seaport/contracts/lib/BasicOrderFulfiller.sol::533 => keccak256(
seaport/contracts/lib/BasicOrderFulfiller.sol::584 => keccak256(
seaport/contracts/lib/BasicOrderFulfiller.sol::695 => keccak256(
seaport/contracts/lib/BasicOrderFulfiller.sol::706 => mstore(BasicOrder_order_offerHashes_ptr, keccak256(0, OneWord))
seaport/contracts/lib/BasicOrderFulfiller.sol::802 => orderHash := keccak256(
seaport/contracts/lib/ConsiderationBase.sol::75 => return keccak256(
seaport/contracts/lib/ConsiderationBase.sol::150 => nameHash = keccak256(bytes(_nameString()));
seaport/contracts/lib/ConsiderationBase.sol::153 => versionHash = keccak256(bytes("1.1"));
seaport/contracts/lib/ConsiderationBase.sol::200 => eip712DomainTypehash = keccak256(
seaport/contracts/lib/ConsiderationBase.sol::212 => offerItemTypehash = keccak256(offerItemTypeString);
seaport/contracts/lib/ConsiderationBase.sol::215 => considerationItemTypehash = keccak256(considerationItemTypeString);
seaport/contracts/lib/ConsiderationBase.sol::218 => orderTypehash = keccak256(
seaport/contracts/lib/CriteriaResolution.sol::257 => let computedHash := keccak256(0, OneWord)
seaport/contracts/lib/CriteriaResolution.sol::285 => computedHash := keccak256(0, TwoWords)
seaport/contracts/lib/FulfillmentApplier.sol::339 => let dataHash := keccak256(
seaport/contracts/lib/FulfillmentApplier.sol::464 => keccak256(
seaport/contracts/lib/FulfillmentApplier.sol::635 => let dataHash := keccak256(
seaport/contracts/lib/FulfillmentApplier.sol::747 => keccak256(
seaport/contracts/lib/GettersAndDerivers.sol::94 => mstore(hashArrPtr, keccak256(ptr, EIP712_OfferItem_size))
seaport/contracts/lib/GettersAndDerivers.sol::105 => offerHash := keccak256(
seaport/contracts/lib/GettersAndDerivers.sol::151 => keccak256(ptr, EIP712_ConsiderationItem_size)
seaport/contracts/lib/GettersAndDerivers.sol::163 => considerationHash := keccak256(
seaport/contracts/lib/GettersAndDerivers.sol::217 => orderHash := keccak256(typeHashPtr, EIP712_Order_size)
seaport/contracts/lib/GettersAndDerivers.sol::274 => keccak256(
seaport/contracts/lib/GettersAndDerivers.sol::365 => value := keccak256(0, EIP712_DigestPayload_size)
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
seaport/contracts/lib/ConsiderationConstants.sol::207 => uint256 constant BasicOrder_basicOrderType_range = 0x18; // 24 values
seaport/contracts/lib/ConsiderationConstants.sol::303 => uint256 constant NoContract_error_length = 0x24; // 4 + 32 == 36
seaport/contracts/lib/TokenTransferrerConstants.sol::57 => uint256 constant ERC20_transferFrom_length = 0x64; // 4 + 32 * 3 == 100
seaport/contracts/lib/TokenTransferrerConstants.sol::72 => uint256 constant ERC1155_safeTransferFrom_length = 0xc4; // 4 + 32 * 6 == 196
seaport/contracts/lib/TokenTransferrerConstants.sol::91 => uint256 constant ERC721_transferFrom_length = 0x64; // 4 + 32 * 3 == 100
seaport/contracts/lib/TokenTransferrerConstants.sol::99 => uint256 constant NoContract_error_length = 0x24; // 4 + 32 == 36
```
#### Tools used
Manual VS Code review