**Overview**

Risk Rating | Number of issues | Estimated savings
--- | --- | ---
Gas Issues | 6 | Around 650

**Table of Contents:**

- [1. Using XOR (`^`) and OR (`|`) bitwise equivalents](#1-using-xor--and-or--bitwise-equivalents)
- [2. Shift left by 5 instead of multiplying by 32](#2-shift-left-by-5-instead-of-multiplying-by-32)
- [3. Using a positive conditional flow to save a NOT opcode](#3-using-a-positive-conditional-flow-to-save-a-not-opcode)
- [4. Swap conditions for a better happy path](#4-swap-conditions-for-a-better-happy-path)
- [5. Optimized operations](#5-optimized-operations)
- [6. Pre-decrements cost less than post-decrements](#6-pre-decrements-cost-less-than-post-decrements)

## 1. Using XOR (`^`) and OR (`|`) bitwise equivalents

*Estimated savings: 73 gas*
*Max savings according to `yarn profile`: 282 gas*

On Remix, given only `uint256` types, the following are logical equivalents, but don't cost the same amount of gas:

- `(a != b || c != d || e != f)` costs 571
- `((a ^ b) | (c ^ d) | (e ^ f)) != 0` costs 498 (saving 73 gas)

Consider rewriting as following to save gas:

```diff
File: FulfillmentApplier.sol
93:         if (
- 94:             execution.item.itemType != considerationItem.itemType ||
- 95:             execution.item.token != considerationItem.token ||
- 96:             execution.item.identifier != considerationItem.identifier
+ 94:             ((uint8(execution.item.itemType) ^ uint8(considerationItem.itemType)) |
+ 95:             (uint160(execution.item.token) ^ uint160(considerationItem.token)) |
+ 96:             (execution.item.identifier ^ considerationItem.identifier)) != 0
97:         ) {
```

**Logic POC**

Given 4 variables `a`, `b`, `c` and `d` represented as such:

```js
0 0 0 0 0 1 1 0 <- a
0 1 1 0 0 1 1 0 <- b
0 0 0 0 0 0 0 0 <- c
1 1 1 1 1 1 1 1 <- d
```

To have `a == b` means that every `0` and `1` match on both variables. Meaning that a XOR (operator `^`) would evaluate to 0 (`(a ^ b) == 0`), as it excludes by definition any equalities.
Now, if `a != b`, this means that there's at least somewhere a `1` and a `0` not matching between `a` and `b`, making `(a ^ b) != 0`.

Both formulas are logically equivalent and using the XOR bitwise operator costs actually the same amount of gas:

```solidity
      function xOrEquivalence(uint a, uint b) external returns (bool) {
        //return a != b; //370
        //return a ^ b != 0; //370
```

However, it is much cheaper to use the bitwise OR operator (`|`) than comparing the truthy or falsy values:

```solidity
    function xOrOrEquivalence(uint a, uint b, uint c, uint d) external returns (bool) {
        //return (a != b || c != d); // 495
        //return (a ^ b | c ^ d) != 0; // 442
    }
```

These are logically equivalent too, as the OR bitwise operator (`|`) would result in a `1` somewhere if any value is not `0` between the XOR (`^`) statements, meaning if any XOR (`^`) statement verifies that its arguments are different.

**Coded POC**

This little POC (use `forge test -m test_XorEq`) also proves that the formulas are equivalent:

```solidity
    function test_XorEq(uint8 a, uint8 b, address c, address d, uint256 e, uint256 f) external {
        assert((a != b || c != d || e != f) == (((a ^ b) | (uint160(c) ^ uint160(d)) | (e ^ f)) != 0));
    }
```

Please keep in mind that Foundry cannot currently fuzz `Enum` types, which is why we're using `uint8` types above, which is [treated the same according to the Solidity documentation](https://docs.soliditylang.org/en/v0.8.17/types.html#enums). However, you can try the following test on Remix to make sure, as it will always pass the asserts:

```solidity
    function test_enum(ItemType a, ItemType b) public {
        assert((a != b) == (uint8(a) != uint8(b)));
        assert((a != b) == ((uint8(a) ^ uint8(b)) != 0));
    }
```

**yarn profile**
This is the diff between the contest repo's `yarn profile` and the added suggestion's `yarn profile`, as `yarn profile` never changes the "Previous Report" it compares the "Current Report" to:

```diff
===============================================================================================
| method                         |          min |           max |           avg |       calls |
===============================================================================================
- | matchAdvancedOrders            | +12 (+0.01%) |     -12 (0%) | -471 (-0.19%) | +2 (+2.67%) |
+ | matchAdvancedOrders            | -40 (-0.02%) |  -92 (-0.03%)| -546 (-0.22%) | +2 (+2.67%) |
- | matchOrders                    | -12 (-0.01%) | -24 (-0.01%) | -234 (-0.09%) | +2 (+1.34%) |
+ | matchOrders                    | -20 (-0.01%) | -176 (-0.05%)| -323 (-0.12%) | +2 (+1.34%) |
- | validate                       |        53206 |        83915 |       -1 (0%) |          27 |
+ | validate                       |        53206 |  -24 (-0.03%)|   -7 (-0.01%) |          27 |
===============================================================================================
- | runtime size                   |        23583 |              |               |             |
+ | runtime size                   | -13 (-0.06%) |              |               |             |
- | init code size                 | +78 (+0.29%) |              |               |             |
+ | init code size                 | +65 (+0.24%) |              |               |             |
===============================================================================================
```

Added together, the max gas saving counted here is 282.

Consider applying the suggested equivalence and **add a comment mentioning what this is equivalent to**, as this is less human-readable, but still understandable once it's been taught.

## 2. Shift left by 5 instead of multiplying by 32

*Estimated savings: 22 gas*
*Max savings according to `yarn profile`: 98 gas*

The equivalent of multiplying by 32 is shifting left by 5. On Remix, a simple POC shows some by replacing one with the other (Optimizer at 10k runs):

```solidity
    function shiftLeft5(uint256 a) public pure returns (uint256) {
        //unchecked { return a * 32; } //346
        //unchecked { return a << 5; } //344
    }
```

This is due to the fact that the MUL opcode costs 5 gas and the SHL opcode costs 3 gas. Therefore, saving those 2 units of gas is expected.

Places where this optimization can be applied are as such:

- A simple multiplication by 32:

```diff
File: OrderCombiner.sol
- 220:             terminalMemoryOffset = (totalOrders + 1) * 32; //@audit-issue << 5
+ 220:             terminalMemoryOffset = (totalOrders + 1) << 5;
```

- Multiplying by the constant `OneWord == 0x20`, as `0x20` in hex is actually `32` in decimals:

```diff
seaport/contracts/lib/ConsiderationDecoder.sol:
-  386:             uint256 tailOffset = arrLength * OneWord;
+  386:             uint256 tailOffset = arrLength << 5;
-  427:             uint256 arrSize = (arrLength + 1) * OneWord;
+  427:             uint256 arrSize = (arrLength + 1) << 5;
-  485:             uint256 tailOffset = arrLength * OneWord;
+  485:             uint256 tailOffset = arrLength << 5;
-  525:             uint256 tailOffset = arrLength * OneWord;
+  525:             uint256 tailOffset = arrLength << 5;
-  617:             uint256 tailOffset = arrLength * OneWord;
+  617:             uint256 tailOffset = arrLength << 5;
-  660:             uint256 tailOffset = arrLength * OneWord;
+  660:             uint256 tailOffset = arrLength << 5;
-  731:             uint256 tailOffset = arrLength * OneWord;
+  731:             uint256 tailOffset = arrLength << 5;

seaport/contracts/lib/ConsiderationEncoder.sol:
-  567:             uint256 headAndTailSize = length * OneWord;
+  567:             uint256 headAndTailSize = length << 5;
-  678:             MemoryPointer srcHeadEnd = srcHead.offset(length * OneWord);
+  678:             MemoryPointer srcHeadEnd = srcHead.offset(length << 5);
```

**POC**

- Run `forge test -m test_shl5`:

```solidity
    function test_shl5(uint256 a) public {
        vm.assume(a <= type(uint256).max / 32); // This is to avoid an overflow
        assert((a * 32) == (a << 5)); // always true 
    }
```

Consider also adding a constant so that the code can be maintainable (`OneWordShiftLength`?)

**yarn profile**

```diff
===============================================================================================
| method                         |          min |           max |           avg |       calls |
===============================================================================================
- | matchAdvancedOrders            | +12 (+0.01%) |     -12 (0%) | -471 (-0.19%) | +2 (+2.67%) |
+ | matchAdvancedOrders            | -84 (-0.05%) |     -12 (0%) | -472 (-0.19%) | +2 (+2.67%) |
- | matchOrders                    | -12 (-0.01%) | -24 (-0.01%) | -234 (-0.09%) | +2 (+1.34%) |
+ | matchOrders                    | -12 (-0.01%) | -24 (-0.01%) | -236 (-0.09%) | +2 (+1.34%) |
```

Added together, the max gas saving counted here is 98.

## 3. Using a positive conditional flow to save a NOT opcode

*Estimated savings: 3 gas*
*Max savings according to `yarn profile`: 150 gas*

The following function either revert or returns some value. To save some gas (NOT opcode costing 3 gas), switch to a positive statement:

```diff
File: OrderValidator.sol
863:     function _revertOrReturnEmpty(
864:         bool revertOnInvalid,
865:         bytes32 contractOrderHash
866:     )
867:         internal
868:         pure
869:         returns (bytes32 orderHash, uint256 numerator, uint256 denominator)
870:     {
- 871:         if (!revertOnInvalid) { //@audit-issue save the NOT opcode
+ 871:         if (revertOnInvalid) {
- 872:             return (contractOrderHash, 0, 0);
+ 872:             _revertInvalidContractOrder(contractOrderHash);
873:         }
874: 
- 875:         _revertInvalidContractOrder(contractOrderHash);
+ 875:         return (contractOrderHash, 0, 0);
876:     }
```

**yarn profile**

```diff
==============================================================================================
| method                         |          min |          max |           avg |       calls |
==============================================================================================
- | cancel                         |        41219 |        58403 |         54019 |          16 |
+ | cancel                         | -12 (-0.03%) |        58403 |  -17 (-0.03%) |          16 |
- | fulfillAdvancedOrder           | +12 (+0.01%) |       225187 |       -7 (0%) |         182 |
+ | fulfillAdvancedOrder           | +12 (+0.01%) |       225187 |  -11 (-0.01%) |         182 |
- | fulfillAvailableAdvancedOrders |       149965 |       217284 |       +3 (0%) |          22 |
+ | fulfillAvailableAdvancedOrders |       149965 |       217284 |       -5 (0%) |          22 |
- | fulfillOrder                   | -12 (-0.01%) |       225067 |       -1 (0%) |         105 |
+ | fulfillOrder                   | -24 (-0.02%) |       225067 |       -3 (0%) |         105 |
- | matchOrders                    | -12 (-0.01%) | -24 (-0.01%) | -234 (-0.09%) | +2 (+1.34%) |
+ | matchOrders                    |       158290 | -24 (-0.01%) | -241 (-0.09%) | +2 (+1.34%) |
- | validate                       |        53206 |        83915 |       -1 (0%) |          27 |
+ | validate                       | -72 (-0.14%) | -48 (-0.06%) |  -18 (-0.02%) |          27 |
- ==============================================================================================
- | runtime size                   |        23583 |              |               |             |
+ | runtime size                   | -15 (-0.06%) |              |               |             |
- | init code size                 | +78 (+0.29%) |              |               |             |
+ | init code size                 | +63 (+0.24%) |              |               |             |
==============================================================================================
```

Added together, the max gas saving counted here is 150.

## 4. Swap conditions for a better happy path

*Estimated savings: 6 gas*
*Max savings according to `yarn profile`: 38 gas*

When a staticcall ends in failure, there will rarely, if ever, be a case of `returndatasize()` being non-zero. However, most often with a staticcall, `success` will be true, while the `returndatasize()` has a higher probability of being 0. The consequence is that, in the current order of conditions, both conditions are more likely to be evaluated. Furthermore, the RETURNDATASIZE opcode costs 2 gas while a MLOAD costs 3 gas. Consider swapping both conditions here for a better happy path:

```diff
File: PointerLibraries.sol
215:         assembly {
216:             let success := staticcall(
217:                 gas(),
218:                 IdentityPrecompileAddress,
219:                 src,
220:                 size,
221:                 dst,
222:                 size
223:             )
- 224:             if or(iszero(success), iszero(returndatasize())) {
+ 224:             if or(iszero(returndatasize()), iszero(success)) {
225:                 revert(0, 0)
226:             }
227:         }
```

**yarn profile**

```diff
==============================================================================================
| method                         |          min |          max |           avg |       calls |
==============================================================================================
- | fulfillAdvancedOrder           | +12 (+0.01%) |       225187 |       -7 (0%) |         182 |
+ | fulfillAdvancedOrder           | +12 (+0.01%) |       225187 |  -31 (-0.02%) |         182 |
- | fulfillAvailableAdvancedOrders |       149965 |       217284 |       +3 (0%) |          22 |
+ | fulfillAvailableAdvancedOrders |       149965 |       217284 |       +2 (0%) |          22 |
- | matchOrders                    | -12 (-0.01%) | -24 (-0.01%) | -234 (-0.09%) | +2 (+1.34%) |
+ | matchOrders                    | -12 (-0.01%) | -24 (-0.01%) | -235 (-0.09%) | +2 (+1.34%) |
- | validate                       |        53206 |        83915 |       -1 (0%) |          27 |
+ | validate                       |        53206 | -12 (-0.01%) |       -1 (0%) |          27 |
```

Added together, the max gas saving counted here is 38.

## 5. Optimized operations

*Estimated savings: 3 gas*
*Max savings according to `yarn profile`: 58 gas*

Tested on Remix: The optimized equivalent of `or(eq(a, 2), eq(a, 3))` is `and(lt(a, 4),gt(a, 1))` (saving 3 gas)

**POC:**
The following opcodes happen for `and(lt(a, 4),gt(a, 1))`:

```
      PUSH 4   4
      DUP2    lt(a, 4)
      LT    lt(a, 4)
      PUSH 1   1
      SWAP1    gt(a, 1)
      SWAP2    gt(a, 1)
      GT    gt(a, 1)
      AND    and(lt(a, 4), gt(a, 1))
      SWAP1    and(lt(a, 4), gt(a, 1))
```

The following opcodes happen for `or(eq(a, 2), eq(a, 3))`:

```
      PUSH 2   2
      DUP2    eq(a, 2)
      EQ    eq(a, 2)
      PUSH 3   3
      SWAP2    eq(a, 3)
      SWAP1    eq(a, 3)
      SWAP2    eq(a, 3)
      EQ    eq(a, 3)
      OR    or(eq(a, 2), eq(a, 3))
      SWAP1    or(eq(a, 2), eq(a, 3))
```

As we can see here, an extra SWAP is costing an extra 3 gas compared to the optimized version.
Consider replacing with the following:

```diff
File: ZoneInteraction.sol
140:     function _isRestrictedAndCallerNotZone(
141:         OrderType orderType,
142:         address zone
143:     ) internal view returns (bool mustValidate) {
144:         assembly {
145:             mustValidate := and(
- 146:                 or(eq(orderType, 2), eq(orderType, 3)),
+ 146:                 and(lt(orderType, 4),gt(orderType, 1)),
147:                 iszero(eq(caller(), zone))
148:             )
149:         }
150:     }
```

**yarn profile**

```diff
==============================================================================================
| method                         |          min |          max |           avg |       calls |
==============================================================================================
- | cancel                         |        41219 |        58403 |         54019 |          16 |
+ | cancel                         | +12 (+0.03%) | -12 (-0.02%) |   -3 (-0.01%) |          16 |
- | fulfillAdvancedOrder           | +12 (+0.01%) |       225187 |       -7 (0%) |         182 |
+ | fulfillAdvancedOrder           |        96287 |       225187 |       +2 (0%) |         182 |
- | fulfillBasicOrder              |        91377 |     -12 (0%) |       -5 (0%) |         187 |
+ | fulfillBasicOrder              | -24 (-0.03%) |      1621539 |       -1 (0%) |         187 |
- | matchOrders                    | -12 (-0.01%) | -24 (-0.01%) | -234 (-0.09%) | +2 (+1.34%) |
+ | matchOrders                    | -12 (-0.01%) | -24 (-0.01%) | -241 (-0.09%) | +2 (+1.34%) |
- | validate                       |        53206 |        83915 |       -1 (0%) |          27 |
+ | validate                       |        53206 |        83915 |   -4 (-0.01%) |          27 |
```

Added together, the max gas saving counted here is 58.

## 6. Pre-decrements cost less than post-decrements

*Estimated savings: 5 gas per iteration*
*Max savings according to `yarn profile`: 61 gas*

For a `uint256 maximumFulfilled` variable, the following is true with the Optimizer enabled at 10k:

- `--maximumFulfilled` costs 5 gas less than `maximumFulfilled--`

Affected code:  

```diff
File: OrderCombiner.sol
- 272:                 maximumFulfilled--;
+ 272:                 --maximumFulfilled;
```

**yarn profile**

```diff
==============================================================================================
| method                         |          min |          max |           avg |       calls |
==============================================================================================
- | matchAdvancedOrders            | +12 (+0.01%) |     -12 (0%) | -471 (-0.19%) | +2 (+2.67%) |
+ | matchAdvancedOrders            | -36 (-0.02%) |     -12 (0%) | -472 (-0.19%) | +2 (+2.67%) |
- | matchOrders                    | -12 (-0.01%) | -24 (-0.01%) | -234 (-0.09%) | +2 (+1.34%) |
+ | matchOrders                    | -12 (-0.01%) | -24 (-0.01%) | -235 (-0.09%) | +2 (+1.34%) |
- | validate                       |        53206 |        83915 |       -1 (0%) |          27 |
+ | validate                       |        53206 | -12 (-0.01%) |   -4 (-0.01%) |          27 |
```

Added together, the max gas saving counted here is 61.
