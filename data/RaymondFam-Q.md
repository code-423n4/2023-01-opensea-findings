## Interfaces and libraries should be separately saved and imported
Some contracts have interface(s) or libraries showing up in its/their entirety at the top/bottom of the contract facilitating an ease of references on the same file page. This has, in certain instances, made the already large contract size to house an excessive code base. Additionally, it might create difficulty locating them when attempting to cross reference the specific interfaces embedded elsewhere but not saved into a particular .sol file. 

Consider saving the interfaces and libraries entailed respectively, and having them imported like all other files.

Here are some of the instances entailed:

[File: PointerLibraries.sol](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/helpers/PointerLibraries.sol)

## Inadequate NatSpec
Solidity contracts can use a special form of comments, i.e., the Ethereum Natural Language Specification Format (NatSpec) to provide rich documentation for functions, return variables and more. Please visit the following link for further details:

https://docs.soliditylang.org/en/v0.8.16/natspec-format.html

Some of the code bases, particularly those entailing assembly, are lacking partial/full NatSpec that will be of added values to the users and developers if adequately provided.

Here are some of the instances entailed:

[File: PointerLibraries.sol](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/helpers/PointerLibraries.sol)

## Typo/grammatical mistakes
[File: ConsiderationDecoder.sol#L41](https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/lib/ConsiderationDecoder.sol#L41)

```diff
-            // Derive the size of the bytes array, rounding up to nearest word
+            // Derive the size of the bytes array, rounding up to the nearest word
```

