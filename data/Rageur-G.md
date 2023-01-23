## GAS-1: Empty blocks should be removed or emit something

### Description

The code should be refactored such that they no longer exist, or the block should do something useful, such as emitting an event or reverting.

### Affected file

* Assertions.sol (Line: 35)
* BasicOrderFulfiller.sol (Line: 41)
* Consideration.sol (Line: 50)
* Executor.sol (Line: 35)
* GettersAndDerivers.sol (Line: 25)
* OrderCombiner.sol (Line: 41)
* OrderFulfiller.sol (Line: 45)
* OrderValidator.sol (Line: 55)
* Seaport.sol (Line: 93)
* Verifiers.sol (Line: 26)

## GAS-2: Functions guaranteed to revert when called by normal users can be marked payable

### Description

If a function modifier such as onlyOwner is used, the function will revert if a normal user tries to pay the function. Marking the function as payable will lower the gas cost for legitimate callers because the compiler will not include checks for whether a payment was provided.

### Affected file

* Conduit.sol (Line: 92, 127, 154)

## GAS-3: Internal functions not called by the contract should be removed to save deployment gas

### Description

If the functions are required by an interface, the contract should inherit from that interface and use the override keyword.

### Affected file

* AmountDeriver.sol (Line: 159)
* Assertions.sol (Line: 50, 93, 114)
* BasicOrderFulfiller.sol (Line: 68)
* ConsiderationBase.sol (Line: 135, 270)
* ConsiderationDecoder.sol (Line: 378, 477, 517, 609, 652, 723, 764, 804, 1010, 1045, 1072, 1099, 1127, 1155, 1183, 1213, 1241, 1269, 1295)
* ConsiderationEncoder.sol (Line: 93, 198, 318, 448)
* ConsiderationStructs.sol (Line: 287, 295, 303, 311, 319, 327, 335, 343, 351, 359, 367, 375, 383, 391, 399, 407, 415, 423, 431, 439, 447, 455, 463, 471, 479, 487, 495, 503, 511, 519, 527, 535)
* CounterManager.sol (Line: 33, 74)
* CriteriaResolution.sol (Line: 44)
* Executor.sol (Line: 51, 125)
* FulfillmentApplier.sol (Line: 48, 166)
* GettersAndDerivers.sol (Line: 40, 245, 310, 344)
* LowLevelHelpers.sol (Line: 18, 81, 98, 114)
* OrderCombiner.sol (Line: 106, 932)
* OrderFulfiller.sol (Line: 75)
* OrderValidator.sol (Line: 65, 110, 649, 736, 828)
* ReentrancyGuard.sol (Line: 37, 53, 73)
* Seaport.sol (Line: 101, 116)
* SignatureVerification.sol (Line: 34)
* TokenTransferrer.sol (Line: 35, 265, 404, 563)
* Verifiers.sol (Line: 39, 71, 230)
* ZoneInteraction.sol (Line: 39, 77)

## GAS-4: Replace modifier with function

### Description

Modifiers make code more elegant, but cost more than normal functions.

### Affected file

* Conduit.sol (Line: 40)

## GAS-5: Storage pointer to a structure is cheaper than copying each value of the structure into memory, same for array and mapping

### Description

It may not be obvious, but every time you copy a storage struct/array/mapping to a memory variable, you are literally copying each member by reading it from storage, which is expensive. And when you use the storage keyword, you are just storing a pointer to the storage, which is much cheaper.

### Affected file

* BasicOrderFulfiller.sol (Line: 206)
* ConsiderationBase.sol (Line: 200, 212, 225, 260)

## GAS-6: Using private rather than public for constants saves gas

### Description

If needed, the values can be read from the verified contract source code, or if there are multiple values there can be a single getter function that returns a tuple of the values of all currently-public constants. Saves 3406-3606 gas in deployment gas due to the compiler not having to create non-payable getter functions for deployment calldata, not having to store the bytes of the value outside of where it’s used, and not adding another entry to the method ID table.

### Affected file

* TypehashDirectory.sol (Line: 14, 15, 18, 20, 21, 22, 23, 24)