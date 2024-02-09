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
use .env file to store private key used for deploying(.gitignre should include .env)
edit .env and then run:
source .env 
echo $FIRST_ANVIL_PRIVATE_KEY
forge script script/DeploySimpleStorage.s.sol --private-key $FIRST_ANVIL_PRIVATE_KEY --rpc-url $ANVIL_RPC_URL --broadcast

use keystore in foundry
store:
cast wallet import BOB --interactive
Enter private key:
Enter password:
BOB keystore was saved successfully. Address: <address-corresponding-to-private-key>
use:
forge script script/DeploySimpleStorage.s.sol --rpc-url $ANVIL_RPC_URL --account BOB --sender <address-corresponding-to-private-key> --broadcast

15.ThirdWeb Deploy
deploy contract just run:
curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.39.7/install.sh | bash
nvm install node
npx thirdweb deploy
then do some operation with your browser and Metamask.

16.Cast Send
interact with deployed contract from command line:
cast send <Contract Address> "store(uint256)" 123 --private-key $FIRST_ANVIL_PRIVATE_KEY --rpc-url $ANVIL_RPC_URL
cast call 0x5FbDB2315678afecb367f032d93F642f64180aa3 "retrieve()"
cast --to-base 0x000000000000000000000000000000000000000000000000000000000000007b dec

17.Deploying to a testnet or a mainnet
node as a service: https://www.alchemy.com/
sign in alchemy wiht google account
create new app, choose network sepolia, name and description is sepolia test 
click API key, we can see HTTPS endpoint, add it to .env as SEPOLIA_RPC_URL
from Metamask export private key add it to .env as SEPOLIA_PRIVATE_KEY, you can get some sepolia eth from faucet and send them to corresponding account
in command line run:
source .env 
forge script script/DeploySimpleStorage.s.sol --private-key $SEPOLIA_PRIVATE_KEY --rpc-url $SEPOLIA_RPC_URL --broadcast

18.Verifying a contract the manual way
go to: https://sepolia.etherscan.io/
look up the contract you just deployed 
click Contract and then Verify and publish
choose compiler type is Solidity(Single file)
choose compiler version is v0.8.19
choose opensource license is MIT 
click continue
copy past source code of the contract be deployed 
give constructor arguments if have any 
click verify and publish

19.Cleaning up the project
format code run:
forge fmt
edit README.md 

20.Alchemy & the mempool
Create App 
view dashboard
view mempool
watch dod and tutorials

21.Summary













