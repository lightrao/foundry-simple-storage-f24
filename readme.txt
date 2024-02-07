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

5.replace the files in script, src, test with the repository's:
DeploySimpleStorage.s.sol 
SimpleStorage.sol 
SimpleStorageTest.t.sol 

6.Compiling in Foundry
forge compile 

7.Deploying to a local chain I (Anvil):
want a eth vm, run:
anvil 
use ctrl+c to quit it 

8.Adding another network to Metamask(Anvil):
Network name: Localhost 
RPC URL: http://127.0.0.1:8545
Chain ID: 31337 
Currency symbol: ETH 
Block explorer URL: null

9.Adding anvil account to Metamask:
copy private key and import it to Metamask








