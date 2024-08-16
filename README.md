
# Allora Worker Node Guide
## Allora Resource

- **Website**: [allora website](https://www.allora.network/)
- **Telegram**: [Join allora discussion](https://t.me/alloranetworkannouncements)
- **Twitter**: [Follow allora on Twitter](https://x.com/AlloraNetwork)
- **GitHub**: [allora github](https://github.com/allora-network)
- **Documentation**: [docs](https://docs.allora.network/)

## System Requirements

| Component       | Minimum Requirements           |
| --------------- | ------------------------------ |
| **Operating System** | Windows, macOS, or Linux       |
| **CPU**              | 1/2 core minimum               |
| **RAM**              | 2 to 4 GB                      |
| **Storage**          | 5 GB SSD or NVMe               |

## Server Prerequisites

- **Update and Upgrade Server**: Ensure your server is up to date.

    ```bash
    sudo apt update && sudo apt upgrade -y
    ```

- **Install Required Packages**: Install the necessary dependencies.

    ```bash
    sudo apt install -y ca-certificates zlib1g-dev libncurses5-dev libgdbm-dev libnss3-dev curl git wget make jq build-essential pkg-config lsb-release libssl-dev libreadline-dev libffi-dev gcc screen unzip lz4
    ```

- **Install Docker**: Use the following command to install Docker.

    ```bash
    curl --proto '=https' --tlsv1.2 -sSfL https://raw.githubusercontent.com/Dedenwrg/dependencies/main/docker/docker.sh | sudo sh
    ```

- **Install Go**: Remove any existing Go installation and install the latest version.

    ```bash
    sudo rm -rf /usr/local/go
    curl -L https://go.dev/dl/go1.22.4.linux-amd64.tar.gz | sudo tar -xzf - -C /usr/local
    echo 'export PATH=$PATH:/usr/local/go/bin:$HOME/go/bin' >> $HOME/.bash_profile
    echo 'export PATH=$PATH:$(go env GOPATH)/bin' >> $HOME/.bash_profile
    source $HOME/.bash_profile
    go version
    ```

- **Install Python & Pip**: Install Python 3 and pip.

    ```bash
    sudo apt install python3
    python3 --version

    sudo apt install python3-pip
    pip3 --version
    ```

## Install Allorad Wallet

- **Clone the Repository and Build the Wallet**: 

    ```bash
    git clone https://github.com/allora-network/allora-chain.git
    cd allora-chain && make all
    allorad version
    ```

## Create a Wallet and Obtain Test Tokens

- **Create a Wallet**: Generate a new wallet and save the mnemonic phrase.

    ```bash
    allorad keys add wallet
    ```

- **Import to Keplr**: Import the mnemonic phrase into Keplr.

- **Connect to the Allora Dashboard**: Use the [Allora Dashboard](https://app.allora.network?ref=eyJyZWZlcnJlcl9pZCI6IjVkNDgxNzNiLTQ2NDItNDM2ZS1iOTkyLTg0Njg2NDFjMTQwMCJ9) with Keplr.

- **Add Allora Chain to Keplr**: Use [this link](https://explorer.edgenet.allora.network/wallet/suggest) to add the Allora chain to Keplr.

- **Get Faucet Tokens**: Obtain test tokens from the [faucet](https://faucet.testnet-1.testnet.allora.network/).

## Install & Run Worker

- **Clone the Worker Repository**:

    ```bash
    cd $HOME
    git clone https://github.com/allora-network/allora-huggingface-walkthrough
    cd allora-huggingface-walkthrough
    ```

- **Prepare the Worker Directory**:

    ```bash
    mkdir -p worker-data
    chmod -R 777 worker-data
    ```

- **Configure Seed Phrase**: Replace `SeedPhrase` with your wallet seed phrase.

    ```bash
    curl -O https://raw.githubusercontent.com/adanothe/allora-testnet/main/config.json
    SEED_PHRASE="SeedPhrase"
    sed -i "s/\"addressRestoreMnemonic\": \"[^\"]*\"/\"addressRestoreMnemonic\": \"$SEED_PHRASE\"/" config.json
    ```

- **Create Coingecko API Key**:

    - Create a demo account on [Coingecko](https://www.coingecko.com/en/developers/dashboard).
    
    - Replace `APIKEY` with your Coingecko API key.

    ```bash
    COINGECKO_API_KEY="APIKEY"
    sed -i "s/<Your Coingecko API key>/$COINGECKO_API_KEY/" app.py
    ```

- **Run Huggingface Worker**:

    ```bash
    chmod +x init.config
    ./init.config
    
    docker compose up -d
    ```

- **View Logs**:

    - **Node Logs**:
        Add the following to your bash profile to easily view logs:
        ```bash
        echo 'export WORKER_COMPOSE="$HOME/allora-huggingface-walkthrough/docker-compose.yaml"' >> ~/.bashrc
        source ~/.bashrc
        ```
        To view logs:
        ```bash
        docker compose logs -f --tail=100
        ```

## Points & Leaderboard

You'll receive points on the [Allora Dashboard](https://app.allora.network/points/leaderboard) within the next few hours.

## Follow Adanothe

- **Telegram**: [Join the discussion](https://t.me/adanode)
- **Twitter**: [Follow us on Twitter](https://twitter.com/adano_the)
- **GitHub**: [View our repositories](https://github.com/adanothe)
- **Documentation**: [docs](https://docs.adanothe.com/)
