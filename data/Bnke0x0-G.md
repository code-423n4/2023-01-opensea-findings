

### [G01] State variables only set in the constructor should be declared `immutable`

#### Impact
Avoids a Gusset (20000 gas)
#### Findings:
```
seaport/contracts/lib/ReentrancyGuard.sol::18 => uint256 private _reentrancyGuard;
```





### [G02] `++i/i++` should be `unchecked{++i}`/`unchecked{++i}` when it is not possible for them to overflow, as is the case when used in `for` and `while` loops


#### Findings:
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
seaport/contracts/lib/OrderValidator.sol::753 => for (uint256 i = 0; i < totalOrders; ++i) {
```


### [G03] Not using the named return variables when a function returns, wastes deployment gas


#### Findings:
```
seaport/contracts/lib/Consideration.sol::711 => return _getOrderStatus(orderHash);
seaport/contracts/lib/OrderValidator.sol::522 => return _revertOrReturnEmpty(revertOnInvalid, orderHash);
seaport/contracts/lib/OrderValidator.sol::535 => return _revertOrReturnEmpty(revertOnInvalid, orderHash);
seaport/contracts/lib/OrderValidator.sol::545 => return _revertOrReturnEmpty(revertOnInvalid, orderHash);
seaport/contracts/lib/OrderValidator.sol::587 => return _revertOrReturnEmpty(revertOnInvalid, orderHash);
seaport/contracts/lib/OrderValidator.sol::630 => return _revertOrReturnEmpty(revertOnInvalid, orderHash);
```



### [G04] It costs more gas to initialize variables to zero than to let the default of zero be applied


#### Findings:
```
seaport/contracts/conduit/Conduit.sol::99 => for (uint256 i = 0; i < totalStandardTransfers; ) {
seaport/contracts/conduit/Conduit.sol::162 => for (uint256 i = 0; i < totalStandardTransfers; ) {
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
seaport/contracts/lib/OrderCombiner.sol::567 => for (uint256 i = 0; i < totalOfferFulfillments; ) {
seaport/contracts/lib/OrderCombiner.sol::596 => for (uint256 i = 0; i < totalConsiderationFulfillments; ) {
seaport/contracts/lib/OrderCombiner.sol::698 => for (uint256 i = 0; i < totalExecutions; ) {
seaport/contracts/lib/OrderCombiner.sol::736 => for (uint256 i = 0; i < totalOrders; ++i) {
seaport/contracts/lib/OrderCombiner.sol::762 => for (uint256 j = 0; j < totalOfferItems; ++j) {
seaport/contracts/lib/OrderCombiner.sol::799 => for (uint256 j = 0; j < totalConsiderationItems; ++j) {
seaport/contracts/lib/OrderCombiner.sol::999 => for (uint256 i = 0; i < totalFulfillments; ++i) {
seaport/contracts/lib/OrderFulfiller.sol::207 => for (uint256 i = 0; i < totalOfferItems; ++i) {
seaport/contracts/lib/OrderFulfiller.sol::301 => for (uint256 i = 0; i < totalConsiderationItems; ++i) {
seaport/contracts/lib/OrderValidator.sol::549 => for (uint256 i = 0; i < originalOfferLength; ) {
seaport/contracts/lib/OrderValidator.sol::591 => for (uint256 i = 0; i < newConsiderationLength; ) {
seaport/contracts/lib/OrderValidator.sol::667 => for (uint256 i = 0; i < totalOrders; ) {
seaport/contracts/lib/OrderValidator.sol::753 => for (uint256 i = 0; i < totalOrders; ++i) {
seaport/contracts/lib/TypehashDirectory.sol::48 => for (uint256 i = 0; i < MaxTreeHeight; ) {
```



### [G05] Usage of `uints`/`ints` smaller than 32 bytes (256 bits) incurs overhead

#### Impact
> When using elements that are smaller than 32 bytes, your 
contract’s gas usage may be higher. This is because the EVM operates on 
32 bytes at a time. Therefore, if the element is smaller than that, the 
EVM must use more operations in order to reduce the size of the element 
from 32 bytes to the desired size.
> 

[https://docs.soliditylang.org/en/v0.8.11/internals/layout_in_storage.html](https://docs.soliditylang.org/en/v0.8.11/internals/layout_in_storage.html)
Use a larger size then downcast where needed
#### Findings:
```
seaport/contracts/conduit/ConduitController.sol::66 => if (address(uint160(bytes20(conduitKey))) != msg.sender) {
seaport/contracts/conduit/ConduitController.sol::73 => uint160(
seaport/contracts/conduit/ConduitController.sol::336 => uint160(
seaport/contracts/helpers/PointerLibraries.sol::614 => ) internal pure returns (uint8 value) {
seaport/contracts/helpers/PointerLibraries.sol::623 => ) internal pure returns (uint16 value) {
seaport/contracts/helpers/PointerLibraries.sol::632 => ) internal pure returns (uint24 value) {
seaport/contracts/helpers/PointerLibraries.sol::641 => ) internal pure returns (uint32 value) {
seaport/contracts/helpers/PointerLibraries.sol::650 => ) internal pure returns (uint40 value) {
seaport/contracts/helpers/PointerLibraries.sol::659 => ) internal pure returns (uint48 value) {
seaport/contracts/helpers/PointerLibraries.sol::668 => ) internal pure returns (uint56 value) {
seaport/contracts/helpers/PointerLibraries.sol::677 => ) internal pure returns (uint64 value) {
seaport/contracts/helpers/PointerLibraries.sol::686 => ) internal pure returns (uint72 value) {
seaport/contracts/helpers/PointerLibraries.sol::695 => ) internal pure returns (uint80 value) {
seaport/contracts/helpers/PointerLibraries.sol::704 => ) internal pure returns (uint88 value) {
seaport/contracts/helpers/PointerLibraries.sol::713 => ) internal pure returns (uint96 value) {
seaport/contracts/helpers/PointerLibraries.sol::722 => ) internal pure returns (uint104 value) {
seaport/contracts/helpers/PointerLibraries.sol::731 => ) internal pure returns (uint112 value) {
seaport/contracts/helpers/PointerLibraries.sol::740 => ) internal pure returns (uint120 value) {
seaport/contracts/helpers/PointerLibraries.sol::749 => ) internal pure returns (uint128 value) {
seaport/contracts/helpers/PointerLibraries.sol::758 => ) internal pure returns (uint136 value) {
seaport/contracts/helpers/PointerLibraries.sol::767 => ) internal pure returns (uint144 value) {
seaport/contracts/helpers/PointerLibraries.sol::776 => ) internal pure returns (uint152 value) {
seaport/contracts/helpers/PointerLibraries.sol::785 => ) internal pure returns (uint160 value) {
seaport/contracts/helpers/PointerLibraries.sol::794 => ) internal pure returns (uint168 value) {
seaport/contracts/helpers/PointerLibraries.sol::803 => ) internal pure returns (uint176 value) {
seaport/contracts/helpers/PointerLibraries.sol::812 => ) internal pure returns (uint184 value) {
seaport/contracts/helpers/PointerLibraries.sol::821 => ) internal pure returns (uint192 value) {
seaport/contracts/helpers/PointerLibraries.sol::830 => ) internal pure returns (uint200 value) {
seaport/contracts/helpers/PointerLibraries.sol::839 => ) internal pure returns (uint208 value) {
seaport/contracts/helpers/PointerLibraries.sol::848 => ) internal pure returns (uint216 value) {
seaport/contracts/helpers/PointerLibraries.sol::857 => ) internal pure returns (uint224 value) {
seaport/contracts/helpers/PointerLibraries.sol::866 => ) internal pure returns (uint232 value) {
seaport/contracts/helpers/PointerLibraries.sol::875 => ) internal pure returns (uint240 value) {
seaport/contracts/helpers/PointerLibraries.sol::884 => ) internal pure returns (uint248 value) {
seaport/contracts/helpers/PointerLibraries.sol::1539 => ) internal pure returns (uint8 value) {
seaport/contracts/helpers/PointerLibraries.sol::1549 => ) internal pure returns (uint16 value) {
seaport/contracts/helpers/PointerLibraries.sol::1559 => ) internal pure returns (uint24 value) {
seaport/contracts/helpers/PointerLibraries.sol::1569 => ) internal pure returns (uint32 value) {
seaport/contracts/helpers/PointerLibraries.sol::1579 => ) internal pure returns (uint40 value) {
seaport/contracts/helpers/PointerLibraries.sol::1589 => ) internal pure returns (uint48 value) {
seaport/contracts/helpers/PointerLibraries.sol::1599 => ) internal pure returns (uint56 value) {
seaport/contracts/helpers/PointerLibraries.sol::1609 => ) internal pure returns (uint64 value) {
seaport/contracts/helpers/PointerLibraries.sol::1619 => ) internal pure returns (uint72 value) {
seaport/contracts/helpers/PointerLibraries.sol::1629 => ) internal pure returns (uint80 value) {
seaport/contracts/helpers/PointerLibraries.sol::1639 => ) internal pure returns (uint88 value) {
seaport/contracts/helpers/PointerLibraries.sol::1649 => ) internal pure returns (uint96 value) {
seaport/contracts/helpers/PointerLibraries.sol::1659 => ) internal pure returns (uint104 value) {
seaport/contracts/helpers/PointerLibraries.sol::1669 => ) internal pure returns (uint112 value) {
seaport/contracts/helpers/PointerLibraries.sol::1679 => ) internal pure returns (uint120 value) {
seaport/contracts/helpers/PointerLibraries.sol::1689 => ) internal pure returns (uint128 value) {
seaport/contracts/helpers/PointerLibraries.sol::1699 => ) internal pure returns (uint136 value) {
seaport/contracts/helpers/PointerLibraries.sol::1709 => ) internal pure returns (uint144 value) {
seaport/contracts/helpers/PointerLibraries.sol::1719 => ) internal pure returns (uint152 value) {
seaport/contracts/helpers/PointerLibraries.sol::1729 => ) internal pure returns (uint160 value) {
seaport/contracts/helpers/PointerLibraries.sol::1739 => ) internal pure returns (uint168 value) {
seaport/contracts/helpers/PointerLibraries.sol::1749 => ) internal pure returns (uint176 value) {
seaport/contracts/helpers/PointerLibraries.sol::1759 => ) internal pure returns (uint184 value) {
seaport/contracts/helpers/PointerLibraries.sol::1769 => ) internal pure returns (uint192 value) {
seaport/contracts/helpers/PointerLibraries.sol::1779 => ) internal pure returns (uint200 value) {
seaport/contracts/helpers/PointerLibraries.sol::1789 => ) internal pure returns (uint208 value) {
seaport/contracts/helpers/PointerLibraries.sol::1799 => ) internal pure returns (uint216 value) {
seaport/contracts/helpers/PointerLibraries.sol::1809 => ) internal pure returns (uint224 value) {
seaport/contracts/helpers/PointerLibraries.sol::1819 => ) internal pure returns (uint232 value) {
seaport/contracts/helpers/PointerLibraries.sol::1829 => ) internal pure returns (uint240 value) {
seaport/contracts/helpers/PointerLibraries.sol::1839 => ) internal pure returns (uint248 value) {
seaport/contracts/helpers/PointerLibraries.sol::2499 => function readUint8(MemoryPointer mPtr) internal pure returns (uint8 value) {
seaport/contracts/helpers/PointerLibraries.sol::2508 => ) internal pure returns (uint16 value) {
seaport/contracts/helpers/PointerLibraries.sol::2517 => ) internal pure returns (uint24 value) {
seaport/contracts/helpers/PointerLibraries.sol::2526 => ) internal pure returns (uint32 value) {
seaport/contracts/helpers/PointerLibraries.sol::2535 => ) internal pure returns (uint40 value) {
seaport/contracts/helpers/PointerLibraries.sol::2544 => ) internal pure returns (uint48 value) {
seaport/contracts/helpers/PointerLibraries.sol::2553 => ) internal pure returns (uint56 value) {
seaport/contracts/helpers/PointerLibraries.sol::2562 => ) internal pure returns (uint64 value) {
seaport/contracts/helpers/PointerLibraries.sol::2571 => ) internal pure returns (uint72 value) {
seaport/contracts/helpers/PointerLibraries.sol::2580 => ) internal pure returns (uint80 value) {
seaport/contracts/helpers/PointerLibraries.sol::2589 => ) internal pure returns (uint88 value) {
seaport/contracts/helpers/PointerLibraries.sol::2598 => ) internal pure returns (uint96 value) {
seaport/contracts/helpers/PointerLibraries.sol::2607 => ) internal pure returns (uint104 value) {
seaport/contracts/helpers/PointerLibraries.sol::2625 => ) internal pure returns (uint120 value) {
seaport/contracts/helpers/PointerLibraries.sol::2634 => ) internal pure returns (uint128 value) {
seaport/contracts/helpers/PointerLibraries.sol::2643 => ) internal pure returns (uint136 value) {
seaport/contracts/helpers/PointerLibraries.sol::2652 => ) internal pure returns (uint144 value) {
seaport/contracts/helpers/PointerLibraries.sol::2661 => ) internal pure returns (uint152 value) {
seaport/contracts/helpers/PointerLibraries.sol::2670 => ) internal pure returns (uint160 value) {
seaport/contracts/helpers/PointerLibraries.sol::2679 => ) internal pure returns (uint168 value) {
seaport/contracts/helpers/PointerLibraries.sol::2688 => ) internal pure returns (uint176 value) {
seaport/contracts/helpers/PointerLibraries.sol::2697 => ) internal pure returns (uint184 value) {
seaport/contracts/helpers/PointerLibraries.sol::2706 => ) internal pure returns (uint192 value) {
seaport/contracts/helpers/PointerLibraries.sol::2715 => ) internal pure returns (uint200 value) {
seaport/contracts/helpers/PointerLibraries.sol::2724 => ) internal pure returns (uint208 value) {
seaport/contracts/helpers/PointerLibraries.sol::2733 => ) internal pure returns (uint216 value) {
seaport/contracts/helpers/PointerLibraries.sol::2742 => ) internal pure returns (uint224 value) {
seaport/contracts/helpers/PointerLibraries.sol::2751 => ) internal pure returns (uint232 value) {
seaport/contracts/helpers/PointerLibraries.sol::2760 => ) internal pure returns (uint240 value) {
seaport/contracts/helpers/PointerLibraries.sol::2769 => ) internal pure returns (uint248 value) {
seaport/contracts/interfaces/SignatureVerificationErrors.sol::17 => error BadSignatureV(uint8 v);
seaport/contracts/lib/BasicOrderFulfiller.sol::178 => (uint160(parameters.considerationToken) |
seaport/contracts/lib/ConsiderationStructs.sol::176 => uint120 numerator;
seaport/contracts/lib/ConsiderationStructs.sol::177 => uint120 denominator;
seaport/contracts/lib/ConsiderationStructs.sol::192 => uint120 numerator;
seaport/contracts/lib/ConsiderationStructs.sol::193 => uint120 denominator;
seaport/contracts/lib/Executor.sol::60 => if ((uint160(item.token) | item.identifier) != 0) {
```


### [G06] Duplicated `require()`/`revert()` checks should be refactored to a modifier or function

#### Impact
See [this](https://github.com/ethereum/solidity/issues/9232) issue for a detailed description of the issue
#### Findings:
```
seaport/contracts/conduit/ConduitController.sol::316 => revert NoConduit();
seaport/contracts/lib/TokenTransferrer.sol::152 => revert(0, returndatasize())
seaport/contracts/lib/TokenTransferrer.sol::422 => revert(Generic_error_selector_offset, NoContract_error_length)
```








### [G07] Multiple `address` mappings can be combined into a single `mapping` of an `address` to a `struct`, where appropriate

#### Impact
Saves a storage slot for the mapping. Depending on the circumstances 
and sizes of types, can avoid a Gsset (20000 gas) per mapping combined. 
#### Findings:
```

seaport/contracts/lib/CounterManager.sol::20 => mapping(address => uint256) private _counters;
seaport/contracts/lib/OrderValidator.sol::45 => mapping(address => uint256) internal _contractNonces;
```





### [G08] Using `bools` for storage incurs overhead


#### Findings:
```
seaport/contracts/conduit/Conduit.sol::34 => mapping(address => bool) private _channels;
seaport/contracts/conduit/ConduitController.sol::144 => bool channelPreviouslyOpen = channelIndexPlusOne != 0;
```





### [G09] Empty blocks should be removed or emit something

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



