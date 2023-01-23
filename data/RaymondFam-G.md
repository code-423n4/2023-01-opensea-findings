## Private function with embedded modifier reduces contract size
Consider having the logic of a modifier embedded through a private function to reduce contract size if need be. A private visibility that saves more gas on function calls than the internal visibility is adopted because the modifier will only be making this call inside the contract.

For instance, the modifier instance below may be refactored as follows:

[File: Conduit.sol#L40-L68](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/conduit/Conduit.sol#L40-L68)

```solidity
    function _onlyOpenChannel() private view {
        // Utilize assembly to access channel storage mapping directly.
        assembly {
            // Write the caller to scratch space.
            mstore(ChannelKey_channel_ptr, caller())

            // Write the storage slot for _channels to scratch space.
            mstore(ChannelKey_slot_ptr, _channels.slot)

            // Derive the position in storage of _channels[msg.sender]
            // and check if the stored value is zero.
            if iszero(
                sload(keccak256(ChannelKey_channel_ptr, ChannelKey_length))
            ) {
                // The caller is not an open channel; revert with
                // ChannelClosed(caller). First, set error signature in memory.
                mstore(ChannelClosed_error_ptr, ChannelClosed_error_signature)

                // Next, set the caller as the argument.
                mstore(ChannelClosed_channel_ptr, caller())

                // Finally, revert, returning full custom error with argument.
                revert(ChannelClosed_error_ptr, ChannelClosed_error_length)
            }
        }
    }

    modifier onlyOpenChannel() {
        _onlyOpenChannel();
        _;
    }
```
## Function order affects gas consumption
The order of function will also have an impact on gas consumption. Because in smart contracts, there is a difference in the order of the functions. Each position will have an extra 22 gas. The order is dependent on method ID. So, if you rename the frequently accessed function to more early method ID, you can save gas cost. Please visit the following site for further information:

https://medium.com/joyso/solidity-how-does-function-name-affect-gas-consumption-in-smart-contract-47d270d8ac92

## Activate the optimizer
Before deploying your contract, activate the optimizer when compiling using “solc --optimize --bin sourceFile.sol”. By default, the optimizer will optimize the contract assuming it is called 200 times across its lifetime. If you want the initial contract deployment to be cheaper and the later function executions to be more expensive, set it to “ --optimize-runs=1”. Conversely, if you expect many transactions and do not care for higher deployment cost and output size, set “--optimize-runs” to a high number.

```
module.exports = {
solidity: {
version: "0.8.13",

settings: {
  optimizer: {
    enabled: true,
    runs: 1000,
  },
},
},
};
```
Please visit the following site for further information:

https://docs.soliditylang.org/en/v0.5.4/using-the-compiler.html#using-the-commandline-compiler

Here's one example of instance on opcode comparison that delineates the gas saving mechanism:

```
for !=0 before optimization
PUSH1 0x00
DUP2
EQ
ISZERO
PUSH1 [cont offset]
JUMPI

after optimization
DUP1
PUSH1 [revert offset]
JUMPI
```
Disclaimer: There have been several bugs with security implications related to optimizations. For this reason, Solidity compiler optimizations are disabled by default, and it is unclear how many contracts in the wild actually use them. Therefore, it is unclear how well they are being tested and exercised. High-severity security issues due to optimization bugs have occurred in the past . A high-severity bug in the emscripten -generated solc-js compiler used by Truffle and Remix persisted until late 2018. The fix for this bug was not reported in the Solidity CHANGELOG. Another high-severity optimization bug resulting in incorrect bit shift results was patched in Solidity 0.5.6. Please measure the gas savings from optimizations, and carefully weigh them against the possibility of an optimization-related bug. Also, monitor the development and adoption of Solidity compiler optimizations to assess their maturity.

## Payable access control functions costs less gas
Consider marking functions with access control as `payable`. This will save 20 gas on each call by their respective permissible callers for not needing to have the compiler check for `msg.value`.

For instance, the function below may be refactored as follows:

[File: Conduit.sol#L92-L111](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/conduit/Conduit.sol#L92-L111)

```diff
    function execute(
        ConduitTransfer[] calldata transfers
-    ) external override onlyOpenChannel returns (bytes4 magicValue) {
+    ) external payable override onlyOpenChannel returns (bytes4 magicValue) {

            [ ... ]
```
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

For instance, the specific instance below may be refactored as follows:

[File: OrderCombiner.sol#L322-L332](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/lib/OrderCombiner.sol#L322-L332)

```solidity
 offerItem.startAmount == offerItem.endAmount
     ? offerItem.startAmount = endAmount
     : offerItem.startAmount = _getFraction(
                            numerator,
                            denominator,
                            offerItem.startAmount
                        );
```
## Non-strict inequalities are cheaper than strict ones
In the EVM, there is no opcode for non-strict inequalities (>=, <=) and two operations are performed (> + = or < + =).

As an example, consider replacing `>=` with the strict counterpart `>` in the following inequality instance:

[File: ConduitController.sol#L432](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/conduit/ConduitController.sol#L432)

```diff
-        if (channelIndex >= totalChannels) {
// Rationale for subtracting 1 on the right side of the inequality:
// x >= 10, [10, 11, 12, ...]
// x > 10 - 1 is the same as x > 9, [10, 11, 12 ...] 
+        if (channelIndex > totalChannels - 1) {
```
## `||` costs less gas than its equivalent `&&`
Rule of thumb: `(x && y)` is `(!(!x || !y))`

Even with the 10k Optimizer enabled: `||`, OR conditions cost less than their equivalent `&&`, AND conditions.

As an example, the instance below may be refactored as follows:

[File: ConduitController.sol#L147](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/conduit/ConduitController.sol#L147)

```diff
-        if (isOpen && !channelPreviouslyOpen) {
+        if (!(!isOpen || channelPreviouslyOpen)) {
```