QA1. https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/lib/OrderValidator.sol#L890
It might be better to change the original name ``doesNotSupportPartialFills`` to ``_attemptToFillPartialOnFull()`` since the former only reflects to check whether it is a full order, not the violation itself.  

QA2. https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/conduit/Conduit.sol#L202
We should emit the old status here as well.


QA3. https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/conduit/ConduitController.sol#L124-L128
We should emit an event here to indicate the change of status. 

QA4. https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/conduit/ConduitController.sol#L436
We can add a check here to ensure the index is correct:
```
if(_conduits[conduit].channelIndexesPlusOne[channel] != channelIndex+1){
        revert ChannelOutOfRange(conduit);
}
```