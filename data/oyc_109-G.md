## [G-01] Don't Initialize Variables with Default Value

Uninitialized variables are assigned with the types default value. Explicitly initializing a variable with it's default value costs unnecesary gas.

```
seaport/contracts/conduit/Conduit.sol::99 => for (uint256 i = 0; i < totalStandardTransfers; ) {
seaport/contracts/conduit/Conduit.sol::162 => for (uint256 i = 0; i < totalStandardTransfers; ) {
seaport/contracts/lib/BasicOrderFulfiller.sol::939 => uint256 i = 0;
seaport/contracts/lib/BasicOrderFulfiller.sol::1079 => for (uint256 i = 0; i < totalAdditionalRecipientsDataSize; ) {
seaport/contracts/lib/ConsiderationDecoder.sol::399 => for (uint256 offset = 0; offset < tailOffset; offset += OneWord) {
seaport/contracts/lib/ConsiderationDecoder.sol::498 => for (uint256 offset = 0; offset < tailOffset; offset += OneWord) {
seaport/contracts/lib/ConsiderationDecoder.sol::538 => for (uint256 offset = 0; offset < tailOffset; offset += OneWord) {
seaport/contracts/lib/ConsiderationDecoder.sol::630 => for (uint256 offset = 0; offset < tailOffset; offset += OneWord) {
seaport/contracts/lib/ConsiderationDecoder.sol::673 => for (uint256 offset = 0; offset < tailOffset; offset += OneWord) {
seaport/contracts/lib/ConsiderationDecoder.sol::744 => for (uint256 offset = 0; offset < tailOffset; offset += OneWord) {
seaport/contracts/lib/CriteriaResolution.sol::57 => for (uint256 i = 0; i < totalCriteriaResolvers; ++i) {
seaport/contracts/lib/CriteriaResolution.sol::141 => for (uint256 i = 0; i < totalAdvancedOrders; ++i) {
seaport/contracts/lib/CriteriaResolution.sol::159 => for (uint256 j = 0; j < totalItems; ++j) {
seaport/contracts/lib/CriteriaResolution.sol::174 => for (uint256 j = 0; j < totalItems; ++j) {
seaport/contracts/lib/OrderCombiner.sol::298 => for (uint256 j = 0; j < totalOfferItems; ++j) {
seaport/contracts/lib/OrderCombiner.sol::356 => for (uint256 j = 0; j < totalConsiderationItems; ++j) {
seaport/contracts/lib/OrderCombiner.sol::564 => uint256 totalFilteredExecutions = 0;
seaport/contracts/lib/OrderCombiner.sol::567 => for (uint256 i = 0; i < totalOfferFulfillments; ) {
seaport/contracts/lib/OrderCombiner.sol::596 => for (uint256 i = 0; i < totalConsiderationFulfillments; ) {
seaport/contracts/lib/OrderCombiner.sol::698 => for (uint256 i = 0; i < totalExecutions; ) {
seaport/contracts/lib/OrderCombiner.sol::736 => for (uint256 i = 0; i < totalOrders; ++i) {
seaport/contracts/lib/OrderCombiner.sol::762 => for (uint256 j = 0; j < totalOfferItems; ++j) {
seaport/contracts/lib/OrderCombiner.sol::799 => for (uint256 j = 0; j < totalConsiderationItems; ++j) {
seaport/contracts/lib/OrderCombiner.sol::996 => uint256 totalFilteredExecutions = 0;
seaport/contracts/lib/OrderCombiner.sol::999 => for (uint256 i = 0; i < totalFulfillments; ++i) {
seaport/contracts/lib/OrderFulfiller.sol::207 => for (uint256 i = 0; i < totalOfferItems; ++i) {
seaport/contracts/lib/OrderFulfiller.sol::301 => for (uint256 i = 0; i < totalConsiderationItems; ++i) {
seaport/contracts/lib/OrderValidator.sol::549 => for (uint256 i = 0; i < originalOfferLength; ) {
seaport/contracts/lib/OrderValidator.sol::591 => for (uint256 i = 0; i < newConsiderationLength; ) {
seaport/contracts/lib/OrderValidator.sol::667 => for (uint256 i = 0; i < totalOrders; ) {
seaport/contracts/lib/OrderValidator.sol::753 => for (uint256 i = 0; i < totalOrders; ++i) {
seaport/contracts/lib/TypehashDirectory.sol::48 => for (uint256 i = 0; i < MaxTreeHeight; ) {
```

## [G-02] Using private rather than public for constants, saves gas

If needed, the value can be read from the verified contract source code. Savings are due to the compiler not having to create non-payable getter functions for deployment calldata, and not adding another entry to the method ID table

```
seaport/contracts/zones/PausableZoneController.sol::46 => bytes32 public immutable zoneCreationCode;
```

## [G-03] Using bools for storage incurs overhead

Booleans are more expensive than uint256 or any type that takes up a full word because each write operation emits an extra SLOAD to first read the slot's contents, replace the bits taken up by the boolean, and then write back. This is the compiler's defense against contract upgrades and pointer aliasing, and it cannot be disabled.
Use uint256(1) and uint256(2) for true/false instead

```
seaport/contracts/conduit/Conduit.sol::34 => mapping(address => bool) private _channels;
```

## [G-04] ++i/i++ should be unchecked{++i}/unchecked{i++} when it is not possible for them to overflow, for example when used in for- and while-loops

The unchecked keyword is new in solidity version 0.8.0, so this only applies to that version or higher, which these instances are. This saves 30-40 gas per loop

```
seaport/contracts/lib/CriteriaResolution.sol::57 => for (uint256 i = 0; i < totalCriteriaResolvers; ++i) {
seaport/contracts/lib/CriteriaResolution.sol::141 => for (uint256 i = 0; i < totalAdvancedOrders; ++i) {
seaport/contracts/lib/CriteriaResolution.sol::159 => for (uint256 j = 0; j < totalItems; ++j) {
seaport/contracts/lib/CriteriaResolution.sol::174 => for (uint256 j = 0; j < totalItems; ++j) {
seaport/contracts/lib/OrderCombiner.sol::298 => for (uint256 j = 0; j < totalOfferItems; ++j) {
seaport/contracts/lib/OrderCombiner.sol::356 => for (uint256 j = 0; j < totalConsiderationItems; ++j) {
seaport/contracts/lib/OrderCombiner.sol::736 => for (uint256 i = 0; i < totalOrders; ++i) {
seaport/contracts/lib/OrderCombiner.sol::762 => for (uint256 j = 0; j < totalOfferItems; ++j) {
seaport/contracts/lib/OrderCombiner.sol::799 => for (uint256 j = 0; j < totalConsiderationItems; ++j) {
seaport/contracts/lib/OrderCombiner.sol::999 => for (uint256 i = 0; i < totalFulfillments; ++i) {
seaport/contracts/lib/OrderFulfiller.sol::207 => for (uint256 i = 0; i < totalOfferItems; ++i) {
seaport/contracts/lib/OrderFulfiller.sol::301 => for (uint256 i = 0; i < totalConsiderationItems; ++i) {
seaport/contracts/lib/OrderValidator.sol::508 => contractNonce = _contractNonces[offerer]++;
seaport/contracts/lib/OrderValidator.sol::753 => for (uint256 i = 0; i < totalOrders; ++i) {
```

## [G-05] <x> += <y> costs more gas than <x> = <x> + <y> for state variables

use <x> = <x> + <y> or <x> = <x> - <y> instead to save gas

```
seaport/contracts/lib/BasicOrderFulfiller.sol::941 => i += AdditionalRecipient_size
seaport/contracts/lib/BasicOrderFulfiller.sol::965 => nativeTokensRemaining -= additionalRecipientAmount;
seaport/contracts/lib/BasicOrderFulfiller.sol::1097 => amount -= additionalRecipientAmount;
seaport/contracts/lib/BasicOrderFulfiller.sol::1112 => i += AdditionalRecipient_size;
seaport/contracts/lib/ConsiderationEncoder.sol::134 => tailOffset += minimumReceivedSize;
seaport/contracts/lib/ConsiderationEncoder.sol::155 => tailOffset += maximumSpentSize;
seaport/contracts/lib/ConsiderationEncoder.sol::172 => tailOffset += contextSize;
seaport/contracts/lib/ConsiderationEncoder.sol::240 => tailOffset += offerSize;
seaport/contracts/lib/ConsiderationEncoder.sol::259 => tailOffset += considerationSize;
seaport/contracts/lib/ConsiderationEncoder.sol::273 => tailOffset += contextSize;
seaport/contracts/lib/ConsiderationEncoder.sol::287 => tailOffset += orderHashesSize;
seaport/contracts/lib/ConsiderationEncoder.sol::379 => tailOffset += offerSize;
seaport/contracts/lib/ConsiderationEncoder.sol::400 => tailOffset += considerationSize;
seaport/contracts/lib/ConsiderationEncoder.sol::413 => tailOffset += extraDataSize;
seaport/contracts/lib/ConsiderationEncoder.sol::429 => tailOffset += orderHashesSize;
seaport/contracts/lib/ConsiderationEncoder.sol::514 => tailOffset += offerAndConsiderationSize;
seaport/contracts/lib/ConsiderationEncoder.sol::523 => tailOffset += OneWord;
```

## [G-06] Not using the named return variables when a function returns, wastes deployment gas

It is not necessary to have both a named return and a return statement.

```
seaport/contracts/lib/AmountDeriver.sol::44 => ) internal view returns (uint256 amount) {
seaport/contracts/lib/AmountDeriver.sol::113 => ) internal pure returns (uint256 newValue) {
seaport/contracts/lib/FulfillmentApplier.sol::53 => ) internal pure returns (Execution memory execution) {
seaport/contracts/lib/OrderCombiner.sol::677 => ) internal returns (bool[] memory /* availableOrders */) {
seaport/contracts/lib/OrderCombiner.sol::986 => ) internal returns (Execution[] memory executions) {
seaport/contracts/lib/OrderValidator.sol::115 => returns (bytes32 orderHash, uint256 numerator, uint256 denominator)
seaport/contracts/lib/OrderValidator.sol::478 => returns (bytes32 orderHash, uint256 numerator, uint256 denominator)
seaport/contracts/lib/OrderValidator.sol::869 => returns (bytes32 orderHash, uint256 numerator, uint256 denominator)
seaport/contracts/lib/Verifiers.sol::235 => ) internal view returns (bool valid) {
```