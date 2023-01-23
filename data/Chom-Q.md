## Missing revert reference comment

In seaport 1.2 there exists revert reference comments such as

```solidity
                // revert(abi.encodeWithSignature(
                //     "TokenTransferGenericFailure(
                //         address,address,address,uint256,uint256
                //     )", token, from, to, identifier, amount
                // ))
```

This comment relies on above every revert assembly script.

```solidity
                revert(
                    Generic_error_selector_offset,
                    TokenTransferGenericFailure_error_length
                )
```

But there are some lines that this reference comment is missing.

Conduit.sol Line 54 - 62

```solidity
                // The caller is not an open channel; revert with
                // ChannelClosed(caller). First, set error signature in memory.
                mstore(ChannelClosed_error_ptr, ChannelClosed_error_signature)

                // Next, set the caller as the argument.
                mstore(ChannelClosed_channel_ptr, caller())

                // Finally, revert, returning full custom error with argument.
                revert(ChannelClosed_error_ptr, ChannelClosed_error_length)
```

CriteriaResolution.sol Line 125 - 128

```solidity
                        assembly {
                            mstore(0, errorSelector)
                            revert(Error_selector_offset, Selector_length)
                        }
```

FulfillmentApplier.sol Line 719 - 726 should use high level revert snippet instead of human language comment

```solidity
                // Store the InvalidFulfillmentComponentData error signature.
                mstore(0, InvalidFulfillmentComponentData_error_selector)

                // Return, supplying InvalidFulfillmentComponentData signature.
                revert(
                    Error_selector_offset,
                    InvalidFulfillmentComponentData_error_length
                )
```

TokenTransferrer.sol Line 664 - 671

```solidity
                    mstore(
                        Invalid1155BatchTransferEncoding_ptr,
                        Invalid1155BatchTransferEncoding_selector
                    )
                    revert(
                        Invalid1155BatchTransferEncoding_ptr,
                        Invalid1155BatchTransferEncoding_length
                    )
```

ZoneInteraction.sol Line 194 - 201

```solidity
                mstore(0, errorSelector)
                mstore(InvalidRestrictedOrder_error_orderHash_ptr, orderHash)
                revert(
                    Error_selector_offset,
                    InvalidRestrictedOrder_error_length
                )
```

ZoneInteraction.sol Line 207 - 214

```solidity
            assembly {
                mstore(0, errorSelector)
                mstore(InvalidRestrictedOrder_error_orderHash_ptr, orderHash)
                revert(
                    Error_selector_offset,
                    InvalidRestrictedOrder_error_length
                )
            }
```

## Errors without parameters but should have parameters

ConsiderationErrors.sol

* _revertInsufficientEtherSupplied() -> _revertInsufficientEtherSupplied(uint256 suppliedAmount, uint256 requiredAmount)
* _revertCannotCancelOrder() -> _revertCannotCancelOrder(bytes32 orderHash)
* _revertConsiderationLengthNotEqualToTotalOriginal() -> _revertConsiderationLengthNotEqualToTotalOriginal(uint256 considerationLength, uint256 originalLength)