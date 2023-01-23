## [G-1] On contract CriteriaResolution.sol add a continue statemnt
On function `\_applyCriteriaResolvers`  the for loop on `L41` which is used for advanceOrders add a continue statemnt on line `156`  as `if (totalItems == 0) continue; ` like done on line `CriteriaResolution.sol#L-77` for `advancedOrder.numerator`.
```solidity
 // Iterate over each advanced order.
            for (uint256 i = 0; i < totalAdvancedOrders; ++i) {
                // Retrieve the advanced order.
                ...

                // Read consideration length from memory and place on stack.
                uint256 totalItems = orderParameters.consideration.length;

                // Iterate over each consideration item on the order.
                for (uint256 j = 0; j < totalItems; ++j) {
                    // Ensure item type no longer indicates criteria usage.
                    ...
                }

                // Read offer length from memory and place on stack.
                totalItems = orderParameters.offer.length;

                // Iterate over each offer item on the order.
                for (uint256 j = 0; j < totalItems; ++j) {
                    // Ensure item type no longer indicates criteria usage.
                    ...
                }
            }
```

## [G-2]In ConsiderationEncoder.sol Declare srcTail outside while loop.
On line `ConsiderationEncoder.sol#L-686` srcTail is being declared again and again, each time variable is declared, a new memory slot is reserved on the stack.
`function \_encodeConsiderationAsReceivedItems`
**Recomendation:** Declare srcTail outside while loop

## [G-3] use `--maximumFulfilled`;  line `272` OrderCombiner.sol as it is inside for loop and preincremnt cost less gas
```solidity
                // Decrement the number of fulfilled orders.
                // Skip underflow check as the condition before
                // implies that maximumFulfilled > 0.
                maximumFulfilled--;
```


## [G-4]On function getConduit in ConduitController.sol use 0xff directly insted of bytes1(0xff)
```solidity
 function getConduit(
        bytes32 conduitKey
    ) external view override returns (address conduit, bool exists) {
        // Derive address from deployer, conduit key and creation code hash.
        conduit = address(
            uint160(
                uint256(
                    keccak256(
                        abi.encodePacked(
		                    - bytes1(0xff),
		                    + 0xff,
                            address(this),
                            conduitKey,
                            _CONDUIT_CREATION_CODE_HASH
                        )
                    )
                )
            )
        );

        // Determine whether conduit exists by retrieving its runtime code.
        exists = (conduit.codehash == _CONDUIT_RUNTIME_CODE_HASH);
    }
```