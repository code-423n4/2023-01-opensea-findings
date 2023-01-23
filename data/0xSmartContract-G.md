| Number | Optimization Details | Context |
|:--:|:-------| :-----:|
| [G-01] | Structs can be packed into fewer storage slots |4 |
| [G-02] |Using ``delete``  instead of setting struct``0`` saves gas (~70 gas)| 2 |
| [G-03] |Using ``delete`` instead of setting ``address(0)`` saves gas  (~70  gas) |4 |
| [G-04] | ] Setting the _constructor_ to `payable` (13 gas)  |14 |
| [G-05] |Optimize names to save gas (22 gas) |All contracts|
| [G-06] |Functions guaranteed to revert_ when callled by normal users can be marked `payable` (21 gas) |3|

Total 6 issues


### [G-01] Structs can be packed into fewer storage slots

One slot can be saved in the  ``OrderComponents``, ``BasicOrderParameters``,  ``OrderParameters`` and ``ZoneParameters`` structures in the ``ConsiderationStructs.sol`` contract.

4 results 1 file:
**_The `OrderComponents` struct can be packed into ``one slot`` less slot as suggested below._**
```diff
contracts\lib\ConsiderationStructs.sol:
  26: struct OrderComponents {
  27:     address offerer;
  28:     address zone;
  29:     OfferItem[] offer;
  30:     ConsiderationItem[] consideration;
  31:     OrderType orderType;
- 32:     uint256 startTime;
+ 32:     uint128 startTime;
- 33:     uint256 endTime;
+ 33:     uint128 endTime;
  34:     bytes32 zoneHash;
  35:     uint256 salt;
  36:     bytes32 conduitKey;
  37:     uint256 counter;
  38: }
```
https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/lib/ConsiderationStructs.sol#L26-L38

**_The `BasicOrderParameters` struct can be packed into ``one slot`` less slot as suggested below._**
```diff
contracts\lib\ConsiderationStructs.sol:
  106: struct BasicOrderParameters {
  107:     // calldata offset
  108:     address considerationToken; // 0x24
  109:     uint256 considerationIdentifier; // 0x44 
  110:     uint256 considerationAmount; // 0x64  
  111:     address payable offerer; // 0x84
  112:     address zone; // 0xa4
  113:     address offerToken; // 0xc4	
  114:     uint256 offerIdentifier; // 0xe4	
  115:     uint256 offerAmount; // 0x104	
  116:     BasicOrderType basicOrderType; // 0x124 	
- 117:     uint256 startTime; // 0x144 	
+ 117:     uint128 startTime; // 0x144
- 118:     uint256 endTime; // 0x164
+ 118:     uint128 endTime; // 0x144
  119:     bytes32 zoneHash; // 0x164 
  120:     uint256 salt; // 0x134	
  121:     bytes32 offererConduitKey; // 0x1a4
  122:     bytes32 fulfillerConduitKey; // 0x1c4 
  123:     uint256 totalOriginalAdditionalRecipients; // 0x1e4
  124:     AdditionalRecipient[] additionalRecipients; // 0x204 
  125:     bytes signature; // 0x224	
  126:     // Total length, excluding dynamic array data: 0x244 0x264 (548) 	
  127: }
```
https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/lib/ConsiderationStructs.sol#L104-L125

**_The ` OrderParameters` struct can be packed into ``one slot`` less slot as suggested below._**
```diff
contracts\lib\ConsiderationStructs.sol:
  149: struct OrderParameters {
  150:     address offerer; // 0x00
  151:     address zone; // 0x20
  152:     OfferItem[] offer; // 0x40
  153:     ConsiderationItem[] consideration; // 0x60
  154:     OrderType orderType; // 0x80
- 155:     uint256 startTime; // 0xa0
+ 155:     uint128 startTime; // 0xa0
- 156:     uint256 endTime; // 0xc0
+ 156:     uint128 endTime; // 0xa0
  157:     bytes32 zoneHash; // 0xc0
  158:     uint256 salt; // 0xe0
  159:     bytes32 conduitKey; // 0x100
  160:     uint256 totalOriginalConsiderationItems; // 0x120
  161:     // offer.length                          // 0x140
  162: }
```
https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/lib/ConsiderationStructs.sol#L143-L156


**_The ` ZoneParameters` struct can be packed into ``one slot`` less slot as suggested below._**
```diff
contracts\lib\ConsiderationStructs.sol:
  262: struct ZoneParameters {
  263:     bytes32 orderHash;
  264:     address fulfiller;
  265:     address offerer;
  266:     SpentItem[] offer;
  267:     ReceivedItem[] consideration;
  268:     bytes extraData;
  269:     bytes32[] orderHashes;
- 270:     uint256 startTime;
+ 270:     uint128 startTime;
- 271:     uint256 endTime;
+ 271:     uint128 endTime;
  272:     bytes32 zoneHash;
  273: }
```
https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/lib/ConsiderationStructs.sol#L256-L267

A total of 4 slots have been won.


### [G-02] Using ``delete``  instead of setting struct``0`` saves gas (~70 gas)

2 results - 1 file:
```solidity
contracts\lib\OrderCombiner.sol:
  239:    advancedOrder.numerator = 0;

  258:    advancedOrder.numerator = 0;
```
https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/lib/OrderCombiner.sol#L239
https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/lib/OrderCombiner.sol#L258

**Recommendation code:**
```diff
contracts\lib\OrderCombiner.sol:
- 239:    advancedOrder.numerator = 0;
+ 239:    delete advancedOrder.numerator;
```

### [G-03] Using ``delete`` instead of setting ``address(0)`` saves gas  (~70  gas)

4 results - 1 file:
```solidity
contracts\lib\FulfillmentApplier.sol:
   78:    considerationExecution.offerer = address(0);

   79:    considerationExecution.item.recipient = payable(0);

  212:    execution.offerer = address(0);

  213:    execution.item.recipient = payable(0);
```
https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/lib/FulfillmentApplier.sol#L78-L79
https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/lib/FulfillmentApplier.sol#L212-L213


**Proof Of Concepts:**
```solidity
contract Example {
    struct Execution {
        address payable offerer;
    }

    Execution execution;

    function setValueStorage() public {
        execution = Execution(payable(0xCA35b7d915458EF540aDe6068dFe2F44E8fa733c));
    }

    //  use for empty value Slot: 23456 gas
    //	use for non empty value Slot: 21456 gas
    function reset() public {
        delete execution.offerer;
    }

    // use for empty value Slot: 23525 gas
    // use for non empty value Slot: 21525 gas 
    function setToZero() public  {
        execution.offerer = payable(0);
    }

    function get() public view returns (address) {
        return execution.offerer;
    }
}
```

### [G-04] Setting the _constructor_ to `payable` (13 gas)

You can cut out 10 opcodes in the creation-time EVM bytecode if you declare a constructor payable. Making the constructor payable eliminates the need for an initial check of ```msg.value == 0``` and saves ```13 gas``` on deployment with no security risks.

14 results - 14 files
```solidity
contracts\Seaport.sol:
  93:    constructor(address conduitController) Consideration(conduitController) {}
```
https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/Seaport.sol#L93

```solidity
contracts\conduit\Conduit.sol:
  73:    constructor() {
```
https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/conduit/Conduit.sol#L73

```solidity
contracts\lib\Assertions.sol:
  35:    constructor(
  36         address conduitController
  37     ) GettersAndDerivers(conduitController) {}
```
https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/lib/Assertions.sol#L35-L37

```solidity
contracts\lib\BasicOrderFulfiller.sol:
  41:    constructor(address conduitController) OrderValidator(conduitController) {}
```
https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/lib/BasicOrderFulfiller.sol#L41

```solidity
contracts\lib\Consideration.sol:
  50:    constructor(address conduitController) OrderCombiner(conduitController) {}
```
https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/lib/Consideration.sol#L50

```solidity
contracts\lib\ConsiderationBase.sol:
  56:    constructor(address conduitController) {
```
https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/lib/ConsiderationBase.sol#L56

```solidity
contracts\lib\Executor.sol:
  35:    constructor(address conduitController) Verifiers(conduitController) {}
```
https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/lib/Executor.sol#L35

```solidity
contracts\lib\GettersAndDerivers.sol:
  25:    constructor(
  26         address conduitController
  27     ) ConsiderationBase(conduitController) {}
```
https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/lib/GettersAndDerivers.sol#L25-L27

```solidity
contracts\lib\OrderCombiner.sol:
  41:    constructor(address conduitController) OrderFulfiller(conduitController) {}
```
https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/lib/OrderCombiner.sol#L41

```solidity  
contracts\lib\OrderFulfiller.sol:
  45:     constructor(
  46         address conduitController
  47     ) BasicOrderFulfiller(conduitController) {}
```
https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/lib/OrderFulfiller.sol#L45-L47

```solidity
contracts\lib\OrderValidator.sol:
  55:     constructor(address conduitController) Executor(conduitController) {}
```
https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/lib/OrderValidator.sol#L55

```solidity
contracts\lib\ReentrancyGuard.sol:
  23:     constructor() {
```
https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/lib/ReentrancyGuard.sol#L23

```solidity
contracts\lib\TypehashDirectory.sol:
  30:     constructor() {
```
https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/lib/TypehashDirectory.sol#L30

```solidity
contracts\lib\Verifiers.sol:
  26:     constructor(address conduitController) Assertions(conduitController) {}
```
https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/lib/Verifiers.sol#L26

**Recommendation:**
Set the constructor to ```payable```


### [G-05] Optimize names to save gas (22 gas)

Contracts most called functions could simply save gas by function ordering via ```Method ID```. Calling a function at runtime will be cheaper if the function is positioned earlier in the order (has a relatively lower Method ID) because ```22 gas``` are added to the cost of a function for every position that came before it. The caller can save on gas if you prioritize most called functions. 

**Context:** 
All Contracts


**Recommendation:** 
Find a lower ```method ID``` name for the most called functions for example Call() vs. Call1() is cheaper by ```22 gas```
For example, the function IDs in the ``` Executor.sol ``` contract will be the most used; A lower method ID may be given.

**Proof of Consept:**
https://medium.com/joyso/solidity-how-does-function-name-affect-gas-consumption-in-smart-contract-47d270d8ac92

Executor.sol function names can be named and sorted according to METHOD ID

```js
Sighash   |   Function Signature
========================
40142041  =>  _transferNativeTokens(address,uint256)
47991382  =>  _trigger(bytes32,bytes)
91353327  =>  _transferERC1155(address,address,address,uint256,uint256,bytes32,bytes)
26bb4f83  =>  _transfer(ReceivedItem,address,bytes32,bytes)
4d0abe39  =>  _transferIndividual721Or1155Item(ItemType,address,address,address,uint256,uint256,bytes32)
1eaee91a  =>  _transferERC20(address,address,address,uint256,bytes32,bytes)
69c575d9  =>  _transferERC721(address,address,address,uint256,uint256,bytes32,bytes)
d2e316d3  =>  _triggerIfArmedAndNotAccumulatable(bytes,bytes32)
0ac8a5bc  =>  _triggerIfArmed(bytes)
0b476195  =>  _callConduitUsingOffsets(bytes32,uint256,uint256)
4c12903a  =>  _getAccumulatorConduitKey(bytes)
376ad5b8  =>  _insert(bytes32,bytes,ConduitItemType,address,address,address,uint256,uint256)
```

### [G-06]  Functions guaranteed to revert_ when callled by normal users can be marked `payable` (21 gas)

If a function modifier or require such as onlyOwner-admin is used, the function will revert if a normal user tries to pay the function. Marking the function as payable will lower the gas cost for legitimate callers because the compiler will not include checks for whether a payment was provided. The extra opcodes avoided are CALLVALUE(2), DUP1(3), ISZERO(3), PUSH2(3), JUMPI(10), PUSH1(3), DUP1(3), REVERT(0), JUMPDEST(1), POP(2) which costs an average of about 21 gas per call to the function, in addition to the extra deployment cost.


3 results - 1 file
```solidity
contracts\conduit\Conduit.sol:
  92     function execute(
  93         ConduitTransfer[] calldata transfers
  94:     ) external override onlyOpenChannel returns (bytes4 magicValue) {

  127     function executeBatch1155(
  128         ConduitBatch1155Transfer[] calldata batchTransfers
  129     ) external override onlyOpenChannel returns (bytes4 magicValue) {

  154     function executeWithBatch1155(
  155         ConduitTransfer[] calldata standardTransfers,
  156         ConduitBatch1155Transfer[] calldata batchTransfers
  157:     ) external override onlyOpenChannel returns (bytes4 magicValue) {
```
https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/conduit/Conduit.sol#L94
https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/conduit/Conduit.sol#L129
https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/conduit/Conduit.sol#L157


**Recommendation:**
Functions guaranteed to revert when called by normal users can be marked payable  (for only ```onlyOpenChannelonly``` functions)