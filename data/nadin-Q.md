[NC-01] It's better to emit after all processing is done
01: https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/lib/OrderValidator.sol#L706-L711
02: https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/lib/OrderValidator.sol#L801-L809

[NC-02] Use of bytes.concat() instead of abi.encodePacked(,)
Rather than using abi.encodePacked for appending bytes, since version 0.8.4, bytes.concat() is enabled
Since version 0.8.4 for appending bytes, bytes.concat() can be used instead of abi.encodePacked(,).
01: https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/lib/TypehashDirectory.sol#L177-L181

[NC-03] NatSpec is incomplete
01: https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/interfaces/EIP1271Interface.sol
02: https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/interfaces/IERC721Receiver.sol

[NC-04] Hex selector 
You can use .selector instead of a hex number, e.g.:
// bytes4(keccak256("isValidSignature(bytes32,bytes)"))
bytes4 constant internal ERC1271_MAGICVALUE_BYTES32 = 0x1626ba7e;
is equivavelent to:
IERC1271Wallet.isValidSignature.selector
https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/lib/ConsiderationConstants.sol

[L-01] _performERC20Transfer function create dirty bits
https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/lib/TokenTransferrer.sol#L59-L67
This explanation should be added in the NatSpec comments of this function that sends ether with call;
Note that this code probably isn't secure or a good use case for assembly because a lot of memory management and security checks are bypassed. Use with caution! Some functions in this contract knowingly create dirty bits at the destination of the free memory pointer.
Recommended Mitigation Steps
+ bool success;
-  let callStatus := call ( https://github.com/ProjectOpenSea/seaport/blob/5de7302bc773d9821ba4759e47fc981680911ea0/contracts/lib/TokenTransferrer.sol#L59-L67)
+ success: = call
