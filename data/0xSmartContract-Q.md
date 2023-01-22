## Summary
### Low Risk Issues List
| Number |Issues Details|Context|
|:--:|:-------|:--:|
|[L-01]| Missing Event for initiazings| 15 |
|[L-02]| Use Create3 for deploy to a new EVM chain|  |

Total 2 issues


### Non-Critical Issues List
| Number |Issues Details|Context|
|:--:|:-------|:--:|
| [N-01]|Use `"memory-safe"` keyword for assembly |All Contracts|
| [N-02] |For modern and more readable code; update import usages  |28 |
| [N-03] |Include return parameters in NatSpec comments | All contracts |
| [N-04] |Use of bytes.concat() instead of abi.encodePacked() | 1 |
| [N-05] |For functions, follow Solidity standard naming conventions (internal function style rule)| 340|
| [N-06] |Pragma version^0.8.17  version too recent to be trusted | All contracts  |
| [N-07] |Tokens accidentally sent to the contract cannot be recovered|  |
| [N-08] |Project Upgrade and Stop Scenario should be |  |
| [N-09] |Use descriptive names for Contracts and Libraries | All Contracts |
| [N-10] |Use a single file for all system-wide constants| 538 |
| [N-11] |Add NatSpec Mapping comment | 6 |
| [N-12] |Initializing state variables with their default values is confusing|9 |
| [N-13] |Add to Event in  `receive()` function |1 |
| [N-14] |Floating pragma |All Contracts |

Total 14 issues

### [L-01] Missing Event for initiazings

**Context:**
```solidity
15 results - 15 files

contracts/Seaport.sol:
  93:     constructor(address conduitController) Consideration(conduitController) {}

contracts/conduit/Conduit.sol:
  73:     constructor() {

contracts/conduit/ConduitController.sol:
  31:     constructor() {

contracts/lib/Assertions.sol:
  35:     constructor(

contracts/lib/BasicOrderFulfiller.sol:
  41:     constructor(address conduitController) OrderValidator(conduitController) {}

contracts/lib/Consideration.sol:
  50:     constructor(address conduitController) OrderCombiner(conduitController) {}

contracts/lib/ConsiderationBase.sol:
  56:     constructor(address conduitController) {

contracts/lib/Executor.sol:
  35:     constructor(address conduitController) Verifiers(conduitController) {}

contracts/lib/GettersAndDerivers.sol:
  25:     constructor(

contracts/lib/OrderCombiner.sol:
  41:     constructor(address conduitController) OrderFulfiller(conduitController) {}

contracts/lib/OrderFulfiller.sol:
  45:     constructor(

contracts/lib/OrderValidator.sol:
  55:     constructor(address conduitController) Executor(conduitController) {}

contracts/lib/ReentrancyGuard.sol:
  23:     constructor() {

contracts/lib/TypehashDirectory.sol:
  30:     constructor() {

contracts/lib/Verifiers.sol:
  26:     constructor(address conduitController) Assertions(conduitController) {}

```

**Description:**
Events help non-contract tools to track changes
Many utilities and analysis frameworks make use of event-emits and are monitored at program startups.

**Recommendation:**
Add Event-Emit


### [L-02] Use Create3 for deploy to a new EVM chain

**Context:**
```js
1 result - 1 file

README.md:
  171  
  172: Rinkeby
  173: Goerli
  174: Kovan
  175: Sepolia
  176: Polygon
  177: Mumbai
  178: Optimism
  179: Optimistic Kovan
  180: Arbitrum
  181: Arbitrum Nova
  182: Arbitrum Rinkeby
  183: Avalanche Fuji
  184: Avalanche C-Chain
  185: Gnosis Chain
  186: BSC
  188: 
  189: To be deployed on other EVM chains, such as:
  190: 
  191: - Klaytn
  192: - Baobab
  193: - Skale
  194: - Celo
  195: - Fantom
  196: - RSK
  197: 
  198: To deploy to a new EVM chain, follow the [steps outlined here](docs/Deployment.md).

Seaport and the ConduitController can be deployed to the same address on all EVM chains using the CREATE2 Factory.

```
https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0/docs/Deployment.md

**Description:**
Deploying a contract to multiple chains with the same address is annoying. One usually would create a new Ethereum account, seed it with enough tokens to pay for gas on every chain, and then deploy the contract naively

This relies on the fact that the new account's nonce is synced on all the chains, therefore resulting in the same contract address. However, deployment is often a complex process that involves several transactions (e.g. for initialization), which means it's easy for nonces to fall out of sync and make it forever impossible to deploy the contract at the desired address.

One could use a CREATE2 factory that deterministically deploys contracts to an address that's unrelated to the deployer's nonce, but the address is still related to the hash of the contract's creation code.

This means if you wanted to use different constructor parameters on different chains, the deployed contracts will have different addresses.

A CREATE3 factory offers the best solution: the address of the deployed contract is determined by only the deployer address and the salt. This makes it far easier to deploy contracts to multiple chains at the same addresses

https://github.com/ZeframLou/create3-factory

### [N-01]  Use `"memory-safe"` keyword for assembly 

Without the use of inline assembly, the compiler can rely on memory to remain in a well-defined state at all times. This is especially relevant for the new code generation pipeline via Yul IR: this code generation path can move local variables from stack to memory to avoid stack-too-deep errors and perform additional memory optimizations, if it can rely on certain assumptions about memory use

While we recommend to always respect Solidity’s memory model, inline assembly allows you to use memory in an incompatible way. Therefore, moving stack variables to memory and additional memory optimizations are, by default, disabled in the presence of any inline assembly block that contains a memory operation or assigns to Solidity variables in memory.

However, you can specifically annotate an assembly block to indicate that it in fact respects Solidity’s memory model as follows:

```solidity
assembly ("memory-safe") {
```

https://docs.soliditylang.org/en/v0.8.16/assembly.html#memory-safety

### [N-02] For modern and more readable code; update import usages

**Context:**

```solidity
28 results - 23 files

contracts/conduit/Conduit.sol:
  14  
  15: import "./lib/ConduitConstants.sol";
  16  

contracts/lib/AmountDeriver.sol:
  7  
  8: import "./ConsiderationConstants.sol";
  9  

contracts/lib/Assertions.sol:
  13  
  14: import "./ConsiderationErrors.sol";
  15  

contracts/lib/BasicOrderFulfiller.sol:
  22  
  23: import "./ConsiderationErrors.sol";
  24  

contracts/lib/Consideration.sol:
  22  
  23: import "../helpers/PointerLibraries.sol";
  24  
  25: import "./ConsiderationConstants.sol";
  26  

contracts/lib/ConsiderationBase.sol:
  11  
  12: import "./ConsiderationConstants.sol";
  13  

contracts/lib/ConsiderationDecoder.sol:
  19  
  20: import "./ConsiderationConstants.sol";
  21  
  22: import "../helpers/PointerLibraries.sol";
  23  

contracts/lib/ConsiderationEncoder.sol:
   3  
   4: import "./ConsiderationConstants.sol";
   5  

  19  
  20: import "../helpers/PointerLibraries.sol";
  21  

contracts/lib/ConsiderationErrors.sol:
  5  
  6: import "./ConsiderationConstants.sol";
  7  

contracts/lib/CounterManager.sol:
   9  
  10: import "./ConsiderationConstants.sol";
  11  

contracts/lib/CriteriaResolution.sol:
  14  
  15: import "./ConsiderationErrors.sol";
  16  
  17: import "../helpers/PointerLibraries.sol";
  18  

contracts/lib/Executor.sol:
  15  
  16: import "./ConsiderationConstants.sol";
  17  
  18: import "./ConsiderationErrors.sol";
  19  

contracts/lib/FulfillmentApplier.sol:
  15  
  16: import "./ConsiderationErrors.sol";
  17  

contracts/lib/GettersAndDerivers.sol:
  7  
  8: import "./ConsiderationConstants.sol";
  9  

contracts/lib/LowLevelHelpers.sol:
  3  
  4: import "./ConsiderationConstants.sol";
  5  

contracts/lib/OrderCombiner.sol:
  22  
  23: import "./ConsiderationErrors.sol";
  24  

contracts/lib/OrderFulfiller.sol:
  22  
  23: import "./ConsiderationErrors.sol";
  24  

contracts/lib/OrderValidator.sol:
  18  
  19: import "./ConsiderationErrors.sol";
  20  

contracts/lib/ReentrancyGuard.sol:
  7  
  8: import "./ConsiderationErrors.sol";
  9  

contracts/lib/SignatureVerification.sol:
  11  
  12: import "./ConsiderationErrors.sol";
  13  

contracts/lib/TokenTransferrer.sol:
  3  
  4: import "./TokenTransferrerConstants.sol";
  5  

contracts/lib/Verifiers.sol:
   9  
  10: import "./ConsiderationErrors.sol";
  11  

contracts/lib/ZoneInteraction.sol:
  15  
  16: import "./ConsiderationEncoder.sol";

```


**Description:**
Solidity code is also cleaner in another way that might not be noticeable: the struct Point. We were importing it previously with global import but not using it. The Point struct `polluted the source code` with an unnecessary object we were not using because we did not need it. 
This was breaking the rule of modularity and modular programming: `only import what you need` Specific imports with curly braces allow us to apply this rule better.

**Recommendation:**
`import {contract1 , contract2} from "filename.sol";`

A good example from the ArtGobblers project;
```js
import {Owned} from "solmate/auth/Owned.sol";
import {ERC721} from "solmate/tokens/ERC721.sol";
import {LibString} from "solmate/utils/LibString.sol";
import {MerkleProofLib} from "solmate/utils/MerkleProofLib.sol";
import {FixedPointMathLib} from "solmate/utils/FixedPointMathLib.sol";
import {ERC1155, ERC1155TokenReceiver} from "solmate/tokens/ERC1155.sol";
import {toWadUnsafe, toDaysWadUnsafe} from "solmate/utils/SignedWadMath.sol";
```

### [N-03] Include return parameters in NatSpec comments

**Context:**
All Contracts

**Description:**
It is recommended that Solidity contracts are fully annotated using NatSpec for all public interfaces (everything in the ABI). It is clearly stated in the Solidity official documentation. In complex projects such as Defi, the interpretation of all functions and their arguments and returns is important for code readability and auditability.

https://docs.soliditylang.org/en/v0.8.15/natspec-format.html

**Recommendation:**
Include return parameters in NatSpec comments

_Recommendation  Code Style: (from Uniswap3)_
```js
    /// @notice Adds liquidity for the given recipient/tickLower/tickUpper position
    /// @dev The caller of this method receives a callback in the form of IUniswapV3MintCallback#uniswapV3MintCallback
    /// in which they must pay any token0 or token1 owed for the liquidity. The amount of token0/token1 due depends
    /// on tickLower, tickUpper, the amount of liquidity, and the current price.
    /// @param recipient The address for which the liquidity will be created
    /// @param tickLower The lower tick of the position in which to add liquidity
    /// @param tickUpper The upper tick of the position in which to add liquidity
    /// @param amount The amount of liquidity to mint
    /// @param data Any data that should be passed through to the callback
    /// @return amount0 The amount of token0 that was paid to mint the given amount of liquidity. Matches the value in the callback
    /// @return amount1 The amount of token1 that was paid to mint the given amount of liquidity. Matches the value in the callback
    function mint(
        address recipient,
        int24 tickLower,
        int24 tickUpper,
        uint128 amount,
        bytes calldata data
    ) external returns (uint256 amount0, uint256 amount1);
```
### [N-04] Use of bytes.concat() instead of abi.encodePacked()

```solidity

contracts/lib/TypehashDirectory.sol:
  176          return
  177:             abi.encodePacked(
  178:                 considerationItemTypeString,
  179:                 offerItemTypeString,
  180:                 orderComponentsPartialTypeString
  181:             );

```
Rather than using `abi.encodePacked` for appending bytes, since version 0.8.4, bytes.concat() is enabled

Since version 0.8.4 for appending bytes, bytes.concat() can be used instead of abi.encodePacked(,)
### [N-05] For functions, follow Solidity standard naming conventions (internal function style rule)

**Context:**
```solidity

340 results - 3 files


Some of the findings to be given as examples;

contracts/helpers/PointerLibraries.sol:
  2785:     function readInt8(MemoryPointer mPtr) internal pure returns (int8 value) {
  2792:     function readInt16(MemoryPointer mPtr) internal pure returns (int16 value) {
  2799:     function readInt24(MemoryPointer mPtr) internal pure returns (int24 value) {
  2806:     function readInt32(MemoryPointer mPtr) internal pure returns (int32 value) {
  2813:     function readInt40(MemoryPointer mPtr) internal pure returns (int40 value) {
  2820:     function readInt48(MemoryPointer mPtr) internal pure returns (int48 value) {
  2827:     function readInt56(MemoryPointer mPtr) internal pure returns (int56 value) {
  2834:     function readInt64(MemoryPointer mPtr) internal pure returns (int64 value) {
  2841:     function readInt72(MemoryPointer mPtr) internal pure returns (int72 value) {
  2848:     function readInt80(MemoryPointer mPtr) internal pure returns (int80 value) {
  2855:     function readInt88(MemoryPointer mPtr) internal pure returns (int88 value) {
  2862:     function readInt96(MemoryPointer mPtr) internal pure returns (int96 value) {
  3051:     function write(MemoryPointer mPtr, MemoryPointer valuePtr) internal pure {
  3058:     function write(MemoryPointer mPtr, bool value) internal pure {
  3065:     function write(MemoryPointer mPtr, address value) internal pure {
  3073:     function writeBytes32(MemoryPointer mPtr, bytes32 value) internal pure {
  3080:     function write(MemoryPointer mPtr, uint256 value) internal pure {
  3088:     function writeInt(MemoryPointer mPtr, int256 value) internal pure {


contracts/lib/TypehashDirectory.sol:
   14:     bytes3 internal constant twoSubstring = 0x5B325D;
   15:     uint256 internal constant twoSubstringLength = 3;
   18:     uint256 internal constant MaxTreeHeight = 24;
   20:     uint256 internal constant InvalidOpcode = 0xfe;
   21:     uint256 internal constant OneWord = 0x20;
   22:     uint256 internal constant OneWordShift = 5;
   23:     uint256 internal constant AlmostOneWord = 0x1f;
   24:     uint256 internal constant FreeMemoryPointerSlot = 0x40;
  131:     function getTreeSubTypes() internal pure returns (bytes memory) {
```


**Description:**
The above codes don't follow Solidity's standard naming convention,

internal and private functions : the mixedCase format starting with an underscore (_mixedCase starting with an underscore)


### [N-06] Pragma version^0.8.17  version too recent to be trusted.

https://github.com/ethereum/solidity/blob/develop/Changelog.md
0.8.17 (2022-09-08)
0.8.16 (2022-08-08)
0.8.15 (2022-06-15)
0.8.10 (2021-11-09)


Unexpected bugs can be reported in recent versions;
Risks related to recent releases
Risks of complex code generation changes
Risks of new language features
Risks of known bugs

Use a non-legacy and more battle-tested version
Use 0.8.10

### [N-07] Tokens accidentally sent to the contract cannot be recovered


It can't be recovered if the tokens accidentally arrive at the contract address, which has happened to many popular projects, so I recommend adding a recovery code to your critical contracts.

### Recommended Mitigation Steps

Add this code:

```solidity
 /**
  * @notice Sends ERC20 tokens trapped in contract to external address
  * @dev Onlyowner is allowed to make this function call
  * @param account is the receiving address
  * @param externalToken is the token being sent
  * @param amount is the quantity being sent
  * @return boolean value indicating whether the operation succeeded.
  *
 */
  function rescueERC20(address account, address externalToken, uint256 amount) public onlyOwner returns (bool) {
    IERC20(externalToken).transfer(account, amount);
    return true;
  }
}

```

### [N-08] Project Upgrade and Stop Scenario should be

At the start of the project, the system may need to be stopped or upgraded, I suggest you have a script beforehand and add it to the documentation.
This can also be called an " EMERGENCY STOP (CIRCUIT BREAKER) PATTERN ".

https://github.com/maxwoe/solidity_patterns/blob/master/security/EmergencyStop.sol

### [N-09] Use descriptive names for Contracts and Libraries


This codebase will be difficult to navigate, as there are no descriptive naming conventions that specify which files should contain meaningful logic.

Prefixes should be added like this by filing:

Interface I_
absctract contracts Abs_
Libraries Lib_

We recommend that you implement this or a similar agreement.

### [N-10] Use a single file for all system-wide constants

There are many addresses and constants used in the system. It is recommended to put the most used ones in one file (for example constants.sol, use inheritance to access these values)

  This will help with readability and easier maintenance for future changes. This also helps with any issues, as some of these hard-coded values are admin addresses.

constants.sol
Use and import this file in contracts that require access to these values. This is just a suggestion, in some use cases this may result in higher gas usage in the distribution.

```solidity
538 results - 19 files
```

### [N-11]  Add NatSpec Mapping comment

**Description:**
Add NatSpec comments describing mapping keys and values


**Context:**

```solidity
6 results - 5 files

contracts/conduit/Conduit.sol:
  34:     mapping(address => bool) private _channels;

contracts/conduit/ConduitController.sol:
  21:     mapping(address => ConduitProperties) internal _conduits;

contracts/interfaces/ConduitControllerInterface.sol:
  20:         mapping(address => uint256) channelIndexesPlusOne;

contracts/lib/CounterManager.sol:
  20:     mapping(address => uint256) private _counters;

contracts/lib/OrderValidator.sol:
  42:     mapping(bytes32 => OrderStatus) private _orderStatus;
  45:     mapping(address => uint256) internal _contractNonces;


```
**Recommendation:**

```solidity

 /// @dev    address(user) -> address(ERC0 Contract Address) -> uint256(allowance amount from user)
    mapping(address => mapping(address => uint256)) public allowance;

```



### [N-12]  Initializing state variables with their default values is confusing


**Description:**
It's not best practice to initialize state variables with their default values, so it won't be confusing to replace the default value with no value

**Context:**

```solidity
9 results - 3 files

contracts/conduit/lib/ConduitConstants.sol:
   8: uint256 constant ChannelClosed_error_ptr = 0x00;
  16: uint256 constant ChannelKey_channel_ptr = 0x00;

contracts/lib/ConsiderationConstants.sol:
   44: uint256 constant information_version_offset = 0;
  108: uint256 constant OrderParameters_offerer_offset = 0x00;
  457: uint256 constant IsValidOrder_sig_ptr = 0x0;
  998: uint256 constant ratifyOrder_offer_head_offset = 0x00;


contracts/lib/TokenTransferrerConstants.sol:
  58: uint256 constant ERC20_transferFrom_sig_ptr = 0x0;
  70: uint256 constant ERC1155_safeTransferFrom_sig_ptr = 0x0;
  92: uint256 constant ERC721_transferFrom_sig_ptr = 0x0;

```


### [N-13] Add to Event in  `receive()` function

The `receiver()` function is important in terms of tracking the amount of Ether sent to the contract (if address sender is added as a parameter, address-based tracking and analysis can be provided)

So it is recommended to add `event-emit` to the function

**Context:**
```solidity

contracts/lib/Consideration.sol:
  65       */
  66:     receive() external payable {
  67:         // Ensure the reentrancy guard is currently set to accept native tokens.
  68:         _assertAcceptingNativeTokens();
  69:     }

```

**Description:**
Events help non-contract tools to track changes
Many utilities and analysis frameworks make use of event-emits and are monitored at program startups.

**Recommendation:**
Add Event-Emit


### [N-14 ] Floating pragma

**Description:**
Contracts should be deployed with the same compiler version and flags that they have been tested with thoroughly. Locking the pragma helps to ensure that contracts do not accidentally get deployed using, for example, an outdated compiler version that might introduce bugs that affect the contract system negatively.
https://swcregistry.io/docs/SWC-103

Floating Pragma List: 
pragma ^0.8.13 - ^0.8.17  (all contracts)

**Recommendation:**
Lock the pragma version and also consider known bugs (https://github.com/ethereum/solidity/releases) for the compiler version that is chosen.
