1.install vscode

2.install git 
ubuntu:
sudo apt install git-all
macOS:
git --version

3.install foundry
a. go to:
https://getfoundry.sh/
b. copy and run
curl -L https://foundry.paradigm.xyz | bash
c. in new terminal run:
foundryup

4.local development setup
a. install vscode extention
Hardhat Solidity Extension
Prettier
Git History
Even Better TOML
Markdown Preview Enhanced
b. run:
mkdir foundry-simple-storage-f24
cd foundry-simple-storage-f24
code .
forge init

5.replace the files in script, src, test with the repository's
DeploySimpleStorage.s.sol 
SimpleStorage.sol 
SimpleStorageTest.t.sol 

6.Compiling in Foundry
forge compile 

7.Deploying to a local chain I (Anvil)
want a eth vm, run:
anvil 
use ctrl+c to quit it 

8.Adding another network to Metamask(Anvil)
Network name: Localhost 
RPC URL: http://127.0.0.1:8545
Chain ID: 31337 
Currency symbol: ETH 
Block explorer URL: null

9.Adding anvil account to Metamask
copy private key and import it to Metamask


10.Deploying to a local chain II (Forge Create)
run one of the following:
forge create SimpleStorage --interactive
forge create SimpleStorage --private-key <PRIVATE_KEY> --rpc-url http://127.0.0.1:8545

11.Private Key Rant I
to clear private key in shell, run:
history -c 
We can get RPC URL of any chain for free using Alchemy.

12.Deploying to a local chain III (Forge Script)
create script file and then run:
forge script script/DeploySimpleStorage.s.sol
forge script script/DeploySimpleStorage.s.sol --private-key <PRIVATE_KEY> --rpc-url http://127.0.0.1:8545 --broadcast 

13.What is a transaction (But actually)
deploy a contract is also a transaction, so you can give it value
Transactions saved to: /home/parallels/LightTechZen/Patrick/foundry-simple-storage-f24/broadcast/DeploySimpleStorage.s.sol/31337/run-latest.json
watch transaction information broadcasted to chain: transactions->transaction
check gas used in decimal, run:
cast --to-base 0x714e1 dec
v,r,s are values for the transaction's signature
when we send transaction, we sign it and then broadcast it
nonce show a same account send same transaction how many times
data field contains opcodes

14.Private Key Rant II



