### Printing Local Miner and Its Amount in Hardhat

Hardhat is an Ethereum development environment that allows you to deploy, test, and interact with smart contracts. To print information like the local miner and its amount, we typically interact with the network via scripts or tasks in Hardhat. Here's how you can go about it.

#### 1. **Installing Hardhat**
Make sure you have Hardhat installed. In your project directory, run:
```bash
npm install --save-dev hardhat
```

#### 2. **Configuring the Local Network**
In your `hardhat.config.js`, set up a local network (Hardhat comes with a default network configuration for a local environment):
```javascript
module.exports = {
  solidity: "0.8.4",
  networks: {
    hardhat: {
      mining: {
        auto: true,
      }
    }
  }
};
```

#### 3. **Creating a Script to Print Miner and Its Amount**
Now, create a script to print the miner address and the amount of Ether (or gas fee) it receives. Here's an example of how you might do this:

```javascript
const { ethers } = require("hardhat");

async function main() {
  // Get the list of accounts
  const accounts = await ethers.getSigners();
  
  // Select the miner's account (in local Hardhat network, it's usually the first account)
  const miner = accounts[0];
  
  // Get the balance of the miner
  const balance = await miner.getBalance();
  
  console.log("Miner address:", miner.address);
  console.log("Miner balance:", ethers.utils.formatEther(balance), "ETH");
}

main().catch((error) => {
  console.error(error);
  process.exitCode = 1;
});
```

#### 4. **Running the Script**
To run the script, you can use Hardhat's built-in task runner:
```bash
npx hardhat run scripts/printMiner.js --network hardhat
```

This script will print the miner's address and balance in Ether.

#### 5. **Additional Information**
- **Auto-mining:** In the Hardhat local environment, mining is done automatically when you send transactions.
- **Mining Rewards:** In a real network, miners get block rewards and transaction fees, but in the Hardhat local network, mining is simulated.

You can use this approach to get the miner's information and print it on the console or store it for further analysis.

---
