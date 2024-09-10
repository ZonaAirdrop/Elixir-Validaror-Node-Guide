# Elixir-Validaror-Node-Guide
Running an Elixir Testnet Validator

## Recommended Hardware Requirements 

|   SPEC      |        Recommend          |
| :---------: | :-----------------------: |
|   **CPU**   | 4 Cores (ARM64 or x86-64) |
|   **RAM**   |        4 GB (DDR4)        |
|   **SSD**   |        100 GB          |
| **NETWORK** |        100 Mbps           |

### Install Dependencies

```
sudo apt update && sudo apt upgrade -y
sudo apt install -y curl git jq lz4 build-essential unzip
```
### Install Docker
Ignore if you already Installed

```
sudo apt install -y ca-certificates curl gnupg lsb-release
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /usr/share/keyrings/docker-archive-keyring.gpg
echo "deb [arch=$(dpkg --print-architecture) signed-by=/usr/share/keyrings/docker-archive-keyring.gpg] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
sudo apt update && sudo apt install -y docker-ce docker-ce-cli containerd.io
sudo usermod -aG docker $USER
newgrp docker
```
### Make a Directory for Elixir
```
mkdir elixir && cd elixir
wget https://files.elixir.finance/validator.env
```
### Install Nano
Ignore if already installed

```
sudo apt install nano
```
### Edit .env file

```
nano validator.env
```

Create a new and dedicated wallet using metamask. Don't use old wallet.

STRATEGY_EXECUTOR_DISPLAY_NAME : Your Validator Name

STRATEGY_EXECUTOR_BENEFICIARY : Wallet Address 

SIGNER_PRIVATE_KEY : Private key 

Ctrl+X - they press Y - Enter

```
docker pull elixirprotocol/validator:v3 --platform linux/amd64
```

### Start the Node

```
docker run -d \
  --env-file ./validator.env \
  --name elixir \
  --restart unless-stopped \
  -p 17690:17690 \
  elixirprotocol/validator:v3
```

### Check Logs
```
docker logs -f elixir
```
### Check Health Status
```
curl 127.0.0.1:17690/health | jq
```

Get OK

## UseFul Commands

**Upgrading Node**
```
docker kill elixir
docker rm elixir
docker pull elixirprotocol/validator:v3 --platform linux/amd64
```
```
docker run -d \
  --env-file ./validator.env \
  --name elixir \
  --restart unless-stopped \
  -p 17690:17690 \
  elixirprotocol/validator:v3
```
**Join Channel For Update** : https://t.me/ZonaAirdr0p
