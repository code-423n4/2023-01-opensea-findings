## Summary<a name="Summary">

### Gas Optimizations
| |Issue|Contexts|Estimated Gas Saved|
|-|:-|:-|:-:|
| [GAS&#x2011;1](#GAS&#x2011;1) | Setting the `constructor` to `payable` | 15 | 195 |
| [GAS&#x2011;2](#GAS&#x2011;2) | Using `delete` statement can save gas | 4 | - |
| [GAS&#x2011;3](#GAS&#x2011;3) | Functions guaranteed to revert when called by normal users can be marked `payable` | 5 | 105 |
| [GAS&#x2011;4](#GAS&#x2011;4) | Use hardcoded address instead `address(this)` | 2 | - |
| [GAS&#x2011;5](#GAS&#x2011;5) | `internal` functions only called once can be inlined to save gas | 1 | - |
| [GAS&#x2011;6](#GAS&#x2011;6) | Optimize names to save gas | 21 | 462 |
| [GAS&#x2011;7](#GAS&#x2011;7) | `<x> += <y>` Costs More Gas Than `<x> = <x> + <y>` For State Variables | 25 | - |
| [GAS&#x2011;8](#GAS&#x2011;8) | Help The Optimizer By Saving A Storage Variable’s Reference Instead Of Repeatedly Fetching It | 4 | - |
| [GAS&#x2011;9](#GAS&#x2011;9) | Usage of `uints`/`ints` smaller than 32 bytes (256 bits) incurs overhead | 8 | - |
| [GAS&#x2011;10](#GAS&#x2011;10) | Use solidity version 0.8.17 to gain some gas boost | 32 | 2816 |
| [GAS&#x2011;11](#GAS&#x2011;11) | Using `storage` instead of `memory` saves gas | 13 | 4550 |

Total: 130 contexts over 11 issues

## Gas Optimizations




### <a href="#Summary">[GAS&#x2011;1]</a><a name="GAS&#x2011;1"> Setting the `constructor` to `payable`

Saves ~13 gas per instance

#### <ins>Proof Of Concept</ins>

```solidity
93: constructor(address conduitController) Consideration(conduitController)
```

https://github.com/ProjectOpenSea/seaport/tree/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/Seaport.sol#L93

```solidity
73: constructor()
```

https://github.com/ProjectOpenSea/seaport/tree/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/conduit/Conduit.sol#L73

```solidity
31: constructor()
```

https://github.com/ProjectOpenSea/seaport/tree/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/conduit/ConduitController.sol#L31

```solidity
35: constructor(
        address conduitController
    ) GettersAndDerivers(conduitController)
```

https://github.com/ProjectOpenSea/seaport/tree/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/lib/Assertions.sol#L35

```solidity
41: constructor(address conduitController) OrderValidator(conduitController)
```

https://github.com/ProjectOpenSea/seaport/tree/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/lib/BasicOrderFulfiller.sol#L41

```solidity
50: constructor(address conduitController) OrderCombiner(conduitController)
```

https://github.com/ProjectOpenSea/seaport/tree/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/lib/Consideration.sol#L50

```solidity
56: constructor(address conduitController)
```

https://github.com/ProjectOpenSea/seaport/tree/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/lib/ConsiderationBase.sol#L56

```solidity
35: constructor(address conduitController) Verifiers(conduitController)
```

https://github.com/ProjectOpenSea/seaport/tree/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/lib/Executor.sol#L35

```solidity
25: constructor(
        address conduitController
    ) ConsiderationBase(conduitController)
```

https://github.com/ProjectOpenSea/seaport/tree/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/lib/GettersAndDerivers.sol#L25

```solidity
41: constructor(address conduitController) OrderFulfiller(conduitController)
```

https://github.com/ProjectOpenSea/seaport/tree/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/lib/OrderCombiner.sol#L41

```solidity
45: constructor(
        address conduitController
    ) BasicOrderFulfiller(conduitController)
```

https://github.com/ProjectOpenSea/seaport/tree/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/lib/OrderFulfiller.sol#L45

```solidity
55: constructor(address conduitController) Executor(conduitController)
```

https://github.com/ProjectOpenSea/seaport/tree/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/lib/OrderValidator.sol#L55

```solidity
23: constructor()
```

https://github.com/ProjectOpenSea/seaport/tree/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/lib/ReentrancyGuard.sol#L23

```solidity
30: constructor()
```

https://github.com/ProjectOpenSea/seaport/tree/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/lib/TypehashDirectory.sol#L30

```solidity
26: constructor(address conduitController) Assertions(conduitController)
```

https://github.com/ProjectOpenSea/seaport/tree/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/lib/Verifiers.sol#L26





### <a href="#Summary">[GAS&#x2011;2]</a><a name="GAS&#x2011;2"> Using `delete` statement can save gas

#### <ins>Proof Of Concept</ins>

```solidity
939: uint256 i = 0;

```

https://github.com/ProjectOpenSea/seaport/tree/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/lib/BasicOrderFulfiller.sol#L939

```solidity
239: advancedOrder.numerator = 0;
```

https://github.com/ProjectOpenSea/seaport/tree/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/lib/OrderCombiner.sol#L239


```solidity
564: uint256 totalFilteredExecutions = 0;

```

https://github.com/ProjectOpenSea/seaport/tree/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/lib/OrderCombiner.sol#L564

```solidity
996: uint256 totalFilteredExecutions = 0;

```

https://github.com/ProjectOpenSea/seaport/tree/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/lib/OrderCombiner.sol#L996





### <a href="#Summary">[GAS&#x2011;3]</a><a name="GAS&#x2011;3"> Functions guaranteed to revert when called by normal users can be marked `payable`

If a function modifier or require such as onlyOwner/onlyX is used, the function will revert if a normal user tries to pay the function. Marking the function as payable will lower the gas cost for legitimate callers because the compiler will not include checks for whether a payment was provided. The extra opcodes avoided are CALLVALUE(2), DUP1(3), ISZERO(3), PUSH2(3), JUMPI(10), PUSH1(3), DUP1(3), REVERT(0), JUMPDEST(1), POP(2) which costs an average of about 21 gas per call to the function, in addition to the extra deployment cost.

#### <ins>Proof Of Concept</ins>

```solidity
92: function execute(
        ConduitTransfer[] calldata transfers
    ) external override onlyOpenChannel returns (bytes4 magicValue) {
127: function execute(
        ConduitTransfer[] calldata transfers
    ) external override onlyOpenChannel returns (bytes4 magicValue) {
154: function execute(
        ConduitTransfer[] calldata transfers
    ) external override onlyOpenChannel returns (bytes4 magicValue) {

```

https://github.com/ProjectOpenSea/seaport/tree/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/conduit/Conduit.sol#L92

https://github.com/ProjectOpenSea/seaport/tree/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/conduit/Conduit.sol#L127

https://github.com/ProjectOpenSea/seaport/tree/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/conduit/Conduit.sol#L154



```solidity
127: function executeBatch1155(
        ConduitBatch1155Transfer[] calldata batchTransfers
    ) external override onlyOpenChannel returns (bytes4 magicValue) {

```

https://github.com/ProjectOpenSea/seaport/tree/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/conduit/Conduit.sol#L127

```solidity
154: function executeWithBatch1155(
        ConduitTransfer[] calldata standardTransfers,
        ConduitBatch1155Transfer[] calldata batchTransfers
    ) external override onlyOpenChannel returns (bytes4 magicValue) {

```

https://github.com/ProjectOpenSea/seaport/tree/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/conduit/Conduit.sol#L154



#### <ins>Recommended Mitigation Steps</ins>
Functions guaranteed to revert when called by normal users can be marked payable.



### <a href="#Summary">[GAS&#x2011;4]</a><a name="GAS&#x2011;4"> Use hardcode address instead `address(this)`

Instead of using `address(this)`, it is more gas-efficient to pre-calculate and use the hardcoded `address`. Foundry's script.sol and solmate's `LibRlp.sol` contracts can help achieve this.

References: 
https://book.getfoundry.sh/reference/forge-std/compute-create-address 

https://twitter.com/transmissions11/status/1518507047943245824

#### <ins>Proof Of Concept</ins>

```solidity
78: address(this),

```

https://github.com/ProjectOpenSea/seaport/tree/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/conduit/ConduitController.sol#L78

```solidity
341: address(this),

```

https://github.com/ProjectOpenSea/seaport/tree/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/conduit/ConduitController.sol#L341



#### <ins>Recommended Mitigation Steps</ins>

Use hardcoded `address`





### <a href="#Summary">[GAS&#x2011;5]</a><a name="GAS&#x2011;5"> `internal` functions only called once can be inlined to save gas

#### <ins>Proof Of Concept</ins>



```solidity
125: function _transferIndividual721Or1155Item

```

https://github.com/ProjectOpenSea/seaport/tree/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/lib/Executor.sol#L125






### <a href="#Summary">[GAS&#x2011;6]</a><a name="GAS&#x2011;6"> Optimize names to save gas

Contracts most called functions could simply save gas by function ordering via Method ID. Calling a function at runtime will be cheaper if the function is positioned earlier in the order (has a relatively lower Method ID) because 22 gas are added to the cost of a function for every position that came before it. The caller can save on gas if you prioritize most called functions. 

See more <a href="https://medium.com/joyso/solidity-how-does-function-name-affect-gas-consumption-in-smart-contract-47d270d8ac92">here</a>

#### <ins>Proof Of Concept</ins>

All in-scope contracts

#### <ins>Recommended Mitigation Steps</ins>
Find a lower method ID name for the most called functions for example Call() vs. Call1() is cheaper by 22 gas
For example, the function IDs in the Gauge.sol contract will be the most used; A lower method ID may be given.



### <a href="#Summary">[GAS&#x2011;7]</a><a name="GAS&#x2011;7"> `<x> += <y>` Costs More Gas Than `<x> = <x> + <y>` For State Variables

#### <ins>Proof Of Concept</ins>


```solidity
941: i += AdditionalRecipient_size
965: nativeTokensRemaining -= additionalRecipientAmount;

```

https://github.com/ProjectOpenSea/seaport/tree/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/lib/BasicOrderFulfiller.sol#L941

https://github.com/ProjectOpenSea/seaport/tree/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/lib/BasicOrderFulfiller.sol#L965



```solidity
1097: amount -= additionalRecipientAmount;
1112: i += AdditionalRecipient_size;

```

https://github.com/ProjectOpenSea/seaport/tree/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/lib/BasicOrderFulfiller.sol#L1097

https://github.com/ProjectOpenSea/seaport/tree/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/lib/BasicOrderFulfiller.sol#L1112



```solidity
399: for (uint256 offset = 0; offset < tailOffset; offset += OneWord) {

```

https://github.com/ProjectOpenSea/seaport/tree/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/lib/ConsiderationDecoder.sol#L399

```solidity
498: for (uint256 offset = 0; offset < tailOffset; offset += OneWord) {

```

https://github.com/ProjectOpenSea/seaport/tree/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/lib/ConsiderationDecoder.sol#L498

```solidity
538: for (uint256 offset = 0; offset < tailOffset; offset += OneWord) {

```

https://github.com/ProjectOpenSea/seaport/tree/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/lib/ConsiderationDecoder.sol#L538

```solidity
630: for (uint256 offset = 0; offset < tailOffset; offset += OneWord) {

```

https://github.com/ProjectOpenSea/seaport/tree/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/lib/ConsiderationDecoder.sol#L630

```solidity
673: for (uint256 offset = 0; offset < tailOffset; offset += OneWord) {

```

https://github.com/ProjectOpenSea/seaport/tree/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/lib/ConsiderationDecoder.sol#L673

```solidity
744: for (uint256 offset = 0; offset < tailOffset; offset += OneWord) {

```

https://github.com/ProjectOpenSea/seaport/tree/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/lib/ConsiderationDecoder.sol#L744

```solidity
134: tailOffset += minimumReceivedSize;
155: tailOffset += maximumSpentSize;
172: tailOffset += contextSize;

```

https://github.com/ProjectOpenSea/seaport/tree/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/lib/ConsiderationEncoder.sol#L134

https://github.com/ProjectOpenSea/seaport/tree/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/lib/ConsiderationEncoder.sol#L155

https://github.com/ProjectOpenSea/seaport/tree/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/lib/ConsiderationEncoder.sol#L172



```solidity
240: tailOffset += offerSize;
259: tailOffset += considerationSize;
273: tailOffset += contextSize;
287: tailOffset += orderHashesSize;

```

https://github.com/ProjectOpenSea/seaport/tree/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/lib/ConsiderationEncoder.sol#L240

https://github.com/ProjectOpenSea/seaport/tree/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/lib/ConsiderationEncoder.sol#L259

https://github.com/ProjectOpenSea/seaport/tree/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/lib/ConsiderationEncoder.sol#L273

https://github.com/ProjectOpenSea/seaport/tree/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/lib/ConsiderationEncoder.sol#L287



```solidity
379: tailOffset += offerSize;
400: tailOffset += considerationSize;
413: tailOffset += extraDataSize;
429: tailOffset += orderHashesSize;

```

https://github.com/ProjectOpenSea/seaport/tree/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/lib/ConsiderationEncoder.sol#L379

https://github.com/ProjectOpenSea/seaport/tree/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/lib/ConsiderationEncoder.sol#L400

https://github.com/ProjectOpenSea/seaport/tree/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/lib/ConsiderationEncoder.sol#L413

https://github.com/ProjectOpenSea/seaport/tree/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/lib/ConsiderationEncoder.sol#L429



```solidity
514: tailOffset += offerAndConsiderationSize;
523: tailOffset += OneWord;

```

https://github.com/ProjectOpenSea/seaport/tree/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/lib/ConsiderationEncoder.sol#L514

https://github.com/ProjectOpenSea/seaport/tree/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/lib/ConsiderationEncoder.sol#L523



```solidity
230: for (uint256 i = 32; i < terminalMemoryOffset; i += 32) {
230: for (uint256 i = 32; i < terminalMemoryOffset; i += 32) {

```

https://github.com/ProjectOpenSea/seaport/tree/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/lib/OrderCombiner.sol#L230

https://github.com/ProjectOpenSea/seaport/tree/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/lib/OrderCombiner.sol#L230







### <a href="#Summary">[GAS&#x2011;8]</a><a name="GAS&#x2011;8"> Help The Optimizer By Saving A Storage Variable's Reference Instead Of Repeatedly Fetching It

To help the optimizer, declare a storage type variable and use it instead of repeatedly fetching the reference in a map or an array.
The effect can be quite significant.
As an example, instead of repeatedly calling someMap[someIndex], save its reference like this: SomeStruct storage someStruct = someMap[someIndex] and use it.

#### <ins>Proof Of Concept</ins>


```solidity
74: AdvancedOrder memory advancedOrder = advancedOrders[orderIndex];
```

https://github.com/ProjectOpenSea/seaport/tree/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/lib/CriteriaResolution.sol#L74

```solidity
508: contractNonce = _contractNonces[offerer]++;
```

https://github.com/ProjectOpenSea/seaport/tree/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/lib/OrderValidator.sol#L508

```solidity
699: orderStatus = _orderStatus[orderHash];
```

https://github.com/ProjectOpenSea/seaport/tree/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/lib/OrderValidator.sol#L699

```solidity
774: orderStatus = _orderStatus[orderHash];
```

https://github.com/ProjectOpenSea/seaport/tree/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/lib/OrderValidator.sol#L774







### <a href="#Summary">[GAS&#x2011;9]</a><a name="GAS&#x2011;9"> Usage of `uints`/`ints` smaller than 32 bytes (256 bits) incurs overhead

When using elements that are smaller than 32 bytes, your contract's gas usage may be higher. This is because the EVM operates on 32 bytes at a time. Therefore, if the element is smaller than that, the EVM must use more operations in order to reduce the size of the element from 32 bytes to the desired size.

https://docs.soliditylang.org/en/v0.8.11/internals/layout_in_storage.html
Each operation involving a `uint8` costs an extra 22-28 gas (depending on whether the other operand is also a variable of type `uint8`) as compared to ones involving `uint256`, due to the compiler having to clear the higher bits of the memory word before operating on the `uint8`, as well as the associated stack operations of doing so. Use a larger size then downcast where needed

#### <ins>Proof Of Concept</ins>


```solidity
192: uint120 numerator;
```

https://github.com/ProjectOpenSea/seaport/tree/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/lib/ConsiderationStructs.sol#L192

```solidity
193: uint120 denominator;
```

https://github.com/ProjectOpenSea/seaport/tree/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/lib/ConsiderationStructs.sol#L193






### <a href="#Summary">[GAS&#x2011;10]</a><a name="GAS&#x2011;10"> Use solidity version 0.8.17 to gain some gas boost

Upgrade to the latest solidity version 0.8.17 to get additional gas savings.

#### <ins>Proof Of Concept</ins>


```solidity
pragma solidity ^0.8.13;
```

https://github.com/ProjectOpenSea/seaport/tree/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/conduit/Conduit.sol#L2

```solidity
pragma solidity ^0.8.13;
```

https://github.com/ProjectOpenSea/seaport/tree/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/conduit/ConduitController.sol#L2

```solidity
pragma solidity ^0.8.13;
```

https://github.com/ProjectOpenSea/seaport/tree/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/conduit/lib/ConduitConstants.sol#L2

```solidity
pragma solidity ^0.8.13;
```

https://github.com/ProjectOpenSea/seaport/tree/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/conduit/lib/ConduitEnums.sol#L2

```solidity
pragma solidity ^0.8.13;
```

https://github.com/ProjectOpenSea/seaport/tree/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/conduit/lib/ConduitStructs.sol#L2

```solidity
pragma solidity ^0.8.13;
```

https://github.com/ProjectOpenSea/seaport/tree/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/helpers/PointerLibraries.sol#L2

```solidity
pragma solidity ^0.8.13;
```

https://github.com/ProjectOpenSea/seaport/tree/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/interfaces/AbridgedTokenInterfaces.sol#L2

```solidity
pragma solidity ^0.8.13;
```

https://github.com/ProjectOpenSea/seaport/tree/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/interfaces/AmountDerivationErrors.sol#L2

```solidity
pragma solidity ^0.8.13;
```

https://github.com/ProjectOpenSea/seaport/tree/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/interfaces/ConduitControllerInterface.sol#L2

```solidity
pragma solidity ^0.8.13;
```

https://github.com/ProjectOpenSea/seaport/tree/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/interfaces/ConduitInterface.sol#L2

```solidity
pragma solidity ^0.8.13;
```

https://github.com/ProjectOpenSea/seaport/tree/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/interfaces/ConsiderationEventsAndErrors.sol#L2

```solidity
pragma solidity ^0.8.13;
```

https://github.com/ProjectOpenSea/seaport/tree/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/interfaces/ConsiderationInterface.sol#L2

```solidity
pragma solidity ^0.8.13;
```

https://github.com/ProjectOpenSea/seaport/tree/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/interfaces/ContractOffererInterface.sol#L2

```solidity
pragma solidity ^0.8.13;
```

https://github.com/ProjectOpenSea/seaport/tree/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/interfaces/CriteriaResolutionErrors.sol#L2

```solidity
pragma solidity ^0.8.13;
```

https://github.com/ProjectOpenSea/seaport/tree/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/interfaces/EIP1271Interface.sol#L2

```solidity
pragma solidity ^0.8.13;
```

https://github.com/ProjectOpenSea/seaport/tree/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/interfaces/FulfillmentApplicationErrors.sol#L2

```solidity
pragma solidity ^0.8.13;
```

https://github.com/ProjectOpenSea/seaport/tree/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/interfaces/IERC721Receiver.sol#L2

```solidity
pragma solidity ^0.8.13;
```

https://github.com/ProjectOpenSea/seaport/tree/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/interfaces/ImmutableCreate2FactoryInterface.sol#L2

```solidity
pragma solidity ^0.8.13;
```

https://github.com/ProjectOpenSea/seaport/tree/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/interfaces/ReentrancyErrors.sol#L2

```solidity
pragma solidity ^0.8.13;
```

https://github.com/ProjectOpenSea/seaport/tree/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/interfaces/SeaportInterface.sol#L2

```solidity
pragma solidity ^0.8.13;
```

https://github.com/ProjectOpenSea/seaport/tree/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/interfaces/SignatureVerificationErrors.sol#L2

```solidity
pragma solidity ^0.8.13;
```

https://github.com/ProjectOpenSea/seaport/tree/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/interfaces/TokenTransferrerErrors.sol#L2

```solidity
pragma solidity ^0.8.13;
```

https://github.com/ProjectOpenSea/seaport/tree/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/interfaces/TransferHelperErrors.sol#L2

```solidity
pragma solidity ^0.8.13;
```

https://github.com/ProjectOpenSea/seaport/tree/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/interfaces/TransferHelperInterface.sol#L2

```solidity
pragma solidity ^0.8.13;
```

https://github.com/ProjectOpenSea/seaport/tree/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/interfaces/ZoneInteractionErrors.sol#L2

```solidity
pragma solidity ^0.8.13;
```

https://github.com/ProjectOpenSea/seaport/tree/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/interfaces/ZoneInterface.sol#L2

```solidity
pragma solidity ^0.8.13;
```

https://github.com/ProjectOpenSea/seaport/tree/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/lib/ConsiderationConstants.sol#L2

```solidity
pragma solidity ^0.8.13;
```

https://github.com/ProjectOpenSea/seaport/tree/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/lib/ConsiderationEncoder.sol#L2

```solidity
pragma solidity ^0.8.13;
```

https://github.com/ProjectOpenSea/seaport/tree/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/lib/ConsiderationEnums.sol#L2

```solidity
pragma solidity ^0.8.13;
```

https://github.com/ProjectOpenSea/seaport/tree/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/lib/ConsiderationStructs.sol#L2

```solidity
pragma solidity ^0.8.13;
```

https://github.com/ProjectOpenSea/seaport/tree/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/lib/TokenTransferrer.sol#L2

```solidity
pragma solidity ^0.8.13;
```

https://github.com/ProjectOpenSea/seaport/tree/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/lib/TokenTransferrerConstants.sol#L2





### <a href="#Summary">[GAS&#x2011;11]</a><a name="GAS&#x2011;11"> Using `storage` instead of `memory` saves gas

When fetching data from a `storage` location, assigning the data to a `memory` variable causes all fields of the struct/array to be read from `storage`, which incurs a Gcoldsload (2100 gas) for each field of the struct/array. If the fields are read from the new `memory` variable, they incur an additional MLOAD rather than a cheap stack read. Instead of declearing the variable with the memory keyword, declaring the variable with the `storage` keyword and caching any fields that need to be re-read in stack variables, will be much cheaper, only incuring the Gcoldsload for the fields actually read. The only time it makes sense to read the whole struct/array into a `memory` variable, is if the full struct/array is being returned by the function, is being passed to a function that requires memory, or if the array/struct is being read from another `memory` array/struct

#### <ins>Proof Of Concept</ins>


```solidity
74: AdvancedOrder memory advancedOrder = advancedOrders[orderIndex];
143: AdvancedOrder memory advancedOrder = advancedOrders[i];

```

https://github.com/ProjectOpenSea/seaport/tree/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/lib/CriteriaResolution.sol#L74

https://github.com/ProjectOpenSea/seaport/tree/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/lib/CriteriaResolution.sol#L143



```solidity
199: OfferItem memory offerItem = offer[componentIndex];

```

https://github.com/ProjectOpenSea/seaport/tree/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/lib/CriteriaResolution.sol#L199

```solidity
122: FulfillmentComponent memory targetComponent = offerComponents[0];

```

https://github.com/ProjectOpenSea/seaport/tree/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/lib/FulfillmentApplier.sol#L122

```solidity
300: OfferItem memory offerItem = offer[j];
763: OfferItem memory offerItem = offer[j];

```

https://github.com/ProjectOpenSea/seaport/tree/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/lib/OrderCombiner.sol#L300

https://github.com/ProjectOpenSea/seaport/tree/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/lib/OrderCombiner.sol#L763



```solidity
700: Execution memory execution = executions[i];
738: AdvancedOrder memory advancedOrder = advancedOrders[i];
300: OfferItem memory offerItem = offer[j];
763: OfferItem memory offerItem = offer[j];

```

https://github.com/ProjectOpenSea/seaport/tree/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/lib/OrderCombiner.sol#L700

https://github.com/ProjectOpenSea/seaport/tree/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/lib/OrderCombiner.sol#L738

https://github.com/ProjectOpenSea/seaport/tree/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/lib/OrderCombiner.sol#L300

https://github.com/ProjectOpenSea/seaport/tree/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/lib/OrderCombiner.sol#L763



```solidity
1001: Fulfillment memory fulfillment = fulfillments[i];

```

https://github.com/ProjectOpenSea/seaport/tree/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/lib/OrderCombiner.sol#L1001

```solidity
209: OfferItem memory offerItem = orderParameters.offer[i];

```

https://github.com/ProjectOpenSea/seaport/tree/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/lib/OrderFulfiller.sol#L209

```solidity
755: Order memory order = orders[i];

```

https://github.com/ProjectOpenSea/seaport/tree/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/lib/OrderValidator.sol#L755




