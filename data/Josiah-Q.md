## ABI.ENCODEPACKED SHOULD BE USED WITH CAUTION ON DYNAMIC TYPES WHEN PASSING RESULT TO KECCAK256()
When passing the result to a hash function such as keccak256(), use abi.encode() instead which will pad items to 32 bytes to prevent hash collisions (e.g. abi.encodePacked(0x123,0x456) => 0x123456 => abi.encodePacked(0x1,0x23456), but abi.encode(0x123,0x456) => 0x0...1230...456). Unless there is a compelling reason, abi.encode should be preferred. If there is only one argument to abi.encodePacked(), it can often be cast to bytes() or bytes32() instead. If all arguments are strings and or bytes, bytes.concat() should be used instead.

Here are the 2 instances found.

[ConduitController.sol#L75-L82](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/conduit/ConduitController.sol#L75-L82)

```
                    keccak256(
                        abi.encodePacked(
                            bytes1(0xff),
                            address(this),
                            conduitKey,
                            _CONDUIT_CREATION_CODE_HASH
                        )
                    )
```
[TransferHelper.sol#L106-L113](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/helpers/TransferHelper.sol#L106-L113)

```
                    keccak256(
                        abi.encodePacked(
                            bytes1(0xff),
                            address(_CONDUIT_CONTROLLER),
                            conduitKey,
                            _CONDUIT_CREATION_CODE_HASH
                        )
                    )
```
## ZERO ADDRESS CHECKS
Zero address checks at the constructor could avoid human errors leading to non-functional calls associated with the mistakes made and unnecessary contract redeployment at the worst.

Here are some of the instances found.

[Seaport.sol#L93](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/Seaport.sol#L93)

```
    constructor(address conduitController) Consideration(conduitController) {}
```
[TransferHelper.sol#L47-L52](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/helpers/TransferHelper.sol#L47-L52)

```
    constructor(address conduitController) {
        // Get the conduit creation code and runtime code hashes from the
        // supplied conduit controller and set them as an immutable.
        ConduitControllerInterface controller = ConduitControllerInterface(
            conduitController
        );
```
[BasicOrderFulfiller.sol#L41](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/lib/BasicOrderFulfiller.sol#L41)

```
    constructor(address conduitController) OrderValidator(conduitController) {}
```
[Consideration.sol#L50](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/lib/Consideration.sol#L50)

```
    constructor(address conduitController) OrderCombiner(conduitController) {}
```
## SOLIDITY COMPILER OPTIMIZATIONS COULD BE PROBLEMATIC
```
hardhat.config.js:
  29  module.exports = {
  30:   solidity: {
  31:     compilers: [
  32:       {
  33:         version: "0.8.17",
  34:         settings: {
  35:           optimizer: {
  36:               enabled: true,
  37:               runs: 1000000
  38
            }
```
Description: Protocol has enabled optional compiler optimizations in Solidity. There have been several optimization bugs with security implications. Moreover, optimizations are actively being developed. Solidity compiler optimizations are disabled by default, and it is unclear how many contracts in the wild actually use them.

Therefore, it is unclear how well they are being tested and exercised. High-severity security issues due to optimization bugs have occurred in the past. A high-severity bug in the emscripten-generated solc-js compiler used by Truffle and Remix persisted until late 2018. The fix for this bug was not reported in the Solidity CHANGELOG.

Another high-severity optimization bug resulting in incorrect bit shift results was patched in Solidity 0.5.6. More recently, another bug due to the incorrect caching of keccak256 was reported. A compiler audit of Solidity from November 2018 concluded that the optional optimizations may not be safe. It is likely that there are latent bugs related to optimization and that new bugs will be introduced due to future optimizations.

Exploit Scenario A latent or future bug in Solidity compiler optimizations—or in the Emscripten transpilation to solc-js—causes a security vulnerability in the contracts.

Recommendation: Short term, measure the gas savings from optimizations and carefully weigh them against the possibility of an optimization-related bug. Long term, monitor the development and adoption of Solidity compiler optimizations to assess their maturity.

## CONTRACT LAYOUT ON FUNCTION WRITINGS COMPLIANCE WITH SOLIDITY'S STYLE GUIDE
As denoted in Solidity's Style Guide:

https://docs.soliditylang.org/en/v0.8.17/style-guide.html

In order to help readers identify which functions they can call, and find the constructor and fallback definitions more easily, functions should be grouped according to their visibility and ordered in the following manner:

constructor, receive function (if exists), fallback function (if exists), external, public, internal, private

And, within a grouping, place the view and pure functions last.

Additionally, inside each contract, library or interface, use the following order:

type declarations, state variables, events, modifiers, functions

Where possible, consider adhering to the above guidelines for all contract instances entailed.

## CONSTANT VARIABLES COMPLIANCE WITH SOLIDITY'S STYLE GUIDE
It is recommended that constant variables utilize the UPPER_CASE_WITH_UNDERSCORES format.

Here is a contract where all other constants should conform to the fully capitalized standard adopted on lines 52 - 54.

[ConsiderationConstants.sol#L52-L54](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/lib/ConsiderationConstants.sol#L52-L54)

```
...
uint256 constant information_version_offset = 0;
uint256 constant information_version_cd_offset = 0x60;
uint256 constant information_domainSeparator_offset = 0x20;
uint256 constant information_conduitController_offset = 0x40;
uint256 constant information_versionLengthPtr = 0x63;
uint256 constant information_versionWithLength = 0x03312e32; // 1.2
uint256 constant information_length = 0xa0;

52: uint256 constant _NOT_ENTERED = 1;
53: uint256 constant _ENTERED = 2;
54: uint256 constant _ENTERED_AND_ACCEPTING_NATIVE_TOKENS = 3;

uint256 constant Offset_fulfillAdvancedOrder_criteriaResolvers = 0x20;
...
```
## DOS ON UNBOUNDED LOOP
Unbounded loop could lead to OOG (Out of Gas) denying the users of needed services. It is recommended setting a threshold for the array length if the array could grow to or entail an excessive size. 

Here are some of the instances found.

[Conduit.sol#L99](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/conduit/Conduit.sol#L99)

```
        for (uint256 i = 0; i < totalStandardTransfers; ) {
```
[TransferHelper.sol#L124](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/helpers/TransferHelper.sol#L124)

```
            for (uint256 i = 0; i < numTransfers; ++i) {
```
[BasicOrderFulfiller.sol#L1079](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/lib/BasicOrderFulfiller.sol#L1079)

```
        for (uint256 i = 0; i < totalAdditionalRecipientsDataSize; ) {
```
## USE MORE RECENT VERSIONS OF SOLIDITY 
Lower versions like 0.8.7, 0.8.13 etc are being used in numerous contracts. For better security, it is best practice to use the latest Solidity version, 0.8.17.

Please visit the versions security fix list in the link below for detailed info:

https://github.com/ethereum/solidity/blob/develop/Changelog.md

## INTERFACES AND LIBRARIES ON THE SAME FILE
Some contracts have interfaces and/or libraries showing up in their entirety in the same file to facilitate the ease of referencing on the same page. This has, in certain instances, made the already large contract size to house an excessive code base. Additionally, it might create difficulty locating them when attempting to cross reference the specific interfaces embedded elsewhere but not saved into a particular .sol file.

Consider saving the interfaces and libraries entailed respectively, and having them imported like all others.

Here are some of the instances found.

[PointerLibraries.sol](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/helpers/PointerLibraries.sol)

```
47: library CalldataPointerLib {

128: library ReturndataPointerLib {

209: library MemoryPointerLib {

296: library CalldataReaders {

1188: library ReturndataReaders {

2177: library MemoryReaders {

3049: library MemoryWriters {
```
## NATSPEC SHOULD BE ADEQUATE
As denoted in the link below:

https://docs.soliditylang.org/en/v0.8.15/natspec-format.html

It is recommended that Solidity contracts are fully annotated using NatSpec for all public interfaces (everything in the ABI). It is clearly stated in the Solidity official documentation. In complex projects such as deFi, the interpretation of all functions and their arguments and returns is important for code readability and auditability.

Additionally, some of the code bases, particularly those entailing assembly, are lacking partial/full NatSpec that will be of added values to the users and developers if adequately provided.

Here are some of the instance found.

[PointerLibraries.sol#L47-L73](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/helpers/PointerLibraries.sol#L47-L73)

```
library CalldataPointerLib {
    function lt(
        CalldataPointer a,
        CalldataPointer b
    ) internal pure returns (bool c) {
        assembly {
            c := lt(a, b)
        }
    }

    function gt(
        CalldataPointer a,
        CalldataPointer b
    ) internal pure returns (bool c) {
        assembly {
            c := gt(a, b)
        }
    }

    function eq(
        CalldataPointer a,
        CalldataPointer b
    ) internal pure returns (bool c) {
        assembly {
            c := eq(a, b)
        }
    }
```
[ConduitStructs.sol#L6-L21](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/conduit/lib/ConduitStructs.sol#L6-L21)

```
struct ConduitTransfer {
    ConduitItemType itemType;
    address token;
    address from;
    address to;
    uint256 identifier;
    uint256 amount;
}

struct ConduitBatch1155Transfer {
    address token;
    address from;
    address to;
    uint256[] ids;
    uint256[] amounts;
}
```
[ConduitEnums.sol](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/conduit/lib/ConduitEnums.sol)

```
enum ConduitItemType {
    NATIVE, // unused
    ERC20,
    ERC721,
    ERC1155
}
```
## TYPO ERRORS
[OrderValidator.sol](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/lib/OrderValidator.sol)

```
    @ status
38: *         and updating their status. 

    @ offer
370:     * @dev Internal pure function to check the compatibility of two offer
```
[ConsiderationDecoder.sol](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/lib/ConsiderationDecoder.sol)

```
    @ ... to the nearest ...
41:            // Derive the size of the bytes array, rounding up to nearest word

    @ length
875:                        // Set first word of scratch space to 0 so length of
876:                        // offer/consideration are set to 0 on invalid encoding.
```
## THE USE OF DELETE TO RESET VARIABLES
`delete a` assigns the initial value for the type to `a`. i.e. for integers it is equivalent to `a = 0`, but it can also be used on arrays, where it assigns a dynamic array of length zero or a static array of the same length with all elements reset. For structs, it assigns a struct with all members reset. Similarly, it can also be used to set an address to zero address or a boolean to false. It has no effect on whole mappings though (as the keys of mappings may be arbitrary and are generally unknown). However, individual keys and what they map to can be deleted: If `a` is a mapping, then `delete a[x]` will delete the value stored at x.

The delete key better conveys the intention and is also more idiomatic.

Here are some of the instances found.

[FulfillmentApplier.sol#L78-L79](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/lib/FulfillmentApplier.sol#L78-L79)

```
            considerationExecution.offerer = address(0);
            considerationExecution.item.recipient = payable(0);
```
[OrderCombiner.sol#L744](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/lib/OrderCombiner.sol#L744)

```
                    availableOrders[i] = false;
```
## THE USE OF DISTINCT VARIABLES
Making the naming of local variables more distinct could prove a long way in helping developers and users to better comprehend the intended function signature, significantly enhancing code readability.

Her are some of the instances found.

[PointerLibraries.sol#L129-L153](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/helpers/PointerLibraries.sol#L129-L153)

```
    function lt(
        ReturndataPointer a,
        ReturndataPointer b
    ) internal pure returns (bool c) {
        assembly {
            c := lt(a, b)
        }
    }

    function gt(
        ReturndataPointer a,
        ReturndataPointer b
    ) internal pure returns (bool c) {
        assembly {
            c := gt(a, b)
        }
    }

    function eq(
        ReturndataPointer a,
        ReturndataPointer b
    ) internal pure returns (bool c) {
        assembly {
            c := eq(a, b)
        }
```
## MODERN MODULARITY ON IMPORT USAGES
For cleaner Solidity code in conjunction with the rule of modularity and modular programming, it is recommended using named imports with curly braces instead of adopting the global import approach.

Here are some of the instances found that could join their counterparts in adopting this method.

[ConsiderationDecoder.sol#L20-L22](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/lib/ConsiderationDecoder.sol#L20-L22)

```
import "./ConsiderationConstants.sol";

import "../helpers/PointerLibraries.sol";
```