[Read this repo for detail](https://github.com/arkprotocol/ics721-tools/tree/main)

# Oraichain

[How to setup and using oraicli](https://github.com/hien-p/Oraichain101)

## CW721 Contract

### Upload wasm to chain

```
yarn oraicli wasm upload  /home/asus/Workspace/transfer-cross-chain/cw-nfts/artifacts/cw721_base.wasm --fees 2500orai
```

<b>Code id:</b>

```
6525
```

### Instantiate contract

```
yarn oraicli wasm instantiate --code-id 6525 --input '{"name":"Orai NFT collection", "symbol":"orai-test-01", "minter":"orai1yzsegvns6vmvf5q29uv26p3th4fd2kzmsq3h6m"}' --label "NFT"
```

<b>Contract address:</b>

```
orai1cqrc6a05px2epcuvvhxzcyes5s7x72hjwqqs30g7lhenpsuus63qaeeayy
```

### Query

```
yarn oraicli wasm query orai1cqrc6a05px2epcuvvhxzcyes5s7x72hjwqqs30g7lhenpsuus63qaeeayy --input '{"num_tokens": {}}'
```

```
yarn oraicli wasm query orai1cqrc6a05px2epcuvvhxzcyes5s7x72hjwqqs30g7lhenpsuus63qaeeayy --input '{"contract_info": {}}'
```

## ICS721 contract

### Upload wasm to chain

```
yarn oraicli wasm upload /home/asus/Workspace/transfer-cross-chain/ICS721/artifacts/cw_ics721_bridge.wasm --fees 2500orai
```

<b>Code id:</b>

```
6526
```

### Instantiate contract

```
yarn oraicli wasm instantiate --code-id 6526 --input '{"cw721_base_code_id": 6525}' --label "ICS721"
```

<b>Contract address:</b>

```
orai1u3hjrupq82c9kxq0y674lxxt872n78ae79xujjskukhhngl6td8qpl5tdw
```

### Query

```
yarn oraicli wasm query orai1u3hjrupq82c9kxq0y674lxxt872n78ae79xujjskukhhngl6td8qpl5tdw --input '{"nft_contract": {"class_id":"DUMMY"}}'
```

# Stargaze

[You can watch the transaction at here](https://testnet-explorer.publicawesome.dev/stargaze/tx/6DF2AE9003C1012498E9BE3FEEC1EE84894A1CCA0E2CC08B1D3228093E7FDE87)
[How to setup CLI & create testnet account](https://docs.stargaze.zone/developers/cosmwasm-smart-contracts/testnet)

## Stargaze testnet account

```
address: stars1a3766060t67u8mu740anrfqwxs7aax9srt4l4r
  name: testnet-key
  pubkey: '{"@type":"/cosmos.crypto.secp256k1.PubKey","key":"A1danmpAnqkS6RQWdzs7NTlL1UWLfo0uZ13MoidP92wg"}'
  type: local
```

## CW721 contract

### Upload wasm to chain

```
starsd tx wasm store /home/asus/Workspace/transfer-cross-chain/cw-nfts/artifacts/cw721_base.wasm --from stars1a3766060t67u8mu740anrfqwxs7aax9srt4l4r --gas-prices 0.025ustars --gas-adjustment 1.7 --gas auto
```

<b>Code id:</b>

```
3430
```

### Instantiate contract

```
starsd tx wasm instantiate 3430 '{"name":"Stargaze NFT collection", "symbol":"starsd-nft-01", "minter":"stars1a3766060t67u8mu740anrfqwxs7aax9srt4l4r"}' --label "ICS721" --admin stars1a3766060t67u8mu740anrfqwxs7aax9srt4l4r --from stars1a3766060t67u8mu740anrfqwxs7aax9srt4l4r --amount "100000ustars" --gas-prices 0.025ustars --gas-adjustment 1.7 --gas auto
```

<b>Contract address:</b>

```
stars10h3qpct2nn2ffjfphkexa5j585k9mf3cp39ajpsggamfs0d4xp9qv8c6zv
```

## ICS721 contract

### Upload wasm to chain

```
starsd tx wasm store /home/asus/Workspace/transfer-cross-chain/ICS721/artifacts/cw_ics721_bridge.wasm --from stars1a3766060t67u8mu740anrfqwxs7aax9srt4l4r --gas-prices 0.025ustars --gas-adjustment 1.7 --gas auto
```

<b>Code id:</b>

```
3431
```

### Instantiate contract

```
starsd tx wasm instantiate 3431 '{"cw721_base_code_id":3430}' --label "ICS721" --admin stars1a3766060t67u8mu740anrfqwxs7aax9srt4l4r --from stars1a3766060t67u8mu740anrfqwxs7aax9srt4l4r --amount "100000ustars" --gas-prices 0.025ustars --gas-adjustment 1.7 --gas auto
```

<b>Contract address:</b>

```
stars1du26qvkqhhc5n6l6ue0h6uwl42a9pdrh3y630vfun2hhqykmqv6sa9zrcv
```

### Query

```
starsd query wasm contract-state smart stars1du26qvkqhhc5n6l6ue0h6uwl42a9pdrh3y630vfun2hhqykmqv6sa9zrcv '{"nft_contract":{"class_id":"DUMMY"}}'
```

```
starsd query wasm contract-state smart stars10h3qpct2nn2ffjfphkexa5j585k9mf3cp39ajpsggamfs0d4xp9qv8c6zv '{"num_tokens":{}}'
```

```
starsd query wasm contract-state smart stars10h3qpct2nn2ffjfphkexa5j585k9mf3cp39ajpsggamfs0d4xp9qv8c6zv '{"all_nft_info":{"token_id": "0"}}'
```

### Execute

#### Mint NFT

```
starsd tx wasm execute stars10h3qpct2nn2ffjfphkexa5j585k9mf3cp39ajpsggamfs0d4xp9qv8c6zv '{"mint": {"token_id":"0", "owner":"stars1a3766060t67u8mu740anrfqwxs7aax9srt4l4r"}}' --from stars1a3766060t67u8mu740anrfqwxs7aax9srt4l4r --gas-prices 0.025ustars --gas-adjustment 1.7 --gas auto
```

# Setup Hermes
https://hermes.informal.systems/documentation/configuration/configure-hermes.html
https://github.com/informalsystems/hermes

## Create an IBC Channel (not working)

hermes --config config.toml create channel --a-chain Oraichain-testnet --b-chain elgafar-1 --a-port wasm.orai1u3hjrupq82c9kxq0y674lxxt872n78ae79xujjskukhhngl6td8qpl5tdw --b-port wasm.stars1du26qvkqhhc5n6l6ue0h6uwl42a9pdrh3y630vfun2hhqykmqv6sa9zrcv --new-client-connection --channel-version 0.0.1 --yes

{ "receiver": "orai1yzsegvns6vmvf5q29uv26p3th4fd2kzmsq3h6m", "channel_id": "SOURCE_ICS721_CHANNEL", "timeout": { "block": { "revision": 1, "height": 3999999 } } }

BASE64_ENCODED_JSON_MSG_FOR_ICS721
