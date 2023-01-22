## += and -= cost more gas
`+=` and `-=` generally cost 22 more gas than writing out the assigned equation explicitly. The amount of gas wasted can be quite sizable when repeatedly operated in a loop.

For instance, the `+=` instance below may be refactored as follows:

[File: ConsiderationDecoder.sol#L673](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/lib/ConsiderationDecoder.sol#L673)

```diff
-            for (uint256 offset = 0; offset < tailOffset; offset += OneWord) {
+            for (uint256 offset = 0; offset < tailOffset; offset = offset + OneWord) {
```
Similarly, the `-=` instance below may be refactored as follows:

[File: BasicOrderFulfiller.sol#L965](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/lib/BasicOrderFulfiller.sol#L965)

```diff
-                nativeTokensRemaining -= additionalRecipientAmount;
+                nativeTokensRemaining = nativeTokensRemaining - additionalRecipientAmount;
```
## Use of named returns for local variables saves gas
You can have further advantages in terms of gas cost by simply using named return values as temporary local variable.

For instance, the code block below may be refactored as follows:

[File: BasicOrderFulfiller.sol#L68-L276](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/lib/BasicOrderFulfiller.sol#L68-L276)

```diff
    function _validateAndFulfillBasicOrder(
        BasicOrderParameters calldata parameters
-    ) internal returns (bool) {
+    ) internal returns (bool status_) {

    [ ... ]

-        return true;
+        status_ = true;
    }
```
## Use storage instead of memory for structs/arrays
A storage pointer is cheaper since copying a state struct in memory would incur as many SLOADs and MSTOREs as there are slots. In another words, this causes all fields of the struct/array to be read from storage, incurring a Gcoldsload (2100 gas) for each field of the struct/array, and then further incurring an additional MLOAD rather than a cheap stack read. As such, declaring the variable with the storage keyword and caching any fields that need to be re-read in stack variables will be much cheaper, involving only Gcoldsload for all associated field reads. Read the whole struct/array into a memory variable only when it is being returned by the function, passed into a function that requires memory, or if the array/struct is being read from another memory array/struct.

For instance, the specific instance below may be refactored as follows:

[File: OrderValidator.sol#L118](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/lib/OrderValidator.sol#L118)

```diff
-        OrderParameters memory orderParameters = advancedOrder.parameters;
+        OrderParameters storage orderParameters = advancedOrder.parameters;
```
## ++i costs less gas than i++, especially when it's used in for loops (--i / i-- too)
The post-increment (i++ or i--) operation costs more (about 5 GAS per iteration), because the compiler typically has to create a temporary variable for returning the initial value of i when incrementing/decrementing i . In contrast, the pre-increment  (++i or --i) operation simply returns the actual incremented value of i without the need for a temporary variable.  The saving impact is particularly prominent when dealing with loops.

For instance, the `i--` instance below may be refactored as follows:

[File: OrderCombiner.sol#L272](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/lib/OrderCombiner.sol#L272)

```diff
-                maximumFulfilled--;
+                --maximumFulfilled;
```
## Ternary over `if ... else`
Using ternary operator instead of the if else statement saves gas.

For instance, the specif instance below may be refactored as follows:

[File: OrderCombiner.sol#L322-L332](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/lib/OrderCombiner.sol#L322-L332)

```solidity
 offerItem.startAmount == offerItem.endAmount
     ? offerItem.startAmount = endAmount;
     : offerItem.startAmount = _getFraction(
                            numerator,
                            denominator,
                            offerItem.startAmount
                        );
```