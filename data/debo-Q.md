## [L-01] 
```
SWC-103 Floating Pragma
```

URL
```
https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/Seaport.sol#L2
```

Description
```
Contracts should be deployed with the same compiler version and flags that they have been tested with thoroughly. Locking the pragma helps to ensure that contracts do not accidentally get deployed using, for example, an outdated compiler version that might introduce bugs that affect the contract system negatively.
```

PoC
```
pragma solidity ^0.8.17;
```

Remediation
```
// remove circumflex or GT & LT operators
pragma solidity 0.8.17;
```