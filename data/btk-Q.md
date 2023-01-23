### Total Low issues

| Number | Issues Details                                                                     | Context       |
|--------|------------------------------------------------------------------------------------|---------------|
| [L-01] | Low level calls with solidity version 0.8.14 and lower can result in optimiser bug | 5             |

### Total Non-Critical issues

| Number  | Issues Details                                                                              | Context        |
|---------|---------------------------------------------------------------------------------------------|----------------|
| [NC-01] | Include `@return` parameters in NatSpec comments                                            | All Contracts  |
| [NC-02] | Contracts should have full test coverage                                                    | All Contracts  |
| [NC-03] | Need Fuzzing test                                                                           | All Contracts  |
| [NC-04] | Use a more recent version of solidity                                                       | 32             |
| [NC-05] | Missing natspec                                                                             | All Contracts  |
| [NC-06] | Constants in comparisons should appear on the left side                                     | 11             |
| [NC-07] | Use `bytes.concat()` and `string.concat()`                                                  | 3              |
| [NC-08] | Add `I` prefix to interface contracts                                                       | All Interfaces |
| [NC-09] | Insufficient coverage                                                                       | All Contracts  |
| [NC-10] | Generate perfect code headers every time                                                    | All Contracts  |
| [NC-11] | Lock pragmas to specific compiler version                                                   | All Contracts  |
| [NC-12] | There is no need to cast a variable that is already an address, such as `uint(x)`           | 2              |
| [NC-13] | Consider using `delete` rather than assigning zero to clear values                          | 2              |
| [NC-14] | Assembly Codes Specific – Should Have Comments                                              | 6              |
| [NC-15] | Adding a `return` statement when the function defines a named return variable, is redundant | 5              |

## [L-01] Low level calls with solidity version 0.8.14 and lower can result in optimiser bug

The protocol is using low level calls with solidity version less then 0.8.14 which can result in optimizer bug.

> Ref: https://medium.com/certora/overly-optimistic-optimizer-certora-bug-disclosure-2101e3f7994d

### Lines of code

- [TokenTransferrer.sol](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/lib/TokenTransferrer.sol#L42)
- [ConsiderationStructs.sol](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/lib/ConsiderationStructs.sol#L290)
- [ConsiderationEncoder.sol](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/lib/ConsiderationEncoder.sol)
- [PointerLibraries.sol](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/helpers/PointerLibraries.sol)
- [Conduit.sol](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/conduit/Conduit.sol)

### Recommended Mitigation Steps

Consider upgrading to solidity 0.8.17

## [NC-01] Include `@return` parameters in NatSpec comments

If Return parameters are declared, you must prefix them with `/// @return`. Some code analysis programs do analysis by reading [NatSpec](https://docs.soliditylang.org/en/v0.8.15/natspec-format.html) details, if they can't see the `@return` tag, they do incomplete analysis.

### Lines of code

- **All Contracts**

### Recommended Mitigation Steps

Include the `@return` argument in the NatSpec comments.

## [NC-02] Contracts should have full test coverage

While 100% code coverage does not guarantee that there are no bugs, it often will catch easy-to-find bugs, and will ensure that there are fewer regressions when the code invariably has to be modified. Furthermore, in order to get full coverage, code authors will often have to re-organize their code so that it is more modular, so that each component can be tested separately, which reduces interdependencies between modules and layers, and makes for code that is easier to reason about and audit.

```solidity
- What is the overall line coverage percentage provided by your tests?: >90%
```

### Lines of code 

- **All Contracts**

### Recommended Mitigation Steps

Line coverage percentage should be 100%.

## [NC-03] Need Fuzzing test

In total 54 contracts, more than 200 `unchecked{}` are used, the functions used are critical. For this reason, there must be fuzzing tests in the tests of the project. Not seen in tests.

### Lines of code

- **All Contracts**

### Recommended Mitigation Steps

Use should fuzzing test like Echidna. As Alberto Cuesta Canada said: Fuzzing is not easy, the tools are rough, and the math is hard, but it is worth it. Fuzzing gives me a level of confidence in my smart contracts that I didn’t have before. Relying just on unit testing anymore and poking around in a testnet seems reckless now.

Ref: https://medium.com/coinmonks/smart-contract-fuzzing-d9b88e0b0a05

## [NC-04] Use a more recent version of solidity

For security, it is best practice to use the latest Solidity version. For the security fix list in the versions.

> https://github.com/ethereum/solidity/blob/develop/Changelog.md

```solidity
       pragma solidity ^0.8.13;
```

### Lines of code

- [ConsiderationConstants.sol:2](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/lib/ConsiderationConstants.sol#L2)
- [TokenTransferrer.sol:2](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/lib/TokenTransferrer.sol#L2)
- [ConsiderationStructs.sol:2](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/lib/ConsiderationStructs.sol#L2)
- [ConsiderationEnums.sol:2](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/lib/ConsiderationEnums.sol#L2)
- [ConsiderationEncoder.sol:2](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/lib/ConsiderationEncoder.sol#L2)
- [ConsiderationConstants.sol:2](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/lib/ConsiderationConstants.sol#L2)
- [ZoneInterface.sol:2](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/interfaces/ZoneInterface.sol#L2)
- [ZoneInteractionErrors.sol:2](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/interfaces/ZoneInteractionErrors.sol#L2)
- [TransferHelperInterface.sol:2](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/interfaces/TransferHelperInterface.sol#L2)
- [TransferHelperErrors.sol:2](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/interfaces/TransferHelperErrors.sol#L2)
- [TokenTransferrerErrors.sol:2](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/interfaces/TokenTransferrerErrors.sol#L2)
- [SignatureVerificationErrors.sol:2](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/interfaces/SignatureVerificationErrors.sol#L2)
- [SeaportInterface.sol:2](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/interfaces/SeaportInterface.sol#L2)
- [ReentrancyErrors.sol:2](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/interfaces/ReentrancyErrors.sol#L2)
- [ImmutableCreate2FactoryInterface.sol:2](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/interfaces/ImmutableCreate2FactoryInterface.sol#L2)
- [IERC721Receiver.sol:2](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/interfaces/IERC721Receiver.sol#L2)
- [FulfillmentApplicationErrors.sol:2](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/interfaces/FulfillmentApplicationErrors.sol#L2)
- [EIP1271Interface.sol:2](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/interfaces/EIP1271Interface.sol#L2)
- [CriteriaResolutionErrors.sol:2](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/interfaces/CriteriaResolutionErrors.sol#L2)
- [ContractOffererInterface.sol:2](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/interfaces/ContractOffererInterface.sol#L2)
- [ConsiderationInterface.sol:2](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/interfaces/ConsiderationInterface.sol#L2)
- [ConsiderationEventsAndErrors.sol:2](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/interfaces/ConsiderationEventsAndErrors.sol#L2)
- [ConduitInterface.sol:2](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/interfaces/ConduitInterface.sol#L2)
- [ConduitControllerInterface.sol:2](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/interfaces/ConduitControllerInterface.sol#L2)
- [AmountDerivationErrors.sol:2](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/interfaces/AmountDerivationErrors.sol#L2)
- [AbridgedTokenInterfaces.sol:2](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/interfaces/AbridgedTokenInterfaces.sol#L2)
- [PointerLibraries.sol:2](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/helpers/PointerLibraries.sol#L2)
- [ConduitStructs.sol:2](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/conduit/lib/ConduitStructs.sol#L2)
- [ConduitEnums.sol:2](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/conduit/lib/ConduitEnums.sol#L2)
- [ConduitConstants.sol:2](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/conduit/lib/ConduitConstants.sol#L2)
- [ConduitController.sol:2](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/conduit/ConduitController.sol#L2)
- [Conduit.sol:2](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/conduit/Conduit.sol#L2)

### Recommended Mitigation Steps

Old version of Solidity is used `(^0.8.13)`, newer version can be used `(0.8.17)`.

## [NC-05] Missing natspec

It is recommended that Solidity contracts are fully annotated using NatSpec, it is clearly stated in the Solidity official documentation.

- In complex projects such as Defi, the interpretation of all functions and their arguments and returns is important for code readability and auditability.

- Some code analysis programs do analysis by reading NatSpec details, if they can't see the tags `(@param, @dev, @return)`, they do incomplete analysis.

### Lines of code

- [ConsiderationStructs.sol:286](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/lib/ConsiderationStructs.sol#L286-L542)
- [PointerLibraries.sol](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/helpers/PointerLibraries.sol)

### Recommended Mitigation Steps 

Include [`NatSpec`](https://docs.soliditylang.org/en/v0.8.15/natspec-format.html) comments in the codebase.

## [NC-06] Constants in comparisons should appear on the left side

Constants in comparisons should appear on the left side, doing so will prevent [typo bug](https://www.moserware.com/2008/01/constants-on-left-are-better-but-this.html).

```solidity
       if (maximumFulfilled == 0) {
```

### Lines of code

- [OrderCombiner.sol:237](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/lib/OrderCombiner.sol#L237)
- [OrderCombiner.sol:256](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/lib/OrderCombiner.sol#L256)
- [OrderCombiner.sol:639](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/lib/OrderCombiner.sol#L639)
- [OrderCombiner.sol:741](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/lib/OrderCombiner.sol#L741)
- [FulfillmentApplier.sol:56](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/lib/FulfillmentApplier.sol#L56)
- [FulfillmentApplier.sol:75](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/lib/FulfillmentApplier.sol#L75)
- [FulfillmentApplier.sol:177](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/lib/FulfillmentApplier.sol#L177)
- [FulfillmentApplier.sol:211](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/lib/FulfillmentApplier.sol#L211)
- [Executor.sol:298](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/lib/Executor.sol#L298)
- [Executor.sol:346](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/lib/Executor.sol#L346)
- [Executor.sol:402](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/lib/Executor.sol#L402)

### Recommended Mitigation Steps

Constants should appear on the left side.

```solidity
       if (0 == maximumFulfilled) {
```

## [NC-07] Use `bytes.concat()` and `string.concat()`

- `bytes.concat()` vs `abi.encodePacked(<bytes>,<bytes>)`
- `string.concat()` vs `abi.encodePacked(<string>,<string>)`

 > https://docs.soliditylang.org/en/v0.8.17/types.html?highlight=bytes.concat#the-functions-bytes-concat-and-string-concat

### Lines of code 

- [ConduitController.sol:76](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/conduit/ConduitController.sol#L76)
- [ConduitController.sol:339](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/conduit/ConduitController.sol#L339)
- [TypehashDirectory.sol:177](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/lib/TypehashDirectory.sol#L177)

### Recommended Mitigation Steps

Use `bytes.concat()` and `string.concat()`.

## [NC-08] Add `I` prefix to interface contracts    

Filename prefixed by `I` usually indicates an interface rather than a contract.

### Lines of code 

- **[All Interfaces](https://github.com/ProjectOpenSea/seaport/tree/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/interfaces)**

### Recommended Mitigation Steps

Add `I` prefix to interface contracts    

## [NC-09] Insufficient coverage   

The test coverage rate of the project is >90%. Testing all functions is best practice in terms of security criteria.

```
- What is the overall line coverage percentage provided by your tests?: >90%
```

### Lines of code

- **All Contracts**

### Recommended Mitigation Steps

Test coverage is expected to be 100%

## [NC-10] Generate perfect code headers every time

I recommend using header for Solidity code layout and readability

> Ref: https://github.com/transmissions11/headers

### Lines of code 

- **All Contracts**

### Recommended Mitigation Steps

```
/*//////////////////////////////////////////////////////////////
                           TESTING 123
//////////////////////////////////////////////////////////////*/
```

## [NC-11] Lock pragmas to specific compiler version

Pragma statements can be allowed to float when a contract is intended for consumption by other developers, as in the case with contracts in a library or EthPM package. Otherwise, the developer would need to manually update the pragma in order to compile locally. 

> Ref: https://swcregistry.io/docs/SWC-103

```solidity
       pragma solidity ^0.8.13;
```

```solidity
       pragma solidity ^0.8.17;
```

### Lines of code 

- **All Contracts**

### Recommended Mitigation Steps

Ethereum Smart Contract Best Practices - Lock pragmas to specific compiler version. 

> https://consensys.github.io/smart-contract-best-practices/development-recommendations/solidity-specific/locking-pragmas/

## [NC-12] There is no need to cast a variable that is already an address, such as `uint(x)`

 There is no need to cast a variable that is already an uint, such as uint(0), 0 is also uint.
 
 ```solidity
        if (identifierOrCriteria != uint256(0)) {
 ```

### Lines of code

- [CriteriaResolution.sol:212](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/lib/CriteriaResolution.sol#L212)
- [Executor.sol:310](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/lib/Executor.sol#L310)

### Recommended Mitigation Steps

Use directly variable.

 ```solidity
        if (identifierOrCriteria != 0) {
 ```
 
## [NC-13] Consider using `delete` rather than assigning zero to clear values    

The `delete` keyword more closely matches the semantics of what is being done, and draws more attention to the changing of state, which may lead to a more thorough audit of its associated logic

```solidity
       advancedOrder.numerator = 0;
```

### Lines of code 

- [OrderCombiner.sol:239](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/lib/OrderCombiner.sol#L239)
- [OrderCombiner.sol:258](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/lib/OrderCombiner.sol#L258)

### Recommended Mitigation Steps

Use the `delete` keyword.

```solidity
       delete advancedOrder.numerator;
```

## [NC-14] Assembly Codes Specific – Should Have Comments  

Since this is a low level language that is more difficult to parse by readers, include extensive documentation, comments on the rationale behind its use, clearly explaining what each assembly instruction does

This will make it easier for users to trust the code, for reviewers to validate the code, and for developers to build on or update the code.

Note that using Aseembly removes several important security features of Solidity, which can make the code more insecure and more error-prone.

### Lines of code

- [PointerLibraries.sol:52](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/helpers/PointerLibraries.sol#L52)
- [PointerLibraries.sol:61](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/helpers/PointerLibraries.sol#L61)
- [PointerLibraries.sol:70](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/helpers/PointerLibraries.sol#L70)
- [ConsiderationBase.sol:274](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/lib/ConsiderationBase.sol#L274)
- [ConsiderationDecoder.sol:563-594](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/lib/ConsiderationDecoder.sol#L563-L594)
- [ConsiderationStructs.sol:286-542](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/lib/ConsiderationStructs.sol#L286-L542)

### Recommended Mitigation Steps

Include NatSpec in assembly codes.

## [NC-15] Adding a `return` statement when the function defines a named return variable, is redundant

```solidity
       return amount;
```

### Lines of code

- [AmountDeriver.sol:87](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/lib/AmountDeriver.sol#L87)
- [BasicOrderFulfiller.sol:902](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/lib/BasicOrderFulfiller.sol#L902)
- [FulfillmentApplier.sol:143](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/lib/FulfillmentApplier.sol#L143)
- [OrderCombiner.sol:651](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/lib/OrderCombiner.sol#L651)
- [OrderCombiner.sol:1047](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/lib/OrderCombiner.sol#L1047)
