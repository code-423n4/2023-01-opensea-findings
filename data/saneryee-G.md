# Gas Optimizations Report

|         | Issue                                                                                                                              | Instances |
| ------- | :--------------------------------------------------------------------------------------------------------------------------------- | :-------: |
| [G-001] | x += y or x -= y costs more gas than x = x + y or x = x - y for state variables                                                    |    25     |
| [G-002] | `storage` pointer to a structure is cheaper than copying each value of the structure into `memory`, same for `array` and `mapping` |     3     |
| [G-003] | Functions guaranteed to revert when called by normal users can be marked payable                                                   |     3     |
| [G-004] | internal functions only called once can be inlined to save gas                                                                     |     6     |
| [G-005] | Replace modifier with function                                                                                                     |     1     |

## [G-001] x += y or x -= y costs more gas than x = x + y or x = x - y for state variables

### Impact

Using the addition operator instead of plus-equals saves 113 gas. Usually does not work with struct and mappings.

### Findings

Total:25

[contracts/lib/ConsiderationDecoder.sol#L399](https://github.com/ProjectOpenSea/seaport/tree/5de7302bc773d9821ba4759e47fc981680911ea0//contracts/lib/ConsiderationDecoder.sol#L399)

```solidity
399:    for (uint256 offset = 0; offset < tailOffset; offset += OneWord) {
```

[contracts/lib/ConsiderationDecoder.sol#L498](https://github.com/ProjectOpenSea/seaport/tree/5de7302bc773d9821ba4759e47fc981680911ea0//contracts/lib/ConsiderationDecoder.sol#L498)

```solidity
498:    for (uint256 offset = 0; offset < tailOffset; offset += OneWord) {
```

[contracts/lib/ConsiderationDecoder.sol#L538](https://github.com/ProjectOpenSea/seaport/tree/5de7302bc773d9821ba4759e47fc981680911ea0//contracts/lib/ConsiderationDecoder.sol#L538)

```solidity
538:    for (uint256 offset = 0; offset < tailOffset; offset += OneWord) {
```

[contracts/lib/ConsiderationDecoder.sol#L630](https://github.com/ProjectOpenSea/seaport/tree/5de7302bc773d9821ba4759e47fc981680911ea0//contracts/lib/ConsiderationDecoder.sol#L630)

```solidity
630:    for (uint256 offset = 0; offset < tailOffset; offset += OneWord) {
```

[contracts/lib/ConsiderationDecoder.sol#L673](https://github.com/ProjectOpenSea/seaport/tree/5de7302bc773d9821ba4759e47fc981680911ea0//contracts/lib/ConsiderationDecoder.sol#L673)

```solidity
673:    for (uint256 offset = 0; offset < tailOffset; offset += OneWord) {
```

[contracts/lib/ConsiderationDecoder.sol#L744](https://github.com/ProjectOpenSea/seaport/tree/5de7302bc773d9821ba4759e47fc981680911ea0//contracts/lib/ConsiderationDecoder.sol#L744)

```solidity
744:    for (uint256 offset = 0; offset < tailOffset; offset += OneWord) {
```

[contracts/lib/BasicOrderFulfiller.sol#L965](https://github.com/ProjectOpenSea/seaport/tree/5de7302bc773d9821ba4759e47fc981680911ea0//contracts/lib/BasicOrderFulfiller.sol#L965)

```solidity
965:    nativeTokensRemaining -= additionalRecipientAmount;
```

[contracts/lib/BasicOrderFulfiller.sol#L1097](https://github.com/ProjectOpenSea/seaport/tree/5de7302bc773d9821ba4759e47fc981680911ea0//contracts/lib/BasicOrderFulfiller.sol#L1097)

```solidity
1097:    amount -= additionalRecipientAmount;
```

[contracts/lib/BasicOrderFulfiller.sol#L1112](https://github.com/ProjectOpenSea/seaport/tree/5de7302bc773d9821ba4759e47fc981680911ea0//contracts/lib/BasicOrderFulfiller.sol#L1112)

```solidity
1112:    i += AdditionalRecipient_size;
```

[contracts/lib/BasicOrderFulfiller.sol#L941](https://github.com/ProjectOpenSea/seaport/tree/5de7302bc773d9821ba4759e47fc981680911ea0//contracts/lib/BasicOrderFulfiller.sol#L941)

```solidity
941:    i += AdditionalRecipient_size
```

[contracts/lib/OrderCombiner.sol#L230](https://github.com/ProjectOpenSea/seaport/tree/5de7302bc773d9821ba4759e47fc981680911ea0//contracts/lib/OrderCombiner.sol#L230)

```solidity
230:    for (uint256 i = 32; i < terminalMemoryOffset; i += 32) {
```

[contracts/lib/OrderCombiner.sol#L451](https://github.com/ProjectOpenSea/seaport/tree/5de7302bc773d9821ba4759e47fc981680911ea0//contracts/lib/OrderCombiner.sol#L451)

```solidity
451:    for (uint256 i = 32; i < terminalMemoryOffset; i += 32) {
```

[contracts/lib/ConsiderationEncoder.sol#L259](https://github.com/ProjectOpenSea/seaport/tree/5de7302bc773d9821ba4759e47fc981680911ea0//contracts/lib/ConsiderationEncoder.sol#L259)

```solidity
259:    tailOffset += considerationSize;
```

[contracts/lib/ConsiderationEncoder.sol#L400](https://github.com/ProjectOpenSea/seaport/tree/5de7302bc773d9821ba4759e47fc981680911ea0//contracts/lib/ConsiderationEncoder.sol#L400)

```solidity
400:    tailOffset += considerationSize;
```

[contracts/lib/ConsiderationEncoder.sol#L172](https://github.com/ProjectOpenSea/seaport/tree/5de7302bc773d9821ba4759e47fc981680911ea0//contracts/lib/ConsiderationEncoder.sol#L172)

```solidity
172:    tailOffset += contextSize;
```

[contracts/lib/ConsiderationEncoder.sol#L273](https://github.com/ProjectOpenSea/seaport/tree/5de7302bc773d9821ba4759e47fc981680911ea0//contracts/lib/ConsiderationEncoder.sol#L273)

```solidity
273:    tailOffset += contextSize;
```

[contracts/lib/ConsiderationEncoder.sol#L413](https://github.com/ProjectOpenSea/seaport/tree/5de7302bc773d9821ba4759e47fc981680911ea0//contracts/lib/ConsiderationEncoder.sol#L413)

```solidity
413:    tailOffset += extraDataSize;
```

[contracts/lib/ConsiderationEncoder.sol#L287](https://github.com/ProjectOpenSea/seaport/tree/5de7302bc773d9821ba4759e47fc981680911ea0//contracts/lib/ConsiderationEncoder.sol#L287)

```solidity
287:    tailOffset += orderHashesSize;
```

[contracts/lib/ConsiderationEncoder.sol#L429](https://github.com/ProjectOpenSea/seaport/tree/5de7302bc773d9821ba4759e47fc981680911ea0//contracts/lib/ConsiderationEncoder.sol#L429)

```solidity
429:    tailOffset += orderHashesSize;
```

[contracts/lib/ConsiderationEncoder.sol#L240](https://github.com/ProjectOpenSea/seaport/tree/5de7302bc773d9821ba4759e47fc981680911ea0//contracts/lib/ConsiderationEncoder.sol#L240)

```solidity
240:    tailOffset += offerSize;
```

[contracts/lib/ConsiderationEncoder.sol#L379](https://github.com/ProjectOpenSea/seaport/tree/5de7302bc773d9821ba4759e47fc981680911ea0//contracts/lib/ConsiderationEncoder.sol#L379)

```solidity
379:    tailOffset += offerSize;
```

[contracts/lib/ConsiderationEncoder.sol#L523](https://github.com/ProjectOpenSea/seaport/tree/5de7302bc773d9821ba4759e47fc981680911ea0//contracts/lib/ConsiderationEncoder.sol#L523)

```solidity
523:    tailOffset += OneWord;
```

[contracts/lib/ConsiderationEncoder.sol#L155](https://github.com/ProjectOpenSea/seaport/tree/5de7302bc773d9821ba4759e47fc981680911ea0//contracts/lib/ConsiderationEncoder.sol#L155)

```solidity
155:    tailOffset += maximumSpentSize;
```

[contracts/lib/ConsiderationEncoder.sol#L134](https://github.com/ProjectOpenSea/seaport/tree/5de7302bc773d9821ba4759e47fc981680911ea0//contracts/lib/ConsiderationEncoder.sol#L134)

```solidity
134:    tailOffset += minimumReceivedSize;
```

[contracts/lib/ConsiderationEncoder.sol#L514](https://github.com/ProjectOpenSea/seaport/tree/5de7302bc773d9821ba4759e47fc981680911ea0//contracts/lib/ConsiderationEncoder.sol#L514)

```solidity
514:    tailOffset += offerAndConsiderationSize;
```

### Recommendation

Same as description

## [G-002] `storage` pointer to a structure is cheaper than copying each value of the structure into `memory`, same for `array` and `mapping`

### Impact

It may not be obvious, but every time you copy a storage `struct/array/mapping` to a `memory` variable, you are literally copying each member by reading it from `storage`, which is expensive. And when you use the `storage` keyword, you are just storing a pointer to the storage, which is much cheaper.

### Findings

Total:3

[contracts/lib/OrderCombiner.sol#L685](https://github.com/ProjectOpenSea/seaport/tree/5de7302bc773d9821ba4759e47fc981680911ea0//contracts/lib/OrderCombiner.sol#L685)

```solidity
685:    bool[] memory availableOrders = new bool[](totalOrders);
```

[contracts/lib/OrderFulfiller.sol#L116](https://github.com/ProjectOpenSea/seaport/tree/5de7302bc773d9821ba4759e47fc981680911ea0//contracts/lib/OrderFulfiller.sol#L116)

```solidity
116:    bytes32[] memory orderHashes = new bytes32[](1);
```

[contracts/lib/TypehashDirectory.sol#L32](https://github.com/ProjectOpenSea/seaport/tree/5de7302bc773d9821ba4759e47fc981680911ea0//contracts/lib/TypehashDirectory.sol#L32)

```solidity
32:    bytes32[] memory typeHashes = new bytes32[](MaxTreeHeight);
```

### Recommendation

Using `storage` instead of `memory`

## [G-003] Functions guaranteed to revert when called by normal users can be marked payable

### Impact

If a function modifier such as `onlyOwner` is used, the function will revert if a normal user tries to pay the function. Marking the function as `payable` will lower the gas cost for legitimate callers because the compiler will not include checks for whether a payment was provided.
The extra opcodes avoided are `CALLVALUE(2)`,`DUP1(3)`,`ISZERO(3)`,`PUSH2(3)`,`JUMPI(10)`,`PUSH1(3)`,`DUP1(3)`,`REVERT(0)`,`JUMPDEST(1)`,`POP(2)`, which costs an average of about 21 gas per call to the function, in addition to the extra deployment cost.

### Findings

Total:3

[contracts/conduit/Conduit.sol#L94](https://github.com/ProjectOpenSea/seaport/tree/5de7302bc773d9821ba4759e47fc981680911ea0//contracts/conduit/Conduit.sol#L94)

```solidity
94:    ) external override onlyOpenChannel returns (bytes4 magicValue) {
```

[contracts/conduit/Conduit.sol#L129](https://github.com/ProjectOpenSea/seaport/tree/5de7302bc773d9821ba4759e47fc981680911ea0//contracts/conduit/Conduit.sol#L129)

```solidity
129:    ) external override onlyOpenChannel returns (bytes4 magicValue) {
```

[contracts/conduit/Conduit.sol#L157](https://github.com/ProjectOpenSea/seaport/tree/5de7302bc773d9821ba4759e47fc981680911ea0//contracts/conduit/Conduit.sol#L157)

```solidity
157:    ) external override onlyOpenChannel returns (bytes4 magicValue) {
```

### Recommendation

Mark the function as payable.

## [G-004] internal functions only called once can be inlined to save gas

### Impact

Not inlining costs 20 to 40 gas because of two extra `JUMP` instructions and additional stack operations needed for function calls.

### Findings

Total:6

[contracts/lib/OrderCombiner.sol#L867](https://github.com/ProjectOpenSea/seaport/tree/5de7302bc773d9821ba4759e47fc981680911ea0//contracts/lib/OrderCombiner.sol#L867)

```solidity
867:    function _emitOrdersMatched(bytes32[] memory orderHashes) internal {
```

[contracts/lib/Executor.sol#L454](https://github.com/ProjectOpenSea/seaport/tree/5de7302bc773d9821ba4759e47fc981680911ea0//contracts/lib/Executor.sol#L454)

```solidity
454:    function _triggerIfArmed(bytes memory accumulator) internal {
```

[contracts/lib/Executor.sol#L479](https://github.com/ProjectOpenSea/seaport/tree/5de7302bc773d9821ba4759e47fc981680911ea0//contracts/lib/Executor.sol#L479)

```solidity
479:    function _trigger(bytes32 conduitKey, bytes memory accumulator) internal {
```

[contracts/lib/GettersAndDerivers.sol#L295](https://github.com/ProjectOpenSea/seaport/tree/5de7302bc773d9821ba4759e47fc981680911ea0//contracts/lib/GettersAndDerivers.sol#L295)

```solidity
295:    function _domainSeparator() internal view returns (bytes32) {
```

[contracts/lib/ConsiderationBase.sol#L161](https://github.com/ProjectOpenSea/seaport/tree/5de7302bc773d9821ba4759e47fc981680911ea0//contracts/lib/ConsiderationBase.sol#L161)

```solidity
161:    function _nameString() internal pure virtual returns (string memory) {
```

[contracts/lib/ReentrancyGuard.sol#L62](https://github.com/ProjectOpenSea/seaport/tree/5de7302bc773d9821ba4759e47fc981680911ea0//contracts/lib/ReentrancyGuard.sol#L62)

```solidity
62:    function _assertNonReentrant() internal view {
```

## [G-005] Replace modifier with function

### Impact

Modifiers make code more elegant, but cost more than normal functions.

### Findings

Total:1

[contracts/conduit/Conduit.sol#L40](https://github.com/ProjectOpenSea/seaport/tree/5de7302bc773d9821ba4759e47fc981680911ea0//contracts/conduit/Conduit.sol#L40)

```solidity
40:    modifier onlyOpenChannel() {
```
