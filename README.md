# Foundry Simple Storage

## 1. Install Visual Studio Code

## 2. Install Git

- **Ubuntu:**
  ```
  sudo apt install git-all
  ```
- **macOS:**
  ```
  git --version
  ```

## 3. Install Foundry

- **a.** Go to [Foundry's website](https://getfoundry.sh/).
- **b.** Copy and run:
  ```
  curl -L https://foundry.paradigm.xyz | bash
  ```
- **c.** In a new terminal, run:
  ```
  foundryup
  ```

## 4. Local Development Setup

- **a.** Install VSCode extensions:
  - Hardhat Solidity Extension
  - Prettier
  - Git History
  - Even Better TOML
  - Markdown Preview Enhanced
- **b.** Run:
  ```
  mkdir foundry-simple-storage-f24
  cd foundry-simple-storage-f24
  code .
  forge init
  ```

## 5. Replace Files

Replace the files in `script`, `src`, `test` with the current repository's files:

- `DeploySimpleStorage.s.sol`
- `SimpleStorage.sol`
- `SimpleStorageTest.t.sol`

## 6. Compiling in Foundry

```
forge compile
```

## 7. Deploying to a Local Chain I (Anvil)

- For an Ethereum VM, run:
  ```
  anvil
  ```
  Use `ctrl+c` to quit.

## 8. Adding Another Network to Metamask (Anvil)

- Network name: Localhost
- RPC URL: http://127.0.0.1:8545
- Chain ID: 31337
- Currency symbol: ETH
- Block explorer URL: null

## 9. Adding Anvil Account to Metamask

Copy the private key and import it to Metamask.

## 10. Deploying to a Local Chain II (Forge Create)

Run one of the following:

```
forge create SimpleStorage --interactive
forge create SimpleStorage --private-key <PRIVATE_KEY> --rpc-url http://127.0.0.1:8545
```

## 11. Private Key Rant I

To clear the private key in shell, run:

```
history -c
```

We can get the RPC URL of any chain for free using Alchemy.

## 12. Deploying to a Local Chain III (Forge Script)

Create a script file for deploying and then run:

```
forge script script/DeploySimpleStorage.s.sol
forge script script/DeploySimpleStorage.s.sol --private-key <PRIVATE_KEY> --rpc-url http://127.0.0.1:8545 --broadcast
```

## 13. What is a Transaction (But Actually)

Deploying a contract is also a transaction, so you can give it value. Transactions are saved to `/home/parallels/LightTechZen/Patrick/foundry-simple-storage-f24/broadcast/DeploySimpleStorage.s.sol/31337/run-latest.json`. For transaction information broadcasted to the chain, check `run-latest.json` file: `transactions->transaction`. To check gas used in decimal, run:

```
cast --to-base 0x714e1 dec
```

`v`, `r`, `s` are values for the transaction's signature. The `nonce` shows how many times the same account sent the same transaction. The `data` field contains opcodes.

## 14. Private Key Rant II

Use a `.env` file to store the private key used for deploying (.gitignore should include `.env`). Edit `.env` and then run:

```
source .env
echo $FIRST_ANVIL_PRIVATE_KEY
forge script script/DeploySimpleStorage.s.sol --private-key $FIRST_ANVIL_PRIVATE_KEY --rpc-url $ANVIL_RPC_URL --broadcast
```

Use keystore in foundry to store:

```
cast wallet import BOB --interactive
```

Enter the private key and password. Then use:

```
forge script script/DeploySimpleStorage.s.sol --rpc-url $ANVIL_RPC_URL --account BOB --sender <address-corresponding-to-private-key> --broadcast
```

## 15. ThirdWeb Deploy

To deploy the contract, run:

```
curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.39.7/install.sh | bash
nvm install node
npx thirdweb deploy
```

Then perform some operations with your browser and Metamask.

## 16. Cast Send

Interact with a deployed contract from the command line:

```
cast send <Contract Address> "store(uint256)" 123 --private-key $FIRST_ANVIL_PRIVATE_KEY --rpc-url $ANVIL_RPC_URL
cast call 0x5FbDB2315678afecb367f032d93F642f64180aa3 "retrieve()"
cast --to-base 0x000000000000000000000000000000000000000000000000000000000000007b dec
```

## 17. Deploying to a Testnet or Mainnet

Use node as a service: [Alchemy](https://www.alchemy.com/). Sign in with a Google account and create a new app. Choose the network (e.g., Sepolia), name, and description. Click the API key to see the HTTPS endpoint. Add it to `.env` as `SEPOLIA_RPC_URL`. Export a private key from Metamask and add it to `.env` as `SEPOLIA_PRIVATE_KEY`. You can get some Sepolia ETH from a faucet and send them to the corresponding account. In the command line, run:

```
source .env
forge script script/DeploySimpleStorage.s.sol --private-key $SEPOLIA_PRIVATE_KEY --rpc-url $SEPOLIA_RPC_URL --broadcast
```

## 18. Verifying a Contract the Manual Way

Go to [Sepolia Etherscan](https://sepolia.etherscan.io/). Look up the contract you just deployed, click 'Contract', then 'Verify and Publish'. Choose the compiler type as Solidity (Single file), the compiler version as v0.8.19, and the opensource license as MIT. Copy-paste the source code of the contract to be deployed. Provide constructor arguments if any. Click 'Verify and Publish'.

## 19. Cleaning Up the Project

To format code, run:

```
forge fmt
```

Edit `README.md` to inform the reader what the project is used for.

## 20. Alchemy & the Mempool

- Create App
- View Dashboard
- View Mempool
- Watch Docs and Tutorials

## 21. Summary
