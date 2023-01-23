




# `block.timestamp` used as time proxy 
## Summary

Risk of using `block.timestamp` for time should be considered. 

## Details

`block.timestamp` is not an ideal proxy for time because of issues with synchronization, miner manipulation and changing block times. 

This kind of issue may affect the code allowing or reverting the code before the expected deadline, modifying the normal functioning or reverting sometimes.
## References

SWC ID: 116

## Code Snippet 

- [AmountDeriver.sol#L58](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0//contracts/lib/AmountDeriver.sol#L58)
`elapsed = block.timestamp - startTime;`

## Recommendation

- Consider the risk of using `block.timestamp` as time proxy and evaluate if block numbers can be used as an approximation for the application logic. Both have risks that need to be factored in. 



## Undocumented parameters

In a some places, a parameter is missing in the documentation:

- [FulfillmentApplicationErrors.sol#L18](https://github.com/ProjectOpenSea/seaport/blob/097c3f236f10da1c3b0f56f936555f57143d4e1b/contracts/interfaces/FulfillmentApplicationErrors.sol#L18)
- [ConduitInterface.sol#L20-L26](https://github.com/ProjectOpenSea/seaport/blob/538266351c64238d1ccc2bc59df1d37893b8d962/contracts/interfaces/ConduitInterface.sol#L20-L26)
- [TransferHelperErrors.sol#L26-L48](https://github.com/ProjectOpenSea/seaport/blob/59f5b0b96d82f98a3becacb86f80b79734da6c47/contracts/interfaces/TransferHelperErrors.sol#L26-L48)
- [TransferHelperErrors.sol#L60-L84](https://github.com/ProjectOpenSea/seaport/blob/59f5b0b96d82f98a3becacb86f80b79734da6c47/contracts/interfaces/TransferHelperErrors.sol#L60-L84)
- [ConsiderationEventsAndErrors.sol#L191](https://github.com/ProjectOpenSea/seaport/blob/4da0c0bc511ffee30ab9729f723546ec5de0a7c1/contracts/interfaces/ConsiderationEventsAndErrors.sol#L191)
- [ConsiderationEventsAndErrors.sol#L148](https://github.com/ProjectOpenSea/seaport/blob/4da0c0bc511ffee30ab9729f723546ec5de0a7c1/contracts/interfaces/ConsiderationEventsAndErrors.sol#L148)
- [ConsiderationEventsAndErrors.sol#L121](https://github.com/ProjectOpenSea/seaport/blob/4da0c0bc511ffee30ab9729f723546ec5de0a7c1/contracts/interfaces/ConsiderationEventsAndErrors.sol#L121)
- [ConsiderationEventsAndErrors.sol#L100](https://github.com/ProjectOpenSea/seaport/blob/4da0c0bc511ffee30ab9729f723546ec5de0a7c1/contracts/interfaces/ConsiderationEventsAndErrors.sol#L100)
- [ConduitControllerInterface.sol#L66-L117](https://github.com/ProjectOpenSea/seaport/blob/538266351c64238d1ccc2bc59df1d37893b8d962/contracts/interfaces/ConduitControllerInterface.sol#L66-L117)



## Include return parameters in natspec comments

If Return parameters are declared, you must prefix them with ”/// @return”. [References](https://docs.soliditylang.org/en/v0.8.17/natspec-format.html)

Some code analysis programs do analysis by reading NatSpec details, if they can’t see the `@return` tag, they do incomplete analysis.

### Recommendation

Include return parameters in NatSpec comments

Recommendation Code Style:

```solidity
    /// @notice information about what a fooFighter function does
		/// @param fooParam what the fooParam represents
		/// @return what is the fooReturnValue returned by fooFighter
		function fooFighter(uint256 fooParam) public returns (uint256 fooReturnValue) {
      ...
    }
```
 

- [EIP1271Interface.sol#L3-L9](https://github.com/ProjectOpenSea/seaport/blob/538266351c64238d1ccc2bc59df1d37893b8d962/contracts/interfaces/EIP1271Interface.sol#L3-L9)
- [ZoneInterface.sol#L6-L10](https://github.com/ProjectOpenSea/seaport/blob/8a5df932a613a20e06e6b4dad4cd7e8fbc28aac5/contracts/interfaces/ZoneInterface.sol#L6-L10)
- [IERC721Receiver.sol#L3-L11](https://github.com/ProjectOpenSea/seaport/blob/538266351c64238d1ccc2bc59df1d37893b8d962/contracts/interfaces/IERC721Receiver.sol#L3-L11)
- [TransferHelperInterface.sol#L15-L19](https://github.com/ProjectOpenSea/seaport/blob/782d7294036eef775d367f027ab086ca406738d9/contracts/interfaces/TransferHelperInterface.sol#L15-L19)
- [ConsiderationStructs.sol#L286-L542](https://github.com/ProjectOpenSea/seaport/blob/ffd5bc04f3cb5f136023868a11c83b5e8870253c/contracts/lib/ConsiderationStructs.sol#L286-L542)
- [AbridgedTokenInterfaces.sol#L4-L16](https://github.com/ProjectOpenSea/seaport/blob/538266351c64238d1ccc2bc59df1d37893b8d962/contracts/interfaces/AbridgedTokenInterfaces.sol#L4-L16)
- [ContractOffererInterface.sol#L6-L45](https://github.com/ProjectOpenSea/seaport/blob/538266351c64238d1ccc2bc59df1d37893b8d962/contracts/interfaces/ContractOffererInterface.sol#L6-L45)
- [ConduitControllerInterface.sol#L290-L296](https://github.com/ProjectOpenSea/seaport/blob/538266351c64238d1ccc2bc59df1d37893b8d962/contracts/interfaces/ConduitControllerInterface.sol#L290-L296)
- [SeaportInterface.sol#L447-L449](https://github.com/ProjectOpenSea/seaport/blob/233444ea8fc35c9301847ef4c15f93e013354a43/contracts/interfaces/SeaportInterface.sol#L447-L449)


## Missing Natspec 

NatSpec is missing for the following functions / constructor / modifiers:

- [EIP1271Interface.sol#L3-L9](https://github.com/ProjectOpenSea/seaport/blob/538266351c64238d1ccc2bc59df1d37893b8d962/contracts/interfaces/EIP1271Interface.sol#L3-L9)
- [ZoneInterface.sol#L6-L10](https://github.com/ProjectOpenSea/seaport/blob/8a5df932a613a20e06e6b4dad4cd7e8fbc28aac5/contracts/interfaces/ZoneInterface.sol#L6-L10)
- [IERC721Receiver.sol#L3-L11](https://github.com/ProjectOpenSea/seaport/blob/538266351c64238d1ccc2bc59df1d37893b8d962/contracts/interfaces/IERC721Receiver.sol#L3-L11)
- [ConsiderationStructs.sol#L286-L542](https://github.com/ProjectOpenSea/seaport/blob/ffd5bc04f3cb5f136023868a11c83b5e8870253c/contracts/lib/ConsiderationStructs.sol#L286-L542)
- [ConduitStructs.sol#L6-L21](https://github.com/ProjectOpenSea/seaport/blob/538266351c64238d1ccc2bc59df1d37893b8d962/contracts/conduit/lib/ConduitStructs.sol#L6-L21)
- [AbridgedTokenInterfaces.sol#L4-L36](https://github.com/ProjectOpenSea/seaport/blob/538266351c64238d1ccc2bc59df1d37893b8d962/contracts/interfaces/AbridgedTokenInterfaces.sol#L4-L36)
- [ContractOffererInterface.sol#L6-L45](https://github.com/ProjectOpenSea/seaport/blob/538266351c64238d1ccc2bc59df1d37893b8d962/contracts/interfaces/ContractOffererInterface.sol#L6-L45)





## Missing spacing in operator

Operator on the comment should include spacing (`!= 0`) to follow general style

- [OrderValidator.sol#L507](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0//contracts/lib/OrderValidator.sol#L507)
// !=0 and revertOnInvalid == false.




## Naming convention of non constants

Non constant variables are expected to be written in `mixedCase`

https://github.com/ProjectOpenSea/seaport/blob/12e7dca6034e1f31572effd0daf2afa85116da86/contracts/lib/ConsiderationBase.sol#L30-L46

https://github.com/ProjectOpenSea/seaport/blob/538266351c64238d1ccc2bc59df1d37893b8d962/contracts/conduit/ConduitController.sol#L23-L25

## Naming convention of constants

Some constants are not using proper style. Constant naming convention is `UPPER_CASE_WITH_UNDERSCORES`


- [PointerLibraries.sol#L19](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0//contracts/helpers/PointerLibraries.sol#L19)
CalldataPointer constant CalldataStart = CalldataPointer.wrap(0x04);

- [PointerLibraries.sol#L20](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0//contracts/helpers/PointerLibraries.sol#L20)
MemoryPointer constant FreeMemoryPPtr = MemoryPointer.wrap(0x40);

- [PointerLibraries.sol#L21](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0//contracts/helpers/PointerLibraries.sol#L21)
uint256 constant IdentityPrecompileAddress = 4;

- [PointerLibraries.sol#L22](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0//contracts/helpers/PointerLibraries.sol#L22)
uint256 constant OffsetOrLengthMask = 0xffffffff;

- [ConsiderationConstants.sol#L41](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0//contracts/lib/ConsiderationConstants.sol#L41)
uint256 constant NameLengthPtr = 77;

- [ConsiderationConstants.sol#L42](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0//contracts/lib/ConsiderationConstants.sol#L42)
uint256 constant NameWithLength = 0x0d436F6E73696465726174696F6E;

- [ConsiderationConstants.sol#L44](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0//contracts/lib/ConsiderationConstants.sol#L44)
uint256 constant information_version_offset = 0;

- [ConsiderationConstants.sol#L45](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0//contracts/lib/ConsiderationConstants.sol#L45)
uint256 constant information_version_cd_offset = 0x60;

- [ConsiderationConstants.sol#L46](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0//contracts/lib/ConsiderationConstants.sol#L46)
uint256 constant information_domainSeparator_offset = 0x20;

- [ConsiderationConstants.sol#L47](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0//contracts/lib/ConsiderationConstants.sol#L47)
uint256 constant information_conduitController_offset = 0x40;

- [ConsiderationConstants.sol#L48](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0//contracts/lib/ConsiderationConstants.sol#L48)
uint256 constant information_versionLengthPtr = 0x63;

- [ConsiderationConstants.sol#L49](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0//contracts/lib/ConsiderationConstants.sol#L49)
uint256 constant information_versionWithLength = 0x03312e32; // 1.2

- [ConsiderationConstants.sol#L50](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0//contracts/lib/ConsiderationConstants.sol#L50)
uint256 constant information_length = 0xa0;

- [ConsiderationConstants.sol#L56](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0//contracts/lib/ConsiderationConstants.sol#L56)
uint256 constant Offset_fulfillAdvancedOrder_criteriaResolvers = 0x20;

- [ConsiderationConstants.sol#L58](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0//contracts/lib/ConsiderationConstants.sol#L58)
uint256 constant Offset_fulfillAvailableOrders_offerFulfillments = 0x20;

- [ConsiderationConstants.sol#L59](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0//contracts/lib/ConsiderationConstants.sol#L59)
uint256 constant Offset_fulfillAvailableOrders_considerationFulfillments = 0x40;

- [ConsiderationConstants.sol#L61](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0//contracts/lib/ConsiderationConstants.sol#L61)
uint256 constant Offset_fulfillAvailableAdvancedOrders_criteriaResolvers = 0x20;

- [ConsiderationConstants.sol#L62](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0//contracts/lib/ConsiderationConstants.sol#L62)
uint256 constant Offset_fulfillAvailableAdvancedOrders_offerFulfillments = 0x40;

- [ConsiderationConstants.sol#L63](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0//contracts/lib/ConsiderationConstants.sol#L63)
uint256 constant Offset_fulfillAvailableAdvancedOrders_cnsdrationFlflmnts = (

- [ConsiderationConstants.sol#L67](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0//contracts/lib/ConsiderationConstants.sol#L67)
uint256 constant Offset_matchOrders_fulfillments = 0x20;

- [ConsiderationConstants.sol#L69](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0//contracts/lib/ConsiderationConstants.sol#L69)
uint256 constant Offset_matchAdvancedOrders_criteriaResolvers = 0x20;

- [ConsiderationConstants.sol#L70](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0//contracts/lib/ConsiderationConstants.sol#L70)
uint256 constant Offset_matchAdvancedOrders_fulfillments = 0x40;

- [ConsiderationConstants.sol#L76](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0//contracts/lib/ConsiderationConstants.sol#L76)
uint256 constant Selector_length = 4;

- [ConsiderationConstants.sol#L78](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0//contracts/lib/ConsiderationConstants.sol#L78)
uint256 constant Common_token_offset = 0x20;

- [ConsiderationConstants.sol#L79](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0//contracts/lib/ConsiderationConstants.sol#L79)
uint256 constant Common_identifier_offset = 0x40;

- [ConsiderationConstants.sol#L80](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0//contracts/lib/ConsiderationConstants.sol#L80)
uint256 constant Common_amount_offset = 0x60;

- [ConsiderationConstants.sol#L81](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0//contracts/lib/ConsiderationConstants.sol#L81)
uint256 constant Common_endAmount_offset = 0x80;

- [ConsiderationConstants.sol#L83](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0//contracts/lib/ConsiderationConstants.sol#L83)
uint256 constant SpentItem_size = 0x80;

- [ConsiderationConstants.sol#L84](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0//contracts/lib/ConsiderationConstants.sol#L84)
uint256 constant SpentItem_size_shift = 7;

- [ConsiderationConstants.sol#L86](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0//contracts/lib/ConsiderationConstants.sol#L86)
uint256 constant OfferItem_size = 0xa0;

- [ConsiderationConstants.sol#L87](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0//contracts/lib/ConsiderationConstants.sol#L87)
uint256 constant OfferItem_size_with_length = 0xc0;

- [ConsiderationConstants.sol#L89](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0//contracts/lib/ConsiderationConstants.sol#L89)
uint256 constant ReceivedItem_size = 0xa0;

- [ConsiderationConstants.sol#L90](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0//contracts/lib/ConsiderationConstants.sol#L90)
uint256 constant ReceivedItem_amount_offset = 0x60;

- [ConsiderationConstants.sol#L91](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0//contracts/lib/ConsiderationConstants.sol#L91)
uint256 constant ReceivedItem_recipient_offset = 0x80;

- [ConsiderationConstants.sol#L93](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0//contracts/lib/ConsiderationConstants.sol#L93)
uint256 constant ReceivedItem_CommonParams_size = 0x60;

- [ConsiderationConstants.sol#L95](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0//contracts/lib/ConsiderationConstants.sol#L95)
uint256 constant ConsiderationItem_size = 0xc0;

- [ConsiderationConstants.sol#L96](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0//contracts/lib/ConsiderationConstants.sol#L96)
uint256 constant ConsiderationItem_size_with_length = 0xe0;

- [ConsiderationConstants.sol#L98](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0//contracts/lib/ConsiderationConstants.sol#L98)
uint256 constant ConsiderationItem_recipient_offset = 0xa0;

- [ConsiderationConstants.sol#L100](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0//contracts/lib/ConsiderationConstants.sol#L100)
uint256 constant ConsiderItem_recipient_offset = 0xa0;

- [ConsiderationConstants.sol#L102](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0//contracts/lib/ConsiderationConstants.sol#L102)
uint256 constant Execution_offerer_offset = 0x20;

- [ConsiderationConstants.sol#L103](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0//contracts/lib/ConsiderationConstants.sol#L103)
uint256 constant Execution_conduit_offset = 0x40;

- [ConsiderationConstants.sol#L105](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0//contracts/lib/ConsiderationConstants.sol#L105)
uint256 constant Panic_arithmetic = 0x11;

- [ConsiderationConstants.sol#L106](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0//contracts/lib/ConsiderationConstants.sol#L106)
uint256 constant Panic_resource = 0x41;

- [ConsiderationConstants.sol#L108](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0//contracts/lib/ConsiderationConstants.sol#L108)
uint256 constant OrderParameters_offerer_offset = 0x00;

- [ConsiderationConstants.sol#L109](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0//contracts/lib/ConsiderationConstants.sol#L109)
uint256 constant OrderParameters_zone_offset = 0x20;

- [ConsiderationConstants.sol#L110](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0//contracts/lib/ConsiderationConstants.sol#L110)
uint256 constant OrderParameters_offer_head_offset = 0x40;

- [ConsiderationConstants.sol#L111](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0//contracts/lib/ConsiderationConstants.sol#L111)
uint256 constant OrderParameters_consideration_head_offset = 0x60;

- [ConsiderationConstants.sol#L112](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0//contracts/lib/ConsiderationConstants.sol#L112)
uint256 constant OrderParameters_orderType_offset = 0x80;

- [ConsiderationConstants.sol#L113](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0//contracts/lib/ConsiderationConstants.sol#L113)
uint256 constant OrderParameters_startTime_offset = 0xa0;

- [ConsiderationConstants.sol#L114](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0//contracts/lib/ConsiderationConstants.sol#L114)
uint256 constant OrderParameters_endTime_offset = 0xc0;

- [ConsiderationConstants.sol#L115](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0//contracts/lib/ConsiderationConstants.sol#L115)
uint256 constant OrderParameters_zoneHash_offset = 0xe0;

- [ConsiderationConstants.sol#L116](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0//contracts/lib/ConsiderationConstants.sol#L116)
uint256 constant OrderParameters_salt_offset = 0x100;

- [ConsiderationConstants.sol#L117](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0//contracts/lib/ConsiderationConstants.sol#L117)
uint256 constant OrderParameters_conduit_offset = 0x120;

- [ConsiderationConstants.sol#L118](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0//contracts/lib/ConsiderationConstants.sol#L118)
uint256 constant OrderParameters_counter_offset = 0x140;

- [ConsiderationConstants.sol#L120](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0//contracts/lib/ConsiderationConstants.sol#L120)
uint256 constant Fulfillment_itemIndex_offset = 0x20;

- [ConsiderationConstants.sol#L122](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0//contracts/lib/ConsiderationConstants.sol#L122)
uint256 constant AdvancedOrder_head_size = 0xa0;

- [ConsiderationConstants.sol#L123](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0//contracts/lib/ConsiderationConstants.sol#L123)
uint256 constant AdvancedOrder_numerator_offset = 0x20;

- [ConsiderationConstants.sol#L124](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0//contracts/lib/ConsiderationConstants.sol#L124)
uint256 constant AdvancedOrder_denominator_offset = 0x40;

- [ConsiderationConstants.sol#L125](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0//contracts/lib/ConsiderationConstants.sol#L125)
uint256 constant AdvancedOrder_signature_offset = 0x60;

- [ConsiderationConstants.sol#L126](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0//contracts/lib/ConsiderationConstants.sol#L126)
uint256 constant AdvancedOrder_extraData_offset = 0x80;

- [ConsiderationConstants.sol#L128](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0//contracts/lib/ConsiderationConstants.sol#L128)
uint256 constant OrderStatus_ValidatedAndNotCancelled = 1;

- [ConsiderationConstants.sol#L129](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0//contracts/lib/ConsiderationConstants.sol#L129)
uint256 constant OrderStatus_filledNumerator_offset = 0x10;

- [ConsiderationConstants.sol#L130](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0//contracts/lib/ConsiderationConstants.sol#L130)
uint256 constant OrderStatus_filledDenominator_offset = 0x88;

- [ConsiderationConstants.sol#L132](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0//contracts/lib/ConsiderationConstants.sol#L132)
uint256 constant AlmostOneWord = 0x1f;

- [ConsiderationConstants.sol#L133](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0//contracts/lib/ConsiderationConstants.sol#L133)
uint256 constant OneWord = 0x20;

- [ConsiderationConstants.sol#L134](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0//contracts/lib/ConsiderationConstants.sol#L134)
uint256 constant TwoWords = 0x40;

- [ConsiderationConstants.sol#L135](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0//contracts/lib/ConsiderationConstants.sol#L135)
uint256 constant ThreeWords = 0x60;

- [ConsiderationConstants.sol#L136](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0//contracts/lib/ConsiderationConstants.sol#L136)
uint256 constant FourWords = 0x80;

- [ConsiderationConstants.sol#L137](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0//contracts/lib/ConsiderationConstants.sol#L137)
uint256 constant FiveWords = 0xa0;

- [ConsiderationConstants.sol#L139](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0//contracts/lib/ConsiderationConstants.sol#L139)
uint256 constant OneWordShift = 5;

- [ConsiderationConstants.sol#L140](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0//contracts/lib/ConsiderationConstants.sol#L140)
uint256 constant TwoWordsShift = 6;

- [ConsiderationConstants.sol#L142](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0//contracts/lib/ConsiderationConstants.sol#L142)
uint256 constant AlmostTwoWords = 0x3f;

- [ConsiderationConstants.sol#L143](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0//contracts/lib/ConsiderationConstants.sol#L143)
uint256 constant OnlyFullWordMask = 0xffffffe0;

- [ConsiderationConstants.sol#L145](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0//contracts/lib/ConsiderationConstants.sol#L145)
uint256 constant FreeMemoryPointerSlot = 0x40;

- [ConsiderationConstants.sol#L146](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0//contracts/lib/ConsiderationConstants.sol#L146)
uint256 constant ZeroSlot = 0x60;

- [ConsiderationConstants.sol#L147](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0//contracts/lib/ConsiderationConstants.sol#L147)
uint256 constant DefaultFreeMemoryPointer = 0x80;

- [ConsiderationConstants.sol#L149](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0//contracts/lib/ConsiderationConstants.sol#L149)
uint256 constant Slot0x80 = 0x80;

- [ConsiderationConstants.sol#L150](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0//contracts/lib/ConsiderationConstants.sol#L150)
uint256 constant Slot0xA0 = 0xa0;

- [ConsiderationConstants.sol#L152](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0//contracts/lib/ConsiderationConstants.sol#L152)
uint256 constant BasicOrder_endAmount_cdPtr = 0x104;

- [ConsiderationConstants.sol#L153](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0//contracts/lib/ConsiderationConstants.sol#L153)
uint256 constant BasicOrder_common_params_size = 0xa0;

- [ConsiderationConstants.sol#L154](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0//contracts/lib/ConsiderationConstants.sol#L154)
uint256 constant BasicOrder_considerationHashesArray_ptr = 0x160;

- [ConsiderationConstants.sol#L156](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0//contracts/lib/ConsiderationConstants.sol#L156)
uint256 constant BasicOrder_receivedItemByteMap = (

- [ConsiderationConstants.sol#L159](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0//contracts/lib/ConsiderationConstants.sol#L159)
uint256 constant BasicOrder_offeredItemByteMap = (

- [ConsiderationConstants.sol#L163](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0//contracts/lib/ConsiderationConstants.sol#L163)
bytes32 constant OrdersMatchedTopic0 = 0x4b9f2d36e1b4c93de62cc077b00b1a91d84b6c31b4a14e012718dcca230689e7;

- [ConsiderationConstants.sol#L165](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0//contracts/lib/ConsiderationConstants.sol#L165)
uint256 constant EIP712_Order_size = 0x180;

- [ConsiderationConstants.sol#L166](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0//contracts/lib/ConsiderationConstants.sol#L166)
uint256 constant EIP712_OfferItem_size = 0xc0;

- [ConsiderationConstants.sol#L167](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0//contracts/lib/ConsiderationConstants.sol#L167)
uint256 constant EIP712_ConsiderationItem_size = 0xe0;

- [ConsiderationConstants.sol#L168](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0//contracts/lib/ConsiderationConstants.sol#L168)
uint256 constant AdditionalRecipient_size = 0x40;

- [ConsiderationConstants.sol#L169](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0//contracts/lib/ConsiderationConstants.sol#L169)
uint256 constant AdditionalRecipient_size_shift = 6;

- [ConsiderationConstants.sol#L171](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0//contracts/lib/ConsiderationConstants.sol#L171)
uint256 constant EIP712_DomainSeparator_offset = 0x02;

- [ConsiderationConstants.sol#L172](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0//contracts/lib/ConsiderationConstants.sol#L172)
uint256 constant EIP712_OrderHash_offset = 0x22;

- [ConsiderationConstants.sol#L173](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0//contracts/lib/ConsiderationConstants.sol#L173)
uint256 constant EIP712_DigestPayload_size = 0x42;

- [ConsiderationConstants.sol#L175](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0//contracts/lib/ConsiderationConstants.sol#L175)
uint256 constant EIP712_domainData_nameHash_offset = 0x20;

- [ConsiderationConstants.sol#L176](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0//contracts/lib/ConsiderationConstants.sol#L176)
uint256 constant EIP712_domainData_versionHash_offset = 0x40;

- [ConsiderationConstants.sol#L177](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0//contracts/lib/ConsiderationConstants.sol#L177)
uint256 constant EIP712_domainData_chainId_offset = 0x60;

- [ConsiderationConstants.sol#L178](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0//contracts/lib/ConsiderationConstants.sol#L178)
uint256 constant EIP712_domainData_verifyingContract_offset = 0x80;

- [ConsiderationConstants.sol#L179](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0//contracts/lib/ConsiderationConstants.sol#L179)
uint256 constant EIP712_domainData_size = 0xa0;

- [ConsiderationConstants.sol#L185](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0//contracts/lib/ConsiderationConstants.sol#L185)
uint256 constant BulkOrderProof_minSize = 0x63;

- [ConsiderationConstants.sol#L186](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0//contracts/lib/ConsiderationConstants.sol#L186)
uint256 constant BulkOrderProof_rangeSize = 0x2e2;

- [ConsiderationConstants.sol#L187](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0//contracts/lib/ConsiderationConstants.sol#L187)
uint256 constant BulkOrderProof_lengthAdjustmentBeforeMask = 0x1d;

- [ConsiderationConstants.sol#L188](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0//contracts/lib/ConsiderationConstants.sol#L188)
uint256 constant BulkOrderProof_lengthRangeAfterMask = 0x2;

- [ConsiderationConstants.sol#L189](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0//contracts/lib/ConsiderationConstants.sol#L189)
uint256 constant BulkOrderProof_keyShift = 0xe8;

- [ConsiderationConstants.sol#L190](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0//contracts/lib/ConsiderationConstants.sol#L190)
uint256 constant BulkOrderProof_keySize = 0x3;

- [ConsiderationConstants.sol#L192](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0//contracts/lib/ConsiderationConstants.sol#L192)
uint256 constant receivedItemsHash_ptr = 0x60;

- [ConsiderationConstants.sol#L230](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0//contracts/lib/ConsiderationConstants.sol#L230)
uint256 constant OrderFulfilled_baseSize = 0x1e0;

- [ConsiderationConstants.sol#L231](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0//contracts/lib/ConsiderationConstants.sol#L231)
uint256 constant OrderFulfilled_selector = (

- [ConsiderationConstants.sol#L238](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0//contracts/lib/ConsiderationConstants.sol#L238)
uint256 constant OrderFulfilled_baseOffset = 0x180;

- [ConsiderationConstants.sol#L239](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0//contracts/lib/ConsiderationConstants.sol#L239)
uint256 constant OrderFulfilled_consideration_length_baseOffset = 0x2a0;

- [ConsiderationConstants.sol#L240](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0//contracts/lib/ConsiderationConstants.sol#L240)
uint256 constant OrderFulfilled_offer_length_baseOffset = 0x200;

- [ConsiderationConstants.sol#L244](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0//contracts/lib/ConsiderationConstants.sol#L244)
address constant IdentityPrecompile = address(4);

- [ConsiderationConstants.sol#L245](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0//contracts/lib/ConsiderationConstants.sol#L245)
uint256 constant OrderFulfilled_baseDataSize = 0x160;

- [ConsiderationConstants.sol#L246](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0//contracts/lib/ConsiderationConstants.sol#L246)
uint256 constant ValidateOrder_offerDataOffset = 0x184;

- [ConsiderationConstants.sol#L248](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0//contracts/lib/ConsiderationConstants.sol#L248)
uint256 constant RatifyOrder_offerDataOffset = 0xc4;

- [ConsiderationConstants.sol#L250](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0//contracts/lib/ConsiderationConstants.sol#L250)
// uint256 constant OrderFulfilled_orderHash_offset = 0x00;

- [ConsiderationConstants.sol#L251](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0//contracts/lib/ConsiderationConstants.sol#L251)
uint256 constant OrderFulfilled_fulfiller_offset = 0x20;

- [ConsiderationConstants.sol#L252](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0//contracts/lib/ConsiderationConstants.sol#L252)
uint256 constant OrderFulfilled_offer_head_offset = 0x40;

- [ConsiderationConstants.sol#L253](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0//contracts/lib/ConsiderationConstants.sol#L253)
uint256 constant OrderFulfilled_offer_body_offset = 0x80;

- [ConsiderationConstants.sol#L254](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0//contracts/lib/ConsiderationConstants.sol#L254)
uint256 constant OrderFulfilled_consideration_head_offset = 0x60;

- [ConsiderationConstants.sol#L255](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0//contracts/lib/ConsiderationConstants.sol#L255)
uint256 constant OrderFulfilled_consideration_body_offset = 0x120;

- [ConsiderationConstants.sol#L258](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0//contracts/lib/ConsiderationConstants.sol#L258)
uint256 constant BasicOrder_parameters_cdPtr = 0x04;

- [ConsiderationConstants.sol#L259](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0//contracts/lib/ConsiderationConstants.sol#L259)
uint256 constant BasicOrder_considerationToken_cdPtr = 0x24;

- [ConsiderationConstants.sol#L260](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0//contracts/lib/ConsiderationConstants.sol#L260)
// uint256 constant BasicOrder_considerationIdentifier_cdPtr = 0x44;

- [ConsiderationConstants.sol#L261](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0//contracts/lib/ConsiderationConstants.sol#L261)
uint256 constant BasicOrder_considerationAmount_cdPtr = 0x64;

- [ConsiderationConstants.sol#L262](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0//contracts/lib/ConsiderationConstants.sol#L262)
uint256 constant BasicOrder_offerer_cdPtr = 0x84;

- [ConsiderationConstants.sol#L263](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0//contracts/lib/ConsiderationConstants.sol#L263)
uint256 constant BasicOrder_zone_cdPtr = 0xa4;

- [ConsiderationConstants.sol#L264](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0//contracts/lib/ConsiderationConstants.sol#L264)
uint256 constant BasicOrder_offerToken_cdPtr = 0xc4;

- [ConsiderationConstants.sol#L265](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0//contracts/lib/ConsiderationConstants.sol#L265)
// uint256 constant BasicOrder_offerIdentifier_cdPtr = 0xe4;

- [ConsiderationConstants.sol#L266](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0//contracts/lib/ConsiderationConstants.sol#L266)
uint256 constant BasicOrder_offerAmount_cdPtr = 0x104;

- [ConsiderationConstants.sol#L267](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0//contracts/lib/ConsiderationConstants.sol#L267)
uint256 constant BasicOrder_basicOrderType_cdPtr = 0x124;

- [ConsiderationConstants.sol#L268](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0//contracts/lib/ConsiderationConstants.sol#L268)
uint256 constant BasicOrder_startTime_cdPtr = 0x144;

- [ConsiderationConstants.sol#L269](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0//contracts/lib/ConsiderationConstants.sol#L269)
// uint256 constant BasicOrder_endTime_cdPtr = 0x164;

- [ConsiderationConstants.sol#L270](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0//contracts/lib/ConsiderationConstants.sol#L270)
// uint256 constant BasicOrder_zoneHash_cdPtr = 0x184;

- [ConsiderationConstants.sol#L271](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0//contracts/lib/ConsiderationConstants.sol#L271)
// uint256 constant BasicOrder_salt_cdPtr = 0x1a4;

- [ConsiderationConstants.sol#L272](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0//contracts/lib/ConsiderationConstants.sol#L272)
uint256 constant BasicOrder_offererConduit_cdPtr = 0x1c4;

- [ConsiderationConstants.sol#L273](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0//contracts/lib/ConsiderationConstants.sol#L273)
uint256 constant BasicOrder_fulfillerConduit_cdPtr = 0x1e4;

- [ConsiderationConstants.sol#L274](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0//contracts/lib/ConsiderationConstants.sol#L274)
uint256 constant BasicOrder_totalOriginalAdditionalRecipients_cdPtr = 0x204;

- [ConsiderationConstants.sol#L275](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0//contracts/lib/ConsiderationConstants.sol#L275)
uint256 constant BasicOrder_additionalRecipients_head_cdPtr = 0x224;

- [ConsiderationConstants.sol#L276](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0//contracts/lib/ConsiderationConstants.sol#L276)
uint256 constant BasicOrder_signature_cdPtr = 0x244;

- [ConsiderationConstants.sol#L277](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0//contracts/lib/ConsiderationConstants.sol#L277)
uint256 constant BasicOrder_additionalRecipients_length_cdPtr = 0x264;

- [ConsiderationConstants.sol#L278](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0//contracts/lib/ConsiderationConstants.sol#L278)
uint256 constant BasicOrder_additionalRecipients_data_cdPtr = 0x284;

- [ConsiderationConstants.sol#L280](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0//contracts/lib/ConsiderationConstants.sol#L280)
uint256 constant BasicOrder_parameters_ptr = 0x20;

- [ConsiderationConstants.sol#L282](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0//contracts/lib/ConsiderationConstants.sol#L282)
uint256 constant BasicOrder_basicOrderType_range = 0x18; // 24 values

- [ConsiderationConstants.sol#L295](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0//contracts/lib/ConsiderationConstants.sol#L295)
uint256 constant BasicOrder_considerationItem_typeHash_ptr = 0x80; // memoryPtr

- [ConsiderationConstants.sol#L296](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0//contracts/lib/ConsiderationConstants.sol#L296)
uint256 constant BasicOrder_considerationItem_itemType_ptr = 0xa0;

- [ConsiderationConstants.sol#L297](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0//contracts/lib/ConsiderationConstants.sol#L297)
uint256 constant BasicOrder_considerationItem_token_ptr = 0xc0;

- [ConsiderationConstants.sol#L298](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0//contracts/lib/ConsiderationConstants.sol#L298)
uint256 constant BasicOrder_considerationItem_identifier_ptr = 0xe0;

- [ConsiderationConstants.sol#L299](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0//contracts/lib/ConsiderationConstants.sol#L299)
uint256 constant BasicOrder_considerationItem_startAmount_ptr = 0x100;

- [ConsiderationConstants.sol#L300](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0//contracts/lib/ConsiderationConstants.sol#L300)
uint256 constant BasicOrder_considerationItem_endAmount_ptr = 0x120;

- [ConsiderationConstants.sol#L301](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0//contracts/lib/ConsiderationConstants.sol#L301)
// uint256 constant BasicOrder_considerationItem_recipient_ptr = 0x140;

- [ConsiderationConstants.sol#L313](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0//contracts/lib/ConsiderationConstants.sol#L313)
uint256 constant BasicOrder_offerItem_typeHash_ptr = DefaultFreeMemoryPointer;

- [ConsiderationConstants.sol#L314](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0//contracts/lib/ConsiderationConstants.sol#L314)
uint256 constant BasicOrder_offerItem_itemType_ptr = 0xa0;

- [ConsiderationConstants.sol#L315](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0//contracts/lib/ConsiderationConstants.sol#L315)
uint256 constant BasicOrder_offerItem_token_ptr = 0xc0;

- [ConsiderationConstants.sol#L318](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0//contracts/lib/ConsiderationConstants.sol#L318)
uint256 constant BasicOrder_offerItem_endAmount_ptr = 0x120;

- [ConsiderationConstants.sol#L336](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0//contracts/lib/ConsiderationConstants.sol#L336)
uint256 constant BasicOrder_order_typeHash_ptr = 0x80;

- [ConsiderationConstants.sol#L337](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0//contracts/lib/ConsiderationConstants.sol#L337)
uint256 constant BasicOrder_order_offerer_ptr = 0xa0;

- [ConsiderationConstants.sol#L339](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0//contracts/lib/ConsiderationConstants.sol#L339)
uint256 constant BasicOrder_order_offerHashes_ptr = 0xe0;

- [ConsiderationConstants.sol#L340](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0//contracts/lib/ConsiderationConstants.sol#L340)
uint256 constant BasicOrder_order_considerationHashes_ptr = 0x100;

- [ConsiderationConstants.sol#L341](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0//contracts/lib/ConsiderationConstants.sol#L341)
uint256 constant BasicOrder_order_orderType_ptr = 0x120;

- [ConsiderationConstants.sol#L342](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0//contracts/lib/ConsiderationConstants.sol#L342)
uint256 constant BasicOrder_order_startTime_ptr = 0x140;

- [ConsiderationConstants.sol#L347](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0//contracts/lib/ConsiderationConstants.sol#L347)
uint256 constant BasicOrder_order_counter_ptr = 0x1e0;

- [ConsiderationConstants.sol#L348](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0//contracts/lib/ConsiderationConstants.sol#L348)
uint256 constant BasicOrder_additionalRecipients_head_ptr = 0x240;

- [ConsiderationConstants.sol#L349](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0//contracts/lib/ConsiderationConstants.sol#L349)
uint256 constant BasicOrder_signature_ptr = 0x260;

- [ConsiderationConstants.sol#L350](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0//contracts/lib/ConsiderationConstants.sol#L350)
uint256 constant BasicOrder_startTimeThroughZoneHash_size = 0x60;

- [ConsiderationConstants.sol#L352](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0//contracts/lib/ConsiderationConstants.sol#L352)
uint256 constant ContractOrder_orderHash_offerer_shift = 0x60;

- [ConsiderationConstants.sol#L354](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0//contracts/lib/ConsiderationConstants.sol#L354)
uint256 constant Counter_blockhash_shift = 0x80;

- [ConsiderationConstants.sol#L357](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0//contracts/lib/ConsiderationConstants.sol#L357)
bytes32 constant EIP2098_allButHighestBitMask = (

- [ConsiderationConstants.sol#L360](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0//contracts/lib/ConsiderationConstants.sol#L360)
bytes32 constant ECDSA_twentySeventhAndTwentyEighthBytesSet = (

- [ConsiderationConstants.sol#L363](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0//contracts/lib/ConsiderationConstants.sol#L363)
uint256 constant ECDSA_MaxLength = 65;

- [ConsiderationConstants.sol#L364](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0//contracts/lib/ConsiderationConstants.sol#L364)
uint256 constant ECDSA_signature_s_offset = 0x40;

- [ConsiderationConstants.sol#L365](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0//contracts/lib/ConsiderationConstants.sol#L365)
uint256 constant ECDSA_signature_v_offset = 0x60;

- [ConsiderationConstants.sol#L367](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0//contracts/lib/ConsiderationConstants.sol#L367)
bytes32 constant EIP1271_isValidSignature_selector = (

- [ConsiderationConstants.sol#L370](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0//contracts/lib/ConsiderationConstants.sol#L370)
uint256 constant EIP1271_isValidSignature_signatureHead_negativeOffset = 0x20;

- [ConsiderationConstants.sol#L371](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0//contracts/lib/ConsiderationConstants.sol#L371)
uint256 constant EIP1271_isValidSignature_digest_negativeOffset = 0x40;

- [ConsiderationConstants.sol#L372](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0//contracts/lib/ConsiderationConstants.sol#L372)
uint256 constant EIP1271_isValidSignature_selector_negativeOffset = 0x44;

- [ConsiderationConstants.sol#L373](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0//contracts/lib/ConsiderationConstants.sol#L373)
uint256 constant EIP1271_isValidSignature_calldata_baseLength = 0x64;

- [ConsiderationConstants.sol#L375](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0//contracts/lib/ConsiderationConstants.sol#L375)
uint256 constant EIP1271_isValidSignature_signature_head_offset = 0x40;

- [ConsiderationConstants.sol#L381](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0//contracts/lib/ConsiderationConstants.sol#L381)
uint256 constant ExtraGasBuffer = 0x20;

- [ConsiderationConstants.sol#L382](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0//contracts/lib/ConsiderationConstants.sol#L382)
uint256 constant CostPerWord = 3;

- [ConsiderationConstants.sol#L383](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0//contracts/lib/ConsiderationConstants.sol#L383)
uint256 constant MemoryExpansionCoefficientShift = 9;

- [ConsiderationConstants.sol#L385](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0//contracts/lib/ConsiderationConstants.sol#L385)
uint256 constant Create2AddressDerivation_ptr = 0x0b;

- [ConsiderationConstants.sol#L386](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0//contracts/lib/ConsiderationConstants.sol#L386)
uint256 constant Create2AddressDerivation_length = 0x55;

- [ConsiderationConstants.sol#L388](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0//contracts/lib/ConsiderationConstants.sol#L388)
uint256 constant MaskOverByteTwelve = (

- [ConsiderationConstants.sol#L392](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0//contracts/lib/ConsiderationConstants.sol#L392)
uint256 constant MaskOverLastTwentyBytes = (

- [ConsiderationConstants.sol#L396](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0//contracts/lib/ConsiderationConstants.sol#L396)
uint256 constant MaskOverFirstFourBytes = (

- [ConsiderationConstants.sol#L400](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0//contracts/lib/ConsiderationConstants.sol#L400)
uint256 constant Conduit_execute_signature = (

- [ConsiderationConstants.sol#L404](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0//contracts/lib/ConsiderationConstants.sol#L404)
uint256 constant MaxUint8 = 0xff;

- [ConsiderationConstants.sol#L405](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0//contracts/lib/ConsiderationConstants.sol#L405)
uint256 constant MaxUint120 = 0xffffffffffffffffffffffffffffff;

- [ConsiderationConstants.sol#L407](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0//contracts/lib/ConsiderationConstants.sol#L407)
uint256 constant Conduit_execute_ConduitTransfer_ptr = 0x20;

- [ConsiderationConstants.sol#L408](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0//contracts/lib/ConsiderationConstants.sol#L408)
uint256 constant Conduit_execute_ConduitTransfer_length = 0x01;

- [ConsiderationConstants.sol#L410](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0//contracts/lib/ConsiderationConstants.sol#L410)
uint256 constant Conduit_execute_ConduitTransfer_offset_ptr = 0x04;

- [ConsiderationConstants.sol#L411](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0//contracts/lib/ConsiderationConstants.sol#L411)
uint256 constant Conduit_execute_ConduitTransfer_length_ptr = 0x24;

- [ConsiderationConstants.sol#L412](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0//contracts/lib/ConsiderationConstants.sol#L412)
uint256 constant Conduit_execute_transferItemType_ptr = 0x44;

- [ConsiderationConstants.sol#L413](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0//contracts/lib/ConsiderationConstants.sol#L413)
uint256 constant Conduit_execute_transferToken_ptr = 0x64;

- [ConsiderationConstants.sol#L414](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0//contracts/lib/ConsiderationConstants.sol#L414)
uint256 constant Conduit_execute_transferFrom_ptr = 0x84;

- [ConsiderationConstants.sol#L415](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0//contracts/lib/ConsiderationConstants.sol#L415)
uint256 constant Conduit_execute_transferTo_ptr = 0xa4;

- [ConsiderationConstants.sol#L416](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0//contracts/lib/ConsiderationConstants.sol#L416)
uint256 constant Conduit_execute_transferIdentifier_ptr = 0xc4;

- [ConsiderationConstants.sol#L417](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0//contracts/lib/ConsiderationConstants.sol#L417)
uint256 constant Conduit_execute_transferAmount_ptr = 0xe4;

- [ConsiderationConstants.sol#L419](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0//contracts/lib/ConsiderationConstants.sol#L419)
uint256 constant OneConduitExecute_size = 0x104;

- [ConsiderationConstants.sol#L422](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0//contracts/lib/ConsiderationConstants.sol#L422)
uint256 constant AccumulatorDisarmed = 0x20;

- [ConsiderationConstants.sol#L423](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0//contracts/lib/ConsiderationConstants.sol#L423)
uint256 constant AccumulatorArmed = 0x40;

- [ConsiderationConstants.sol#L424](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0//contracts/lib/ConsiderationConstants.sol#L424)
uint256 constant Accumulator_conduitKey_ptr = 0x20;

- [ConsiderationConstants.sol#L425](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0//contracts/lib/ConsiderationConstants.sol#L425)
uint256 constant Accumulator_selector_ptr = 0x40;

- [ConsiderationConstants.sol#L426](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0//contracts/lib/ConsiderationConstants.sol#L426)
uint256 constant Accumulator_array_offset_ptr = 0x44;

- [ConsiderationConstants.sol#L427](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0//contracts/lib/ConsiderationConstants.sol#L427)
uint256 constant Accumulator_array_length_ptr = 0x64;

- [ConsiderationConstants.sol#L429](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0//contracts/lib/ConsiderationConstants.sol#L429)
uint256 constant Accumulator_itemSizeOffsetDifference = 0x3c;

- [ConsiderationConstants.sol#L431](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0//contracts/lib/ConsiderationConstants.sol#L431)
uint256 constant Accumulator_array_offset = 0x20;

- [ConsiderationConstants.sol#L432](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0//contracts/lib/ConsiderationConstants.sol#L432)
uint256 constant Conduit_transferItem_size = 0xc0;

- [ConsiderationConstants.sol#L433](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0//contracts/lib/ConsiderationConstants.sol#L433)
uint256 constant Conduit_transferItem_token_ptr = 0x20;

- [ConsiderationConstants.sol#L434](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0//contracts/lib/ConsiderationConstants.sol#L434)
uint256 constant Conduit_transferItem_from_ptr = 0x40;

- [ConsiderationConstants.sol#L435](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0//contracts/lib/ConsiderationConstants.sol#L435)
uint256 constant Conduit_transferItem_to_ptr = 0x60;

- [ConsiderationConstants.sol#L436](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0//contracts/lib/ConsiderationConstants.sol#L436)
uint256 constant Conduit_transferItem_identifier_ptr = 0x80;

- [ConsiderationConstants.sol#L437](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0//contracts/lib/ConsiderationConstants.sol#L437)
uint256 constant Conduit_transferItem_amount_ptr = 0xa0;

- [ConsiderationConstants.sol#L439](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0//contracts/lib/ConsiderationConstants.sol#L439)
uint256 constant Ecrecover_precompile = 1;

- [ConsiderationConstants.sol#L440](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0//contracts/lib/ConsiderationConstants.sol#L440)
uint256 constant Ecrecover_args_size = 0x80;

- [ConsiderationConstants.sol#L441](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0//contracts/lib/ConsiderationConstants.sol#L441)
uint256 constant Signature_lower_v = 27;

- [ConsiderationConstants.sol#L444](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0//contracts/lib/ConsiderationConstants.sol#L444)
uint256 constant NonMatchSelector_MagicMask = (

- [ConsiderationConstants.sol#L450](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0//contracts/lib/ConsiderationConstants.sol#L450)
uint256 constant NonMatchSelector_InvalidErrorValue = (

- [ConsiderationConstants.sol#L454](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0//contracts/lib/ConsiderationConstants.sol#L454)
uint256 constant IsValidOrder_signature = (

- [ConsiderationConstants.sol#L457](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0//contracts/lib/ConsiderationConstants.sol#L457)
uint256 constant IsValidOrder_sig_ptr = 0x0;

- [ConsiderationConstants.sol#L458](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0//contracts/lib/ConsiderationConstants.sol#L458)
uint256 constant IsValidOrder_orderHash_ptr = 0x04;

- [ConsiderationConstants.sol#L459](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0//contracts/lib/ConsiderationConstants.sol#L459)
uint256 constant IsValidOrder_caller_ptr = 0x24;

- [ConsiderationConstants.sol#L460](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0//contracts/lib/ConsiderationConstants.sol#L460)
uint256 constant IsValidOrder_offerer_ptr = 0x44;

- [ConsiderationConstants.sol#L461](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0//contracts/lib/ConsiderationConstants.sol#L461)
uint256 constant IsValidOrder_zoneHash_ptr = 0x64;

- [ConsiderationConstants.sol#L462](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0//contracts/lib/ConsiderationConstants.sol#L462)
uint256 constant IsValidOrder_length = 0x84; // 4 + 32 * 4 == 132

- [ConsiderationConstants.sol#L464](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0//contracts/lib/ConsiderationConstants.sol#L464)
uint256 constant Error_selector_offset = 0x1c;

- [ConsiderationConstants.sol#L474](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0//contracts/lib/ConsiderationConstants.sol#L474)
uint256 constant MissingFulfillmentComponentOnAggregation_error_selector = (

- [ConsiderationConstants.sol#L477](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0//contracts/lib/ConsiderationConstants.sol#L477)
uint256 constant MissingFulfillmentComponentOnAggregation_error_side_ptr = 0x20;

- [ConsiderationConstants.sol#L478](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0//contracts/lib/ConsiderationConstants.sol#L478)
uint256 constant MissingFulfillmentComponentOnAggregation_error_length = 0x24;

- [ConsiderationConstants.sol#L487](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0//contracts/lib/ConsiderationConstants.sol#L487)
uint256 constant OfferAndConsiderationRequiredOnFulfillment_error_selector = (

- [ConsiderationConstants.sol#L490](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0//contracts/lib/ConsiderationConstants.sol#L490)
uint256 constant OfferAndConsiderationRequiredOnFulfillment_error_length = 0x04;

- [ConsiderationConstants.sol#L502](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0//contracts/lib/ConsiderationConstants.sol#L502)
uint256 constant MismatchedFulfillmentOfferAndConsiderationComponents_error_selector = 0xbced929d;

- [ConsiderationConstants.sol#L503](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0//contracts/lib/ConsiderationConstants.sol#L503)
uint256 constant MismatchedFulfillmentOfferAndConsiderationComponents_error_fulfillmentIndex_ptr = 0x20;

- [ConsiderationConstants.sol#L504](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0//contracts/lib/ConsiderationConstants.sol#L504)
uint256 constant MismatchedFulfillmentOfferAndConsiderationComponents_error_length = 0x24;

- [ConsiderationConstants.sol#L513](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0//contracts/lib/ConsiderationConstants.sol#L513)
uint256 constant InvalidFulfillmentComponentData_error_selector = 0x7fda7279;

- [ConsiderationConstants.sol#L514](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0//contracts/lib/ConsiderationConstants.sol#L514)
uint256 constant InvalidFulfillmentComponentData_error_length = 0x04;

- [ConsiderationConstants.sol#L523](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0//contracts/lib/ConsiderationConstants.sol#L523)
uint256 constant InexactFraction_error_selector = 0xc63cf089;

- [ConsiderationConstants.sol#L524](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0//contracts/lib/ConsiderationConstants.sol#L524)
uint256 constant InexactFraction_error_length = 0x04;

- [ConsiderationConstants.sol#L534](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0//contracts/lib/ConsiderationConstants.sol#L534)
uint256 constant OrderCriteriaResolverOutOfRange_error_selector = 0x133c37c6;

- [ConsiderationConstants.sol#L535](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0//contracts/lib/ConsiderationConstants.sol#L535)
uint256 constant OrderCriteriaResolverOutOfRange_error_side_ptr = 0x20;

- [ConsiderationConstants.sol#L536](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0//contracts/lib/ConsiderationConstants.sol#L536)
uint256 constant OrderCriteriaResolverOutOfRange_error_length = 0x24;

- [ConsiderationConstants.sol#L547](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0//contracts/lib/ConsiderationConstants.sol#L547)
uint256 constant UnresolvedOfferCriteria_error_selector = 0xd6929332;

- [ConsiderationConstants.sol#L548](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0//contracts/lib/ConsiderationConstants.sol#L548)
uint256 constant UnresolvedOfferCriteria_error_orderIndex_ptr = 0x20;

- [ConsiderationConstants.sol#L549](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0//contracts/lib/ConsiderationConstants.sol#L549)
uint256 constant UnresolvedOfferCriteria_error_offerIndex_ptr = 0x40;

- [ConsiderationConstants.sol#L550](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0//contracts/lib/ConsiderationConstants.sol#L550)
uint256 constant UnresolvedOfferCriteria_error_length = 0x44;

- [ConsiderationConstants.sol#L561](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0//contracts/lib/ConsiderationConstants.sol#L561)
uint256 constant UnresolvedConsiderationCriteria_error_selector = 0xa8930e9a;

- [ConsiderationConstants.sol#L562](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0//contracts/lib/ConsiderationConstants.sol#L562)
uint256 constant UnresolvedConsiderationCriteria_error_orderIndex_ptr = 0x20;

- [ConsiderationConstants.sol#L563](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0//contracts/lib/ConsiderationConstants.sol#L563)
uint256 constant UnresolvedConsiderationCriteria_error_considerationIndex_ptr = 0x40;

- [ConsiderationConstants.sol#L564](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0//contracts/lib/ConsiderationConstants.sol#L564)
uint256 constant UnresolvedConsiderationCriteria_error_length = 0x44;

- [ConsiderationConstants.sol#L573](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0//contracts/lib/ConsiderationConstants.sol#L573)
uint256 constant OfferCriteriaResolverOutOfRange_error_selector = 0xbfb3f8ce;

- [ConsiderationConstants.sol#L574](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0//contracts/lib/ConsiderationConstants.sol#L574)
uint256 constant OfferCriteriaResolverOutOfRange_error_length = 0x04;

- [ConsiderationConstants.sol#L583](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0//contracts/lib/ConsiderationConstants.sol#L583)
uint256 constant ConsiderationCriteriaResolverOutOfRange_error_selector = 0x6088d7de;

- [ConsiderationConstants.sol#L584](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0//contracts/lib/ConsiderationConstants.sol#L584)
uint256 constant ConsiderationCriteriaResolverOutOfRange_err_selector = 0x6088d7de;

- [ConsiderationConstants.sol#L585](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0//contracts/lib/ConsiderationConstants.sol#L585)
uint256 constant ConsiderationCriteriaResolverOutOfRange_error_length = 0x04;

- [ConsiderationConstants.sol#L594](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0//contracts/lib/ConsiderationConstants.sol#L594)
uint256 constant CriteriaNotEnabledForItem_error_selector = 0x94eb6af6;

- [ConsiderationConstants.sol#L595](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0//contracts/lib/ConsiderationConstants.sol#L595)
uint256 constant CriteriaNotEnabledForItem_error_length = 0x04;

- [ConsiderationConstants.sol#L604](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0//contracts/lib/ConsiderationConstants.sol#L604)
uint256 constant InvalidProof_error_selector = 0x09bde339;

- [ConsiderationConstants.sol#L605](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0//contracts/lib/ConsiderationConstants.sol#L605)
uint256 constant InvalidProof_error_length = 0x04;

- [ConsiderationConstants.sol#L615](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0//contracts/lib/ConsiderationConstants.sol#L615)
uint256 constant InvalidRestrictedOrder_error_selector = 0xfb5014fc;

- [ConsiderationConstants.sol#L616](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0//contracts/lib/ConsiderationConstants.sol#L616)
uint256 constant InvalidRestrictedOrder_error_orderHash_ptr = 0x20;

- [ConsiderationConstants.sol#L617](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0//contracts/lib/ConsiderationConstants.sol#L617)
uint256 constant InvalidRestrictedOrder_error_length = 0x24;

- [ConsiderationConstants.sol#L627](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0//contracts/lib/ConsiderationConstants.sol#L627)
uint256 constant InvalidContractOrder_error_selector = 0x93979285;

- [ConsiderationConstants.sol#L628](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0//contracts/lib/ConsiderationConstants.sol#L628)
uint256 constant InvalidContractOrder_error_orderHash_ptr = 0x20;

- [ConsiderationConstants.sol#L629](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0//contracts/lib/ConsiderationConstants.sol#L629)
uint256 constant InvalidContractOrder_error_length = 0x24;

- [ConsiderationConstants.sol#L639](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0//contracts/lib/ConsiderationConstants.sol#L639)
uint256 constant BadSignatureV_error_selector = 0x1f003d0a;

- [ConsiderationConstants.sol#L640](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0//contracts/lib/ConsiderationConstants.sol#L640)
uint256 constant BadSignatureV_error_v_ptr = 0x20;

- [ConsiderationConstants.sol#L641](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0//contracts/lib/ConsiderationConstants.sol#L641)
uint256 constant BadSignatureV_error_length = 0x24;

- [ConsiderationConstants.sol#L650](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0//contracts/lib/ConsiderationConstants.sol#L650)
uint256 constant InvalidSigner_error_selector = 0x815e1d64;

- [ConsiderationConstants.sol#L651](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0//contracts/lib/ConsiderationConstants.sol#L651)
uint256 constant InvalidSigner_error_length = 0x04;

- [ConsiderationConstants.sol#L660](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0//contracts/lib/ConsiderationConstants.sol#L660)
uint256 constant InvalidSignature_error_selector = 0x8baa579f;

- [ConsiderationConstants.sol#L661](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0//contracts/lib/ConsiderationConstants.sol#L661)
uint256 constant InvalidSignature_error_length = 0x04;

- [ConsiderationConstants.sol#L670](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0//contracts/lib/ConsiderationConstants.sol#L670)
uint256 constant BadContractSignature_error_selector = 0x4f7fb80d;

- [ConsiderationConstants.sol#L671](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0//contracts/lib/ConsiderationConstants.sol#L671)
uint256 constant BadContractSignature_error_length = 0x04;

- [ConsiderationConstants.sol#L681](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0//contracts/lib/ConsiderationConstants.sol#L681)
uint256 constant InvalidERC721TransferAmount_error_selector = 0x69f95827;

- [ConsiderationConstants.sol#L682](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0//contracts/lib/ConsiderationConstants.sol#L682)
uint256 constant InvalidERC721TransferAmount_error_amount_ptr = 0x20;

- [ConsiderationConstants.sol#L683](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0//contracts/lib/ConsiderationConstants.sol#L683)
uint256 constant InvalidERC721TransferAmount_error_length = 0x24;

- [ConsiderationConstants.sol#L692](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0//contracts/lib/ConsiderationConstants.sol#L692)
uint256 constant MissingItemAmount_error_selector = 0x91b3e514;

- [ConsiderationConstants.sol#L693](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0//contracts/lib/ConsiderationConstants.sol#L693)
uint256 constant MissingItemAmount_error_length = 0x04;

- [ConsiderationConstants.sol#L702](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0//contracts/lib/ConsiderationConstants.sol#L702)
uint256 constant UnusedItemParameters_error_selector = 0x6ab37ce7;

- [ConsiderationConstants.sol#L703](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0//contracts/lib/ConsiderationConstants.sol#L703)
uint256 constant UnusedItemParameters_error_length = 0x04;

- [ConsiderationConstants.sol#L716](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0//contracts/lib/ConsiderationConstants.sol#L716)
uint256 constant BadReturnValueFromERC20OnTransfer_error_selector = 0x98891923;

- [ConsiderationConstants.sol#L717](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0//contracts/lib/ConsiderationConstants.sol#L717)
uint256 constant BadReturnValueFromERC20OnTransfer_error_token_ptr = 0x20;

- [ConsiderationConstants.sol#L718](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0//contracts/lib/ConsiderationConstants.sol#L718)
uint256 constant BadReturnValueFromERC20OnTransfer_error_from_ptr = 0x40;

- [ConsiderationConstants.sol#L719](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0//contracts/lib/ConsiderationConstants.sol#L719)
uint256 constant BadReturnValueFromERC20OnTransfer_error_to_ptr = 0x60;

- [ConsiderationConstants.sol#L720](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0//contracts/lib/ConsiderationConstants.sol#L720)
uint256 constant BadReturnValueFromERC20OnTransfer_error_amount_ptr = 0x80;

- [ConsiderationConstants.sol#L721](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0//contracts/lib/ConsiderationConstants.sol#L721)
uint256 constant BadReturnValueFromERC20OnTransfer_error_length = 0x84;

- [ConsiderationConstants.sol#L731](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0//contracts/lib/ConsiderationConstants.sol#L731)
uint256 constant NoContract_error_selector = 0x5f15d672;

- [ConsiderationConstants.sol#L732](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0//contracts/lib/ConsiderationConstants.sol#L732)
uint256 constant NoContract_error_account_ptr = 0x20;

- [ConsiderationConstants.sol#L733](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0//contracts/lib/ConsiderationConstants.sol#L733)
uint256 constant NoContract_error_length = 0x24;

- [ConsiderationConstants.sol#L742](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0//contracts/lib/ConsiderationConstants.sol#L742)
uint256 constant Invalid1155BatchTransferEncoding_error_selector = 0xeba2084c;

- [ConsiderationConstants.sol#L743](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0//contracts/lib/ConsiderationConstants.sol#L743)
uint256 constant Invalid1155BatchTransferEncoding_error_length = 0x04;

- [ConsiderationConstants.sol#L752](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0//contracts/lib/ConsiderationConstants.sol#L752)
uint256 constant NoReentrantCalls_error_selector = 0x7fa8a987;

- [ConsiderationConstants.sol#L753](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0//contracts/lib/ConsiderationConstants.sol#L753)
uint256 constant NoReentrantCalls_error_length = 0x04;

- [ConsiderationConstants.sol#L763](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0//contracts/lib/ConsiderationConstants.sol#L763)
uint256 constant OrderAlreadyFilled_error_selector = 0x10fda3e1;

- [ConsiderationConstants.sol#L764](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0//contracts/lib/ConsiderationConstants.sol#L764)
uint256 constant OrderAlreadyFilled_error_orderHash_ptr = 0x20;

- [ConsiderationConstants.sol#L765](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0//contracts/lib/ConsiderationConstants.sol#L765)
uint256 constant OrderAlreadyFilled_error_length = 0x24;

- [ConsiderationConstants.sol#L776](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0//contracts/lib/ConsiderationConstants.sol#L776)
uint256 constant InvalidTime_error_selector = 0x21ccfeb7;

- [ConsiderationConstants.sol#L777](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0//contracts/lib/ConsiderationConstants.sol#L777)
uint256 constant InvalidTime_error_startTime_ptr = 0x20;

- [ConsiderationConstants.sol#L778](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0//contracts/lib/ConsiderationConstants.sol#L778)
uint256 constant InvalidTime_error_endTime_ptr = 0x40;

- [ConsiderationConstants.sol#L779](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0//contracts/lib/ConsiderationConstants.sol#L779)
uint256 constant InvalidTime_error_length = 0x44;

- [ConsiderationConstants.sol#L790](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0//contracts/lib/ConsiderationConstants.sol#L790)
uint256 constant InvalidConduit_error_selector = 0x1cf99b26;

- [ConsiderationConstants.sol#L791](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0//contracts/lib/ConsiderationConstants.sol#L791)
uint256 constant InvalidConduit_error_conduitKey_ptr = 0x20;

- [ConsiderationConstants.sol#L792](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0//contracts/lib/ConsiderationConstants.sol#L792)
uint256 constant InvalidConduit_error_conduit_ptr = 0x40;

- [ConsiderationConstants.sol#L793](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0//contracts/lib/ConsiderationConstants.sol#L793)
uint256 constant InvalidConduit_error_length = 0x44;

- [ConsiderationConstants.sol#L802](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0//contracts/lib/ConsiderationConstants.sol#L802)
uint256 constant MissingOriginalConsiderationItems_error_selector = 0x466aa616;

- [ConsiderationConstants.sol#L803](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0//contracts/lib/ConsiderationConstants.sol#L803)
uint256 constant MissingOriginalConsiderationItems_error_length = 0x04;

- [ConsiderationConstants.sol#L813](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0//contracts/lib/ConsiderationConstants.sol#L813)
uint256 constant InvalidCallToConduit_error_selector = 0xd13d53d4;

- [ConsiderationConstants.sol#L814](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0//contracts/lib/ConsiderationConstants.sol#L814)
uint256 constant InvalidCallToConduit_error_conduit_ptr = 0x20;

- [ConsiderationConstants.sol#L815](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0//contracts/lib/ConsiderationConstants.sol#L815)
uint256 constant InvalidCallToConduit_error_length = 0x24;

- [ConsiderationConstants.sol#L827](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0//contracts/lib/ConsiderationConstants.sol#L827)
uint256 constant ConsiderationNotMet_error_selector = 0xa5f54208;

- [ConsiderationConstants.sol#L828](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0//contracts/lib/ConsiderationConstants.sol#L828)
uint256 constant ConsiderationNotMet_error_orderIndex_ptr = 0x20;

- [ConsiderationConstants.sol#L829](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0//contracts/lib/ConsiderationConstants.sol#L829)
uint256 constant ConsiderationNotMet_error_considerationIndex_ptr = 0x40;

- [ConsiderationConstants.sol#L830](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0//contracts/lib/ConsiderationConstants.sol#L830)
uint256 constant ConsiderationNotMet_error_shortfallAmount_ptr = 0x60;

- [ConsiderationConstants.sol#L831](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0//contracts/lib/ConsiderationConstants.sol#L831)
uint256 constant ConsiderationNotMet_error_length = 0x64;

- [ConsiderationConstants.sol#L840](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0//contracts/lib/ConsiderationConstants.sol#L840)
uint256 constant InsufficientEtherSupplied_error_selector = 0x1a783b8d;

- [ConsiderationConstants.sol#L841](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0//contracts/lib/ConsiderationConstants.sol#L841)
uint256 constant InsufficientEtherSupplied_error_length = 0x04;

- [ConsiderationConstants.sol#L852](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0//contracts/lib/ConsiderationConstants.sol#L852)
uint256 constant EtherTransferGenericFailure_error_selector = 0x470c7c1d;

- [ConsiderationConstants.sol#L853](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0//contracts/lib/ConsiderationConstants.sol#L853)
uint256 constant EtherTransferGenericFailure_error_account_ptr = 0x20;

- [ConsiderationConstants.sol#L854](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0//contracts/lib/ConsiderationConstants.sol#L854)
uint256 constant EtherTransferGenericFailure_error_amount_ptr = 0x40;

- [ConsiderationConstants.sol#L855](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0//contracts/lib/ConsiderationConstants.sol#L855)
uint256 constant EtherTransferGenericFailure_error_length = 0x44;

- [ConsiderationConstants.sol#L864](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0//contracts/lib/ConsiderationConstants.sol#L864)
uint256 constant PartialFillsNotEnabledForOrder_error_selector = 0xa11b63ff;

- [ConsiderationConstants.sol#L865](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0//contracts/lib/ConsiderationConstants.sol#L865)
uint256 constant PartialFillsNotEnabledForOrder_error_length = 0x04;

- [ConsiderationConstants.sol#L875](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0//contracts/lib/ConsiderationConstants.sol#L875)
uint256 constant OrderIsCancelled_error_selector = 0x1a515574;

- [ConsiderationConstants.sol#L876](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0//contracts/lib/ConsiderationConstants.sol#L876)
uint256 constant OrderIsCancelled_error_orderHash_ptr = 0x20;

- [ConsiderationConstants.sol#L877](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0//contracts/lib/ConsiderationConstants.sol#L877)
uint256 constant OrderIsCancelled_error_length = 0x24;

- [ConsiderationConstants.sol#L887](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0//contracts/lib/ConsiderationConstants.sol#L887)
uint256 constant OrderPartiallyFilled_error_selector = 0xee9e0e63;

- [ConsiderationConstants.sol#L888](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0//contracts/lib/ConsiderationConstants.sol#L888)
uint256 constant OrderPartiallyFilled_error_orderHash_ptr = 0x20;

- [ConsiderationConstants.sol#L889](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0//contracts/lib/ConsiderationConstants.sol#L889)
uint256 constant OrderPartiallyFilled_error_length = 0x24;

- [ConsiderationConstants.sol#L898](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0//contracts/lib/ConsiderationConstants.sol#L898)
uint256 constant CannotCancelOrder_error_selector = 0xfed398fc;

- [ConsiderationConstants.sol#L899](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0//contracts/lib/ConsiderationConstants.sol#L899)
uint256 constant CannotCancelOrder_error_length = 0x04;

- [ConsiderationConstants.sol#L908](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0//contracts/lib/ConsiderationConstants.sol#L908)
uint256 constant BadFraction_error_selector = 0x5a052b32;

- [ConsiderationConstants.sol#L909](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0//contracts/lib/ConsiderationConstants.sol#L909)
uint256 constant BadFraction_error_length = 0x04;

- [ConsiderationConstants.sol#L919](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0//contracts/lib/ConsiderationConstants.sol#L919)
uint256 constant InvalidMsgValue_error_selector = 0xa61be9f0;

- [ConsiderationConstants.sol#L920](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0//contracts/lib/ConsiderationConstants.sol#L920)
uint256 constant InvalidMsgValue_error_value_ptr = 0x20;

- [ConsiderationConstants.sol#L921](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0//contracts/lib/ConsiderationConstants.sol#L921)
uint256 constant InvalidMsgValue_error_length = 0x24;

- [ConsiderationConstants.sol#L930](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0//contracts/lib/ConsiderationConstants.sol#L930)
uint256 constant InvalidBasicOrderParameterEncoding_error_selector = 0x39f3e3fd;

- [ConsiderationConstants.sol#L931](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0//contracts/lib/ConsiderationConstants.sol#L931)
uint256 constant InvalidBasicOrderParameterEncoding_error_length = 0x04;

- [ConsiderationConstants.sol#L940](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0//contracts/lib/ConsiderationConstants.sol#L940)
uint256 constant NoSpecifiedOrdersAvailable_error_selector = 0xd5da9a1b;

- [ConsiderationConstants.sol#L941](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0//contracts/lib/ConsiderationConstants.sol#L941)
uint256 constant NoSpecifiedOrdersAvailable_error_length = 0x04;

- [ConsiderationConstants.sol#L950](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0//contracts/lib/ConsiderationConstants.sol#L950)
uint256 constant InvalidNativeOfferItem_error_selector = 0x12d3f5a3;

- [ConsiderationConstants.sol#L951](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0//contracts/lib/ConsiderationConstants.sol#L951)
uint256 constant InvalidNativeOfferItem_error_length = 0x04;

- [ConsiderationConstants.sol#L960](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0//contracts/lib/ConsiderationConstants.sol#L960)
uint256 constant ConsiderationLengthNotEqualToTotalOriginal_error_selector = (

- [ConsiderationConstants.sol#L963](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0//contracts/lib/ConsiderationConstants.sol#L963)
uint256 constant ConsiderationLengthNotEqualToTotalOriginal_error_length = 0x04;

- [ConsiderationConstants.sol#L973](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0//contracts/lib/ConsiderationConstants.sol#L973)
uint256 constant Panic_error_selector = 0x4e487b71;

- [ConsiderationConstants.sol#L974](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0//contracts/lib/ConsiderationConstants.sol#L974)
uint256 constant Panic_error_code_ptr = 0x20;

- [ConsiderationConstants.sol#L975](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0//contracts/lib/ConsiderationConstants.sol#L975)
uint256 constant Panic_error_length = 0x24;

- [ConsiderationConstants.sol#L987](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0//contracts/lib/ConsiderationConstants.sol#L987)
uint256 constant generateOrder_selector = 0x98919765;

- [ConsiderationConstants.sol#L988](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0//contracts/lib/ConsiderationConstants.sol#L988)
uint256 constant generateOrder_selector_offset = 0x1c;

- [ConsiderationConstants.sol#L989](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0//contracts/lib/ConsiderationConstants.sol#L989)
uint256 constant generateOrder_head_offset = 0x04;

- [ConsiderationConstants.sol#L990](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0//contracts/lib/ConsiderationConstants.sol#L990)
uint256 constant generateOrder_minimumReceived_head_offset = 0x20;

- [ConsiderationConstants.sol#L991](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0//contracts/lib/ConsiderationConstants.sol#L991)
uint256 constant generateOrder_maximumSpent_head_offset = 0x40;

- [ConsiderationConstants.sol#L992](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0//contracts/lib/ConsiderationConstants.sol#L992)
uint256 constant generateOrder_context_head_offset = 0x60;

- [ConsiderationConstants.sol#L993](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0//contracts/lib/ConsiderationConstants.sol#L993)
uint256 constant generateOrder_base_tail_offset = 0x80;

- [ConsiderationConstants.sol#L995](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0//contracts/lib/ConsiderationConstants.sol#L995)
uint256 constant ratifyOrder_selector = 0xf4dd92ce;

- [ConsiderationConstants.sol#L996](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0//contracts/lib/ConsiderationConstants.sol#L996)
uint256 constant ratifyOrder_selector_offset = 0x1c;

- [ConsiderationConstants.sol#L997](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0//contracts/lib/ConsiderationConstants.sol#L997)
uint256 constant ratifyOrder_head_offset = 0x04;

- [ConsiderationConstants.sol#L998](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0//contracts/lib/ConsiderationConstants.sol#L998)
uint256 constant ratifyOrder_offer_head_offset = 0x00;

- [ConsiderationConstants.sol#L999](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0//contracts/lib/ConsiderationConstants.sol#L999)
uint256 constant ratifyOrder_consideration_head_offset = 0x20;

- [ConsiderationConstants.sol#L1000](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0//contracts/lib/ConsiderationConstants.sol#L1000)
uint256 constant ratifyOrder_context_head_offset = 0x40;

- [ConsiderationConstants.sol#L1001](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0//contracts/lib/ConsiderationConstants.sol#L1001)
uint256 constant ratifyOrder_orderHashes_head_offset = 0x60;

- [ConsiderationConstants.sol#L1002](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0//contracts/lib/ConsiderationConstants.sol#L1002)
uint256 constant ratifyOrder_contractNonce_offset = 0x80;

- [ConsiderationConstants.sol#L1003](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0//contracts/lib/ConsiderationConstants.sol#L1003)
uint256 constant ratifyOrder_base_tail_offset = 0xa0;

- [ConsiderationConstants.sol#L1005](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0//contracts/lib/ConsiderationConstants.sol#L1005)
uint256 constant validateOrder_selector = 0x17b1f942;

- [ConsiderationConstants.sol#L1006](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0//contracts/lib/ConsiderationConstants.sol#L1006)
uint256 constant validateOrder_selector_offset = 0x1c;

- [ConsiderationConstants.sol#L1007](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0//contracts/lib/ConsiderationConstants.sol#L1007)
uint256 constant validateOrder_head_offset = 0x04;

- [ConsiderationConstants.sol#L1008](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0//contracts/lib/ConsiderationConstants.sol#L1008)
uint256 constant validateOrder_zoneParameters_offset = 0x20;

- [ConsiderationConstants.sol#L1010](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0//contracts/lib/ConsiderationConstants.sol#L1010)
uint256 constant ZoneParameters_orderHash_offset = 0x00;

- [ConsiderationConstants.sol#L1011](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0//contracts/lib/ConsiderationConstants.sol#L1011)
uint256 constant ZoneParameters_fulfiller_offset = 0x20;

- [ConsiderationConstants.sol#L1012](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0//contracts/lib/ConsiderationConstants.sol#L1012)
uint256 constant ZoneParameters_offerer_offset = 0x40;

- [ConsiderationConstants.sol#L1013](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0//contracts/lib/ConsiderationConstants.sol#L1013)
uint256 constant ZoneParameters_offer_head_offset = 0x60;

- [ConsiderationConstants.sol#L1014](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0//contracts/lib/ConsiderationConstants.sol#L1014)
uint256 constant ZoneParameters_consideration_head_offset = 0x80;

- [ConsiderationConstants.sol#L1015](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0//contracts/lib/ConsiderationConstants.sol#L1015)
uint256 constant ZoneParameters_extraData_head_offset = 0xa0;

- [ConsiderationConstants.sol#L1016](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0//contracts/lib/ConsiderationConstants.sol#L1016)
uint256 constant ZoneParameters_orderHashes_head_offset = 0xc0;

- [ConsiderationConstants.sol#L1017](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0//contracts/lib/ConsiderationConstants.sol#L1017)
uint256 constant ZoneParameters_startTime_offset = 0xe0;

- [ConsiderationConstants.sol#L1018](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0//contracts/lib/ConsiderationConstants.sol#L1018)
uint256 constant ZoneParameters_endTime_offset = 0x100;

- [ConsiderationConstants.sol#L1019](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0//contracts/lib/ConsiderationConstants.sol#L1019)
uint256 constant ZoneParameters_zoneHash_offset = 0x120;

- [ConsiderationConstants.sol#L1020](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0//contracts/lib/ConsiderationConstants.sol#L1020)
uint256 constant ZoneParameters_base_tail_offset = 0x140;

- [ConsiderationConstants.sol#L1021](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0//contracts/lib/ConsiderationConstants.sol#L1021)
uint256 constant ZoneParameters_selectorAndPointer_length = 0x24;

- [ConsiderationConstants.sol#L1022](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0//contracts/lib/ConsiderationConstants.sol#L1022)
uint256 constant ZoneParameters_basicOrderFixedElements_length = 0x64;

- [ConsiderationConstants.sol#L1025](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0//contracts/lib/ConsiderationConstants.sol#L1025)
uint256 constant BasicOrderParameters_head_size = 0x0240;

- [ConsiderationConstants.sol#L1026](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0//contracts/lib/ConsiderationConstants.sol#L1026)
uint256 constant BasicOrderParameters_fixed_segment_0 = 0x0200;

- [ConsiderationConstants.sol#L1027](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0//contracts/lib/ConsiderationConstants.sol#L1027)
uint256 constant BasicOrderParameters_additionalRecipients_offset = 0x0200;

- [ConsiderationConstants.sol#L1028](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0//contracts/lib/ConsiderationConstants.sol#L1028)
uint256 constant BasicOrderParameters_signature_offset = 0x0220;

- [ConsiderationConstants.sol#L1030](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0//contracts/lib/ConsiderationConstants.sol#L1030)
uint256 constant OrderParameters_head_size = 0x0160;

- [ConsiderationConstants.sol#L1031](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0//contracts/lib/ConsiderationConstants.sol#L1031)
uint256 constant OrderParameters_totalOriginalConsiderationItems_offset = (

- [ConsiderationConstants.sol#L1034](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0//contracts/lib/ConsiderationConstants.sol#L1034)
uint256 constant AdvancedOrderPlusOrderParameters_head_size = 0x0200;

- [ConsiderationConstants.sol#L1036](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0//contracts/lib/ConsiderationConstants.sol#L1036)
uint256 constant Order_signature_offset = 0x20;

- [ConsiderationConstants.sol#L1037](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0//contracts/lib/ConsiderationConstants.sol#L1037)
uint256 constant Order_head_size = 0x40;

- [ConsiderationConstants.sol#L1039](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0//contracts/lib/ConsiderationConstants.sol#L1039)
uint256 constant AdvancedOrder_fixed_segment_0 = 0x40;

- [ConsiderationConstants.sol#L1041](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0//contracts/lib/ConsiderationConstants.sol#L1041)
uint256 constant CriteriaResolver_head_size = 0xa0;

- [ConsiderationConstants.sol#L1042](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0//contracts/lib/ConsiderationConstants.sol#L1042)
uint256 constant CriteriaResolver_fixed_segment_0 = 0x80;

- [ConsiderationConstants.sol#L1043](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0//contracts/lib/ConsiderationConstants.sol#L1043)
uint256 constant CriteriaResolver_criteriaProof_offset = 0x80;

- [ConsiderationConstants.sol#L1045](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0//contracts/lib/ConsiderationConstants.sol#L1045)
uint256 constant FulfillmentComponent_mem_tail_size = 0x40;

- [ConsiderationConstants.sol#L1046](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0//contracts/lib/ConsiderationConstants.sol#L1046)
uint256 constant FulfillmentComponent_mem_tail_size_shift = 6;

- [ConsiderationConstants.sol#L1047](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0//contracts/lib/ConsiderationConstants.sol#L1047)
uint256 constant Fulfillment_head_size = 0x40;

- [ConsiderationConstants.sol#L1048](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0//contracts/lib/ConsiderationConstants.sol#L1048)
uint256 constant Fulfillment_considerationComponents_offset = 0x20;

- [ConsiderationConstants.sol#L1050](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0//contracts/lib/ConsiderationConstants.sol#L1050)
uint256 constant OrderComponents_OrderParameters_common_head_size = 0x0140;

- [TypehashDirectory.sol#L14](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0//contracts/lib/TypehashDirectory.sol#L14)
    bytes3 internal constant twoSubstring = 0x5B325D;

- [TypehashDirectory.sol#L15](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0//contracts/lib/TypehashDirectory.sol#L15)
    uint256 internal constant twoSubstringLength = 3;

- [TypehashDirectory.sol#L18](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0//contracts/lib/TypehashDirectory.sol#L18)
    uint256 internal constant MaxTreeHeight = 24;

- [TypehashDirectory.sol#L20](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0//contracts/lib/TypehashDirectory.sol#L20)
    uint256 internal constant InvalidOpcode = 0xfe;

- [TypehashDirectory.sol#L21](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0//contracts/lib/TypehashDirectory.sol#L21)
    uint256 internal constant OneWord = 0x20;

- [TypehashDirectory.sol#L22](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0//contracts/lib/TypehashDirectory.sol#L22)
    uint256 internal constant OneWordShift = 5;

- [TypehashDirectory.sol#L23](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0//contracts/lib/TypehashDirectory.sol#L23)
    uint256 internal constant AlmostOneWord = 0x1f;

- [TypehashDirectory.sol#L24](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0//contracts/lib/TypehashDirectory.sol#L24)
    uint256 internal constant FreeMemoryPointerSlot = 0x40;

- [TokenTransferrerConstants.sol#L36](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0//contracts/lib/TokenTransferrerConstants.sol#L36)
uint256 constant AlmostOneWord = 0x1f;

- [TokenTransferrerConstants.sol#L37](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0//contracts/lib/TokenTransferrerConstants.sol#L37)
uint256 constant OneWord = 0x20;

- [TokenTransferrerConstants.sol#L38](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0//contracts/lib/TokenTransferrerConstants.sol#L38)
uint256 constant TwoWords = 0x40;

- [TokenTransferrerConstants.sol#L39](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0//contracts/lib/TokenTransferrerConstants.sol#L39)
uint256 constant ThreeWords = 0x60;

- [TokenTransferrerConstants.sol#L41](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0//contracts/lib/TokenTransferrerConstants.sol#L41)
uint256 constant OneWordShift = 5;

- [TokenTransferrerConstants.sol#L42](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0//contracts/lib/TokenTransferrerConstants.sol#L42)
uint256 constant TwoWordsShift = 6;

- [TokenTransferrerConstants.sol#L44](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0//contracts/lib/TokenTransferrerConstants.sol#L44)
uint256 constant FreeMemoryPointerSlot = 0x40;

- [TokenTransferrerConstants.sol#L45](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0//contracts/lib/TokenTransferrerConstants.sol#L45)
uint256 constant ZeroSlot = 0x60;

- [TokenTransferrerConstants.sol#L46](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0//contracts/lib/TokenTransferrerConstants.sol#L46)
uint256 constant DefaultFreeMemoryPointer = 0x80;

- [TokenTransferrerConstants.sol#L48](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0//contracts/lib/TokenTransferrerConstants.sol#L48)
uint256 constant Slot0x80 = 0x80;

- [TokenTransferrerConstants.sol#L49](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0//contracts/lib/TokenTransferrerConstants.sol#L49)
uint256 constant Slot0xA0 = 0xa0;

- [TokenTransferrerConstants.sol#L50](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0//contracts/lib/TokenTransferrerConstants.sol#L50)
uint256 constant Slot0xC0 = 0xc0;

- [TokenTransferrerConstants.sol#L52](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0//contracts/lib/TokenTransferrerConstants.sol#L52)
uint256 constant Generic_error_selector_offset = 0x1c;

- [TokenTransferrerConstants.sol#L55](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0//contracts/lib/TokenTransferrerConstants.sol#L55)
uint256 constant ERC20_transferFrom_signature = (

- [TokenTransferrerConstants.sol#L58](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0//contracts/lib/TokenTransferrerConstants.sol#L58)
uint256 constant ERC20_transferFrom_sig_ptr = 0x0;

- [TokenTransferrerConstants.sol#L59](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0//contracts/lib/TokenTransferrerConstants.sol#L59)
uint256 constant ERC20_transferFrom_from_ptr = 0x04;

- [TokenTransferrerConstants.sol#L60](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0//contracts/lib/TokenTransferrerConstants.sol#L60)
uint256 constant ERC20_transferFrom_to_ptr = 0x24;

- [TokenTransferrerConstants.sol#L61](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0//contracts/lib/TokenTransferrerConstants.sol#L61)
uint256 constant ERC20_transferFrom_amount_ptr = 0x44;

- [TokenTransferrerConstants.sol#L62](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0//contracts/lib/TokenTransferrerConstants.sol#L62)
uint256 constant ERC20_transferFrom_length = 0x64; // 4 + 32 * 3 == 100

- [TokenTransferrerConstants.sol#L67](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0//contracts/lib/TokenTransferrerConstants.sol#L67)
uint256 constant ERC1155_safeTransferFrom_signature = (

- [TokenTransferrerConstants.sol#L70](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0//contracts/lib/TokenTransferrerConstants.sol#L70)
uint256 constant ERC1155_safeTransferFrom_sig_ptr = 0x0;

- [TokenTransferrerConstants.sol#L71](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0//contracts/lib/TokenTransferrerConstants.sol#L71)
uint256 constant ERC1155_safeTransferFrom_from_ptr = 0x04;

- [TokenTransferrerConstants.sol#L72](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0//contracts/lib/TokenTransferrerConstants.sol#L72)
uint256 constant ERC1155_safeTransferFrom_to_ptr = 0x24;

- [TokenTransferrerConstants.sol#L73](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0//contracts/lib/TokenTransferrerConstants.sol#L73)
uint256 constant ERC1155_safeTransferFrom_id_ptr = 0x44;

- [TokenTransferrerConstants.sol#L74](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0//contracts/lib/TokenTransferrerConstants.sol#L74)
uint256 constant ERC1155_safeTransferFrom_amount_ptr = 0x64;

- [TokenTransferrerConstants.sol#L75](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0//contracts/lib/TokenTransferrerConstants.sol#L75)
uint256 constant ERC1155_safeTransferFrom_data_offset_ptr = 0x84;

- [TokenTransferrerConstants.sol#L76](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0//contracts/lib/TokenTransferrerConstants.sol#L76)
uint256 constant ERC1155_safeTransferFrom_data_length_ptr = 0xa4;

- [TokenTransferrerConstants.sol#L77](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0//contracts/lib/TokenTransferrerConstants.sol#L77)
uint256 constant ERC1155_safeTransferFrom_length = 0xc4; // 4 + 32 * 6 == 196

- [TokenTransferrerConstants.sol#L78](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0//contracts/lib/TokenTransferrerConstants.sol#L78)
uint256 constant ERC1155_safeTransferFrom_data_length_offset = 0xa0;

- [TokenTransferrerConstants.sol#L83](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0//contracts/lib/TokenTransferrerConstants.sol#L83)
uint256 constant ERC1155_safeBatchTransferFrom_signature = (

- [TokenTransferrerConstants.sol#L87](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0//contracts/lib/TokenTransferrerConstants.sol#L87)
bytes4 constant ERC1155_safeBatchTransferFrom_selector = bytes4(

- [TokenTransferrerConstants.sol#L91](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0//contracts/lib/TokenTransferrerConstants.sol#L91)
uint256 constant ERC721_transferFrom_signature = ERC20_transferFrom_signature;

- [TokenTransferrerConstants.sol#L92](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0//contracts/lib/TokenTransferrerConstants.sol#L92)
uint256 constant ERC721_transferFrom_sig_ptr = 0x0;

- [TokenTransferrerConstants.sol#L93](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0//contracts/lib/TokenTransferrerConstants.sol#L93)
uint256 constant ERC721_transferFrom_from_ptr = 0x04;

- [TokenTransferrerConstants.sol#L94](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0//contracts/lib/TokenTransferrerConstants.sol#L94)
uint256 constant ERC721_transferFrom_to_ptr = 0x24;

- [TokenTransferrerConstants.sol#L95](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0//contracts/lib/TokenTransferrerConstants.sol#L95)
uint256 constant ERC721_transferFrom_id_ptr = 0x44;

- [TokenTransferrerConstants.sol#L96](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0//contracts/lib/TokenTransferrerConstants.sol#L96)
uint256 constant ERC721_transferFrom_length = 0x64; // 4 + 32 * 3 == 100

- [TokenTransferrerConstants.sol#L106](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0//contracts/lib/TokenTransferrerConstants.sol#L106)
uint256 constant NoContract_error_selector = 0x5f15d672;

- [TokenTransferrerConstants.sol#L107](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0//contracts/lib/TokenTransferrerConstants.sol#L107)
uint256 constant NoContract_error_account_ptr = 0x20;

- [TokenTransferrerConstants.sol#L108](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0//contracts/lib/TokenTransferrerConstants.sol#L108)
uint256 constant NoContract_error_length = 0x24;

- [TokenTransferrerConstants.sol#L122](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0//contracts/lib/TokenTransferrerConstants.sol#L122)
uint256 constant TokenTransferGenericFailure_error_selector = 0xf486bc87;

- [TokenTransferrerConstants.sol#L123](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0//contracts/lib/TokenTransferrerConstants.sol#L123)
uint256 constant TokenTransferGenericFailure_error_token_ptr = 0x20;

- [TokenTransferrerConstants.sol#L124](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0//contracts/lib/TokenTransferrerConstants.sol#L124)
uint256 constant TokenTransferGenericFailure_error_from_ptr = 0x40;

- [TokenTransferrerConstants.sol#L125](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0//contracts/lib/TokenTransferrerConstants.sol#L125)
uint256 constant TokenTransferGenericFailure_error_to_ptr = 0x60;

- [TokenTransferrerConstants.sol#L126](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0//contracts/lib/TokenTransferrerConstants.sol#L126)
uint256 constant TokenTransferGenericFailure_error_identifier_ptr = 0x80;

- [TokenTransferrerConstants.sol#L127](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0//contracts/lib/TokenTransferrerConstants.sol#L127)
uint256 constant TokenTransferGenericFailure_err_identifier_ptr = 0x80;

- [TokenTransferrerConstants.sol#L128](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0//contracts/lib/TokenTransferrerConstants.sol#L128)
uint256 constant TokenTransferGenericFailure_error_amount_ptr = 0xa0;

- [TokenTransferrerConstants.sol#L129](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0//contracts/lib/TokenTransferrerConstants.sol#L129)
uint256 constant TokenTransferGenericFailure_error_length = 0xa4;

- [TokenTransferrerConstants.sol#L131](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0//contracts/lib/TokenTransferrerConstants.sol#L131)
uint256 constant ExtraGasBuffer = 0x20;

- [TokenTransferrerConstants.sol#L132](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0//contracts/lib/TokenTransferrerConstants.sol#L132)
uint256 constant CostPerWord = 3;

- [TokenTransferrerConstants.sol#L133](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0//contracts/lib/TokenTransferrerConstants.sol#L133)
uint256 constant MemoryExpansionCoefficientShift = 9;

- [TokenTransferrerConstants.sol#L137](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0//contracts/lib/TokenTransferrerConstants.sol#L137)
uint256 constant BatchTransfer1155Params_ptr = 0x24;

- [TokenTransferrerConstants.sol#L138](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0//contracts/lib/TokenTransferrerConstants.sol#L138)
uint256 constant BatchTransfer1155Params_ids_head_ptr = 0x64;

- [TokenTransferrerConstants.sol#L139](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0//contracts/lib/TokenTransferrerConstants.sol#L139)
uint256 constant BatchTransfer1155Params_amounts_head_ptr = 0x84;

- [TokenTransferrerConstants.sol#L140](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0//contracts/lib/TokenTransferrerConstants.sol#L140)
uint256 constant BatchTransfer1155Params_data_head_ptr = 0xa4;

- [TokenTransferrerConstants.sol#L141](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0//contracts/lib/TokenTransferrerConstants.sol#L141)
uint256 constant BatchTransfer1155Params_data_length_basePtr = 0xc4;

- [TokenTransferrerConstants.sol#L142](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0//contracts/lib/TokenTransferrerConstants.sol#L142)
uint256 constant BatchTransfer1155Params_calldata_baseSize = 0xc4;

- [TokenTransferrerConstants.sol#L144](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0//contracts/lib/TokenTransferrerConstants.sol#L144)
uint256 constant BatchTransfer1155Params_ids_length_ptr = 0xc4;

- [TokenTransferrerConstants.sol#L146](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0//contracts/lib/TokenTransferrerConstants.sol#L146)
uint256 constant BatchTransfer1155Params_ids_length_offset = 0xa0;

- [TokenTransferrerConstants.sol#L147](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0//contracts/lib/TokenTransferrerConstants.sol#L147)
uint256 constant BatchTransfer1155Params_amounts_length_baseOffset = 0xc0;

- [TokenTransferrerConstants.sol#L148](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0//contracts/lib/TokenTransferrerConstants.sol#L148)
uint256 constant BatchTransfer1155Params_data_length_baseOffset = 0xe0;

- [TokenTransferrerConstants.sol#L150](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0//contracts/lib/TokenTransferrerConstants.sol#L150)
uint256 constant ConduitBatch1155Transfer_usable_head_size = 0x80;

- [TokenTransferrerConstants.sol#L152](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0//contracts/lib/TokenTransferrerConstants.sol#L152)
uint256 constant ConduitBatch1155Transfer_from_offset = 0x20;

- [TokenTransferrerConstants.sol#L153](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0//contracts/lib/TokenTransferrerConstants.sol#L153)
uint256 constant ConduitBatch1155Transfer_ids_head_offset = 0x60;

- [TokenTransferrerConstants.sol#L154](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0//contracts/lib/TokenTransferrerConstants.sol#L154)
uint256 constant ConduitBatch1155Transfer_amounts_head_offset = 0x80;

- [TokenTransferrerConstants.sol#L155](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0//contracts/lib/TokenTransferrerConstants.sol#L155)
uint256 constant ConduitBatch1155Transfer_ids_length_offset = 0xa0;

- [TokenTransferrerConstants.sol#L156](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0//contracts/lib/TokenTransferrerConstants.sol#L156)
uint256 constant ConduitBatch1155Transfer_amounts_length_baseOffset = 0xc0;

- [TokenTransferrerConstants.sol#L157](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0//contracts/lib/TokenTransferrerConstants.sol#L157)
uint256 constant ConduitBatch1155Transfer_calldata_baseSize = 0xc0;

- [TokenTransferrerConstants.sol#L160](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0//contracts/lib/TokenTransferrerConstants.sol#L160)
uint256 constant ConduitBatchTransfer_amounts_head_offset = 0x80;

- [TokenTransferrerConstants.sol#L162](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0//contracts/lib/TokenTransferrerConstants.sol#L162)
uint256 constant Invalid1155BatchTransferEncoding_ptr = 0x00;

- [TokenTransferrerConstants.sol#L163](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0//contracts/lib/TokenTransferrerConstants.sol#L163)
uint256 constant Invalid1155BatchTransferEncoding_length = 0x04;

- [TokenTransferrerConstants.sol#L164](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0//contracts/lib/TokenTransferrerConstants.sol#L164)
uint256 constant Invalid1155BatchTransferEncoding_selector = (

- [TokenTransferrerConstants.sol#L168](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0//contracts/lib/TokenTransferrerConstants.sol#L168)
uint256 constant ERC1155BatchTransferGenericFailure_error_signature = (

- [TokenTransferrerConstants.sol#L171](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0//contracts/lib/TokenTransferrerConstants.sol#L171)
uint256 constant ERC1155BatchTransferGenericFailure_token_ptr = 0x04;

- [TokenTransferrerConstants.sol#L172](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0//contracts/lib/TokenTransferrerConstants.sol#L172)
uint256 constant ERC1155BatchTransferGenericFailure_ids_offset = 0xc0;

- [TokenTransferrerConstants.sol#L185](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0//contracts/lib/TokenTransferrerConstants.sol#L185)
uint256 constant BadReturnValueFromERC20OnTransfer_error_selector = 0x98891923;

- [TokenTransferrerConstants.sol#L186](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0//contracts/lib/TokenTransferrerConstants.sol#L186)
uint256 constant BadReturnValueFromERC20OnTransfer_error_token_ptr = 0x20;

- [TokenTransferrerConstants.sol#L187](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0//contracts/lib/TokenTransferrerConstants.sol#L187)
uint256 constant BadReturnValueFromERC20OnTransfer_error_from_ptr = 0x40;

- [TokenTransferrerConstants.sol#L188](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0//contracts/lib/TokenTransferrerConstants.sol#L188)
uint256 constant BadReturnValueFromERC20OnTransfer_error_to_ptr = 0x60;

- [TokenTransferrerConstants.sol#L189](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0//contracts/lib/TokenTransferrerConstants.sol#L189)
uint256 constant BadReturnValueFromERC20OnTransfer_error_amount_ptr = 0x80;

- [TokenTransferrerConstants.sol#L190](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0//contracts/lib/TokenTransferrerConstants.sol#L190)
uint256 constant BadReturnValueFromERC20OnTransfer_error_length = 0x84;

- [ConduitConstants.sol#L5](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0//contracts/conduit/lib/ConduitConstants.sol#L5)
uint256 constant ChannelClosed_error_signature = (

- [ConduitConstants.sol#L8](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0//contracts/conduit/lib/ConduitConstants.sol#L8)
uint256 constant ChannelClosed_error_ptr = 0x00;

- [ConduitConstants.sol#L9](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0//contracts/conduit/lib/ConduitConstants.sol#L9)
uint256 constant ChannelClosed_channel_ptr = 0x4;

- [ConduitConstants.sol#L10](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0//contracts/conduit/lib/ConduitConstants.sol#L10)
uint256 constant ChannelClosed_error_length = 0x24;

- [ConduitConstants.sol#L16](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0//contracts/conduit/lib/ConduitConstants.sol#L16)
uint256 constant ChannelKey_channel_ptr = 0x00;

- [ConduitConstants.sol#L17](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0//contracts/conduit/lib/ConduitConstants.sol#L17)
uint256 constant ChannelKey_slot_ptr = 0x20;

- [ConduitConstants.sol#L18](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0//contracts/conduit/lib/ConduitConstants.sol#L18)
uint256 constant ChannelKey_length = 0x40;






