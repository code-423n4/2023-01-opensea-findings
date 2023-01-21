**seaport/contracts/lib/OrderValidator.sol**
- L508 - Instead of variable-- it is less expensive to do unchecked{--variable;}


**seaport/contracts/lib/OrderCombiner.sol**
- L122/138 - When a variable is only used once, it could save gas by not creating the variable and using the operation directly inside where it is needed.

- L272 - Instead of variable-- it is less expensive to do unchecked{--variable;}


**seaport/contracts/lib/Executor.sol**
- L438/441/461/464 - When a variable is only used once, it could save gas by not creating the variable and using the operation directly inside where it is needed.


**seaport/contracts/lib/ConsiderationEncoder.sol**
- L127/134/143/149/162/166/228/234/252/259/266/273/280/287/367/373/388/394/406/413/422/429/498/508 - When a variable is only used once, it could save gas by not creating the variable and using the operation directly inside where it is needed.


**seaport/contracts/lib/OrderFulfiller.sol**
- L260/264 - When a variable is only used once, it could save gas by not creating the variable and using the operation directly inside where it is needed.


**seaport/contracts/conduit/ConduitController.sol**
- L429/432 - When a variable is only used once, it could save gas by not creating the variable and using the operation directly inside where it is needed.


**seaport/contracts/lib/GettersAndDerivers.sol**
- L320/323/328/329 - When a variable is only used once, it could save gas by not creating the variable and using the operation directly inside where it is needed.
