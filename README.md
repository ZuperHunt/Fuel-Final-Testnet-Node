![image](https://github.com/user-attachments/assets/3ca72387-514b-48d4-9bea-1917cbaa241c)


Penulis: [Naufal](https://x.com/0xfal)

> [!NOTE]
> **WHAT IS Fuel?**\
> Fuel is an operating system purpose-built for Ethereum rollups. Fuel's unique architecture allows rollups to solve for PSI (parallelization, state minimized execution, interoperability). Powered by the FuelVM, Fuel aims to expand Ethereum's capability set without compromising security or decentralization.

# Tutorial Fuel Final Testnet Node

## Needs

### Computer

You can use either VPS or your local PC with requirements:

| ✅ Linux | ✅ macOS | ✅ Windows (WSL) |
| ------------- | ------------- | ------------- |

| Part | Minimum | Recommended |
| ------------- | ------------- | ------------- |
| CPU | 2 Core | 8 Core |
| RAM | 4 GB | 12 GB |
| SSD | 30 GB | 100 GB |

This tutorial was created using Linux (Ubuntu), for other operating systems it may be slightly different.

### Sepolia (Ethereum Testnet) API Key
An API key from any RPC provider that supports the Sepolia network will work. We recommend either [Infura](https://www.infura.io/) **or** [Alchemy](https://www.alchemy.com/).

The endpoints should look like the following:

**Infura**
```
https://sepolia.infura.io/v3/{YOUR_API_KEY}
```
**Alchemy**
```
https://eth-sepolia.g.alchemy.com/v2/{YOUR_API_KEY}
```

Will use to `<YOUR_ETHEREUM_SEPOLIA_RPC>` in the next step!!

## Dependencies

### Install Fuel toolchain:
```
curl https://install.fuel.network | sh
```
## Run Node

### Generating a P2P Key

Do not share or lose this private key, and do not forget to **BACKUP** it, will use to `<YOUR_KEYPAIR_SECRET>` in the next step!! Press any key to complete.
```
fuel-core-keygen new --key-type peering
```

### Chain Configuration

```
git clone https://github.com/FuelLabs/chain-configuration.git
```

### Create tmux

```
tmux
```

### Running a Local Node

Copy below and change `<YOUR_KEYPAIR_SECRET>` and `<YOUR_ETHEREUM_SEPOLIA_RPC>` to yours, paste to your terminal and press `enter` on your keyboard.
```
fuel-core run \
--service-name=zuperfuel \
--keypair <YOUR_KEYPAIR_SECRET> \
--relayer <YOUR_ETHEREUM_SEPOLIA_RPC> \
--ip=0.0.0.0 --port=4000 --peering-port=30333 \
--db-path=~/.fuel-sepolia-testnet \
--snapshot ./chain-configuration/ignition/ \
--utxo-validation --poa-instant false --enable-p2p \
--reserved-nodes /dns4/p2p-testnet.fuel.network/tcp/30333/p2p/16Uiu2HAmDxoChB7AheKNvCVpD4PHJwuDGn8rifMBEHmEynGHvHrf \
--sync-header-batch-size 100 \
--enable-relayer \
--relayer-v2-listening-contracts=0x01855B78C1f8868DE70e84507ec735983bf262dA \
--relayer-da-deploy-height=5827607 \
--relayer-log-page-size=500 \
--sync-block-stream-buffer-size 30
```

Run the service:
```
sudo systemctl daemon-reload && \
sudo systemctl enable fueld && \
sudo systemctl start fueld && \
sudo systemctl status fueld.service
```

The output should be like this:
![image](https://github.com/user-attachments/assets/9bc8426b-a643-4bf0-8aae-c95bb6764423)


# Help

## How to check the logs?

```
sudo journalctl -u fueld -f -o cat
```

## How to restart my node?

```
sudo systemctl restart fueld
```

## How to detach from tmux session?

Press `ctrl` + `b` + `d` on your keyboard

## How to attach to last tmux session?

Run following command:
```
tmux a
```

---

Reach us if you have more questions:\
ZuperHunt's [Discord server](https://discord.gg/ZuperHunt) | [X(Twitter)](https://twitter.com/ZuperHunt)

# Acknowledgements

* [Running a local Fuel node connected to Testnet using P2P](https://docs.fuel.network/guides/running-a-node/running-a-testnet-node/)
* [tmux cheatsheet](https://quickref.me/tmux.html)
