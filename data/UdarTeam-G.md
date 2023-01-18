# [G-01] CACHE THE MSG.SENDER WHEN USING MULTIPLE TIMES

https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/conduit/ConduitController.sol#L255

```diff
     function acceptOwnership(address conduit) external override {
         // Ensure that the conduit in question exists.
         _assertConduitExists(conduit);
+        address potentialOwner = msg.sender;
 
         // If caller does not match current potential owner of the conduit...
-        if (msg.sender != _conduits[conduit].potentialOwner) {
+        if (potentialOwner != _conduits[conduit].potentialOwner) {
             // Revert, indicating that caller is not current potential owner.
             revert CallerIsNotNewPotentialOwner(conduit);
         }
@@ -272,11 +273,11 @@ contract ConduitController is ConduitControllerInterface {
         emit OwnershipTransferred(
             conduit,
             _conduits[conduit].owner,
-            msg.sender
+            potentialOwner
         );
 
         // Set the caller as the owner of the conduit.
-        _conduits[conduit].owner = msg.sender;
+        _conduits[conduit].owner = potentialOwner;
     }
```

## Gas report diff running ```forge snapshot -diff .gas-snapshot```

```
...
testFulfillAvailableAdvancedOrdersWithCriteria((uint256[8],uint8)) (gas: 1 (0.000%)) 
testFulfillAdvancedOrderWithCriteriaPreimage((uint256[8],uint8)) (gas: -1 (-0.000%)) 
testNoNativeOffersFulfillAdvanced(uint8[8]) (gas: 20 (0.000%)) 
testRevertUnusedItemParametersIdentifierSetOnNativeConsideration((address,uint256,uint128,bytes32,uint256),uint128,uint256) (gas: 20 (0.001%)) 
testFulfillBasicOrderRevertInvalidAdditionalRecipientsLength(uint256,uint256) (gas: 25 (0.005%)) 
testSignatureVerification() (gas: 9077 (0.006%)) 
testNoNativeOffers(uint8[8]) (gas: 3487 (0.074%)) 
testNoNativeOffersFulfillAvailableAdvanced(uint8[8]) (gas: 7135 (0.103%)) 
testNoNativeOffersFulfillAvailable(uint8[8]) (gas: 7302 (0.106%)) 
testExecuteWithBatch1155(((uint8,address,address,uint128,uint128,uint8)[10],(address,address,(uint256,uint128)[10])[10])) (gas: -66757 (-0.193%)) 
testExecute(((uint8,address,address,uint128,uint128,uint8)[20])) (gas: 60732 (0.234%)) 
testFulfillAdvancedFuzz(uint8) (gas: -85478 (-0.999%)) 
testFulfillOrderEthToErc1155WithErc20Tips((address,uint128,bytes32,uint256,uint128[3],bool,uint120,uint120,uint16),uint256,uint8) (gas: 81208 (1.007%)) 
testFulfillOrderRevertInvalidConsiderationItemsLength(uint256,uint256) (gas: -213279 (-1.497%)) 
testFulfillOrderEthToErc1155WithErc1155Tips((address,uint128,bytes32,uint256,uint128[3],bool,uint120,uint120,uint16),uint256,uint8) (gas: -349303 (-3.201%)) 
testFulfillOrderEthToErc721WithMultipleTips((address,uint128,bytes32,uint256,uint128[3],bool,uint120,uint120,uint16),uint8) (gas: 334766 (4.800%)) 
testBasicStateful(uint8,uint8) (gas: -5315544 (-6.261%)) 
```
```
Overall gas change: -5526589 (-5.814%)
```