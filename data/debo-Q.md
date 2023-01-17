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

## [L-02] 
```
SWC-103 Floating Pragma
```

URL
```
https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/lib/TypehashDirectory.sol#L2
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

## [L-03] 
```
SWC-103 Floating Pragma
```

URL
```
https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/lib/LowLevelHelpers.sol#L2
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

## [L-04] 
```
SWC-100 Function Default Visibility 
```

URL
```
https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/lib/ConsiderationErrors.sol#L11-L631
```

Description
```
Functions that do not have a function visibility type specified are public by default. This could lead to a vulnerability if a developer forgot to set the visibility and a malicious user is able to make unauthorized or unintended state changes.
```

PoC
```
function _revertBadFraction() pure {
```

Remediation
```
// Add visibility e.g., internal
function _revertBadFraction() internal pure {
```

## [L-05] 
```
SWC-103 Floating Pragma
```

URL
```
https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/lib/ConsiderationEncoder.sol#L2
```

Description
```
Contracts should be deployed with the same compiler version and flags that they have been tested with thoroughly. Locking the pragma helps to ensure that contracts do not accidentally get deployed using, for example, an outdated compiler version that might introduce bugs that affect the contract system negatively.
```

PoC
```
pragma solidity ^0.8.13;
```

Remediation
```
// remove circumflex or GT & LT operators
pragma solidity 0.8.17;
```