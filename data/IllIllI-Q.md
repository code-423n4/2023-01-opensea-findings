

## Summary

### Non-critical Issues
| |Issue|Instances|
|-|:-|:-:|
| [N&#x2011;01] | Import declarations should import specific identifiers, rather than the whole file | 28 | 
| [N&#x2011;02] | Adding a `return` statement when the function defines a named return variable, is redundant | 4 | 
| [N&#x2011;03] | Non-assembly method available | 3 | 
| [N&#x2011;04] | `constant`s should be defined rather than using magic numbers | 45 | 
| [N&#x2011;05] | Events that mark critical parameter changes should contain both the old and the new value | 1 | 
| [N&#x2011;06] | Typos | 2 | 
| [N&#x2011;07] | File is missing NatSpec | 10 | 
| [N&#x2011;08] | NatSpec is incomplete | 2 | 
| [N&#x2011;09] | Not using the named return variables anywhere in the function is confusing | 13 | 
| [N&#x2011;10] | Large assembly blocks should have extensive comments | 6 | 
| [N&#x2011;11] | Contracts should have full test coverage | 1 | 
| [N&#x2011;12] | Function ordering does not follow the Solidity style guide | 1 | 
| [N&#x2011;13] | Interfaces should be indicated with an `I` prefix in the contract name | 9 | 

Total: 125 instances over 13 issues





## Non-critical Issues

### [N&#x2011;01]  Import declarations should import specific identifiers, rather than the whole file
Using import declarations of the form `import {<identifier_name>} from "some/file.sol"` avoids polluting the symbol namespace making flattened files smaller, and speeds up compilation

*There are 28 instances of this issue:*

```solidity
File: contracts/conduit/Conduit.sol

15:   import "./lib/ConduitConstants.sol";

```
https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/conduit/Conduit.sol#L15

```solidity
File: contracts/lib/AmountDeriver.sol

8:    import "./ConsiderationConstants.sol";

```
https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/lib/AmountDeriver.sol#L8

```solidity
File: contracts/lib/Assertions.sol

14:   import "./ConsiderationErrors.sol";

```
https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/lib/Assertions.sol#L14

```solidity
File: contracts/lib/BasicOrderFulfiller.sol

23:   import "./ConsiderationErrors.sol";

```
https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/lib/BasicOrderFulfiller.sol#L23

```solidity
File: contracts/lib/ConsiderationBase.sol

12:   import "./ConsiderationConstants.sol";

```
https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/lib/ConsiderationBase.sol#L12

```solidity
File: contracts/lib/ConsiderationDecoder.sol

20:   import "./ConsiderationConstants.sol";

22:   import "../helpers/PointerLibraries.sol";

```
https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/lib/ConsiderationDecoder.sol#L20

```solidity
File: contracts/lib/ConsiderationEncoder.sol

4:    import "./ConsiderationConstants.sol";

20:   import "../helpers/PointerLibraries.sol";

```
https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/lib/ConsiderationEncoder.sol#L4

```solidity
File: contracts/lib/ConsiderationErrors.sol

6:    import "./ConsiderationConstants.sol";

```
https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/lib/ConsiderationErrors.sol#L6

```solidity
File: contracts/lib/Consideration.sol

23:   import "../helpers/PointerLibraries.sol";

25:   import "./ConsiderationConstants.sol";

```
https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/lib/Consideration.sol#L23

```solidity
File: contracts/lib/CounterManager.sol

10:   import "./ConsiderationConstants.sol";

```
https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/lib/CounterManager.sol#L10

```solidity
File: contracts/lib/CriteriaResolution.sol

15:   import "./ConsiderationErrors.sol";

17:   import "../helpers/PointerLibraries.sol";

```
https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/lib/CriteriaResolution.sol#L15

```solidity
File: contracts/lib/Executor.sol

16:   import "./ConsiderationConstants.sol";

18:   import "./ConsiderationErrors.sol";

```
https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/lib/Executor.sol#L16

```solidity
File: contracts/lib/FulfillmentApplier.sol

16:   import "./ConsiderationErrors.sol";

```
https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/lib/FulfillmentApplier.sol#L16

```solidity
File: contracts/lib/GettersAndDerivers.sol

8:    import "./ConsiderationConstants.sol";

```
https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/lib/GettersAndDerivers.sol#L8

```solidity
File: contracts/lib/LowLevelHelpers.sol

4:    import "./ConsiderationConstants.sol";

```
https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/lib/LowLevelHelpers.sol#L4

```solidity
File: contracts/lib/OrderCombiner.sol

23:   import "./ConsiderationErrors.sol";

```
https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/lib/OrderCombiner.sol#L23

```solidity
File: contracts/lib/OrderFulfiller.sol

23:   import "./ConsiderationErrors.sol";

```
https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/lib/OrderFulfiller.sol#L23

```solidity
File: contracts/lib/OrderValidator.sol

19:   import "./ConsiderationErrors.sol";

```
https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/lib/OrderValidator.sol#L19

```solidity
File: contracts/lib/ReentrancyGuard.sol

8:    import "./ConsiderationErrors.sol";

```
https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/lib/ReentrancyGuard.sol#L8

```solidity
File: contracts/lib/SignatureVerification.sol

12:   import "./ConsiderationErrors.sol";

```
https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/lib/SignatureVerification.sol#L12

```solidity
File: contracts/lib/TokenTransferrer.sol

4:    import "./TokenTransferrerConstants.sol";

```
https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/lib/TokenTransferrer.sol#L4

```solidity
File: contracts/lib/Verifiers.sol

10:   import "./ConsiderationErrors.sol";

```
https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/lib/Verifiers.sol#L10

```solidity
File: contracts/lib/ZoneInteraction.sol

16:   import "./ConsiderationEncoder.sol";

```
https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/lib/ZoneInteraction.sol#L16

### [N&#x2011;02]  Adding a `return` statement when the function defines a named return variable, is redundant

*There are 4 instances of this issue:*

```solidity
File: contracts/lib/AmountDeriver.sol

87:               return amount;

```
https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/lib/AmountDeriver.sol#L87

```solidity
File: contracts/lib/BasicOrderFulfiller.sol

902:          return orderHash;

```
https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/lib/BasicOrderFulfiller.sol#L902

```solidity
File: contracts/lib/FulfillmentApplier.sol

143:          return execution; // Execution(considerationItem, offerer, conduitKey);

```
https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/lib/FulfillmentApplier.sol#L143

```solidity
File: contracts/lib/OrderCombiner.sol

1047:         return executions;

```
https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/lib/OrderCombiner.sol#L1047

### [N&#x2011;03]  Non-assembly method available 
`assembly{ id := chainid() }` => `uint256 id = block.chainid`, `assembly { size := extcodesize() }` => `uint256 size = address().code.length`, `assembly { hash := extcodehash() }` => `bytes32 hash = address().codehash`
There are some automated tools that will flag a project as having higher complexity if there is inline-assembly, so it's best to avoid using it where it's not necessary

*There are 3 instances of this issue:*

```solidity
File: contracts/lib/ConsiderationBase.sol

110:              mstore(EIP712_domainData_chainId_offset, chainid())

```
https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/lib/ConsiderationBase.sol#L110

```solidity
File: contracts/lib/TokenTransferrer.sol

274:              if iszero(extcodesize(token)) {

414:              if iszero(extcodesize(token)) {

```
https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/lib/TokenTransferrer.sol#L274

### [N&#x2011;04]  `constant`s should be defined rather than using magic numbers
Even [assembly](https://github.com/code-423n4/2022-05-opensea-seaport/blob/9d7ce4d08bf3c3010304a0476a785c70c0e90ae7/contracts/lib/TokenTransferrer.sol#L35-L39) can benefit from using readable constants instead of hex/numeric literals

*There are 45 instances of this issue:*

```solidity
File: contracts/lib/BasicOrderFulfiller.sol

/// @audit 3
86:               orderType := and(basicOrderType, 3)

/// @audit 2
89:               route := shr(2, basicOrderType)

/// @audit 3
127:                  offerTypeIsAdditionalRecipientsType := gt(route, 3)

```
https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/lib/BasicOrderFulfiller.sol#L86

```solidity
File: contracts/lib/ConsiderationConstants.sol

/// @audit 4
244:  address constant IdentityPrecompile = address(4);

```
https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/lib/ConsiderationConstants.sol#L244

```solidity
File: contracts/lib/ConsiderationDecoder.sol

/// @audit 0xffff
872:                              gt(or(offerLength, considerationLength), 0xffff),

```
https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/lib/ConsiderationDecoder.sol#L872

```solidity
File: contracts/lib/CounterManager.sol

/// @audit 1
43:                   blockhash(sub(number(), 1))

```
https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/lib/CounterManager.sol#L43

```solidity
File: contracts/lib/CriteriaResolution.sol

/// @audit 3
/// @audit 4
229:              newItemType := sub(3, eq(itemType, 4))

/// @audit 3
253:              withCriteria := gt(itemType, 3)

```
https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/lib/CriteriaResolution.sol#L229

```solidity
File: contracts/lib/FulfillmentApplier.sol

/// @audit 1
326:                              shl(1, lt(newAmount, amount)),

/// @audit 1
437:                  if eq(errorBuffer, 1) {

/// @audit 1
601:                              shl(1, lt(newAmount, amount)),

/// @audit 1
701:                  if eq(errorBuffer, 1) {

```
https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/lib/FulfillmentApplier.sol#L326

```solidity
File: contracts/lib/OrderCombiner.sol

/// @audit 32
220:              terminalMemoryOffset = (totalOrders + 1) * 32;

/// @audit 32
/// @audit 32
230:              for (uint256 i = 32; i < terminalMemoryOffset; i += 32) {

/// @audit 4
292:                          let isNonContract := lt(orderType, 4)

/// @audit 32
/// @audit 32
451:              for (uint256 i = 32; i < terminalMemoryOffset; i += 32) {

```
https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/lib/OrderCombiner.sol#L220

```solidity
File: contracts/lib/OrderFulfiller.sol

/// @audit 4
264:                          lt(orderType, 4),

```
https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/lib/OrderFulfiller.sol#L264

```solidity
File: contracts/lib/OrderValidator.sol

/// @audit 1
157:                  invalidFraction := xor(mul(numerator, denominator), 1)

/// @audit 1
237:              } 1 {

/// @audit 1
253:                  if eq(denominator, 1) {

/// @audit 3
392:              if and(gt(itemType, 3), iszero(identifier)) {

/// @audit 3
/// @audit 4
394:                  itemType := sub(3, eq(itemType, 4))

/// @audit 4
683:                              eq(orderType, 4),

/// @audit 1
902:                  iszero(and(orderType, 1))

```
https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/lib/OrderValidator.sol#L157

```solidity
File: contracts/lib/SignatureVerification.sol

/// @audit 1
73:                   if iszero(gt(lenDiff, 1)) {

/// @audit 1
229:                          if gt(sub(ECDSA_MaxLength, signatureLength), 1) {

```
https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/lib/SignatureVerification.sol#L73

```solidity
File: contracts/lib/TokenTransferrer.sol

/// @audit 1
/// @audit 31
75:                       and(eq(mload(0), 1), gt(returndatasize(), 31)),

/// @audit 1
370:                  mstore(TokenTransferGenericFailure_error_amount_ptr, 1)

```
https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/lib/TokenTransferrer.sol#L75

```solidity
File: contracts/lib/TypehashDirectory.sol

/// @audit 1
86:                   add(shl(OneWordShift, MaxTreeHeight), 1)

```
https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/lib/TypehashDirectory.sol#L86

```solidity
File: contracts/lib/Verifiers.sol

/// @audit 1
165:              let signatureLength := sub(ECDSA_MaxLength, and(fullLength, 1))

/// @audit 1
184:              let scratchPtr1 := shl(OneWordShift, and(key, 1))

/// @audit 1
195:                  let scratchPtr := shl(OneWordShift, and(shr(i, key), 1))

```
https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/lib/Verifiers.sol#L165

```solidity
File: contracts/lib/ZoneInteraction.sol

/// @audit 2
/// @audit 3
146:                  or(eq(orderType, 2), eq(orderType, 3)),

```
https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/lib/ZoneInteraction.sol#L146

```solidity
File: contracts/Seaport.sol

/// @audit 0x20
/// @audit 0x20
104:              mstore(0x20, 0x20)

/// @audit 0x47
/// @audit 0x07536561706f7274
105:              mstore(0x47, 0x07536561706f7274)

/// @audit 0x20
/// @audit 0x60
106:              return(0x20, 0x60)

```
https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/Seaport.sol#L104

### [N&#x2011;05]  Events that mark critical parameter changes should contain both the old and the new value
This should especially be done if the new value is not required to be different from the old value

*There is 1 instance of this issue:*

```solidity
File: contracts/conduit/Conduit.sol

/// @audit updateChannel()
202:          emit ChannelUpdated(channel, isOpen);

```
https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/conduit/Conduit.sol#L202

### [N&#x2011;06]  Typos

*There are 2 instances of this issue:*

```solidity
File: contracts/lib/ConsiderationEncoder.sol

/// @audit paramaters
345:  // Get the memory pointer to the order paramaters struct.

```
https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/lib/ConsiderationEncoder.sol#L345

```solidity
File: contracts/lib/TypehashDirectory.sol

/// @audit writter
31:   // Declare an array where each type hash will be writter.

```
https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/lib/TypehashDirectory.sol#L31

### [N&#x2011;07]  File is missing NatSpec

*There are 10 instances of this issue:*

```solidity
File: contracts/conduit/lib/ConduitConstants.sol


```
https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/conduit/lib/ConduitConstants.sol

```solidity
File: contracts/conduit/lib/ConduitEnums.sol


```
https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/conduit/lib/ConduitEnums.sol

```solidity
File: contracts/conduit/lib/ConduitStructs.sol


```
https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/conduit/lib/ConduitStructs.sol

```solidity
File: contracts/interfaces/AbridgedTokenInterfaces.sol


```
https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/interfaces/AbridgedTokenInterfaces.sol

```solidity
File: contracts/interfaces/ContractOffererInterface.sol


```
https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/interfaces/ContractOffererInterface.sol

```solidity
File: contracts/interfaces/EIP1271Interface.sol


```
https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/interfaces/EIP1271Interface.sol

```solidity
File: contracts/interfaces/IERC721Receiver.sol


```
https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/interfaces/IERC721Receiver.sol

```solidity
File: contracts/interfaces/ZoneInterface.sol


```
https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/interfaces/ZoneInterface.sol

```solidity
File: contracts/lib/ConsiderationEnums.sol


```
https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/lib/ConsiderationEnums.sol

```solidity
File: contracts/lib/TokenTransferrerConstants.sol


```
https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/lib/TokenTransferrerConstants.sol

### [N&#x2011;08]  NatSpec is incomplete

*There are 2 instances of this issue:*

```solidity
File: contracts/interfaces/TransferHelperInterface.sol

/// @audit Missing: '@return'
13         * @param conduitKey  The key of the conduit performing the bulk transfer.
14         */
15        function bulkTransfer(
16            TransferHelperItemsWithRecipient[] calldata items,
17            bytes32 conduitKey
18:       ) external returns (bytes4);

```
https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/interfaces/TransferHelperInterface.sol#L13-L18

```solidity
File: contracts/lib/ConsiderationEncoder.sol

/// @audit Missing: '@param dst'
54        /**
55         * @dev Takes a bytes array in memory and copies it to a new location in
56         *      memory.
57         *
58         * @param src A memory pointer referencing the bytes array to be copied (and
59         *            pointing to the length of the bytes array).
60         * @param src A memory pointer referencing the location in memory to copy
61         *            the bytes array to (and pointing to the length of the copied
62         *            bytes array).
63         *
64         * @return size The size of the bytes array.
65         */
66        function _encodeBytes(
67            MemoryPointer src,
68            MemoryPointer dst
69:       ) internal view returns (uint256 size) {

```
https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/lib/ConsiderationEncoder.sol#L54-L69

### [N&#x2011;09]  Not using the named return variables anywhere in the function is confusing
Consider changing the variable to be an unnamed one

*There are 13 instances of this issue:*

```solidity
File: contracts/lib/Consideration.sol

/// @audit isValidated
/// @audit isCancelled
/// @audit totalFilled
/// @audit totalSize
697       function getOrderStatus(
698           bytes32 orderHash
699       )
700           external
701           view
702           override
703           returns (
704               bool isValidated,
705               bool isCancelled,
706               uint256 totalFilled,
707:              uint256 totalSize

/// @audit version
/// @audit domainSeparator
/// @audit conduitController
735       function information()
736           external
737           view
738           override
739           returns (
740               string memory version,
741               bytes32 domainSeparator,
742:              address conduitController

```
https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/lib/Consideration.sol#L697-L707

```solidity
File: contracts/lib/OrderValidator.sol

/// @audit numerator
/// @audit denominator
472       function _getGeneratedOrder(
473           OrderParameters memory orderParameters,
474           bytes memory context,
475           bool revertOnInvalid
476       )
477           internal
478:          returns (bytes32 orderHash, uint256 numerator, uint256 denominator)

/// @audit isValidated
/// @audit isCancelled
/// @audit totalFilled
/// @audit totalSize
828       function _getOrderStatus(
829           bytes32 orderHash
830       )
831           internal
832           view
833           returns (
834               bool isValidated,
835               bool isCancelled,
836               uint256 totalFilled,
837:              uint256 totalSize

```
https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/lib/OrderValidator.sol#L472-L478

### [N&#x2011;10]  Large assembly blocks should have extensive comments
Assembly blocks are take a lot more time to audit than normal Solidity code, and often have gotchas and side-effects that the Solidity versions of the same code do not. Consider adding more comments explaining what is being done in every step of the assembly code

*There are 6 instances of this issue:*

```solidity
File: contracts/helpers/PointerLibraries.sol

215           assembly {
216               let success := staticcall(
217                   gas(),
218                   IdentityPrecompileAddress,
219                   src,
220                   size,
221                   dst,
222                   size
223               )
224               if or(iszero(success), iszero(returndatasize())) {
225                   revert(0, 0)
226               }
227:          }

```
https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/helpers/PointerLibraries.sol#L215-L227

```solidity
File: contracts/lib/ConsiderationDecoder.sol

563           assembly {
564               let arrLength := and(calldataload(cdPtrLength), OffsetOrLengthMask)
565   
566               // Get the current free memory pointer.
567               mPtrLength := mload(FreeMemoryPointerSlot)
568   
569               mstore(mPtrLength, arrLength)
570               let mPtrHead := add(mPtrLength, OneWord)
571               let mPtrTail := add(mPtrHead, shl(OneWordShift, arrLength))
572               let mPtrTailNext := mPtrTail
573               calldatacopy(
574                   mPtrTail,
575                   add(cdPtrLength, OneWord),
576                   shl(FulfillmentComponent_mem_tail_size_shift, arrLength)
577               )
578               let mPtrHeadNext := mPtrHead
579               for {
580   
581               } lt(mPtrHeadNext, mPtrTail) {
582   
583               } {
584                   mstore(mPtrHeadNext, mPtrTailNext)
585                   mPtrHeadNext := add(mPtrHeadNext, OneWord)
586                   mPtrTailNext := add(
587                       mPtrTailNext,
588                       FulfillmentComponent_mem_tail_size
589                   )
590               }
591   
592               // Update the free memory pointer.
593               mstore(FreeMemoryPointerSlot, mPtrTailNext)
594:          }

```
https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/lib/ConsiderationDecoder.sol#L563-L594

```solidity
File: contracts/lib/Executor.sol

622               assembly {
623                   mstore(accumulator, AccumulatorArmed) // "arm" the accumulator.
624                   mstore(add(accumulator, Accumulator_conduitKey_ptr), conduitKey)
625                   mstore(add(accumulator, Accumulator_selector_ptr), selector)
626                   mstore(
627                       add(accumulator, Accumulator_array_offset_ptr),
628                       Accumulator_array_offset
629                   )
630                   mstore(add(accumulator, Accumulator_array_length_ptr), elements)
631:              }

644           assembly {
645               let itemPointer := sub(
646                   add(accumulator, mul(elements, Conduit_transferItem_size)),
647                   Accumulator_itemSizeOffsetDifference
648               )
649               mstore(itemPointer, itemType)
650               mstore(add(itemPointer, Conduit_transferItem_token_ptr), token)
651               mstore(add(itemPointer, Conduit_transferItem_from_ptr), from)
652               mstore(add(itemPointer, Conduit_transferItem_to_ptr), to)
653               mstore(
654                   add(itemPointer, Conduit_transferItem_identifier_ptr),
655                   identifier
656               )
657               mstore(add(itemPointer, Conduit_transferItem_amount_ptr), amount)
658:          }

```
https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/lib/Executor.sol#L622-L631

```solidity
File: contracts/lib/GettersAndDerivers.sol

326           assembly {
327               mstore(information_version_offset, information_version_cd_offset)
328               mstore(information_domainSeparator_offset, domainSeparator)
329               mstore(information_conduitController_offset, conduitController)
330               mstore(information_versionLengthPtr, information_versionWithLength)
331               return(information_version_offset, information_length)
332:          }

```
https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/lib/GettersAndDerivers.sol#L326-L332

```solidity
File: contracts/lib/Verifiers.sol

122           assembly {
123               validLength := and(
124                   lt(
125                       sub(signatureLength, BulkOrderProof_minSize),
126                       BulkOrderProof_rangeSize
127                   ),
128                   lt(
129                       and(
130                           add(
131                               signatureLength,
132                               BulkOrderProof_lengthAdjustmentBeforeMask
133                           ),
134                           AlmostOneWord
135                       ),
136                       BulkOrderProof_lengthRangeAfterMask
137                   )
138               )
139:          }

```
https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/lib/Verifiers.sol#L122-L139

### [N&#x2011;11]  Contracts should have full test coverage
While 100% code coverage does not guarantee that there are no bugs, it often will catch easy-to-find bugs, and will ensure that there are fewer regressions when the code invariably has to be modified. Furthermore, in order to get full coverage, code authors will often have to re-organize their code so that it is more modular, so that each component can be tested separately, which reduces interdependencies between modules and layers, and makes for code that is easier to reason about and audit.

*There is 1 instance of this issue:*

```solidity
File: Various Files


```

### [N&#x2011;12]  Function ordering does not follow the Solidity style guide
According to the [Solidity style guide](https://docs.soliditylang.org/en/v0.8.17/style-guide.html#order-of-functions), functions should be laid out in the following order :`constructor()`, `receive()`, `fallback()`, `external`, `public`, `internal`, `private`, but the cases below do not follow this pattern

*There is 1 instance of this issue:*

```solidity
File: contracts/helpers/PointerLibraries.sol

/// @audit setFreeMemoryPointer() came earlier
48        function lt(
49            CalldataPointer a,
50            CalldataPointer b
51:       ) internal pure returns (bool c) {

```
https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/helpers/PointerLibraries.sol#L48-L51

### [N&#x2011;13]  Interfaces should be indicated with an `I` prefix in the contract name

*There are 9 instances of this issue:*

```solidity
File: contracts/interfaces/AmountDerivationErrors.sol

9:    interface AmountDerivationErrors {

```
https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/interfaces/AmountDerivationErrors.sol#L9

```solidity
File: contracts/interfaces/ConsiderationEventsAndErrors.sol

15:   interface ConsiderationEventsAndErrors {

```
https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/interfaces/ConsiderationEventsAndErrors.sol#L15

```solidity
File: contracts/interfaces/CriteriaResolutionErrors.sol

12:   interface CriteriaResolutionErrors {

```
https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/interfaces/CriteriaResolutionErrors.sol#L12

```solidity
File: contracts/interfaces/FulfillmentApplicationErrors.sol

12:   interface FulfillmentApplicationErrors {

```
https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/interfaces/FulfillmentApplicationErrors.sol#L12

```solidity
File: contracts/interfaces/ReentrancyErrors.sol

9:    interface ReentrancyErrors {

```
https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/interfaces/ReentrancyErrors.sol#L9

```solidity
File: contracts/interfaces/SignatureVerificationErrors.sol

10:   interface SignatureVerificationErrors {

```
https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/interfaces/SignatureVerificationErrors.sol#L10

```solidity
File: contracts/interfaces/TokenTransferrerErrors.sol

7:    interface TokenTransferrerErrors {

```
https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/interfaces/TokenTransferrerErrors.sol#L7

```solidity
File: contracts/interfaces/TransferHelperErrors.sol

7:    interface TransferHelperErrors {

```
https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/interfaces/TransferHelperErrors.sol#L7

```solidity
File: contracts/interfaces/ZoneInteractionErrors.sol

9:    interface ZoneInteractionErrors {

```
https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/interfaces/ZoneInteractionErrors.sol#L9


___

## Excluded findings
These findings are excluded from awards calculations because there are publicly-available automated tools that find them. The valid ones appear here for completeness

## Summary

### Non-critical Issues
| |Issue|Instances|
|-|:-|:-:|
| [N&#x2011;01] | Non-library/interface files should use fixed compiler versions, not floating ones | 24 | 
| [N&#x2011;02] | Event is missing `indexed` fields | 6 | 

Total: 30 instances over 2 issues





## Non-critical Issues

### [N&#x2011;01]  Non-library/interface files should use fixed compiler versions, not floating ones

*There are 24 instances of this issue:*

```solidity
File: contracts/conduit/Conduit.sol

/// @audit (valid but excluded finding)
2:    pragma solidity ^0.8.13;

```
https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/conduit/Conduit.sol#L2

```solidity
File: contracts/lib/AmountDeriver.sol

/// @audit (valid but excluded finding)
2:    pragma solidity ^0.8.17;

```
https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/lib/AmountDeriver.sol#L2

```solidity
File: contracts/lib/Assertions.sol

/// @audit (valid but excluded finding)
2:    pragma solidity ^0.8.17;

```
https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/lib/Assertions.sol#L2

```solidity
File: contracts/lib/BasicOrderFulfiller.sol

/// @audit (valid but excluded finding)
2:    pragma solidity ^0.8.17;

```
https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/lib/BasicOrderFulfiller.sol#L2

```solidity
File: contracts/lib/ConsiderationBase.sol

/// @audit (valid but excluded finding)
2:    pragma solidity ^0.8.17;

```
https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/lib/ConsiderationBase.sol#L2

```solidity
File: contracts/lib/ConsiderationDecoder.sol

/// @audit (valid but excluded finding)
2:    pragma solidity ^0.8.17;

```
https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/lib/ConsiderationDecoder.sol#L2

```solidity
File: contracts/lib/ConsiderationEncoder.sol

/// @audit (valid but excluded finding)
2:    pragma solidity ^0.8.13;

```
https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/lib/ConsiderationEncoder.sol#L2

```solidity
File: contracts/lib/Consideration.sol

/// @audit (valid but excluded finding)
2:    pragma solidity ^0.8.17;

```
https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/lib/Consideration.sol#L2

```solidity
File: contracts/lib/CounterManager.sol

/// @audit (valid but excluded finding)
2:    pragma solidity ^0.8.17;

```
https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/lib/CounterManager.sol#L2

```solidity
File: contracts/lib/CriteriaResolution.sol

/// @audit (valid but excluded finding)
2:    pragma solidity ^0.8.17;

```
https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/lib/CriteriaResolution.sol#L2

```solidity
File: contracts/lib/Executor.sol

/// @audit (valid but excluded finding)
2:    pragma solidity ^0.8.17;

```
https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/lib/Executor.sol#L2

```solidity
File: contracts/lib/FulfillmentApplier.sol

/// @audit (valid but excluded finding)
2:    pragma solidity ^0.8.17;

```
https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/lib/FulfillmentApplier.sol#L2

```solidity
File: contracts/lib/GettersAndDerivers.sol

/// @audit (valid but excluded finding)
2:    pragma solidity ^0.8.17;

```
https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/lib/GettersAndDerivers.sol#L2

```solidity
File: contracts/lib/LowLevelHelpers.sol

/// @audit (valid but excluded finding)
2:    pragma solidity ^0.8.17;

```
https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/lib/LowLevelHelpers.sol#L2

```solidity
File: contracts/lib/OrderCombiner.sol

/// @audit (valid but excluded finding)
2:    pragma solidity ^0.8.17;

```
https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/lib/OrderCombiner.sol#L2

```solidity
File: contracts/lib/OrderFulfiller.sol

/// @audit (valid but excluded finding)
2:    pragma solidity ^0.8.17;

```
https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/lib/OrderFulfiller.sol#L2

```solidity
File: contracts/lib/OrderValidator.sol

/// @audit (valid but excluded finding)
2:    pragma solidity ^0.8.17;

```
https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/lib/OrderValidator.sol#L2

```solidity
File: contracts/lib/ReentrancyGuard.sol

/// @audit (valid but excluded finding)
2:    pragma solidity ^0.8.17;

```
https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/lib/ReentrancyGuard.sol#L2

```solidity
File: contracts/lib/SignatureVerification.sol

/// @audit (valid but excluded finding)
2:    pragma solidity ^0.8.17;

```
https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/lib/SignatureVerification.sol#L2

```solidity
File: contracts/lib/TokenTransferrer.sol

/// @audit (valid but excluded finding)
2:    pragma solidity ^0.8.13;

```
https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/lib/TokenTransferrer.sol#L2

```solidity
File: contracts/lib/TypehashDirectory.sol

/// @audit (valid but excluded finding)
2:    pragma solidity ^0.8.17;

```
https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/lib/TypehashDirectory.sol#L2

```solidity
File: contracts/lib/Verifiers.sol

/// @audit (valid but excluded finding)
2:    pragma solidity ^0.8.17;

```
https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/lib/Verifiers.sol#L2

```solidity
File: contracts/lib/ZoneInteraction.sol

/// @audit (valid but excluded finding)
2:    pragma solidity ^0.8.17;

```
https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/lib/ZoneInteraction.sol#L2

```solidity
File: contracts/Seaport.sol

/// @audit (valid but excluded finding)
2:    pragma solidity ^0.8.17;

```
https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/Seaport.sol#L2

### [N&#x2011;02]  Event is missing `indexed` fields
Index event fields make the field more quickly accessible [to off-chain tools](https://ethereum.stackexchange.com/questions/40396/can-somebody-please-explain-the-concept-of-event-indexing) that parse events. However, note that each index field costs extra gas during emission, so it's not necessarily best to index the maximum allowed per event (three fields). Each `event` should use three `indexed` fields if there are three or more fields, and gas usage is not particularly of concern for the events in question. If there are fewer than three fields, all of the fields should be indexed.

*There are 6 instances of this issue:*

```solidity
File: contracts/interfaces/ConduitInterface.sol

/// @audit (valid but excluded finding)
46:       event ChannelUpdated(address indexed channel, bool open);

```
https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/interfaces/ConduitInterface.sol#L46

```solidity
File: contracts/interfaces/ConsiderationEventsAndErrors.sol

/// @audit (valid but excluded finding)
31        event OrderFulfilled(
32            bytes32 orderHash,
33            address indexed offerer,
34            address indexed zone,
35            address recipient,
36            SpentItem[] offer,
37            ReceivedItem[] consideration
38:       );

/// @audit (valid but excluded finding)
47        event OrderCancelled(
48            bytes32 orderHash,
49            address indexed offerer,
50            address indexed zone
51:       );

/// @audit (valid but excluded finding)
61:       event OrderValidated(bytes32 orderHash, OrderParameters orderParameters);

/// @audit (valid but excluded finding)
69:       event OrdersMatched(bytes32[] orderHashes);

/// @audit (valid but excluded finding)
77:       event CounterIncremented(uint256 newCounter, address indexed offerer);

```
https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/interfaces/ConsiderationEventsAndErrors.sol#L31-L38



