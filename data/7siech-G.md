In function `OrderValidator._validate`, increment counter inside body of loop for gas efficiency.

https://github.com/ProjectOpenSea/seaport/blob/0e40bf9f8fc759e32b616c41853e2f7f4766797e/contracts/lib/OrderValidator.sol#L750

```
for (uint256 i = 0; i < totalOrders; ++i) {
```
