# Add non-validator node (mainnet)

1. Requirements: Linux: tested on Ubuntu and Debian. 

---
description:
  Setup a non-validator node.
  To become a validator, node must get votes from at least 2/3 of current validators.
---

# OneNG Node Setup

## Run the following combined command. You can divide it in to commands:
sudo apt update

## Install screen:
sudo apt install screen

## Setup Java:
sudo apt install default-jre default-jdk

## Download latest OneNG client Hyperledger Besu (check for new versions if necessary)
wget https://hyperledger.jfrog.io/artifactory/besu-binaries/besu/22.1.1/besu-22.1.1.zip

## Install Unzip, if not already installed:
sudo apt install unzip

## Unzip the file, and rename it for ease:
sudo unzip besu-22.1.1.zip; sudo mv besu-22.1.1 .ongc

## Add environment so you can run OneNG client from anywhere:
sudo nano ~/.bashrc

## Add the following line to the end of the file. Make sure to put your username:
export PATH=/home/YOUR_USERNAME/.ongc/bin:$PATH

## Relaod bashrc file:
source ~/.bashrc

## Create a directory structure like this:
mkdir -p ongc/node01/data
cd ongc

## Create the genesis file, and paste the contents from the genesis file into it:
# Genesis File: https://github.com/OneNGchain/blockchain-files/blob/master/documentation/genesis.json
sudo nano genesis.json
   ( Save using Ctrl + O , then exit with Ctrl + x )
   
## create static-node.json file and paste the contents of static-nodes file into it:
# Static-nodes: https://github.com/OneNGchain/blockchain-files/blob/master/documentation/static-node.json
sudo nano static-nodes.json
   ( Save using Ctrl + O , then exit with Ctrl + x )

## Create a file called node-config.toml in node01 folder. Paste contents of config.toml into it:
# Config File: https://github.com/OneNGchain/blockchain-files/blob/master/documentation/node-config.toml
cd node01
sudo nano node-config.toml

## Run screen, to keep node running if you close the terminal:
screen , then hit Enter key.

## Run OneNG client from node01 folder:
besu --config-file=config.toml

## When the node runs, exit the current screen so it's safe if you close the terminal:
Press Ctrl + A , then press C . 
Now you can either close the terminal window, or work on other processes.

It should start synchronization in few moments, or minutes. Depending on your machine.

# To run more than one node on the same machine, you must set different port numbers in config.toml per each node. 

# Default ports used:
rpc-http-port=8545
rpc-ws-port=8546
graphql-http-port=8547
metrics-port=9545
p2p-port=30303

# To use WEB3 API, make sure WEB3 is enabled. This is the default setting in config.toml
