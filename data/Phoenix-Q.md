address(0) can be set 

conduitController address is never validated. Not in the contract and not in the children contracts (contracts inherits ConsiderationBase contract).

https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/lib/OrderValidator.sol#L55
https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/lib/ConsiderationBase.sol#L74

```solidity=
contract ConsiderationBase
ConduitControllerInterface internal immutable _CONDUIT_CONTROLLER;

    constructor(address conduitController) {
        // Derive name and version hashes alongside required EIP-712 typehashes.
        (
            _NAME_HASH,
            _VERSION_HASH,
            _EIP_712_DOMAIN_TYPEHASH,
            _OFFER_ITEM_TYPEHASH,
            _CONSIDERATION_ITEM_TYPEHASH,
            _ORDER_TYPEHASH
        ) = _deriveTypehashes();

        _BULK_ORDER_TYPEHASH_DIRECTORY = new TypehashDirectory();

        // Store the current chainId and derive the current domain separator.
        _CHAIN_ID = block.chainid;
        _DOMAIN_SEPARATOR = _deriveDomainSeparator();

        // Set the supplied conduit controller.
        _CONDUIT_CONTROLLER = ConduitControllerInterface(conduitController);

        // Retrieve the conduit creation code hash from the supplied controller.
        (_CONDUIT_CREATION_CODE_HASH, ) = (
            _CONDUIT_CONTROLLER.getConduitCodeHashes()
        );
    }
```