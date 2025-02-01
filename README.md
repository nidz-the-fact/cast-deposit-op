## Add ERC20 to Bridge - Function: createOptimismMintableERC20 (OptimismMintableERC20Factory on L2)
**Call function.[createOptimismMintableERC20](https://github.com/ethereum-optimism/optimism/blob/op-contracts/v2.0.0-beta.3/packages/contracts-bedrock/src/universal/OptimismMintableERC20Factory.sol#L91C1-L105C6)** (`OptimismMintableERC20Factory:0x4200000000000000000000000000000000000012` on L2)
```
cast send <$OPTIMISM_MINTABLE_ERC20_FACTORY> \
"createOptimismMintableERC20(address,string,string)" \
<$TOKEN_ON_L1> \
<$NAME_TOKEN> \
<$SYMBOL_TOKEN> \
--private-key <$PRIVATE_KEY> \
--rpc-url <$RPC_CHAIN_URL>
```

or

**Call function.[createOptimismMintableERC20WithDecimals](https://github.com/ethereum-optimism/optimism/blob/op-contracts/v2.0.0-beta.3/packages/contracts-bedrock/src/universal/OptimismMintableERC20Factory.sol#L107C1-L139C6)** (`OptimismMintableERC20Factory:0x4200000000000000000000000000000000000012` on L2)
```
cast send <$OPTIMISM_MINTABLE_ERC20_FACTORY> \
"createOptimismMintableERC20WithDecimals(address,string,string,uint8)" \
<$TOKEN_ON_L1> \
<$NAME_TOKEN> \
<$SYMBOL_TOKEN> \
<$DEC_TOKEN_6_OR_XX> \
--private-key <$PRIVATE_KEY> \
--rpc-url <$RPC_CHAIN_URL>
```

---

## Deposit
### ERC20 to ERC20 - Function: bridgeERC20To (L1StandardBridge on L1)
1. **Approve** (Tokens to `L1StandardBridge on L1`)
```
cast send <$TOKEN> \
"approve(address,uint256)" \
<$L1_STANDARD_BRIDGE> \
<$AMOUNT> \
--private-key <$PRIVATE_KEY> \
--rpc-url <$RPC_CHAIN_URL>
```

2. **Call function.[bridgeERC20To](https://github.com/ethereum-optimism/optimism/blob/op-contracts/v2.0.0-beta.3/packages/contracts-bedrock/src/L1/L1StandardBridge.sol#L178C1-L200C6)** (to `L1StandardBridge`)
> [!NOTE]  
> If the decimal token is 6, use the value [10^6](https://etherscan.io/unitconverter).
```
cast send <$L1_STANDARD_BRIDGE> \
"bridgeERC20To(address,address,address,uint256,uint32,bytes)" \
<$TOKEN_LOCAL_L1> \
<$TOKEN_REMOTE_L2> \
<$TO_YOU_ADDRESS_WALLET> \
<$AMOUNT> \
21000 \
0x \
--private-key <$PRIVATE_KEY> \
--rpc-url <$RPC_CHAIN_URL>
```

---

## Withdraw
### ERC20 to ERC20 - Function: bridgeERC20 (L2StandardBridge on L2)

1. **Approve** (Tokens to `L2StandardBridge:0x4200000000000000000000000000000000000010`)
```
cast send <$TOKEN> \
"approve(address,uint256)" \
<$L2_STANDARD_BRIDGE> \
<$AMOUNT> \
--private-key <$PRIVATE_KEY> \
--rpc-url <$RPC_CHAIN_URL>
```

2. **Call function.[bridgeERC20](https://github.com/ethereum-optimism/optimism/blob/op-contracts/v2.0.0-beta.3/packages/contracts-bedrock/src/universal/StandardBridge.sol#L191C1-L211C6)** (to `L2StandardBridge`)
> [!NOTE]  
> If the decimal token is 6, use the value [10^6](https://etherscan.io/unitconverter).
```
cast send <$L2_STANDARD_BRIDGE> \
"bridgeERC20To(address,address,uint256,uint32,bytes)" \
<$TOKEN_LOCAL_L2> \
<$TOKEN_REMOTE_L1> \
<$AMOUNT> \
21000 \
0x \
--private-key <$PRIVATE_KEY> \
--rpc-url <$RPC_CHAIN_URL>
```

---

## proveWithdrawalTransaction (on L1) - use [Opstack Kit](https://opstack-kit.pages.dev/docs/getting-started#installation) `npm i -g opstack-kit`
### Prove withdrawal using transaction hash, "OptimismPortal.[proveWithdrawalTransaction](https://github.com/ethereum-optimism/optimism/blob/op-contracts/v2.0.0-beta.3/packages/contracts-bedrock/src/L1/OptimismPortal.sol#L243C1-L322C6)" address.
```
ok prove <WithdrawalTxHashL2> --privateKey <0x-key> --chainIdL1 <id> --rpcUrlL1 <url> --chainIdL2 <id> --rpcUrlL2 <url> --portal <address> --l2OutputOracle <address> --disputeGameFactory <address> --scanL1Url <url>
```

---

## finalizeWithdrawalTransaction (on L1) - use [Opstack Kit](https://opstack-kit.pages.dev/docs/getting-started#installation) `npm i -g opstack-kit`
### Finalize withdrawal using transaction hash after proving, "OptimismPortal.[finalizeWithdrawalTransaction](https://github.com/ethereum-optimism/optimism/blob/op-contracts/v2.0.0-beta.3/packages/contracts-bedrock/src/L1/OptimismPortal.sol#L324C1-L444C6)" address.
```
ok finalize <WithdrawalTxHashL2> --privateKey <0x-key> --chainIdL1 <id> --rpcUrlL1 <url> --chainIdL2 <id> --rpcUrlL2 <url> --portal <address> --scanL1Url <url>
```
