<<<<<<< HEAD
<strong><p style="font-size:14px" align="left">Founder :
<h3><p style="font-size:14px" align="right">Founder :
<a href="https://discord.gg/nodexcapital" target="_blank">NodeX Capital Discord Community</a></p></h3>
<h3><p style="font-size:14px" align="right">Visit Our Website :
<a href="https://discord.gg/nodexcapital" target="_blank">NodeX Capital Official</a></p></h3>
<h3><p style="font-size:14px" align="right">Hetzner :
<a href="https://hetzner.cloud/?ref=bMTVi7dcwSgA" target="_blank">Deploy Hetzner VPS Get 20€ Bonus!</a></h3>
<hr>

<p align="center">
  <img height="100" height="auto" src="https://user-images.githubusercontent.com/34649601/207593974-32d7cb69-eca9-4096-bc96-246fe7038c88.png">
</p>

# Migrate your validator to another machine

### 1. Run a new full node on a new machine
To setup full node you can follow my guide [Nolus node setup for Testnet](https://github.com/nodexcapital/testnet/blob/main/nolus/README.md)

### 2. Confirm that you have the recovery seed phrase information for the active key running on the old machine

#### To backup your key
```
nolusd keys export mykey
```
> _This prints the private key that you can then paste into the file `mykey.backup`_

#### To get list of keys
```
nolusd keys list
```

### 3. Recover the active key of the old machine on the new machine

#### This can be done with the mnemonics
```
nolusd keys add mykey --recover
```

#### Or with the backup file `mykey.backup` from the previous step
```
nolusd keys import mykey mykey.backup
```

### 4. Wait for the new full node on the new machine to finish catching-up

#### To check synchronization status
```
nolusd status 2>&1 | jq .SyncInfo
```
> _`catching_up` should be equal to `false`_

### 5. After the new node has caught-up, stop the validator node

> _To prevent double signing, you should stop the validator node before stopping the new full node to ensure the new node is at a greater block height than the validator node_
> _If the new node is behind the old validator node, then you may double-sign blocks_

#### Stop and disable service on old machine
```
sudo systemctl stop nolusd
sudo systemctl disable nolusd
```
> _The validator should start missing blocks at this point_

### 6. Stop service on new machine
```
sudo systemctl stop nolusd
```

### 7. Move the validator's private key from the old machine to the new machine
#### Private key is located in: `~/.nolus/config/priv_validator_key.json`

> _After being copied, the key `priv_validator_key.json` should then be removed from the old node's config directory to prevent double-signing if the node were to start back up_
```
sudo mv ~/.nolus/config/priv_validator_key.json ~/.nolus/bak_priv_validator_key.json
```

### 8. Start service on a new validator node
```
sudo systemctl start nolusd
```
> _The new node should start signing blocks once caught-up_

### 9. Make sure your validator is not jailed
#### To unjail your validator
```
nolusd tx slashing unjail --chain-id $NOLUS_CHAIN_ID --from mykey --gas=auto -y
```

### 10. After you ensure your validator is producing blocks and is healthy you can shut down old validator server
=======
<strong><p style="font-size:14px" align="left">Founder :
<h3><p style="font-size:14px" align="right">Founder :
<a href="https://discord.gg/nodexcapital" target="_blank">NodeX Capital Discord Community</a></p></h3>
<h3><p style="font-size:14px" align="right">Visit Our Website :
<a href="https://discord.gg/nodexcapital" target="_blank">NodeX Capital Official</a></p></h3>
<h3><p style="font-size:14px" align="right">Hetzner :
<a href="https://hetzner.cloud/?ref=bMTVi7dcwSgA" target="_blank">Deploy Hetzner VPS Get 20€ Bonus!</a></h3>
<hr>

<p align="center">
  <img height="100" height="auto" src="https://user-images.githubusercontent.com/34649601/207593974-32d7cb69-eca9-4096-bc96-246fe7038c88.png">
</p>

# Migrate your validator to another machine

### 1. Run a new full node on a new machine
To setup full node you can follow my guide [Nolus node setup for Testnet](https://github.com/nodexcapital/testnet/blob/main/nolus/README.md)

### 2. Confirm that you have the recovery seed phrase information for the active key running on the old machine

#### To backup your key
```
nolusd keys export mykey
```
> _This prints the private key that you can then paste into the file `mykey.backup`_

#### To get list of keys
```
nolusd keys list
```

### 3. Recover the active key of the old machine on the new machine

#### This can be done with the mnemonics
```
nolusd keys add mykey --recover
```

#### Or with the backup file `mykey.backup` from the previous step
```
nolusd keys import mykey mykey.backup
```

### 4. Wait for the new full node on the new machine to finish catching-up

#### To check synchronization status
```
nolusd status 2>&1 | jq .SyncInfo
```
> _`catching_up` should be equal to `false`_

### 5. After the new node has caught-up, stop the validator node

> _To prevent double signing, you should stop the validator node before stopping the new full node to ensure the new node is at a greater block height than the validator node_
> _If the new node is behind the old validator node, then you may double-sign blocks_

#### Stop and disable service on old machine
```
sudo systemctl stop nolusd
sudo systemctl disable nolusd
```
> _The validator should start missing blocks at this point_

### 6. Stop service on new machine
```
sudo systemctl stop nolusd
```

### 7. Move the validator's private key from the old machine to the new machine
#### Private key is located in: `~/.nolus/config/priv_validator_key.json`

> _After being copied, the key `priv_validator_key.json` should then be removed from the old node's config directory to prevent double-signing if the node were to start back up_
```
sudo mv ~/.nolus/config/priv_validator_key.json ~/.nolus/bak_priv_validator_key.json
```

### 8. Start service on a new validator node
```
sudo systemctl start nolusd
```
> _The new node should start signing blocks once caught-up_

### 9. Make sure your validator is not jailed
#### To unjail your validator
```
nolusd tx slashing unjail --chain-id $NOLUS_CHAIN_ID --from mykey --gas=auto -y
```

### 10. After you ensure your validator is producing blocks and is healthy you can shut down old validator server
>>>>>>> main/main
