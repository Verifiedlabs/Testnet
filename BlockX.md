# Tesnet Node BlockX Incentivized (Airdrop Confirmed)

## Source
* [Code-1](https://github.com/nodexcapital/testnet/tree/main/blockx)
* [Code-2](https://services.sxlzptprjkt.xyz/testnet/blockx/cheatsheet)
* [Discord](https://discord.gg/vDm6vuv367)
* [Explorer](https://explorer.nodexcapital.com/blockx)
* [Faucet](https://faucet.blockxnet.com)
  ``Submit 0x Address``

## TASK
* Set commision 5% - 7%
* Claim Staking Reward
* Delegate at least 100 BCX to another validator
* Claim [Faucet](https://faucet.blockxnet.com) and claim free tokens then transfer 5 BCX to your Validator address
* Create a token with the validator name as the token name
* Vote Proposal #1 Yes and Proposal #2 No
* Additional Task 
* ``https://docs.blockxnet.com/introduction/deploying-smart-contracts/remix``
* ``https://docs.blockxnet.com/introduction/deploying-smart-contracts/hardhat``
* ``Don't Forget to filled form``
* [Form Incentivized](https://forms.gle/qnht8Hkik79b9bU28)
     
## Spesification 
| Hardware | Software |
|----------|----------|
|CPU 4 Cores|Ubuntu 22.04++|
|RAM 8 GB DDR4 RAM|Go|
|Storage 160 GB SSD|

### Update Packages
```bash
sudo apt update && sudo apt upgrade -y
```

### Install Dependencies
```bash
sudo apt install curl build-essential git wget jq make gcc tmux -y
```

### Automatic Installer
```bash
wget -O blockx.sh https://raw.githubusercontent.com/nodexcapital/testnet/main/blockx/blockx.sh && chmod +x blockx.sh && ./blockx.sh
```
``Wait Installation Completed Est 2-5 minutes``

### Snapshot
```bash
sudo systemctl stop blockxd
cp $HOME/.blockxd/data/priv_validator_state.json $HOME/.blockxd/priv_validator_state.json.backup
rm -rf $HOME/.blockxd/data

curl -L https://snap.nodexcapital.com/blockx/blockx-latest.tar.lz4 | tar -Ilz4 -xf - -C $HOME/.blockxd/
mv $HOME/.blockxd/priv_validator_state.json.backup $HOME/.blockxd/data/priv_validator_state.json

sudo systemctl start blockxd && sudo journalctl -fu blockxd -o cat
```
``waiting for block sync 100% before next step``


## Cheat Sheet

#### Add new key
```bash
blockxd keys add wallet
```
``Save Pharse Key On your device``
#### Recover existing key
```bash
blockxd keys add wallet --recover
```
#### List all keys
```bash
blockxd keys list
```
#### Delete key
```bash
blockxd keys delete wallet
```
#### Export key to the file
```bash
blockxd keys export wallet
```
#### Import key from the file
```bash
blockxd keys import wallet wallet.backup
```
#### Query wallet balance
```bash
blockxd q bank balances $(blockxd keys show wallet -a)
```

## Validator management

#### Create New Validator
```bash
blockxd tx staking create-validator \
--amount=10000000000000000000abcx \
--pubkey=$(blockxd tendermint show-validator) \
--moniker="YOUR_MONIKER_NAME" \
--identity="YOUR_KEYBASE_ID" \
--details="YOUR_DETAILS" \
--website="YOUR_WEBSITE_URL" \
--chain-id=blockx_12345-2 \
--commission-rate=0.05 \
--commission-max-rate=0.07 \
--commission-max-change-rate=0.05 \
--min-self-delegation=1 \
--from=wallet \
--gas="1000000" \
--gas-adjustment="1.15"
```

#### Edit Validator
```bash
blockxd tx staking edit-validator \
--new-moniker="YOUR_MONIKER_NAME" \
--identity="YOUR_KEYBASE_ID" \
--details="YOUR_DETAILS" \
--website="YOUR_WEBSITE_URL"
--chain-id=blockx_12345-2 \
--commission-rate=0.05 \
--from=wallet \
--gas="1000000" \
--gas-adjustment="1.15"
```

#### Unjail Validator
```bash
blockxd tx slashing unjail --broadcast-mode=block --from wallet --chain-id blockx_12345-2 --gas="1000000" --gas-adjustment="1.15"
```

## Token Management
#### Withdraw rewards from all validators
```bash
blockxd tx distribution withdraw-all-rewards --from wallet --chain-id blockx_12345-2 --gas="1000000" --gas-adjustment="1.15"
```
#### Withdraw commission and rewards from your validator
```bash
blockxd tx distribution withdraw-rewards $(blockxd keys show wallet --bech val -a) --commission --from wallet --chain-id blockx_12345-2 --gas="1000000" --gas-adjustment="1.15"
```
#### Delegate tokens to yourself
```bash
blockxd tx staking delegate $(blockxd keys show wallet --bech val -a) 100000000000000000abcx --from wallet --chain-id blockx_12345-2 --gas="1000000" --gas-adjustment="1.15"
```
#### Delegate tokens to validator
```bash
blockxd tx staking delegate <TO_VALOPER_ADDRESS> 100000000000000000abcx --from wallet --chain-id blockx_12345-2 --gas="1000000" --gas-adjustment="1.15"
```
#### Redelegate tokens to another validator
```bash
blockxd tx staking redelegate $(blockxd keys show wallet --bech val -a) <TO_VALOPER_ADDRESS> 100000000000000000abcx --from wallet --chain-id blockx_12345-2 --gas="1000000" --gas-adjustment="1.15"
```
#### Unbond tokens from your validator
```bash
blockxd tx staking unbond $(blockxd keys show wallet --bech val -a) 100000000000000000abcx --from wallet --chain-id blockx_12345-2 --gas="1000000" --gas-adjustment="1.15"
```
#### Send tokens to the wallet
```bash
blockxd tx bank send wallet <TO_WALLET_ADDRESS> 100000000000000000abcx --from wallet --chain-id blockx_12345-2 --gas="1000000" --gas-adjustment="1.15"
```
## Governance Management
#### List all proposals
```bash
blockxd query gov proposals
```
#### View proposal by id
```bash
blockxd query gov proposal 1
```
#### Vote 'Yes'
```bash
blockxd tx gov vote 1 yes --from wallet --chain-id blockx_12345-2 --gas="1000000" --gas-adjustment="1.15"
```
#### Vote 'No'
```bash
blockxd tx gov vote 1 no --from wallet --chain-id blockx_12345-2 --gas="1000000" --gas-adjustment="1.15"
```
#### Vote 'Abstain'
```bash
blockxd tx gov vote 1 abstain --from wallet --chain-id blockx_12345-2 --gas="1000000" --gas-adjustment="1.15"
```
#### Vote 'NoWithVeto'
```bash
blockxd tx gov vote 1 nowithveto --from wallet --chain-id blockx_12345-2 --gas="1000000" --gas-adjustment="1.15"
```


