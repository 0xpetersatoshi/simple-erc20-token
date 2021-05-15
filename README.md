# Simple ERC20 Token using Hardhat

This is a simple, barebones ERC20 token along with tests and a deployment script.

## Compiling

```bash
npx hardhat compile
```

## Running tests

```bash
npx hardhat test
```

## Deploying your contract locally

**NOTE**: Before you can run the deploy script, you must first run a local hardhat blockchain network.

In a separate terminal window, run:

```bash
npx hardhat node
```

In another terminal window, run:

```bash
npx hardhat run scripts/deploy.js --network localhost
```

**NOTE**: You will need the contract address in the last step.

## Interacting with your deployed contract

Lastly, to intercat with your contract in a local environment, run:

```bash
npx hardhat console --network localhost
```

And in the console, run:

```javascript
// Instantiate token object and attach to contract address
const Token = await ethers.getContractFactory("PeterToken");
const token = Token.attach("<CONTRACT ADDRESS>");

// Get owner account address and other addresses
const [owner, addr1, addr2, ...addrs] = await ethers.getSigners();
```

Make a transaction:

```javascript
// Get the owner balance and send your first transaction
const ownerBalance = await token.balanceOf(owner.address);

// Use .toString() method to avoid integer overflow errors
console.log(ownerBalance.toString());

// Send some PTK
const tx = await token.transfer(addr1.address, 5000);

// View transaction info
console.log(tx)

// Verify balance of addr1
const addr1Balance = await token.balanceOf(addr1.address);
addr1Balance.toString();
```
