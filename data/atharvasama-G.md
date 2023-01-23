# Gas Optimizations list

| Number | Details                                                                    | Instances |
| ------ | -------------------------------------------------------------------------- | --------- |
| 1      | X += Y costs more gas than X = X + Y. X -= Y costs more gas than X = X - Y | 25        |
| 2      | Can declare the variable outside the loop to save gas                      | 32        |
| 3      | Internal functions only called once can be inlined to save gas             | 9         |
| 4      | Using function instead of modifier                                         | 1         |

# Gas Optimizations
## [G-01] ```x += y``` costs more gas than ```x = x + y```. ```x -= y``` costs more gas than ```x = x - y```
Using the addition operator instead of plus-equals saves gas.
>contracts\lib\BasicOrderFulfiller.sol:  
>```js
>940                  i < totalAdditionalRecipientsDataSize;  
>941:                 i += AdditionalRecipient_size  
>942              ) {  
>
>1111              unchecked {  
>1112:                 i += AdditionalRecipient_size;  
>1113              }  
>
>964                  // subtracted value is confirmed above as less than remaining.
>965:                 nativeTokensRemaining -= additionalRecipientAmount;
>966  
>
>1096              if (fromOfferer) {
>1097:                 amount -= additionalRecipientAmount;
>1098              }
>```
>contracts\lib\ConsiderationDecoder.sol:  
>```js
>398              // Iterate over each pointer, word by word, until tail is reached.  
>399:             for (uint256 offset = 0; offset < tailOffset; offset += OneWord) {  
>400                  // Resolve Order calldata offset, use it to decode and copy from  
>  
>497              // Iterate over each pointer, word by word, until tail is reached.  
>498:             for (uint256 offset = 0; offset < tailOffset; offset += OneWord) {  
>499                  // Resolve CriteriaResolver calldata offset, use it to decode  
>
>537              // Iterate over each pointer, word by word, until tail is reached.  
>538:             for (uint256 offset = 0; offset < tailOffset; offset += OneWord) {  
>539                  // Resolve Order calldata offset, use it to decode and copy  
>
>629              // Iterate over each pointer, word by word, until tail is reached.  
>630:             for (uint256 offset = 0; offset < tailOffset; offset += OneWord) {  
>631                  // Resolve FulfillmentComponents array calldata offset, use it  
>
>672              // Iterate over each pointer, word by word, until tail is reached.  
>673:             for (uint256 offset = 0; offset < tailOffset; offset += OneWord) {  
>674                  // Resolve AdvancedOrder calldata offset, use it to decode and  
>
>743              // Iterate over each pointer, word by word, until tail is reached.
>744:             for (uint256 offset = 0; offset < tailOffset; offset += OneWord) {  
>745                  // Resolve Fulfillment calldata offset, use it to decode and  
>```
>contracts\lib\ConsiderationEncoder.sol:
>```js
>133              // Increment tail offset, now used to populate maximumSpent array.
>134:             tailOffset += minimumReceivedSize;
>135          }
>
>154              // Increment tail offset, now used to populate context array.
>155:             tailOffset += maximumSpentSize;
>156          }
>
>171              // Increment the tail offset, now used to determine final size.
>172:             tailOffset += contextSize;
>173  
>
>239              // Increment tail offset, now used to populate consideration array.
>240:             tailOffset += offerSize;
>241          }
>
>258              // Increment tail offset, now used to populate context array.
>259:             tailOffset += considerationSize;
>260          }
>
>272              // Increment tail offset, now used to populate orderHashes array.
>273:             tailOffset += contextSize;
>274          }
>
>286              // Increment the tail offset, now used to determine final size.
>287:             tailOffset += orderHashesSize;
>288  
>
>378              // Increment tail offset, now used to populate consideration array.
>379:             tailOffset += offerSize;
>380          }
>
>399              // Increment tail offset, now used to populate extraData array.
>400:             tailOffset += considerationSize;
>401          }
>
>412              // Increment tail offset, now used to populate orderHashes array.
>413:             tailOffset += extraDataSize;
>414          }
>
>428              // Increment the tail offset, now used to determine final size.
>429:             tailOffset += orderHashesSize;
>430  
>
>513              // Increment tail offset, now used to populate extraData array.
>514:             tailOffset += offerAndConsiderationSize;
>515          }
>
>522              // Increment tail offset, now used to populate orderHashes array.
>523:             tailOffset += OneWord;
>524          }
>```
>contracts\lib\OrderCombiner.sol:
>```js
>229              // Iterate over each order.
>230:             for (uint256 i = 32; i < terminalMemoryOffset; i += 32) {
>231                  // Retrieve order using assembly to bypass out-of-range check.
>
>450              // Iterate over each order.
>451:             for (uint256 i = 32; i < terminalMemoryOffset; i += 32) {
>452                  assembly {
>```


## [G-02] Can declare the variable outside the loop to save gas
Declaring the loop variable outside is more gas efficient. 
>contracts\conduit\Conduit.sol:
>```js
>98          // Iterate over each transfer.
>99:         for (uint256 i = 0; i < totalStandardTransfers; ) {
>100              // Retrieve the transfer in question and perform the transfer.
>
>161          // Iterate over each standard transfer.
>162:         for (uint256 i = 0; i < totalStandardTransfers; ) {
>163              // Retrieve the transfer in question and perform the transfer.
>```
>contracts\lib\BasicOrderFulfiller.sol:
>```js
>937              // Iterate over additional recipient data by two-word element.
>938:             for (
>939                  uint256 i = 0;
>
>1078          // Iterate over each additional recipient.
>1079:         for (uint256 i = 0; i < totalAdditionalRecipientsDataSize; ) {
>1080              assembly {
>```
>contracts\lib\ConsiderationDecoder.sol:
>```js
>398              // Iterate over each pointer, word by word, until tail is reached.
>399:             for (uint256 offset = 0; offset < tailOffset; offset += OneWord) {
>400                  // Resolve Order calldata offset, use it to decode and copy from
>
>497              // Iterate over each pointer, word by word, until tail is reached.
>498:             for (uint256 offset = 0; offset < tailOffset; offset += OneWord) {
>499                  // Resolve CriteriaResolver calldata offset, use it to decode
>
>537              // Iterate over each pointer, word by word, until tail is reached.
>538:             for (uint256 offset = 0; offset < tailOffset; offset += OneWord) {
>539                  // Resolve Order calldata offset, use it to decode and copy
>
>629              // Iterate over each pointer, word by word, until tail is reached.
>630:             for (uint256 offset = 0; offset < tailOffset; offset += OneWord) {
>631                  // Resolve FulfillmentComponents array calldata offset, use it
>
>672              // Iterate over each pointer, word by word, until tail is reached.
>673:             for (uint256 offset = 0; offset < tailOffset; offset += OneWord) {
>674                  // Resolve AdvancedOrder calldata offset, use it to decode and
>
>743              // Iterate over each pointer, word by word, until tail is reached.
>744:             for (uint256 offset = 0; offset < tailOffset; offset += OneWord) {
>745                  // Resolve Fulfillment calldata offset, use it to decode and
>```
>contracts\lib\CriteriaResolution.sol:
>```js
>56              // Iterate over each criteria resolver.
>57:             for (uint256 i = 0; i < totalCriteriaResolvers; ++i) {
>58                  // Retrieve the criteria resolver.
>
>140              // Iterate over each advanced order.
>141:             for (uint256 i = 0; i < totalAdvancedOrders; ++i) {
>142                  // Retrieve the advanced order.
>
>158                  // Iterate over each consideration item on the order.
>159:                 for (uint256 j = 0; j < totalItems; ++j) {
>160                      // Ensure item type no longer indicates criteria usage.
>
>173                  // Iterate over each offer item on the order.
>174:                 for (uint256 j = 0; j < totalItems; ++j) {
>175                      // Ensure item type no longer indicates criteria usage.
>```
>contracts\lib\OrderCombiner.sol:
>```js
>229              // Iterate over each order.
>230:             for (uint256 i = 32; i < terminalMemoryOffset; i += 32) {
>231                  // Retrieve order using assembly to bypass out-of-range check.
>
>297                  // Iterate over each offer item on the order.
>298:                 for (uint256 j = 0; j < totalOfferItems; ++j) {
>299                      // Retrieve the offer item.
>
>355                  // Iterate over each consideration item on the order.
>356:                 for (uint256 j = 0; j < totalConsiderationItems; ++j) {
>357                      // Retrieve the consideration item.
>
>450              // Iterate over each order.
>451:             for (uint256 i = 32; i < terminalMemoryOffset; i += 32) {
>452                  assembly {
>
>566              // Iterate over each offer fulfillment.
>567:             for (uint256 i = 0; i < totalOfferFulfillments; ) {
>568                  // Derive aggregated execution corresponding with fulfillment.
>
>595              // Iterate over each consideration fulfillment.
>596:             for (uint256 i = 0; i < totalConsiderationFulfillments; ) {
>597                  // Derive aggregated execution corresponding with fulfillment.
>
>697          // Iterate over each execution.
>698:         for (uint256 i = 0; i < totalExecutions; ) {
>699              // Retrieve the execution and the associated received item.
>
>735              // Iterate over orders to ensure all consideration items are met.
>736:             for (uint256 i = 0; i < totalOrders; ++i) {
>737                  // Retrieve the order in question.
>
>761                      // Iterate over each offer item to restore it.
>762:                     for (uint256 j = 0; j < totalOfferItems; ++j) {
>763                          OfferItem memory offerItem = offer[j];
>
>798                      // Iterate over each consideration item to ensure it is met.
>799:                     for (uint256 j = 0; j < totalConsiderationItems; ++j) {
>800                          ConsiderationItem memory considerationItem = (
>
>998              // Iterate over each fulfillment.
>999:             for (uint256 i = 0; i < totalFulfillments; ++i) {
>1000                  /// Retrieve the fulfillment in question.
>```
>contracts\lib\OrderFulfiller.sol:
>```js
>206              // Skip overflow check as for loop is indexed starting at zero.
>207:             for (uint256 i = 0; i < totalOfferItems; ++i) {
>208                  // Retrieve the offer item.
>
>300              // Skip overflow check as for loop is indexed starting at zero.
>301:             for (uint256 i = 0; i < totalConsiderationItems; ++i) {
>302                  // Retrieve the consideration item.
>```
>contracts\lib\OrderValidator.sol:
>```js
>548              // Iterate over each specified offer (e.g. minimumReceived) item.
>549:             for (uint256 i = 0; i < originalOfferLength; ) {
>550                  // Retrieve the pointer to the originally supplied item.
>
>590              // Iterate over returned consideration & do not exceed maximumSpent.
>591:             for (uint256 i = 0; i < newConsiderationLength; ) {
>592                  // Retrieve the pointer to the originally supplied item.
>
>666              // Iterate over each order.
>667:             for (uint256 i = 0; i < totalOrders; ) {
>668                  // Retrieve the order.
>
>752              // Iterate over each order.
>753:             for (uint256 i = 0; i < totalOrders; ++i) {
>754                  // Retrieve the order.
>```
>contracts\lib\TypehashDirectory.sol:
>```js
>47          // Iterate over each tree height.
>48:         for (uint256 i = 0; i < MaxTreeHeight; ) {
>49              // The actual height is one greater than its respective index.
>```

## [G-03] Internal functions only called once can be inlined to save gas
Not inlining costs 20 to 40 gas because of two extra ```JUMP``` instructions and additional stack operations needed for function calls.
>
>contracts\lib\ConsiderationBase.sol`  
>[ConsiderationBase.sol#L180-L268](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/lib/ConsiderationBase.sol#L180-L268)
>```js
>180:     function _deriveTypehashes()
>181:         internal
>182:         pure
>183:         returns (
>184:             bytes32 nameHash,
>185:             bytes32 versionHash,
>186:             bytes32 eip712DomainTypehash,
>187:             bytes32 offerItemTypehash,
>188:             bytes32 considerationItemTypehash,
>189:             bytes32 orderTypehash
>190:         )
>```
>
>contracts\lib\BasicOrderFulfiller.sol`  
>[BasicOrderFulfiller.sol#L1006-L1118](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/lib/BasicOrderFulfiller.sol#L1006-L1118)  
>[BasicOrderFulfiller.sol#L916-L991](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/lib/BasicOrderFulfiller.sol#L916-L991)  
>[BasicOrderFulfiller.sol#L304-903](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/lib/BasicOrderFulfiller.sol#L304-L903)
>```js
>1006:     function _transferERC20AndFinalize(
>1007:         address offerer,
>1008:         BasicOrderParameters calldata parameters,
>1009:         bool fromOfferer,
>1010:         bytes memory accumulator
>1011:     ) internal {
>
>916:     function _transferNativeTokensAndFinalize(
>917:         uint256 amount,
>918:         address payable to
>919:     ) internal {
>
>304:     function _prepareBasicFulfillmentFromCalldata(
>305:         BasicOrderParameters calldata parameters,
>306:         OrderType orderType,
>307:         ItemType receivedItemType,
>308:         ItemType additionalRecipientsItemType,
>309:         address additionalRecipientsToken,
>310:         ItemType offeredItemType
>311:     ) internal returns (bytes32 orderHash) {
>```
>
>contracts\lib\CriteriaResolution.sol`  
>[CriteriaResolution.sol#L193-L235](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/lib/CriteriaResolution.sol#L193-L235)
>```js
>193:     function _updateCriteriaItem(
>194:         OfferItem[] memory offer,
>195:         uint256 componentIndex,
>196:         CriteriaResolver memory criteriaResolver
>197:     ) internal pure {
>```
>
>contracts\lib\OrderCombiner.sol`  
>[OrderCombiner.sol#L867-L892](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/lib/OrderCombiner.sol#L867-L892)
>```js
>867:     function _emitOrdersMatched(bytes32[] memory orderHashes) internal {
>```
>
>contracts\lib\OrderValidator.sol`  
>[OrderValidator.sol#L439-L451](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/lib/OrderValidator.sol#L439-L451)
>```js
>439:     function _checkRecipients(
>440:         address originalRecipient,
>441:         address newRecipient
>442:     ) internal pure returns (uint256 isInvalid) {
>```
>
>contracts\lib\TypehashDirectory.sol`  
>[TypehashDirectory.sol#L131-L182](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/lib/TypehashDirectory.sol#L131-L182)  
>[TypehashDirectory.sol#L99-L123](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/lib/TypehashDirectory.sol#L99-L123)
>```js
>131:     function getTreeSubTypes() internal pure returns (bytes memory) {
>
>099:     function getMaxTreeBrackets(
>100:         uint256 maxHeight
>101:     ) internal pure returns (bytes memory) {
>```

## [G-04] Using function instead of modifier
Since modifier code is inlined, having a function execute the modifier logic reduces the contract size by invoking the function every time the modifier is required. This could save a modest amount of gas during deployment.  

>contracts\conduit\Conduit.sol`
>```js
>40:     modifier onlyOpenChannel() {
>41:         // Utilize assembly to access channel storage mapping directly.
>42:         assembly {
>43:             // Write the caller to scratch space.
>44:             mstore(ChannelKey_channel_ptr, caller())
>45: 
>46:             // Write the storage slot for _channels to scratch space.
>47:             mstore(ChannelKey_slot_ptr, _channels.slot)
>48: 
>49:             // Derive the position in storage of _channels[msg.sender]
>50:             // and check if the stored value is zero.
>51:             if iszero(
>52:                 sload(keccak256(ChannelKey_channel_ptr, ChannelKey_length))
>53:             ) {
>54:                 // The caller is not an open channel; revert with
>55:                 // ChannelClosed(caller). First, set error signature in memory.
>56:                 mstore(ChannelClosed_error_ptr, ChannelClosed_error_signature)
>57: 
>58:                 // Next, set the caller as the argument.
>59:                 mstore(ChannelClosed_channel_ptr, caller())
>60: 
>61:                 // Finally, revert, returning full custom error with argument.
>62:                 revert(ChannelClosed_error_ptr, ChannelClosed_error_length)
>63:             }
>64:         }
>65: 
>66:         // Continue with function execution.
>67:         _;
>68:     }
>```
>The above code can be refactored as follows
>```js
>40:     function isOpenChannel() internal view{
>41:         assembly {
>42:             // Write the caller to scratch space.
>43:             mstore(ChannelKey_channel_ptr, caller())
>44: 
>45:             // Write the storage slot for _channels to scratch space.
>46:             mstore(ChannelKey_slot_ptr, _channels.slot)
>47: 
>48:             // Derive the position in storage of _channels[msg.sender]
>49:             // and check if the stored value is zero.
>50:             if iszero(
>51:                 sload(keccak256(ChannelKey_channel_ptr, ChannelKey_length))
>52:             ) {
>53:                 // The caller is not an open channel; revert with
>54:                 // ChannelClosed(caller). First, set error signature in memory.
>55:                 mstore(ChannelClosed_error_ptr, ChannelClosed_error_signature)
>56: 
>57:                 // Next, set the caller as the argument.
>58:                 mstore(ChannelClosed_channel_ptr, caller())
>59: 
>60:                 // Finally, revert, returning full custom error with argument.
>61:                 revert(ChannelClosed_error_ptr, ChannelClosed_error_length)
>62:             }
>63:         }
>64:     }
>65:     modifier onlyOpenChannel() {
>66:         isOpenChannel();
>67:         // Continue with function execution.
>68:         _;
>69:     }
>```