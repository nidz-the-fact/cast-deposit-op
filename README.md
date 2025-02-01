## ERC20 to ERC20 - Function: bridgeERC20To (L1StandardBridge)
1. **Approve** (Tokens to `L1StandardBridge`)
```
cast send <$TOKEN> \
"approve(address,uint256)" \
<$TO_ADDRESS_STANDARDBRIDGE> \
<$AMOUNT> \
--private-key <$PRIVATE_KEY> \
--rpc-url <$RPC_CHAIN_URL>
```

2. **Call function.[bridgeERC20To](https://github.com/ethereum-optimism/optimism/blob/op-contracts/v2.0.0-beta.3/packages/contracts-bedrock/src/L1/L1StandardBridge.sol#L178C1-L200C6)** (to `L1StandardBridge`)
```
cast send <$TO_ADDRESS_STANDARDBRIDGE> \
"bridgeERC20To(address,address,address,uint256,uint32,bytes)" \
<$TOKEN_LOCAL_L1> \
<$TOKEN_REMOTE_L2> \
<$TO_YOU_ADDRESS_WALLET> \
<$AMOUNT_DEC18_OR_6> \
21000 \
0x \
--private-key <$PRIVATE_KEY> \
--rpc-url <$RPC_CHAIN_URL>
```

---

## Add ERC20 to Bridge - Function: createOptimismMintableERC20 (OptimismMintableERC20Factory on L2)
**Call function.[createOptimismMintableERC20](https://github.com/ethereum-optimism/optimism/blob/op-contracts/v2.0.0-beta.3/packages/contracts-bedrock/src/universal/OptimismMintableERC20Factory.sol#L91C1-L105C6) (`OptimismMintableERC20Factory:0x4200000000000000000000000000000000000012` on L2)**
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

**Call function.[createOptimismMintableERC20WithDecimals](https://github.com/ethereum-optimism/optimism/blob/op-contracts/v2.0.0-beta.3/packages/contracts-bedrock/src/universal/OptimismMintableERC20Factory.sol#L107C1-L139C6) (`OptimismMintableERC20Factory:0x4200000000000000000000000000000000000012` on L2)**
```
cast send <$OPTIMISM_MINTABLE_ERC20_FACTORY> \
"createOptimismMintableERC20WithDecimals(address,string,string,uint8)" \
<$TOKEN_ON_L1> \
<$NAME_TOKEN> \
<$SYMBOL_TOKEN_DEC6> \
--private-key <$PRIVATE_KEY> \
--rpc-url <$RPC_CHAIN_URL>
```
