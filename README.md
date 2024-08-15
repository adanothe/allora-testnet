<h1 align="center">Allora Worker Node Guide</h1>

## System Requirements

| Requirement       | Minimum                    | 
| ----------------- | -------------------------- | 
| OS                | Windows, macOS, or Linux   | 
| CPU               | Minimum of 1/2 core        | 
| RAM               | 2 to 4 GB                  | 
| Storage           | least 5GB SSD or NVMe      | 


#### Install Server Prerequisites

- Server Prerequisites
```shell
sudo apt update & sudo apt upgrade -y

sudo apt install ca-certificates zlib1g-dev libncurses5-dev libgdbm-dev libnss3-dev curl git wget make jq build-essential pkg-config lsb-release libssl-dev libreadline-dev libffi-dev gcc screen unzip lz4 -y
```

- Docker
```shell
curl --proto '=https' --tlsv1.2 -sSfL https://raw.githubusercontent.com/Dedenwrg/dependencies/main/docker/docker.sh | sudo sh
```

- Go
```shell
sudo rm -rf /usr/local/go
curl -L https://go.dev/dl/go1.22.4.linux-amd64.tar.gz | sudo tar -xzf - -C /usr/local
echo 'export PATH=$PATH:/usr/local/go/bin:$HOME/go/bin' >> $HOME/.bash_profile
echo 'export PATH=$PATH:$(go env GOPATH)/bin' >> $HOME/.bash_profile
source .bash_profile
go version
```

- Python & pip
```shell
sudo apt install python3
python3 --version

sudo apt install python3-pip
pip3 --version
```

### Intall allorad wallet
```shell
git clone https://github.com/allora-network/allora-chain.git
cd allora-chain && make all
allorad version
```
#### Create Wallet & Get faucet
- Save & Import phrase to keplr 

```shell
allorad keys add wallet
```
- Connect to Allora dashboard to find your Allora address or run allorad keys list