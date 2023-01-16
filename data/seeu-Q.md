## Insecure random number generation, usage of block variables

### Description

Bad Randomness arises when the attacker can predict the result of a random number. A miner can choose whether to broadcast or delete a block using a technique known as "selective packing." Because of this, a malevolent miner has the chance to get the outcome they want and forecast random numbers.

### Findings

- [seaport/reference/lib/ReferenceCounterManager.sol#L36](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0/reference/lib/ReferenceCounterManager.sol#L36) => `uint256 quasiRandomNumber = uint256(blockhash(block.number - 1)) >> 128;`

### Resources

- [Predicting Random Numbers in Ethereum Smart Contracts](https://blog.positive.com/predicting-random-numbers-in-ethereum-smart-contracts-e5358c6b8620)
- [Bad Randomness | DASP Top 10](https://dasp.co/#item-6)