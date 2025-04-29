# Akash-Network
Akash-Network
Install Prerequisites bash Copy Edit
Install Go (if you don't have it)
Make sure it's Go 1.21 or newer
sudo apt update sudo apt install -y golang gcc g++ make curl git

Confirm Go version
go version 2. Set Up Environment Variables bash Copy Edit

Set Go environment (if not already)
export GOPATH=$HOME/go export PATH=$PATH:$GOPATH/bin

Optionally add these lines to your ~/.bashrc or ~/.zshrc
echo 'export GOPATH=$HOME/go' >> ~/.bashrc echo 'export PATH=$PATH:$GOPATH/bin' >> ~/.bashrc source ~/.bashrc 3. Clone Akash Source Code bash Copy Edit

Clone the Akash node repo
git clone https://github.com/akash-network/node.git

Go inside the repo
cd node 4. Build Akash Binary bash Copy Edit

Build using Makefile
make akash

The akash binary will be placed in .cache/bin/akash
You can also move it to /usr/local/bin if you want system-wide access
sudo cp .cache/bin/akash /usr/local/bin/ ✅ Now you have the akash binary ready!

Initialize a Local Node bash Copy Edit
Initialize your local node (replace 'mynode' with any name you like)
akash init mynode --chain-id localnet This creates .akash folder in your home directory with configs.

Configure Your Node bash Copy Edit
Create a local validator account
akash keys add validator --keyring-backend test

Get the validator's address
VALIDATOR_ADDR=$(akash keys show validator -a --keyring-backend test)

Add genesis account
akash add-genesis-account "$VALIDATOR_ADDR" 1000000000uakt --keyring-backend test

Generate genesis transaction
akash gentx validator 100000000uakt --chain-id localnet --keyring-backend test

Collect all gentxs
akash collect-gentxs 7. Run the Node 🎯 bash Copy Edit

Start the Akash blockchain node
akash start It will start syncing, and you should see log output like:

css Copy Edit I[2025-04-28|14:32:01.123] Starting ABCI with Tendermint 🎉 You now have a local Akash blockchain node running!

⚡ Bonus: Helpful Tips Your local config files are in ~/.akash/

If you want to reset the chain and start fresh:

bash Copy Edit akash tendermint unsafe-reset-all Default ports used:

RPC: 26657

P2P: 26656

You can use akash query and akash tx commands to interact with the chain.

🚀 Quick Summary Flow: bash Copy Edit

Install deps ➔ clone repo ➔ make akash ➔ init node ➔ add keys ➔ start node
