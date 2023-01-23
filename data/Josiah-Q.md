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