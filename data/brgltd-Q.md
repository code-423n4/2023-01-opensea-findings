# [01] Potential locked ether when calling `BasicOrderFulfiller._validateAndFulfillBasicOrder()`

`_validateAndFulfillBasicOrder()` will make different transfers depending on the `ItemType`. For transfers where `additionalRecipientsItemType` is not `ItemType.NATIVE` (transfers between ERC20, ERC721 and ERC1155), an improvement that can be made is to check if `msg.value` is zero.

Otherwise, if ether is sent accidentally during these transfer, the `msg.value` will be locked.

https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/lib/BasicOrderFulfiller.sol#L200-L267

# [02] Unsafe downcast

Downcasting in solidity can lead to silent overflows. The ideal approach would be to use a safe wrapper that reverts if the number being casted is bigger than the expected range. Alternative, for each one of the values being downcasted, if the idea is to be as much gas efficient as possible and an overflow cannot happen, consider adding a comment for clarity.

https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/conduit/ConduitController.sol#L66

https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/conduit/ConduitController.sol#L72-L85

https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/conduit/ConduitController.sol#L335-L348

https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/lib/Executor.sol#L60

# [03] Lack of address(0) check for Conduit.updateChannel()

Setting `_channels[address(0)]` to true can result in unexpected behavior for the project. Consider adding an address(0) check for the `channel` parameter.

https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/conduit/Conduit.sol#L187-L203

# [04] Usage of abi.encodePacked

To prevent hash collisions, `abi.encode` is generally preferred over `abi.encodePacked` . If there's a compelling reason to use abi.encodePacked, consider adding a comment.

https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/conduit/ConduitController.sol#L72-L85

https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/conduit/ConduitController.sol#L335-L348

https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/lib/TypehashDirectory.sol#L177-L181

# [05] Repeated validation statements can be converted into a function modifier

Creating a modifier for repeated validation logic can improve code reusability and gas usage. Also, aside from reverting if the conduit doens't exist, the function `ConduitController._assertConduitExists()` could return `true` indicating when it exists.

https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/conduit/ConduitController.sol#L497-L503

https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/conduit/ConduitController.sol#L308-L318

# [06] Order of functions 

The solidity [documentation](https://docs.soliditylang.org/en/v0.8.17/style-guide.html#order-of-functions) recommends adding pure functions bellow view functions.

The instances bellow highlight pure above view.

https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/lib/AmountDeriver.sol#L109-L113

https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/lib/AmountDeriver.sol#L159-L167

# [07] Nameless imports

Naming all the used imports can improve the explicitness of the code

https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/lib/ZoneInteraction.sol#L16

https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/lib/ConsiderationEncoder.sol#L20

https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/conduit/Conduit.sol#L15

https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/lib/Assertions.sol#L14

# [08] Usage of return named variables and explicit values

Some functions return named variables, others return explicit values.

Following function returns an explicit value.

https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/lib/BasicOrderFulfiller.sol#L68-L70

Following function return returns a named variable.

https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/lib/BasicOrderFulfiller.sol#L304-L311

Consider adopting the same approach throughout the codebase to improve the explicitness and readability of the code.

# [09] Constant redefined elsewhere

If possible, consider importing/reusing the same constant to improve code reusability.

https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/lib/ConsiderationConstants.sol#L145

https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/lib/TypehashDirectory.sol#L24

https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/lib/TokenTransferrerConstants.sol#L44

# [10] Constants should be all uppercase

The usual approach for defining constants in solidity and other programming languages is in an all uppercase format, e.g. MY_CONSTANT instead of MyConstant.

https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/lib/TokenTransferrerConstants.sol#L36-L39

It's understandable if Seaport wants to maintain the current approach, since it's following consistently throughout all constant variables. However, please note that most common linters will complain about not defining constant in all uppercase.

# [11] Yul loop empty blocks

Instead of declaring an empty line for each empty block for the loop inside assembly blocks, a more concise approach can be to declare the empty block without the empty line. 

E.g. replacing 

```
for {

} lt(value1, value2) {

} {
```

With the following


```
for {} lt(value1, value2) {} {
```

https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/lib/ConsiderationDecoder.sol#L110-L114

https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/lib/ConsiderationDecoder.sol#L175-L179

https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/lib/ConsiderationDecoder.sol#L579-L583
