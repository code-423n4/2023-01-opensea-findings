link : https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/lib/GettersAndDerivers.sol#L43

Scenario: A developer creates another contract that attempts to call the "_deriveOrderHash" function in order to calculate the hash of an order.

Example:

contract ExternalContract{

  function calculateOrderHash(address gettersAndDerivers, OrderParameters memory orderParameters, uint256 counter) external view returns(bytes32){

    return GettersAndDerivers(gettersAndDerivers)._deriveOrderHash(orderParameters,counter);

  }

}

Proof of concept: When trying to execute the function calculateOrderHash from ExternalContract, it will throw an error because the function _deriveOrderHash is internal and can't be accessed from other contracts.