## [QA-01] Use latest Solidity version

Solidity pragma versioning should be upgraded to latest available version.
***

## [QA-02] Use stable pragma statement

Using a floating pragma statement (`^0.8.13`, `^0.8.7`) is discouraged as code can compile to different bytecodes with different compiler versions. Use a stable pragma statement to get a deterministic bytecode.
***

## [QA-03] Different pragma directives are used

Use one Solidity version on each contract.
***

## [QA-04] Constant variables should be written in UPPERCASE
Add constant and change VariableName to VARIABLE_NAME
```
Check the following contract:
lib/ConsiderationConstants.sol
```
***

## [QA-05] Solidity compiler optimizations can be problematic
```
hardhat.config.ts:
26:const config: HardhatUserConfig = {
27:  solidity: {
28:    compilers: [
29:      {
30:        version: "0.8.14",
31:        settings: {
32:         viaIR: true,
33:          optimizer: {
34:            enabled: true,
35:            runs: 18000,
36:          },
37:        },
38:      },
39:    ],
 ```
 
Protocol has enabled optional compiler optimizations in Solidity. There have been several optimization bugs with security implications. Moreover, optimizations are actively being developed. Solidity compiler optimizations are disabled by default, and it is unclear how many contracts in the wild actually use them.

Therefore, it is unclear how well they are being tested and exercised. High-severity security issues due to optimization bugs have occurred in the past. A high-severity bug in the emscripten-generated solc-js compiler used by Truffle and Remix persisted until late 2018. The fix for this bug was not reported in the Solidity CHANGELOG.

**Recommendation**: Short term, measure the gas savings from optimizations and carefully weigh them against the possibility of an optimization-related bug. Long term, monitor the development and adoption of Solidity compiler optimizations to assess their maturity.
***