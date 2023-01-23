## Interfaces and libraries should be separately saved and imported
Some contracts have interface(s) or libraries showing up in its/their entirety at the top/bottom of the contract facilitating an ease of references on the same file page. This has, in certain instances, made the already large contract size to house an excessive code base. Additionally, it might create difficulty locating them when attempting to cross reference the specific interfaces embedded elsewhere but not saved into a particular .sol file. 

Consider saving the interfaces and libraries entailed respectively, and having them imported like all other files.

Here are some of the instances entailed:

[File: PointerLibraries.sol](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/helpers/PointerLibraries.sol)

## Inadequate NatSpec
Solidity contracts can use a special form of comments, i.e., the Ethereum Natural Language Specification Format (NatSpec) to provide rich documentation for functions, return variables and more. Please visit the following link for further details:

https://docs.soliditylang.org/en/v0.8.16/natspec-format.html

Some of the code bases, particularly those entailing assembly, are lacking partial/full NatSpec that will be of added values to the users and developers if adequately provided.

Here are some of the instances entailed:

[File: PointerLibraries.sol](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/helpers/PointerLibraries.sol)
[File: ConduitStructs.sol](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/conduit/lib/ConduitStructs.sol)
[File: ConduitEnums.sol](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/conduit/lib/ConduitEnums.sol)

## Typo/grammatical mistakes
[File: ConsiderationDecoder.sol#L41](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/lib/ConsiderationDecoder.sol#L41)

```diff
-            // Derive the size of the bytes array, rounding up to nearest word
+            // Derive the size of the bytes array, rounding up to the nearest word
```
[File: OrderValidator.sol#L370](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/lib/OrderValidator.sol#L370)

```diff
-     * @dev Internal pure function to check the compatibility of two offer
+     * @dev Internal pure function to check the compatibility of two offers
```
[File: OrderValidator.sol#L38](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/lib/OrderValidator.sol#L38)

```diff
- *         and updating their status.
+ *         and updating their statuses.
```
[File: ConsiderationDecoder.sol#L875-L876](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/lib/ConsiderationDecoder.sol#L875-L876)

```diff
-                        // Set first word of scratch space to 0 so length of
+                        // Set first word of scratch space to 0 so lengths of
                        // offer/consideration are set to 0 on invalid encoding.
```
## `constant` variables should be capitalized
Constants should be named with all capital letters with underscores separating words if need be. 

For instance, in ConsiderationConstants.sol, all other constants should conform to the full capitalized standard adopted on lines 52 - 54:

[File: ConsiderationConstants.sol](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/lib/ConsiderationConstants.sol)

```solidity
            [ ...]

- uint256 constant information_versionWithLength = 0x03312e32; // 1.2
+ uint256 constant INFORMATION_VERSIONWITHLENGTH = 0x03312e32; // 1.2
- uint256 constant information_length = 0xa0;
+ uint256 constant INFORMATION_LENGTH = 0xa0;

uint256 constant _NOT_ENTERED = 1;
uint256 constant _ENTERED = 2;
uint256 constant _ENTERED_AND_ACCEPTING_NATIVE_TOKENS = 3;

- uint256 constant Offset_fulfillAdvancedOrder_criteriaResolvers = 0x20;
+ uint256 constant OFFSET_FULFILLADVANCEDORDER_CRITERIARESOLVERS = 0x20;

            [ ... ]
```
## Use `delete` to clear variables
`delete a` assigns the initial value for the type to `a`. i.e. for integers it is equivalent to `a = 0`, but it can also be used on arrays, where it assigns a dynamic array of length zero or a static array of the same length with all elements reset. For structs, it assigns a struct with all members reset. Similarly, it can also be used to set an address to zero address or a boolean to false. It has no effect on whole mappings though (as the keys of mappings may be arbitrary and are generally unknown). However, individual keys and what they map to can be deleted: If `a` is a mapping, then `delete a[x]` will delete the value stored at x.

The delete key better conveys the intention and is also more idiomatic.

For instance, the `a = false` instance below may be refactored as follows:

[File: OrderValidator.sol#L88](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/lib/OrderValidator.sol#L88)

```diff
-        orderStatus.isCancelled = false;
+        delete orderStatus.isCancelled;
```
## Sanity checks at the constructor
Adequate zero address and zero value checks should be implemented at the constructor to avoid accidental error(s) that could result in non-functional calls associated with it particularly when assigning immutable variables.

For instance, the specific instance below may be refactored as follows:

[File: OrderValidator.sol#L55](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/lib/OrderValidator.sol#L55)

```diff
-    constructor(address conduitController) Executor(conduitController) {}
+    constructor(address conduitController) Executor(conduitController) {
+            require(conduitController != address(0));
+    }
```
## `abi.encodePacked()` should not be used with dynamic types when passing the result to a hash function such as `keccak256()`
Use abi.encode() instead which will pad items to 32 bytes, which will prevent hash collisions (e.g. abi.encodePacked(0x123,0x456) => 0x123456 => abi.encodePacked(0x1,0x23456), but abi.encode(0x123,0x456) => 0x0...1230...456). "Unless there is a compelling reason, abi.encode should be preferred". If there is only one argument to abi.encodePacked(), it can often be cast to bytes() or bytes32() instead. If all arguments are strings and or bytes, bytes.concat() should be used instead.

For instance, the specific instance below may be refactored as follows:

[File: ConduitController.sol#L72-L85](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/conduit/ConduitController.sol#L72-L85)

```diff
        conduit = address(
            uint160(
                uint256(
                    keccak256(
-                        abi.encodePacked(
+                        abi.encode(
                            bytes1(0xff),
                            address(this),
                            conduitKey,
                            _CONDUIT_CREATION_CODE_HASH
                        )
                    )
                )
            )
        );
```
## Solidity's Style Guide on contract layout
According to Solidity's Style Guide below:

https://docs.soliditylang.org/en/v0.8.17/style-guide.html

In order to help readers identify which functions they can call, and find the constructor and fallback definitions more easily, functions should be grouped according to their visibility and ordered in the following manner:

constructor, receive function (if exists), fallback function (if exists), external, public, internal, private

And, within a grouping, place the view and pure functions last.

Additionally, inside each contract, library or interface, use the following order:

type declarations, state variables, events, modifiers, functions

Consider adhering to the above guidelines for all contract instances entailed.

## Descriptive and Verbose Options
Consider making the naming of local variables more verbose and descriptive so all other peer developers would better be able to comprehend the intended statement logic, significantly enhancing the code readability.

For instance, the local variables of the function below may be rewritten as follows:

[File: PointerLibraries.sol#L48-L55](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/helpers/PointerLibraries.sol#L48-L55)

```diff
    function lt(
-        CalldataPointer a,
+        CalldataPointer aCdPtr,
-        CalldataPointer b
+        CalldataPointer bCdPtr
-    ) internal pure returns (bool c) {
+    ) internal pure returns (bool status_) {
        assembly {
-            c := lt(a, b)
+            status_ := lt(aCdPtr, bCdPtr)
        }
    }
```
## Modularity on import usages
For cleaner Solidity code in conjunction with the rule of modularity and modular programming, use named imports with curly braces instead of adopting the global import approach.

For instance, the import instances below could be refactored conforming to most other instances in the code bases as follows:

[File: ConsiderationDecoder.sol#L20-L22](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/lib/ConsiderationDecoder.sol#L20-L22)

```diff
- import "./ConsiderationConstants.sol";
+ import {ConsiderationConstants} from "./ConsiderationConstants.sol";

- import "../helpers/PointerLibraries.sol";
+ import {PointerLibraries} from "../helpers/PointerLibraries.sol";
```
## Function Calls in Loop Could Lead to Denial of Service
Function calls made in unbounded loop are error-prone with potential resource exhaustion as it can trap the contract due to the gas limitations or failed transactions. 

For instance, the iteration in the for loop below over each pointer, word by word, until the tail is reached could end up running out of gas if a huge array devoid of a boundary option is entailed:

[File: ConsiderationDecoder.sol#L399-L405](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/lib/ConsiderationDecoder.sol#L399-L405)

```solidity
            for (uint256 offset = 0; offset < tailOffset; offset += OneWord) {
                // Resolve Order calldata offset, use it to decode and copy from
                // calldata, and write resultant AdvancedOrder offset to memory.
                mPtrHead.offset(offset).write(
                    _decodeOrderAsAdvancedOrder(cdPtrHead.pptr(offset))
                );
            }
```
## Use a more recent version of solidity
The protocol adopts version 0.8.7 on quite a number of contracts. For better security, it is best practice to use the latest Solidity version, 0.8.17.

Security fix list in the versions can be found in the link below:

https://github.com/ethereum/solidity/blob/develop/Changelog.md