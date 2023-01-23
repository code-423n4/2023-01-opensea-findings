## Summary

### Non-critical findings

| Issue | Description | Instances |
| -- | ----------- | -------- |
|1| Named return variables are not used when a function returns|1|
|2| Duplicate code|1|
|3| Long indentation within some Natspec statements reduces readability|3 + multiple|
|4| `@param` statements are missing for `structs`|1 + multiple|
|5| Typos|1|
|6| `pragma solidity` version should be upgraded to latest version before finalization|1|
|| Total|8 + multiple|


| No. | Description |
|--| ----------- | 
|1|**Named return variables are not used when a function returns**|
|  |Below, none of the four named return variables is ever used|

[OrderValidator.sol: L828-838](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/lib/OrderValidator.sol#L828-L838)
```solidity
    function _getOrderStatus(
        bytes32 orderHash
    )
        internal
        view
        returns (
            bool isValidated,
            bool isCancelled,
            uint256 totalFilled,
            uint256 totalSize
        )
```
___

| No. | Description |
|--| ----------- | 
|2|**Duplicate code**|
|  |Large sections of identical code are repeated in two different interface contracts, as shown below:|

[ConsiderationInterface: L107-458](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/interfaces/ConsiderationInterface.sol#L107-L458)

is identical to

[SeaportInterface: L106-457](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/interfaces/SeaportInterface.sol#L106-L457)

___

| No. | Description |
|--| ----------- | 
|3|**Long indentation within some Natspec statements reduces readability**|
|  |While the choice of comment spacing is up to the developers, it should be made consistent throughout. Four spaces is a commonly used unit of indentation. However, when `@param`, `@custom:param` or `@return` statements wrap within Opensea Seaport, the indentation after the first line often is very large, as much as 20 spaces.|

Below is an example of the appropriate spacing of `@dev` statements used throughout the contest. `@notice` statements also normally have similar suitable spacing.

[PointerLibraries.sol: L75-77](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/helpers/PointerLibraries.sol#L75-L77)
```solidity
    /// @dev Resolves an offset stored at `cdPtr + headOffset` to a calldata.
    ///      pointer `cdPtr` must point to some parent object with a dynamic
    ///      type's head stored at `cdPtr + headOffset`.
```

On the other hand, as the examples below show, `@param`, `@custom:param` and `@return` statements tend to have extra-wide spacing when they wrap. This should be corrected.

___
[Consideration.sol: L236-240](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/lib/Consideration.sol#L236-L240)
```solidity
     * @custom:param considerationFulfillments An array of FulfillmentComponent
     *                                         arrays indicating which
     *                                         consideration items to attempt to
     *                                         aggregate when preparing
     *                                         executions.
```
___
[Consideration.sol: L373-376](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/lib/Consideration.sol#L373-L376)
```solidity
     * @param recipient                        The intended recipient for all
     *                                         received items, with `address(0)`
     *                                         indicating that the caller should
     *                                         receive the offer items.
```
___
[ConsiderationDecoder.sol: L28-32](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/lib/ConsiderationDecoder.sol#L28-L32)
```solidity
     * @param cdPtrLength A calldata pointer to the start of the bytes array in
     *                    calldata which contains the length of the array.
     *
     * @return mPtrLength A memory pointer to the start of the bytes array in
     *                    memory which contains the length of the array.
```
___

| No. | Description |
|--| ----------- | 
|4|**`@param` statements are missing for `structs`**|
|  |The `structs` in `ConsiderationStructs.sol` are preceded by `@dev` statements with extensive commentary, as shown below. These contain information that could fairly easily be converted into `@param` statements. This would have the advantage of conforming to Natspec guidelines and standardizing the descriptions of the `struct` variables.|


[ConsiderationStructs.sol: L16-38](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/lib/ConsiderationStructs.sol#L16-L38)
```solidity
/**
 * @dev An order contains eleven components: an offerer, a zone (or account that
 *      can cancel the order or restrict who can fulfill the order depending on
 *      the type), the order type (specifying partial fill support as well as
 *      restricted order status), the start and end time, a hash that will be
 *      provided to the zone when validating restricted orders, a salt, a key
 *      corresponding to a given conduit, a counter, and an arbitrary number of
 *      offer items that can be spent along with consideration items that must
 *      be received by their respective recipient.
 */
struct OrderComponents {
    address offerer;
    address zone;
    OfferItem[] offer;
    ConsiderationItem[] consideration;
    OrderType orderType;
    uint256 startTime;
    uint256 endTime;
    bytes32 zoneHash;
    uint256 salt;
    bytes32 conduitKey;
    uint256 counter;
}
```
___

| No. | Description |
|--| ----------- | 
|5|**Typos**|

___
[TypehashDirectory.sol: L31](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/lib/TypehashDirectory.sol#L31)
```solidity
        // Declare an array where each type hash will be writter.
```
Change `writter` to `writer`
___

| No. | Description |
|--| ----------- | 
|6|**`pragma solidity` version should be upgraded to latest version before finalization**|
|  |About 40% of the in-scope contracts use the latest solidity version, `pragma solidity ^0.8.17`. The remainder use `^0.8.13`, as shown below, and should be upgraded before implementation. Only the latest version receives security fixes. |


[ConsiderationEncoder.sol: L2](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/lib/ConsiderationEncoder.sol#L2)
```solidity
pragma solidity ^0.8.13;
```
___
___