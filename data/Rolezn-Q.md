## Summary<a name="Summary">

### Low Risk Issues
| |Issue|Contexts|
|-|:-|:-:|
| [LOW&#x2011;1](#LOW&#x2011;1) | Low Level Calls With Solidity Version 0.8.14 Can Result In Optimiser Bug | 3 |
| [LOW&#x2011;2](#LOW&#x2011;2) | Missing Checks for Address(0x0)  | 2 |
| [LOW&#x2011;3](#LOW&#x2011;3) | Remove unused code | 1 |
| [LOW&#x2011;4](#LOW&#x2011;4) | Use `safeTransferOwnership` instead of `transferOwnership` function | 1 |

Total: 7 contexts over 3 issues

### Non-critical Issues
| |Issue|Contexts|
|-|:-|:-:|
| [NC&#x2011;1](#NC&#x2011;1) | Compliance with Solidity Style rules in Constant expressions | All in-scope contracts |
| [NC&#x2011;2](#NC&#x2011;2) | Function creates dirty bits | 8 |
| [NC&#x2011;3](#NC&#x2011;3) | Function writing that does not comply with the Solidity Style Guide  | All in-scope contracts |
| [NC&#x2011;4](#NC&#x2011;4) | Use `delete` to Clear Variables | 1 |
| [NC&#x2011;5](#NC&#x2011;5) | NatSpec return parameters should be included in contracts | All in-scope contracts |
| [NC&#x2011;6](#NC&#x2011;6) | No need to initialize uints to zero | 3 |
| [NC&#x2011;7](#NC&#x2011;7) | Implementation contract may not be initialized | 15 |
| [NC&#x2011;8](#NC&#x2011;8) | NatSpec comments should be increased in contracts | All in-scope contracts |
| [NC&#x2011;9](#NC&#x2011;9) | Non-usage of specific imports | 28 |
| [NC&#x2011;10](#NC&#x2011;10) | Use a more recent version of Solidity | 32 |
| [NC&#x2011;11](#NC&#x2011;11) | Omissions in Events | 1 |
| [NC&#x2011;12](#NC&#x2011;12) | Adding A Return Statement When The Function Defines A Named Return Variable, Is Redundant | 2 |
| [NC&#x2011;13](#NC&#x2011;13) | Use `bytes.concat()` | 3 |

Total: 309 contexts over 13 issues

## Low Risk Issues

### <a href="#Summary">[LOW&#x2011;1]</a><a name="LOW&#x2011;1"> Low Level Calls With Solidity Version Before 0.8.14 Can Result In Optimiser Bug

The project contracts in scope are using low level calls with solidity version before 0.8.14 which can result in optimizer bug.
https://medium.com/certora/overly-optimistic-optimizer-certora-bug-disclosure-2101e3f7994d

Simliar findings in Code4rena contests for reference:
https://code4rena.com/reports/2022-06-illuminate/#5-low-level-calls-with-solidity-version-0814-can-result-in-optimiser-bug

#### <ins>Proof Of Concept</ins>

POC can be found in the above medium reference url.

Functions that execute low level calls in contracts with solidity version under 0.8.14

```solidity
29: assembly {
        mPtr := mload(0x40)
        mstore(0x40, add(mPtr, size))
    }
```

https://github.com/ProjectOpenSea/seaport/tree/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/helpers/PointerLibraries.sol#L29

```solidity
3081: assembly {
            mstore(mPtr, value)
        }
```

https://github.com/ProjectOpenSea/seaport/tree/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/helpers/PointerLibraries.sol#L3081

```solidity
3074: assembly {
            mstore(mPtr, value)
        }
```

https://github.com/ProjectOpenSea/seaport/tree/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/helpers/PointerLibraries.sol#L3074






#### <ins>Recommended Mitigation Steps</ins>

Consider upgrading to at least solidity v0.8.15.



### <a href="#Summary">[LOW&#x2011;2]</a><a name="LOW&#x2011;2"> Missing Checks for Address(0x0) 

Lack of zero-address validation on address parameters may lead to transaction reverts, waste gas, require resubmission of transactions and may even force contract redeployments in certain cases within the protocol.

#### <ins>Proof Of Concept</ins>


```solidity
126: function updateChannel: address channel
```

https://github.com/ProjectOpenSea/seaport/tree/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/conduit/ConduitController.sol#L126



#### <ins>Recommended Mitigation Steps</ins>

Consider adding explicit zero-address validation on input parameters of address type.



### <a href="#Summary">[LOW&#x2011;3]</a><a name="LOW&#x2011;3"> Remove unused code
This code is not used in the main project contract files, remove it or add event-emit
Code that is not in use, suggests that they should not be present and could potentially contain insecure functionalities.

#### <ins>Proof Of Concept</ins>


```solidity
function writeInt(MemoryPointer mPtr, int256 value) internal pure {
        assembly {
            mstore(mPtr, value)
        }
    }
```

https://github.com/ProjectOpenSea/seaport/tree/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/helpers/PointerLibraries.sol#L3088






### <a href="#Summary">[LOW&#x2011;4]</a><a name="LOW&#x2011;4"> Use `safeTransferOwnership` instead of `transferOwnership` function

Use `safeTransferOwnership` which is safer. Use it as it is more secure due to 2-stage ownership transfer.

#### <ins>Proof Of Concept</ins>


```solidity
202: function transferOwnership: function transferOwnership(
```

https://github.com/ProjectOpenSea/seaport/tree/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/conduit/ConduitController.sol#L202



#### <ins>Recommended Mitigation Steps</ins>

Use <a href="https://github.com/OpenZeppelin/openzeppelin-contracts/blob/master/contracts/access/Ownable2Step.sol">Ownable2Step.sol</a>

```solidity
    function acceptOwnership() external {
        address sender = _msgSender();
        require(pendingOwner() == sender, "Ownable2Step: caller is not the new owner");
        _transferOwnership(sender);
    }
}
```



## Non Critical Issues





### <a href="#Summary">[NC&#x2011;1]</a><a name="NC&#x2011;1"> Compliance with Solidity Style rules in Constant expressions

#### <ins>Proof Of Concept</ins>

Here are following some examples, but this issue persists thorugh all in-scope contracts.


```solidity
5: uint256 constant ChannelClosed_error_signature = (
```

https://github.com/ProjectOpenSea/seaport/tree/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/conduit/lib/ConduitConstants.sol#L5

```solidity
8: uint256 constant ChannelClosed_error_ptr = 0x00;
```

https://github.com/ProjectOpenSea/seaport/tree/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/conduit/lib/ConduitConstants.sol#L8

```solidity
9: uint256 constant ChannelClosed_channel_ptr = 0x4;
```

https://github.com/ProjectOpenSea/seaport/tree/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/conduit/lib/ConduitConstants.sol#L9

```solidity
10: uint256 constant ChannelClosed_error_length = 0x24;
```

https://github.com/ProjectOpenSea/seaport/tree/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/conduit/lib/ConduitConstants.sol#L10

```solidity
16: uint256 constant ChannelKey_channel_ptr = 0x00;
```

https://github.com/ProjectOpenSea/seaport/tree/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/conduit/lib/ConduitConstants.sol#L16

```solidity
17: uint256 constant ChannelKey_slot_ptr = 0x20;
```

https://github.com/ProjectOpenSea/seaport/tree/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/conduit/lib/ConduitConstants.sol#L17

```solidity
18: uint256 constant ChannelKey_length = 0x40;
```

https://github.com/ProjectOpenSea/seaport/tree/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/conduit/lib/ConduitConstants.sol#L18

```solidity
19: CalldataPointer constant CalldataStart = CalldataPointer.wrap(0x04);
```

https://github.com/ProjectOpenSea/seaport/tree/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/helpers/PointerLibraries.sol#L19

```solidity
20: MemoryPointer constant FreeMemoryPPtr = MemoryPointer.wrap(0x40);
```

https://github.com/ProjectOpenSea/seaport/tree/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/helpers/PointerLibraries.sol#L20

```solidity
21: uint256 constant IdentityPrecompileAddress = 4;
```

https://github.com/ProjectOpenSea/seaport/tree/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/helpers/PointerLibraries.sol#L21

```solidity
22: uint256 constant OffsetOrLengthMask = 0xffffffff;
```

https://github.com/ProjectOpenSea/seaport/tree/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/helpers/PointerLibraries.sol#L22


```solidity
41: uint256 constant NameLengthPtr = 77;
```

https://github.com/ProjectOpenSea/seaport/tree/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/lib/ConsiderationConstants.sol#L41

```solidity
42: uint256 constant NameWithLength = 0x0d436F6E73696465726174696F6E;
```

https://github.com/ProjectOpenSea/seaport/tree/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/lib/ConsiderationConstants.sol#L42

```solidity
44: uint256 constant information_version_offset = 0;
```

https://github.com/ProjectOpenSea/seaport/tree/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/lib/ConsiderationConstants.sol#L44









### <a href="#Summary">[NC&#x2011;2]</a><a name="NC&#x2011;2"> Function creates dirty bits

This explanation should be added in the NatSpec comments of this function that sends ether with call;

Note that this code probably isn’t secure or a good use case for assembly because a lot of memory management and security checks are bypassed.
Use with caution! Some functions in this contract knowingly create dirty bits at the destination of the free memory pointer.

#### <ins>Proof Of Concept</ins>


```solidity
241: function _transferNativeTokens(
        address payable to,
        uint256 amount
    ) internal {
        
        _assertNonZeroAmount(amount);

        
        bool success;

        assembly {
            
            success := call(gas(), to, amount, 0, 0, 0, 0)
        }

        
        if (!success) {
            
            _revertWithReasonIfOneIsReturned();

            
            assembly {
                
                mstore(0, EtherTransferGenericFailure_error_selector)
                mstore(EtherTransferGenericFailure_error_account_ptr, to)
                mstore(EtherTransferGenericFailure_error_amount_ptr, amount)

                
                
                
                revert(
                    Error_selector_offset,
                    EtherTransferGenericFailure_error_length
                )
            }
        }
    }

```

https://github.com/ProjectOpenSea/seaport/tree/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/lib/Executor.sol#L241

```solidity
538: function _callConduitUsingOffsets(
        bytes32 conduitKey,
        uint256 callDataOffset,
        uint256 callDataSize
    ) internal {
        
        address conduit = _deriveConduit(conduitKey);

        bool success;
        bytes4 result;

        
        assembly {
            
            mstore(0, 0)

            
            success := call(
                gas(),
                conduit,
                0,
                callDataOffset,
                callDataSize,
                0,
                OneWord
            )

            
            result := mload(0)
        }

        
        if (!success) {
            
            _revertWithReasonIfOneIsReturned();

            
            _revertInvalidCallToConduit(conduit);
        }

        
        if (result != ConduitInterface.execute.selector) {
            _revertInvalidConduit(conduitKey, conduit);
        }
    }

```

https://github.com/ProjectOpenSea/seaport/tree/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/lib/Executor.sol#L538

```solidity
497: function _getGeneratedOrder(
        OrderParameters memory orderParameters,
        bytes memory context,
        bool revertOnInvalid
    )
        internal
        returns (bytes32 orderHash, uint256 numerator, uint256 denominator)
    {
        
        
        if (
            orderParameters.consideration.length !=
            orderParameters.totalOriginalConsiderationItems
        ) {
            _revertConsiderationLengthNotEqualToTotalOriginal();
        }

        {
            address offerer = orderParameters.offerer;
            bool success;
            (MemoryPointer cdPtr, uint256 size) = _encodeGenerateOrder(
                orderParameters,
                context
            );
            assembly {
                success := call(gas(), offerer, 0, cdPtr, size, 0, 0)
            }

            {
                
                uint256 contractNonce;
                unchecked {
                    
                    
                    
                    
                    contractNonce = _contractNonces[offerer]++;
                }

                assembly {
                    
                    orderHash := xor(
                        contractNonce,
                        shl(ContractOrder_orderHash_offerer_shift, offerer)
                    )
                }
            }

            
            if (!success) {
                return _revertOrReturnEmpty(revertOnInvalid, orderHash);
            }
        }

        
        (
            uint256 errorBuffer,
            OfferItem[] memory offer,
            ConsiderationItem[] memory consideration
        ) = _convertGetGeneratedOrderResult(_decodeGenerateOrderReturndata)();

        
        if (errorBuffer != 0) {
            return _revertOrReturnEmpty(revertOnInvalid, orderHash);
        }

        {
            
            uint256 originalOfferLength = orderParameters.offer.length;
            uint256 newOfferLength = offer.length;

            
            if (originalOfferLength > newOfferLength) {
                return _revertOrReturnEmpty(revertOnInvalid, orderHash);
            }

            
            for (uint256 i = 0; i < originalOfferLength; ) {
                
                MemoryPointer mPtrOriginal = orderParameters
                    .offer[i]
                    .toMemoryPointer();

                
                MemoryPointer mPtrNew = offer[i].toMemoryPointer();

                
                errorBuffer |=
                    _cast(
                        mPtrOriginal
                            .offset(Common_amount_offset)
                            .readUint256() >
                            mPtrNew.offset(Common_amount_offset).readUint256()
                    ) |
                    _compareItems(mPtrOriginal, mPtrNew);

                
                unchecked {
                    ++i;
                }
            }

            
            orderParameters.offer = offer;
        }

        {
            
            ConsiderationItem[] memory originalConsiderationArray = (
                orderParameters.consideration
            );
            uint256 newConsiderationLength = consideration.length;

            
            if (newConsiderationLength > originalConsiderationArray.length) {
                return _revertOrReturnEmpty(revertOnInvalid, orderHash);
            }

            
            for (uint256 i = 0; i < newConsiderationLength; ) {
                
                MemoryPointer mPtrOriginal = originalConsiderationArray[i]
                    .toMemoryPointer();

                
                MemoryPointer mPtrNew = consideration[i].toMemoryPointer();

                
                
                errorBuffer |=
                    _cast(
                        mPtrNew.offset(Common_amount_offset).readUint256() >
                            mPtrOriginal
                                .offset(Common_amount_offset)
                                .readUint256()
                    ) |
                    _compareItems(mPtrOriginal, mPtrNew) |
                    _checkRecipients(
                        mPtrOriginal
                            .offset(ConsiderItem_recipient_offset)
                            .readAddress(),
                        mPtrNew
                            .offset(ConsiderItem_recipient_offset)
                            .readAddress()
                    );

                
                unchecked {
                    ++i;
                }
            }

            
            orderParameters.consideration = consideration;
        }

        
        if (errorBuffer != 0) {
            return _revertOrReturnEmpty(revertOnInvalid, orderHash);
        }

        
        return (orderHash, 1, 1);
    }

```

https://github.com/ProjectOpenSea/seaport/tree/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/lib/OrderValidator.sol#L497

```solidity
59: function _performERC20Transfer(
        address token,
        address from,
        address to,
        uint256 amount
    ) internal {
        
        assembly {
            
            
            let memPointer := mload(FreeMemoryPointerSlot)

            
            mstore(ERC20_transferFrom_sig_ptr, ERC20_transferFrom_signature)
            mstore(ERC20_transferFrom_from_ptr, from)
            mstore(ERC20_transferFrom_to_ptr, to)
            mstore(ERC20_transferFrom_amount_ptr, amount)

            
            
            
            
            
            
            let callStatus := call(
                gas(),
                token,
                0,
                ERC20_transferFrom_sig_ptr,
                ERC20_transferFrom_length,
                0,
                OneWord
            )

            
            let success := and(
                
                
                
                or(
                    and(eq(mload(0), 1), gt(returndatasize(), 31)),
                    iszero(returndatasize())
                ),
                callStatus
            )

            
            
            
            
            if iszero(and(success, iszero(iszero(returndatasize())))) {
                
                
                
                if iszero(and(iszero(iszero(extcodesize(token))), success)) {
                    
                    if iszero(success) {
                        
                        if iszero(callStatus) {
                            
                            
                            if returndatasize() {
                                
                                
                                
                                
                                
                                let returnDataWords := shr(
                                    OneWordShift,
                                    add(returndatasize(), AlmostOneWord)
                                )

                                
                                
                                
                                
                                let msizeWords := shr(OneWordShift, memPointer)

                                
                                let cost := mul(CostPerWord, returnDataWords)

                                
                                if gt(returnDataWords, msizeWords) {
                                    cost := add(
                                        cost,
                                        add(
                                            mul(
                                                sub(
                                                    returnDataWords,
                                                    msizeWords
                                                ),
                                                CostPerWord
                                            ),
                                            shr(
                                                MemoryExpansionCoefficientShift,
                                                sub(
                                                    mul(
                                                        returnDataWords,
                                                        returnDataWords
                                                    ),
                                                    mul(msizeWords, msizeWords)
                                                )
                                            )
                                        )
                                    )
                                }

                                
                                
                                
                                if lt(add(cost, ExtraGasBuffer), gas()) {
                                    
                                    
                                    returndatacopy(0, 0, returndatasize())

                                    
                                    
                                    revert(0, returndatasize())
                                }
                            }

                            
                            mstore(
                                0,
                                TokenTransferGenericFailure_error_selector
                            )
                            mstore(
                                TokenTransferGenericFailure_error_token_ptr,
                                token
                            )
                            mstore(
                                TokenTransferGenericFailure_error_from_ptr,
                                from
                            )
                            mstore(TokenTransferGenericFailure_error_to_ptr, to)
                            mstore(
                                TokenTransferGenericFailure_err_identifier_ptr,
                                0
                            )
                            mstore(
                                TokenTransferGenericFailure_error_amount_ptr,
                                amount
                            )

                            
                            
                            
                            
                            
                            revert(
                                Generic_error_selector_offset,
                                TokenTransferGenericFailure_error_length
                            )
                        }

                        
                        

                        
                        mstore(
                            0,
                            BadReturnValueFromERC20OnTransfer_error_selector
                        )
                        mstore(
                            BadReturnValueFromERC20OnTransfer_error_token_ptr,
                            token
                        )
                        mstore(
                            BadReturnValueFromERC20OnTransfer_error_from_ptr,
                            from
                        )
                        mstore(
                            BadReturnValueFromERC20OnTransfer_error_to_ptr,
                            to
                        )
                        mstore(
                            BadReturnValueFromERC20OnTransfer_error_amount_ptr,
                            amount
                        )

                        
                        
                        
                        
                        
                        revert(
                            Generic_error_selector_offset,
                            BadReturnValueFromERC20OnTransfer_error_length
                        )
                    }

                    
                    
                    mstore(0, NoContract_error_selector)
                    mstore(NoContract_error_account_ptr, token)

                    
                    
                    
                    revert(
                        Generic_error_selector_offset,
                        NoContract_error_length
                    )
                }

                
                
                
            }

            
            mstore(FreeMemoryPointerSlot, memPointer)

            
            mstore(ZeroSlot, 0)
        }
    }

```

https://github.com/ProjectOpenSea/seaport/tree/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/lib/TokenTransferrer.sol#L59

```solidity
296: function _performERC721Transfer(
        address token,
        address from,
        address to,
        uint256 identifier
    ) internal {
        
        assembly {
            
            if iszero(extcodesize(token)) {
                
                mstore(0, NoContract_error_selector)
                mstore(NoContract_error_account_ptr, token)

                
                
                
                revert(Generic_error_selector_offset, NoContract_error_length)
            }

            
            
            let memPointer := mload(FreeMemoryPointerSlot)

            
            mstore(ERC721_transferFrom_sig_ptr, ERC721_transferFrom_signature)
            mstore(ERC721_transferFrom_from_ptr, from)
            mstore(ERC721_transferFrom_to_ptr, to)
            mstore(ERC721_transferFrom_id_ptr, identifier)

            
            let success := call(
                gas(),
                token,
                0,
                ERC721_transferFrom_sig_ptr,
                ERC721_transferFrom_length,
                0,
                0
            )

            
            if iszero(success) {
                
                
                if returndatasize() {
                    
                    
                    
                    
                    let returnDataWords := shr(
                        OneWordShift,
                        add(returndatasize(), AlmostOneWord)
                    )

                    
                    
                    
                    let msizeWords := shr(OneWordShift, memPointer)

                    
                    let cost := mul(CostPerWord, returnDataWords)

                    
                    if gt(returnDataWords, msizeWords) {
                        cost := add(
                            cost,
                            add(
                                mul(
                                    sub(returnDataWords, msizeWords),
                                    CostPerWord
                                ),
                                shr(
                                    MemoryExpansionCoefficientShift,
                                    sub(
                                        mul(returnDataWords, returnDataWords),
                                        mul(msizeWords, msizeWords)
                                    )
                                )
                            )
                        )
                    }

                    
                    
                    
                    if lt(add(cost, ExtraGasBuffer), gas()) {
                        
                        returndatacopy(0, 0, returndatasize())

                        
                        revert(0, returndatasize())
                    }
                }

                
                
                mstore(0, TokenTransferGenericFailure_error_selector)
                mstore(TokenTransferGenericFailure_error_token_ptr, token)
                mstore(TokenTransferGenericFailure_error_from_ptr, from)
                mstore(TokenTransferGenericFailure_error_to_ptr, to)
                mstore(
                    TokenTransferGenericFailure_error_identifier_ptr,
                    identifier
                )
                mstore(TokenTransferGenericFailure_error_amount_ptr, 1)

                
                
                
                
                
                revert(
                    Generic_error_selector_offset,
                    TokenTransferGenericFailure_error_length
                )
            }

            
            mstore(FreeMemoryPointerSlot, memPointer)

            
            mstore(ZeroSlot, 0)
        }
    }

```

https://github.com/ProjectOpenSea/seaport/tree/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/lib/TokenTransferrer.sol#L296

```solidity
448: function _performERC1155Transfer(
        address token,
        address from,
        address to,
        uint256 identifier,
        uint256 amount
    ) internal {
        
        assembly {
            
            if iszero(extcodesize(token)) {
                
                mstore(0, NoContract_error_selector)
                mstore(NoContract_error_account_ptr, token)

                
                
                
                revert(Generic_error_selector_offset, NoContract_error_length)
            }

            
            
            let memPointer := mload(FreeMemoryPointerSlot)
            let slot0x80 := mload(Slot0x80)
            let slot0xA0 := mload(Slot0xA0)
            let slot0xC0 := mload(Slot0xC0)

            
            mstore(
                ERC1155_safeTransferFrom_sig_ptr,
                ERC1155_safeTransferFrom_signature
            )
            mstore(ERC1155_safeTransferFrom_from_ptr, from)
            mstore(ERC1155_safeTransferFrom_to_ptr, to)
            mstore(ERC1155_safeTransferFrom_id_ptr, identifier)
            mstore(ERC1155_safeTransferFrom_amount_ptr, amount)
            mstore(
                ERC1155_safeTransferFrom_data_offset_ptr,
                ERC1155_safeTransferFrom_data_length_offset
            )
            mstore(ERC1155_safeTransferFrom_data_length_ptr, 0)

            
            let success := call(
                gas(),
                token,
                0,
                ERC1155_safeTransferFrom_sig_ptr,
                ERC1155_safeTransferFrom_length,
                0,
                0
            )

            
            if iszero(success) {
                
                
                if returndatasize() {
                    
                    
                    
                    
                    let returnDataWords := shr(
                        OneWordShift,
                        add(returndatasize(), AlmostOneWord)
                    )

                    
                    
                    
                    let msizeWords := shr(OneWordShift, memPointer)

                    
                    let cost := mul(CostPerWord, returnDataWords)

                    
                    if gt(returnDataWords, msizeWords) {
                        cost := add(
                            cost,
                            add(
                                mul(
                                    sub(returnDataWords, msizeWords),
                                    CostPerWord
                                ),
                                shr(
                                    MemoryExpansionCoefficientShift,
                                    sub(
                                        mul(returnDataWords, returnDataWords),
                                        mul(msizeWords, msizeWords)
                                    )
                                )
                            )
                        )
                    }

                    
                    
                    
                    if lt(add(cost, ExtraGasBuffer), gas()) {
                        
                        returndatacopy(0, 0, returndatasize())

                        
                        revert(0, returndatasize())
                    }
                }

                

                
                mstore(0, TokenTransferGenericFailure_error_selector)
                mstore(TokenTransferGenericFailure_error_token_ptr, token)
                mstore(TokenTransferGenericFailure_error_from_ptr, from)
                mstore(TokenTransferGenericFailure_error_to_ptr, to)
                mstore(
                    TokenTransferGenericFailure_error_identifier_ptr,
                    identifier
                )
                mstore(TokenTransferGenericFailure_error_amount_ptr, amount)

                
                
                
                
                
                revert(
                    Generic_error_selector_offset,
                    TokenTransferGenericFailure_error_length
                )
            }

            mstore(Slot0x80, slot0x80) 
            mstore(Slot0xA0, slot0xA0) 
            mstore(Slot0xC0, slot0xC0) 

            
            mstore(FreeMemoryPointerSlot, memPointer)

            
            mstore(ZeroSlot, 0)
        }
    }

```

https://github.com/ProjectOpenSea/seaport/tree/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/lib/TokenTransferrer.sol#L448

```solidity
723: function _performERC1155BatchTransfers(
        ConduitBatch1155Transfer[] calldata batchTransfers
    ) internal {
        
        assembly {
            let len := batchTransfers.length
            
            
            
            let nextElementHeadPtr := batchTransfers.offset

            
            
            
            let arrayHeadPtr := nextElementHeadPtr

            
            
            mstore(
                ConduitBatch1155Transfer_from_offset,
                ERC1155_safeBatchTransferFrom_signature
            )

            
            for {
                let i := 0
            } lt(i, len) {
                i := add(i, 1)
            } {
                
                
                
                let elementPtr := add(
                    arrayHeadPtr,
                    calldataload(nextElementHeadPtr)
                )

                
                let token := calldataload(elementPtr)

                
                if iszero(extcodesize(token)) {
                    
                    mstore(0, NoContract_error_selector)
                    mstore(NoContract_error_account_ptr, token)

                    
                    
                    
                    revert(
                        Generic_error_selector_offset,
                        NoContract_error_length
                    )
                }

                
                let idsLength := calldataload(
                    add(elementPtr, ConduitBatch1155Transfer_ids_length_offset)
                )

                
                let expectedAmountsOffset := add(
                    ConduitBatch1155Transfer_amounts_length_baseOffset,
                    shl(OneWordShift, idsLength)
                )

                
                let invalidEncoding := iszero(
                    and(
                        
                        eq(
                            idsLength,
                            calldataload(add(elementPtr, expectedAmountsOffset))
                        ),
                        and(
                            
                            eq(
                                calldataload(
                                    add(
                                        elementPtr,
                                        ConduitBatch1155Transfer_ids_head_offset
                                    )
                                ),
                                ConduitBatch1155Transfer_ids_length_offset
                            ),
                            
                            eq(
                                calldataload(
                                    add(
                                        elementPtr,
                                        ConduitBatchTransfer_amounts_head_offset
                                    )
                                ),
                                expectedAmountsOffset
                            )
                        )
                    )
                )

                
                if invalidEncoding {
                    mstore(
                        Invalid1155BatchTransferEncoding_ptr,
                        Invalid1155BatchTransferEncoding_selector
                    )
                    revert(
                        Invalid1155BatchTransferEncoding_ptr,
                        Invalid1155BatchTransferEncoding_length
                    )
                }

                
                nextElementHeadPtr := add(nextElementHeadPtr, OneWord)

                
                calldatacopy(
                    BatchTransfer1155Params_ptr,
                    add(elementPtr, ConduitBatch1155Transfer_from_offset),
                    ConduitBatch1155Transfer_usable_head_size
                )

                
                
                let idsAndAmountsSize := add(
                    TwoWords,
                    shl(TwoWordsShift, idsLength)
                )

                
                mstore(
                    BatchTransfer1155Params_data_head_ptr,
                    add(
                        BatchTransfer1155Params_ids_length_offset,
                        idsAndAmountsSize
                    )
                )

                
                mstore(
                    add(
                        BatchTransfer1155Params_data_length_basePtr,
                        idsAndAmountsSize
                    ),
                    0
                )

                
                let transferDataSize := add(
                    BatchTransfer1155Params_calldata_baseSize,
                    idsAndAmountsSize
                )

                
                calldatacopy(
                    BatchTransfer1155Params_ids_length_ptr,
                    add(elementPtr, ConduitBatch1155Transfer_ids_length_offset),
                    idsAndAmountsSize
                )

                
                let success := call(
                    gas(),
                    token,
                    0,
                    ConduitBatch1155Transfer_from_offset, 
                    transferDataSize, 
                    0,
                    0
                )

                
                if iszero(success) {
                    
                    
                    if returndatasize() {
                        
                        
                        
                        
                        let returnDataWords := shr(
                            OneWordShift,
                            add(returndatasize(), AlmostOneWord)
                        )

                        
                        
                        
                        
                        
                        
                        
                        
                        let msizeWords := shr(OneWordShift, transferDataSize)

                        
                        let cost := mul(CostPerWord, returnDataWords)

                        
                        if gt(returnDataWords, msizeWords) {
                            cost := add(
                                cost,
                                add(
                                    mul(
                                        sub(returnDataWords, msizeWords),
                                        CostPerWord
                                    ),
                                    shr(
                                        MemoryExpansionCoefficientShift,
                                        sub(
                                            mul(
                                                returnDataWords,
                                                returnDataWords
                                            ),
                                            mul(msizeWords, msizeWords)
                                        )
                                    )
                                )
                            )
                        }

                        
                        
                        
                        if lt(add(cost, ExtraGasBuffer), gas()) {
                            
                            returndatacopy(0, 0, returndatasize())

                            
                            revert(0, returndatasize())
                        }
                    }

                    
                    mstore(
                        0,
                        ERC1155BatchTransferGenericFailure_error_signature
                    )

                    
                    mstore(ERC1155BatchTransferGenericFailure_token_ptr, token)

                    
                    mstore(
                        BatchTransfer1155Params_ids_head_ptr,
                        ERC1155BatchTransferGenericFailure_ids_offset
                    )

                    
                    mstore(
                        BatchTransfer1155Params_amounts_head_ptr,
                        add(
                            OneWord,
                            mload(BatchTransfer1155Params_amounts_head_ptr)
                        )
                    )

                    
                    
                    revert(0, transferDataSize)
                }
            }

            
            
            
            
            mstore(FreeMemoryPointerSlot, DefaultFreeMemoryPointer)
        }
    }
}

```

https://github.com/ProjectOpenSea/seaport/tree/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/lib/TokenTransferrer.sol#L723

```solidity
182: function _callAndCheckStatus(
        address target,
        bytes32 orderHash,
        MemoryPointer callData,
        uint256 size,
        uint256 errorSelector
    ) internal {
        bool success;
        bool magicMatch;
        assembly {
            
            let magic := and(mload(callData), MaskOverFirstFourBytes)

            
            mstore(0, 0)

            
            success := call(gas(), target, 0, callData, size, 0, OneWord)

            
            magicMatch := eq(magic, mload(0))
        }

        
        if (!success) {
            
            _revertWithReasonIfOneIsReturned();

            
            assembly {
                mstore(0, errorSelector)
                mstore(InvalidRestrictedOrder_error_orderHash_ptr, orderHash)
                revert(
                    Error_selector_offset,
                    InvalidRestrictedOrder_error_length
                )
            }
        }

        
        if (!magicMatch) {
            
            assembly {
                mstore(0, errorSelector)
                mstore(InvalidRestrictedOrder_error_orderHash_ptr, orderHash)
                revert(
                    Error_selector_offset,
                    InvalidRestrictedOrder_error_length
                )
            }
        }
    }
}

```

https://github.com/ProjectOpenSea/seaport/tree/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/lib/ZoneInteraction.sol#L182




#### <ins>Recommended Mitigation Steps</ins>
Add this comment to the function:
```
/// @dev Use with caution! Some functions in this contract knowingly create dirty bits at the destination of the free memory pointer. Note that this code probably isn’t secure or a good use case for assembly because a lot of memory management and security checks are bypassed.
```



### <a href="#Summary">[NC&#x2011;3]</a><a name="NC&#x2011;3"> Function writing that does not comply with the Solidity Style Guide

Order of Functions; ordering helps readers identify which functions they can call and to find the constructor and fallback definitions easier. But there are contracts in the project that do not comply with this.

https://docs.soliditylang.org/en/v0.8.17/style-guide.html

Functions should be grouped according to their visibility and ordered:
- constructor
- receive function (if exists)
- fallback function (if exists)
- external
- public
- internal
- private
- within a grouping, place the view and pure functions last

#### <ins>Proof Of Concept</ins>

All in-scope contracts




### <a href="#Summary">[NC&#x2011;4]</a><a name="NC&#x2011;4"> Use `delete` to Clear Variables

`delete a` assigns the initial value for the type to `a`. i.e. for integers it is equivalent to `a = 0`, but it can also be used on arrays, where it assigns a dynamic array of length zero or a static array of the same length with all elements reset. For structs, it assigns a struct with all members reset. Similarly, it can also be used to set an address to zero address. It has no effect on whole mappings though (as the keys of mappings may be arbitrary and are generally unknown). However, individual keys and what they map to can be deleted: If `a` is a mapping, then `delete a[x]` will delete the value stored at `x`.

The `delete` key better conveys the intention and is also more idiomatic. Consider replacing assignments of zero with `delete` statements.

#### <ins>Proof Of Concept</ins>

```solidity
239: advancedOrder.numerator = 0;
```

https://github.com/ProjectOpenSea/seaport/tree/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/lib/OrderCombiner.sol#L239







### <a href="#Summary">[NC&#x2011;5]</a><a name="NC&#x2011;5"> NatSpec return parameters should be included in contracts

It is recommended that Solidity contracts are fully annotated using NatSpec for all public interfaces (everything in the ABI). It is clearly stated in the Solidity official documentation. In complex projects such as Defi, the interpretation of all functions and their arguments and returns is important for code readability and auditability.

https://docs.soliditylang.org/en/v0.8.15/natspec-format.html
#### <ins>Proof Of Concept</ins>


All in-scope contracts


#### <ins>Recommended Mitigation Steps</ins>

Include return parameters in NatSpec comments

Recommendation Code Style: (from Uniswap3)

```solidity
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



### <a href="#Summary">[NC&#x2011;6]</a><a name="NC&#x2011;6"> No need to initialize uints to zero

There is no need to initialize `uint` variables to zero as their default value is `0`

#### <ins>Proof Of Concept</ins>

```solidity
939: uint256 i = 0;

```

https://github.com/ProjectOpenSea/seaport/tree/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/lib/BasicOrderFulfiller.sol#L939

```solidity
564: uint256 totalFilteredExecutions = 0;

```

https://github.com/ProjectOpenSea/seaport/tree/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/lib/OrderCombiner.sol#L564

```solidity
996: uint256 totalFilteredExecutions = 0;

```

https://github.com/ProjectOpenSea/seaport/tree/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/lib/OrderCombiner.sol#L996






### <a href="#Summary">[NC&#x2011;7]</a><a name="NC&#x2011;7"> Implementation contract may not be initialized

OpenZeppelin recommends that the initializer modifier be applied to constructors. 
Per OZs Post implementation contract should be initialized to avoid potential griefs or exploits.
https://forum.openzeppelin.com/t/uupsupgradeable-vulnerability-post-mortem/15680/5

#### <ins>Proof Of Concept</ins>


```solidity
93: constructor(address conduitController) Consideration(conduitController)
```

https://github.com/ProjectOpenSea/seaport/tree/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/Seaport.sol#L93

```solidity
73: constructor()
```

https://github.com/ProjectOpenSea/seaport/tree/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/conduit/Conduit.sol#L73

```solidity
31: constructor()
```

https://github.com/ProjectOpenSea/seaport/tree/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/conduit/ConduitController.sol#L31

```solidity
35: constructor(
        address conduitController
    ) GettersAndDerivers(conduitController)
```

https://github.com/ProjectOpenSea/seaport/tree/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/lib/Assertions.sol#L35

```solidity
41: constructor(address conduitController) OrderValidator(conduitController)
```

https://github.com/ProjectOpenSea/seaport/tree/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/lib/BasicOrderFulfiller.sol#L41

```solidity
50: constructor(address conduitController) OrderCombiner(conduitController)
```

https://github.com/ProjectOpenSea/seaport/tree/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/lib/Consideration.sol#L50

```solidity
56: constructor(address conduitController)
```

https://github.com/ProjectOpenSea/seaport/tree/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/lib/ConsiderationBase.sol#L56

```solidity
35: constructor(address conduitController) Verifiers(conduitController)
```

https://github.com/ProjectOpenSea/seaport/tree/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/lib/Executor.sol#L35

```solidity
25: constructor(
        address conduitController
    ) ConsiderationBase(conduitController)
```

https://github.com/ProjectOpenSea/seaport/tree/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/lib/GettersAndDerivers.sol#L25

```solidity
41: constructor(address conduitController) OrderFulfiller(conduitController)
```

https://github.com/ProjectOpenSea/seaport/tree/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/lib/OrderCombiner.sol#L41

```solidity
45: constructor(
        address conduitController
    ) BasicOrderFulfiller(conduitController)
```

https://github.com/ProjectOpenSea/seaport/tree/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/lib/OrderFulfiller.sol#L45

```solidity
55: constructor(address conduitController) Executor(conduitController)
```

https://github.com/ProjectOpenSea/seaport/tree/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/lib/OrderValidator.sol#L55

```solidity
23: constructor()
```

https://github.com/ProjectOpenSea/seaport/tree/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/lib/ReentrancyGuard.sol#L23

```solidity
30: constructor()
```

https://github.com/ProjectOpenSea/seaport/tree/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/lib/TypehashDirectory.sol#L30

```solidity
26: constructor(address conduitController) Assertions(conduitController)
```

https://github.com/ProjectOpenSea/seaport/tree/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/lib/Verifiers.sol#L26





### <a href="#Summary">[NC&#x2011;8]</a><a name="NC&#x2011;8"> NatSpec comments should be increased in contracts

It is recommended that Solidity contracts are fully annotated using NatSpec for all public interfaces (everything in the ABI). It is clearly stated in the Solidity official documentation. In complex projects such as Defi, the interpretation of all functions and their arguments and returns is important for code readability and auditability. https://docs.soliditylang.org/en/v0.8.15/natspec-format.html

#### <ins>Proof Of Concept</ins>


All in-scope contracts


#### <ins>Recommended Mitigation Steps</ins>

NatSpec comments should be increased in contracts



### <a href="#Summary">[NC&#x2011;9]</a><a name="NC&#x2011;9"> Non-usage of specific imports

The current form of relative path import is not recommended for use because it can unpredictably pollute the namespace.
Instead, the Solidity docs recommend specifying imported symbols explicitly.
https://docs.soliditylang.org/en/v0.8.15/layout-of-source-files.html#importing-other-source-files

A good example:
```solidity
import {OwnableUpgradeable} from "openzeppelin-contracts-upgradeable/contracts/access/OwnableUpgradeable.sol";
import {SafeTransferLib} from "solmate/utils/SafeTransferLib.sol";
import {SafeCastLib} from "solmate/utils/SafeCastLib.sol";
import {ERC20} from "solmate/tokens/ERC20.sol";
import {IProducer} from "src/interfaces/IProducer.sol";
import {GlobalState, UserState} from "src/Common.sol";
```

#### <ins>Proof Of Concept</ins>


```solidity
15: import "./lib/ConduitConstants.sol";

```

https://github.com/ProjectOpenSea/seaport/tree/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/conduit/Conduit.sol#L15

```solidity
8: import "./ConsiderationConstants.sol";

```

https://github.com/ProjectOpenSea/seaport/tree/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/lib/AmountDeriver.sol#L8

```solidity
14: import "./ConsiderationErrors.sol";

```

https://github.com/ProjectOpenSea/seaport/tree/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/lib/Assertions.sol#L14

```solidity
23: import "./ConsiderationErrors.sol";

```

https://github.com/ProjectOpenSea/seaport/tree/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/lib/BasicOrderFulfiller.sol#L23

```solidity
23: import "../helpers/PointerLibraries.sol";
25: import "./ConsiderationConstants.sol";

```

https://github.com/ProjectOpenSea/seaport/tree/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/lib/Consideration.sol#L23

https://github.com/ProjectOpenSea/seaport/tree/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/lib/Consideration.sol#L25



```solidity
12: import "./ConsiderationConstants.sol";

```

https://github.com/ProjectOpenSea/seaport/tree/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/lib/ConsiderationBase.sol#L12

```solidity
20: import "./ConsiderationConstants.sol";
22: import "../helpers/PointerLibraries.sol";

```

https://github.com/ProjectOpenSea/seaport/tree/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/lib/ConsiderationDecoder.sol#L20

https://github.com/ProjectOpenSea/seaport/tree/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/lib/ConsiderationDecoder.sol#L22



```solidity
4: import "./ConsiderationConstants.sol";
20: import "../helpers/PointerLibraries.sol";

```

https://github.com/ProjectOpenSea/seaport/tree/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/lib/ConsiderationEncoder.sol#L4

https://github.com/ProjectOpenSea/seaport/tree/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/lib/ConsiderationEncoder.sol#L20



```solidity
6: import "./ConsiderationConstants.sol";

```

https://github.com/ProjectOpenSea/seaport/tree/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/lib/ConsiderationErrors.sol#L6

```solidity
10: import "./ConsiderationConstants.sol";

```

https://github.com/ProjectOpenSea/seaport/tree/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/lib/CounterManager.sol#L10

```solidity
15: import "./ConsiderationErrors.sol";
17: import "../helpers/PointerLibraries.sol";

```

https://github.com/ProjectOpenSea/seaport/tree/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/lib/CriteriaResolution.sol#L15

https://github.com/ProjectOpenSea/seaport/tree/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/lib/CriteriaResolution.sol#L17



```solidity
16: import "./ConsiderationConstants.sol";
18: import "./ConsiderationErrors.sol";

```

https://github.com/ProjectOpenSea/seaport/tree/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/lib/Executor.sol#L16

https://github.com/ProjectOpenSea/seaport/tree/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/lib/Executor.sol#L18



```solidity
16: import "./ConsiderationErrors.sol";

```

https://github.com/ProjectOpenSea/seaport/tree/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/lib/FulfillmentApplier.sol#L16

```solidity
8: import "./ConsiderationConstants.sol";

```

https://github.com/ProjectOpenSea/seaport/tree/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/lib/GettersAndDerivers.sol#L8

```solidity
4: import "./ConsiderationConstants.sol";

```

https://github.com/ProjectOpenSea/seaport/tree/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/lib/LowLevelHelpers.sol#L4

```solidity
23: import "./ConsiderationErrors.sol";

```

https://github.com/ProjectOpenSea/seaport/tree/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/lib/OrderCombiner.sol#L23

```solidity
23: import "./ConsiderationErrors.sol";

```

https://github.com/ProjectOpenSea/seaport/tree/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/lib/OrderFulfiller.sol#L23

```solidity
19: import "./ConsiderationErrors.sol";

```

https://github.com/ProjectOpenSea/seaport/tree/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/lib/OrderValidator.sol#L19

```solidity
8: import "./ConsiderationErrors.sol";

```

https://github.com/ProjectOpenSea/seaport/tree/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/lib/ReentrancyGuard.sol#L8

```solidity
12: import "./ConsiderationErrors.sol";

```

https://github.com/ProjectOpenSea/seaport/tree/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/lib/SignatureVerification.sol#L12

```solidity
4: import "./TokenTransferrerConstants.sol";

```

https://github.com/ProjectOpenSea/seaport/tree/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/lib/TokenTransferrer.sol#L4

```solidity
10: import "./ConsiderationErrors.sol";

```

https://github.com/ProjectOpenSea/seaport/tree/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/lib/Verifiers.sol#L10

```solidity
16: import "./ConsiderationEncoder.sol";

```

https://github.com/ProjectOpenSea/seaport/tree/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/lib/ZoneInteraction.sol#L16




#### <ins>Recommended Mitigation Steps</ins>

Use specific imports syntax per solidity docs recommendation.



### <a href="#Summary">[NC&#x2011;10]</a><a name="NC&#x2011;10"> Use a more recent version of Solidity


<a href="https://blog.soliditylang.org/2022/03/16/solidity-0.8.13-release-announcement/">0.8.13</a>: 
Ability to use using for with a list of free functions

<a href="https://blog.soliditylang.org/2022/05/18/solidity-0.8.14-release-announcement/">0.8.14</a>:

ABI Encoder: When ABI-encoding values from calldata that contain nested arrays, correctly validate the nested array length against calldatasize() in all cases.
Override Checker: Allow changing data location for parameters only when overriding external functions.

<a href="https://blog.soliditylang.org/2022/06/15/solidity-0.8.15-release-announcement/">0.8.15</a>:

Code Generation: Avoid writing dirty bytes to storage when copying bytes arrays.
Yul Optimizer: Keep all memory side-effects of inline assembly blocks.

<a href="https://blog.soliditylang.org/2022/08/08/solidity-0.8.16-release-announcement/">0.8.16</a>:

Code Generation: Fix data corruption that affected ABI-encoding of calldata values represented by tuples: structs at any nesting level; argument lists of external functions, events and errors; return value lists of external functions. The 32 leading bytes of the first dynamically-encoded value in the tuple would get zeroed when the last component contained a statically-encoded array.

<a href="https://blog.soliditylang.org/2022/09/08/solidity-0.8.17-release-announcement/">0.8.17</a>:

Yul Optimizer: Prevent the incorrect removal of storage writes before calls to Yul functions that conditionally terminate the external EVM call.

#### <ins>Proof Of Concept</ins>


```solidity
pragma solidity ^0.8.13;
```

https://github.com/ProjectOpenSea/seaport/tree/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/conduit/Conduit.sol#L2

```solidity
pragma solidity ^0.8.13;
```

https://github.com/ProjectOpenSea/seaport/tree/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/conduit/ConduitController.sol#L2

```solidity
pragma solidity ^0.8.13;
```

https://github.com/ProjectOpenSea/seaport/tree/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/conduit/lib/ConduitConstants.sol#L2

```solidity
pragma solidity ^0.8.13;
```

https://github.com/ProjectOpenSea/seaport/tree/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/conduit/lib/ConduitEnums.sol#L2

```solidity
pragma solidity ^0.8.13;
```

https://github.com/ProjectOpenSea/seaport/tree/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/conduit/lib/ConduitStructs.sol#L2

```solidity
pragma solidity ^0.8.13;
```

https://github.com/ProjectOpenSea/seaport/tree/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/helpers/PointerLibraries.sol#L2

```solidity
pragma solidity ^0.8.13;
```

https://github.com/ProjectOpenSea/seaport/tree/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/interfaces/AbridgedTokenInterfaces.sol#L2

```solidity
pragma solidity ^0.8.13;
```

https://github.com/ProjectOpenSea/seaport/tree/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/interfaces/AmountDerivationErrors.sol#L2

```solidity
pragma solidity ^0.8.13;
```

https://github.com/ProjectOpenSea/seaport/tree/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/interfaces/ConduitControllerInterface.sol#L2

```solidity
pragma solidity ^0.8.13;
```

https://github.com/ProjectOpenSea/seaport/tree/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/interfaces/ConduitInterface.sol#L2

```solidity
pragma solidity ^0.8.13;
```

https://github.com/ProjectOpenSea/seaport/tree/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/interfaces/ConsiderationEventsAndErrors.sol#L2

```solidity
pragma solidity ^0.8.13;
```

https://github.com/ProjectOpenSea/seaport/tree/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/interfaces/ConsiderationInterface.sol#L2

```solidity
pragma solidity ^0.8.13;
```

https://github.com/ProjectOpenSea/seaport/tree/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/interfaces/ContractOffererInterface.sol#L2

```solidity
pragma solidity ^0.8.13;
```

https://github.com/ProjectOpenSea/seaport/tree/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/interfaces/CriteriaResolutionErrors.sol#L2

```solidity
pragma solidity ^0.8.13;
```

https://github.com/ProjectOpenSea/seaport/tree/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/interfaces/EIP1271Interface.sol#L2

```solidity
pragma solidity ^0.8.13;
```

https://github.com/ProjectOpenSea/seaport/tree/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/interfaces/FulfillmentApplicationErrors.sol#L2

```solidity
pragma solidity ^0.8.13;
```

https://github.com/ProjectOpenSea/seaport/tree/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/interfaces/IERC721Receiver.sol#L2

```solidity
pragma solidity ^0.8.13;
```

https://github.com/ProjectOpenSea/seaport/tree/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/interfaces/ImmutableCreate2FactoryInterface.sol#L2

```solidity
pragma solidity ^0.8.13;
```

https://github.com/ProjectOpenSea/seaport/tree/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/interfaces/ReentrancyErrors.sol#L2

```solidity
pragma solidity ^0.8.13;
```

https://github.com/ProjectOpenSea/seaport/tree/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/interfaces/SeaportInterface.sol#L2

```solidity
pragma solidity ^0.8.13;
```

https://github.com/ProjectOpenSea/seaport/tree/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/interfaces/SignatureVerificationErrors.sol#L2

```solidity
pragma solidity ^0.8.13;
```

https://github.com/ProjectOpenSea/seaport/tree/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/interfaces/TokenTransferrerErrors.sol#L2

```solidity
pragma solidity ^0.8.13;
```

https://github.com/ProjectOpenSea/seaport/tree/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/interfaces/TransferHelperErrors.sol#L2

```solidity
pragma solidity ^0.8.13;
```

https://github.com/ProjectOpenSea/seaport/tree/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/interfaces/TransferHelperInterface.sol#L2

```solidity
pragma solidity ^0.8.13;
```

https://github.com/ProjectOpenSea/seaport/tree/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/interfaces/ZoneInteractionErrors.sol#L2

```solidity
pragma solidity ^0.8.13;
```

https://github.com/ProjectOpenSea/seaport/tree/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/interfaces/ZoneInterface.sol#L2

```solidity
pragma solidity ^0.8.13;
```

https://github.com/ProjectOpenSea/seaport/tree/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/lib/ConsiderationConstants.sol#L2

```solidity
pragma solidity ^0.8.13;
```

https://github.com/ProjectOpenSea/seaport/tree/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/lib/ConsiderationEncoder.sol#L2

```solidity
pragma solidity ^0.8.13;
```

https://github.com/ProjectOpenSea/seaport/tree/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/lib/ConsiderationEnums.sol#L2

```solidity
pragma solidity ^0.8.13;
```

https://github.com/ProjectOpenSea/seaport/tree/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/lib/ConsiderationStructs.sol#L2

```solidity
pragma solidity ^0.8.13;
```

https://github.com/ProjectOpenSea/seaport/tree/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/lib/TokenTransferrer.sol#L2

```solidity
pragma solidity ^0.8.13;
```

https://github.com/ProjectOpenSea/seaport/tree/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/lib/TokenTransferrerConstants.sol#L2



#### <ins>Recommended Mitigation Steps</ins>

Consider updating to a more recent solidity version.



### <a href="#Summary">[NC&#x2011;11]</a><a name="NC&#x2011;11"> Omissions in Events

Throughout the codebase, events are generally emitted when sensitive changes are made to the contracts. However, some events are missing important parameters

#### <ins>Proof Of Concept</ins>


```solidity
51: event PotentialOwnerUpdated(address indexed newPotentialOwner);
```

https://github.com/ProjectOpenSea/seaport/tree/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/interfaces/ConduitControllerInterface.sol#L51




#### <ins>Recommended Mitigation Steps</ins>
The events should include the new value and old value where possible.



### <a href="#Summary">[NC&#x2011;12]</a><a name="NC&#x2011;12"> Adding A Return Statement When The Function Defines A Named Return Variable, Is Redundant

#### <ins>Proof Of Concept</ins>


```solidity
87: return amount
```

https://github.com/ProjectOpenSea/seaport/tree/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/lib/AmountDeriver.sol#L87

```solidity
902: return orderHash
```

https://github.com/ProjectOpenSea/seaport/tree/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/lib/BasicOrderFulfiller.sol#L902







### <a href="#Summary">[NC&#x2011;13]</a><a name="NC&#x2011;13"> Use `bytes.concat()`

Solidity version 0.8.4 introduces `bytes.concat()` (vs `abi.encodePacked(<bytes>,<bytes>)`)

#### <ins>Proof Of Concept</ins>


```solidity
76: abi.encodePacked(
                            bytes1(0xff)
339: abi.encodePacked(
                            bytes1(0xff)
```

https://github.com/ProjectOpenSea/seaport/tree/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/conduit/ConduitController.sol#L76

https://github.com/ProjectOpenSea/seaport/tree/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/conduit/ConduitController.sol#L339


```solidity
177: abi.encodePacked(
                considerationItemTypeString,
                offerItemTypeString,
                orderComponentsPartialTypeString
            )

```

https://github.com/ProjectOpenSea/seaport/tree/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/lib/TypehashDirectory.sol#L177




#### <ins>Recommended Mitigation Steps</ins>

Use `bytes.concat()` and upgrade to at least Solidity version 0.8.4 if required. 








