## Noncritical

### Replace "ETH" with "Native token"

Seaport 1.2. has mostly replaced references to "ETH" in comments and function names with "native token," but there are a few exceptions. Consider replacing the following usages of "ETH" with "native token" or similar.

[`Seaport.sol`](https://github.com/horsefacts/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/Seaport.sol#L77-L83):

```solidity
 * @notice Seaport is a generalized ETH/ERC20/ERC721/ERC1155 marketplace with
 *         lightweight methods for common routes as well as more flexible
 *         methods for composing advanced orders or groups of orders. Each order
 *         contains an arbitrary number of items that may be spent (the "offer")
 *         along with an arbitrary number of items that must be received back by
 *         the indicated recipients (the "consideration").
 */
```

[`SeaportInterface.sol`](https://github.com/horsefacts/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/interfaces/SeaportInterface.sol#L19-L23):

```solidity
 * @notice Seaport is a generalized ETH/ERC20/ERC721/ERC1155 marketplace. It
 *         minimizes external calls to the greatest extent possible and provides
 *         lightweight methods for common routes as well as more flexible
 *         methods for composing advanced orders.
 *
```

[`Consideration.sol`](https://github.com/horsefacts/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/lib/Consideration.sol#L34-L40):

```solidity
 * @notice Consideration is a generalized ETH/ERC20/ERC721/ERC1155 marketplace
 *         that provides lightweight methods for common routes as well as more
 *         flexible methods for composing advanced orders or groups of orders.
 *         Each order contains an arbitrary number of items that may be spent
 *         (the "offer") along with an arbitrary number of items that must be
 *         received back by the indicated recipients (the "consideration").
 */
```

[`ConsiderationInterface.sol`](https://github.com/horsefacts/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/interfaces/ConsiderationInterface.sol#L19-L23):

```solidity
 * @notice Consideration is a generalized ETH/ERC20/ERC721/ERC1155 marketplace.
 *         It minimizes external calls to the greatest extent possible and
 *         provides lightweight methods for common routes as well as more
 *         flexible methods for composing advanced orders.
 *
```

[`ConsiderationEventsAndErrors.sol`](https://github.com/horsefacts/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/interfaces/ConsiderationEventsAndErrors.sol#L205-L210):

```solidity
    /**
     * @dev Revert with an error when attempting to fulfill an order with an
     *      offer for ETH outside of matching orders.
     */
    error InvalidNativeOfferItem();
}
```

[`BasicOrderFulfiller#_validateAndFulfillBasicOrder`](https://github.com/horsefacts/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/lib/BasicOrderFulfiller.sol#L90-L92):

```solidity

            // If route > 1 additionalRecipient items are ERC20 (1) else Eth (0)
            additionalRecipientsItemType := gt(route, 1)
```

[`BasicOrderFulfiller#_validateAndFulfillBasicOrder`](https://github.com/horsefacts/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/lib/BasicOrderFulfiller.sol#L140-L142):

```solidity
                // If route > 2, receivedItemType is route - 2. If route is 2,
                // the receivedItemType is ERC20 (1). Otherwise, it is Eth (0).
                receivedItemType := byte(route, BasicOrder_receivedItemByteMap)
```

[`Executor#_transferNativeTokens`](https://github.com/horsefacts/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/lib/Executor.sol#L239-L242):

```solidity
        assembly {
            // Transfer the ETH and store if it succeeded or not.
            success := call(gas(), to, amount, 0, 0, 0, 0)
        }
```

[`ConsiderationEventsAndErrors#InsufficientEtherSupplied`](https://github.com/horsefacts/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/interfaces/ConsiderationEventsAndErrors.sol#L138-L143):

```solidity

    /**
     * @dev Revert with an error when insufficient ether is supplied as part of
     *      msg.value when fulfilling orders.
     */
    error InsufficientEtherSupplied();
```

[`ConsiderationConstants.sol`](https://github.com/horsefacts/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/lib/ConsiderationConstants.sol#L833-L841):

```solidity
/*
 *  error InsufficientEtherSupplied()
 *    - Defined in ConsiderationEventsAndErrors.sol
 *  Memory layout:
 *    - 0x00: Left-padded selector (data begins at 0x1c)
 * Revert buffer is memory[0x1c:0x20]
 */
uint256 constant InsufficientEtherSupplied_error_selector = 0x1a783b8d;
uint256 constant InsufficientEtherSupplied_error_length = 0x04;
```

[`ConsiderationErrors.sol`](https://github.com/horsefacts/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/lib/ConsiderationErrors.sol#L77-L90):

```solidity
/**
 * @dev Reverts the current transaction with an "InsufficientEtherSupplied"
 *      error message.
 */
function _revertInsufficientEtherSupplied() pure {
    assembly {
        // Store left-padded selector with push4 (reduces bytecode),
        // mem[28:32] = selector
        mstore(0, InsufficientEtherSupplied_error_selector)

        // revert(abi.encodeWithSignature("InsufficientEtherSupplied()"))
        revert(Error_selector_offset, InsufficientEtherSupplied_error_length)
    }
}
```

[`ConsiderationEventsAndErrors.sol`](https://github.com/horsefacts/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/interfaces/ConsiderationEventsAndErrors.sol#L145-L148):

```solidity
    /**
     * @dev Revert with an error when an ether transfer reverts.
     */
    error EtherTransferGenericFailure(address account, uint256 amount);
```

[`ConsiderationConstants.sol`](https://github.com/horsefacts/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/lib/ConsiderationConstants.sol#L843-L855):

```solidity
/*
 *  error EtherTransferGenericFailure(address account, uint256 amount)
 *    - Defined in ConsiderationEventsAndErrors.sol
 *  Memory layout:
 *    - 0x00: Left-padded selector (data begins at 0x1c)
 *    - 0x20: account
 *    - 0x40: amount
 * Revert buffer is memory[0x1c:0x60]
 */
uint256 constant EtherTransferGenericFailure_error_selector = 0x470c7c1d;
uint256 constant EtherTransferGenericFailure_error_account_ptr = 0x20;
uint256 constant EtherTransferGenericFailure_error_amount_ptr = 0x40;
uint256 constant EtherTransferGenericFailure_error_length = 0x44;
```

[`Executor.sol`](https://github.com/horsefacts/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/lib/Executor.sol#L249-L263):

```solidity
            // Otherwise, revert with a generic error message.
            assembly {
                // Store left-padded selector with push4, mem[28:32] = selector
                mstore(0, EtherTransferGenericFailure_error_selector)
                mstore(EtherTransferGenericFailure_error_account_ptr, to)
                mstore(EtherTransferGenericFailure_error_amount_ptr, amount)

                // revert(abi.encodeWithSignature(
                //   "EtherTransferGenericFailure(address,uint256)", to, amount)
                // )
                revert(
                    Error_selector_offset,
                    EtherTransferGenericFailure_error_length
                )
            }
```

### Extract or use named constants

The Seaport codebase has done an impressive job avoiding "magic numbers" and using named constants, which makes inline assembly much easier to read, understand, and verify. However, there are a few remaining numbers that could be replaced with more readable named constants.

The `malloc` free function in `PointerLibraries.sol` can use `FreeMemoryPointerSlot` in place of `0x40`:

[`PointerLibraries#malloc`](https://github.com/horsefacts/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/helpers/PointerLibraries.sol#L24-L33):

```solidity
/// @dev Allocates `size` bytes in memory by increasing the free memory pointer
///    and returns the memory pointer to the first byte of the allocated region.
// (Free functions cannot have visibility.)
// solhint-disable-next-line func-visibility
function malloc(uint256 size) pure returns (MemoryPointer mPtr) {
    assembly {
        mPtr := mload(0x40)
        mstore(0x40, add(mPtr, size))
    }
}
```

Calldata readers in `PointerLibraries.sol` can use `OneWord` in place of `0x20`:

[`CallDataReaders#readBool`](https://github.com/horsefacts/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/helpers/PointerLibraries.sol#L1196-L1204)

```solidity
    /// @dev Reads the bool at `rdPtr` in returndata.
    function readBool(
        ReturndataPointer rdPtr
    ) internal pure returns (bool value) {
        assembly {
            returndatacopy(0, rdPtr, 0x20)
            value := mload(0)
        }
    }
```

(Note that `returndatacopy(0, rdPtr, 0x20)` is repeated in every `CallDataReaders#readType` function.)

`CalldataPointerLib#next` can use `OneWord` in place of `32`:

[`CalldataPointerLib#next`](https://github.com/horsefacts/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/helpers/PointerLibraries.sol#L96-L103)

```solidity
    /// @dev Returns the calldata pointer one word after `cdPtr`.
    function next(
        CalldataPointer cdPtr
    ) internal pure returns (CalldataPointer cdPtrNext) {
        assembly {
            cdPtrNext := add(cdPtr, 32)
        }
    }
```

Similar usages:
- [`MemoryPointerLib#next`](https://github.com/horsefacts/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/helpers/PointerLibraries.sol#L257-L264)
- [`ReturnDataPointerLib#next`](https://github.com/horsefacts/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/helpers/PointerLibraries.sol#L177-L184)

`OrderCombiner` iterates in increments of 32, which could be replaced with `OneWord`:

[`OrderCombiner`](https://github.com/horsefacts/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/lib/OrderCombiner.sol#L219-L220):

```solidity
            // Determine the memory offset to terminate on during loops.
            terminalMemoryOffset = (totalOrders + 1) * 32;
```

[`OrderCombiner`](https://github.com/horsefacts/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/lib/OrderCombiner.sol#L229-L234):

```solidity
            // Iterate over each order.
            for (uint256 i = 32; i < terminalMemoryOffset; i += 32) {
                // Retrieve order using assembly to bypass out-of-range check.
                assembly {
                    advancedOrder := mload(add(advancedOrders, i))
                }
```

### Fragile check for contract order type

The `OrderType` enum defines five order types. Only one of these represents contract orders:

[`ConsiderationEnums.sol`](https://github.com/horsefacts/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/lib/ConsiderationEnums.sol#L5-L20):

```solidity
enum OrderType {
    // 0: no partial fills, anyone can execute
    FULL_OPEN,

    // 1: partial fills supported, anyone can execute
    PARTIAL_OPEN,

    // 2: no partial fills, only offerer or zone can execute
    FULL_RESTRICTED,

    // 3: partial fills supported, only offerer or zone can execute
    PARTIAL_RESTRICTED,

    // 4: contract order type
    CONTRACT
}
```

[`OrderCombiner#_validateOrdersAndPrepareToFulfill`](https://github.com/horsefacts/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/lib/OrderCombiner.sol#L286-L295) defines non-contract orders as any order with a type less than 4:

```solidity
                {
                    // Create a variable indicating if the order is not a
                    // contract order. Cache in scratch space to avoid stack
                    // depth errors.
                    OrderType orderType = advancedOrder.parameters.orderType;
                    assembly {
                        let isNonContract := lt(orderType, 4)
                        mstore(0, isNonContract)
                    }
                }
```

This is fine for now, but could be fragile: if an additional type is added in the future, it may break this implicit assumption. Consider checking for an exact match against order type 4, which is more robust:

```solidity
                {
                    // Create a variable indicating if the order is not a
                    // contract order. Cache in scratch space to avoid stack
                    // depth errors.
                    OrderType orderType = advancedOrder.parameters.orderType;
                    assembly {
                        let isNonContract := iszero(eq(orderType, 4))
                        mstore(0, isNonContract)
                    }
                }
```

[`OrderFulfiller#_applyFractionsAndTransferEach`](https://github.com/horsefacts/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/lib/OrderFulfiller.sol#L258-L271) performs a similar check using `lt(orderType, 4)`:

```solidity
            // If non-contract order has native offer items, throw InvalidNativeOfferItem.
            {
                OrderType orderType = orderParameters.orderType;
                uint256 invalidNativeOfferItem;
                assembly {
                    invalidNativeOfferItem := and(
                        lt(orderType, 4),
                        anyNativeItems
                    )
                }
                if (invalidNativeOfferItem != 0) {
                    _revertInvalidNativeOfferItem();
                }
            }
```


### Inconsistent use of hex vs. decimal values

Almost all values except for bit shifts are defined in hex, with the following few exceptions:

`CalldataPointerLib` uses `32` rather than `0x20` in a few places:

[`CalldataPointerLib#next`](https://github.com/horsefacts/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/helpers/PointerLibraries.sol#L96-L103)

```solidity
    /// @dev Returns the calldata pointer one word after `cdPtr`.
    function next(
        CalldataPointer cdPtr
    ) internal pure returns (CalldataPointer cdPtrNext) {
        assembly {
            cdPtrNext := add(cdPtr, 32)
        }
    }
```

Similar usages:
- [`MemoryPointerLib#next`](https://github.com/horsefacts/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/helpers/PointerLibraries.sol#L257-L264)
- [`ReturnDataPointerLib#next`](https://github.com/horsefacts/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/helpers/PointerLibraries.sol#L177-L184)

Two lengths in `ConsiderationConstants`:

[`NameLengthPtr`](https://github.com/horsefacts/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/lib/ConsiderationConstants.sol#L41-L42):

```solidity
uint256 constant NameLengthPtr = 77;
```

[`Selector_length`](https://github.com/horsefacts/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/lib/ConsiderationConstants.sol#L76-L77):

```solidity
uint256 constant Selector_length = 4;
```

Precompile addresses:

[`PointerLibraries#IdentityPrecompileAddress`](https://github.com/horsefacts/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/helpers/PointerLibraries.sol#L21-L22):

```solidity
uint256 constant IdentityPrecompileAddress = 4;
```
[`ConsiderationConstants.sol`](https://github.com/horsefacts/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/lib/ConsiderationConstants.sol#L244-L245):

```solidity
address constant IdentityPrecompile = address(4);
```
[`ConsiderationConstants.sol`](https://github.com/horsefacts/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/lib/ConsiderationConstants.sol#L439-L440):

```solidity
uint256 constant Ecrecover_precompile = 1;
```

Consider converting all of these to hex to enhance readability.

### Custom comment typos:

There are two `@custom:name` comments on functions in `Consideration.sol` that are meant to annotate unnamed input arguments, but are incorrectly annotating the function's return type:

[`Consideration#validate`](https://github.com/horsefacts/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/lib/Consideration.sol#L615-L629):

```solidity
    function validate(
        Order[] calldata
    )
        external
        override
        returns (
            /**
             * @custom:name orders
             */
            bool /* validated */
        )
    {
        return
            _validate(_toOrdersReturnType(_decodeOrders)(CalldataStart.pptr()));
    }
```

[`Consideration#getOrderHash`](https://github.com/horsefacts/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/lib/Consideration.sol#L651-L674):

```solidity
    function getOrderHash(
        OrderComponents calldata
    )
        external
        view
        override
        returns (
            /**
             * @custom:name order
             */
            bytes32 orderHash
        )
    {
        CalldataPointer orderPointer = CalldataStart.pptr();

        // Derive order hash by supplying order parameters along with counter.
        orderHash = _deriveOrderHash(
            _toOrderParametersReturnType(
                _decodeOrderComponentsAsOrderParameters
            )(orderPointer),
            // Read order counter
            orderPointer.offset(OrderParameters_counter_offset).readUint256()
        );
    }
```

### `AlmostOneWord` is confusing

I find the `AlmostOneWord` constant, which is equal to 31 bytes, pretty confusing in context, since it's not clear from the name what it means to be equal to "almost one word." Consider whether `ThirtyOneBytes` or similar might be a clearer name.

### Typos in comments

The default order numerator + denominator values are _always_ 1 and 1, so this `e.g.` in [`ConsiderationDecoder.sol`](https://github.com/horsefacts/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/lib/ConsiderationDecoder.sol#L351-L353) should be an `i.e.`:

```solidity
        // Write default Order numerator and denominator values (e.g. 1/1).
        mPtr.offset(AdvancedOrder_numerator_offset).write(1);
        mPtr.offset(AdvancedOrder_denominator_offset).write(1);
```

### Duplicated constants

[`TypeHashDirectory`](https://github.com/horsefacts/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/lib/TypehashDirectory.sol#L20-L24) defines several constants, like `OneWord`, `OneWordShift`, `AlmostOneWord`, and `FreeMemoryPointerSlot` that are defined elsewhere in the codebase. Consider extracting these to a shared constants file:

```solidity
    uint256 internal constant OneWord = 0x20;
    uint256 internal constant OneWordShift = 5;
    uint256 internal constant AlmostOneWord = 0x1f;
    uint256 internal constant FreeMemoryPointerSlot = 0x40;
```