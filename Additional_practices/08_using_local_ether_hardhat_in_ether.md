To use a local Hardhat wallet with `ethers.js`, you need to set up and interact with a Hardhat local blockchain network. This involves configuring Hardhat to run a local Ethereum node and then using `ethers.js` to interact with that node. Here’s a step-by-step guide:

### 1. **Set Up Hardhat**

1. **Initialize a Hardhat Project:**
   If you haven't already set up a Hardhat project, do so by running:

   ```bash
   mkdir hardhat-project
   cd hardhat-project
   npx hardhat
   ```

2. **Install Dependencies:**
   Install the necessary Hardhat packages:

   ```bash
   npm install --save-dev @nomiclabs/hardhat-ethers ethers
   ```

### 2. **Configure Hardhat Network**

1. **Start the Hardhat Local Network:**
   Start the local Hardhat network, which will provide local Ethereum accounts and a local Ethereum blockchain:

   ```bash
   npx hardhat node
   ```

   This command starts a local Ethereum network and provides a list of accounts with their private keys. You’ll use these accounts for testing.

### 3. **Write a Script to Interact with Hardhat Local Network**

1. **Create a Script:**
   Create a script file, e.g., `interact.js`, in the root directory of your Hardhat project:

   ```javascript
   const { ethers } = require("ethers");

   async function main() {
     // Connect to Hardhat local network
     const provider = new ethers.JsonRpcProvider("http://localhost:8545");

     // Use one of the Hardhat provided accounts
     const privateKey = "YOUR_LOCAL_ACCOUNT_PRIVATE_KEY"; // Replace with one of the private keys from `npx hardhat node`
     const wallet = new ethers.Wallet(privateKey, provider);

     // Check wallet balance
     const balance = await wallet.getBalance();
     console.log(`Balance: ${ethers.utils.formatEther(balance)} ETH`);

     // Example transaction
     const tx = {
       to: "0xRecipientAddress", // Replace with a recipient address
       value: ethers.utils.parseEther("0.01"), // Amount of ETH to send
     };

     const txResponse = await wallet.sendTransaction(tx);
     console.log(`Transaction hash: ${txResponse.hash}`);

     // Wait for transaction to be mined
     await txResponse.wait();
     console.log("Transaction confirmed!");
   }

   main().catch(console.error);
   ```

2. **Replace Placeholders:**
   - Replace `YOUR_LOCAL_ACCOUNT_PRIVATE_KEY` with one of the private keys provided when you started the Hardhat local network.
   - Replace `"0xRecipientAddress"` with a valid Ethereum address.

### 4. **Run the Script**

1. **Execute the Script:**
   Run the script using Node.js:

   ```bash
   node interact.js
   ```

   This will connect to the local Hardhat network, check the balance of the account, and optionally send a transaction.

### Summary

1. **Start the Hardhat local network** using `npx hardhat node` to obtain local accounts and private keys.
2. **Create a script** that connects to the local network using `ethers.js` and performs actions such as checking balances or sending transactions.
3. **Run the script** to interact with your local Hardhat blockchain.

By following these steps, you'll be able to use a local Hardhat wallet with `ethers.js` to test and develop smart contracts on your local Ethereum blockchain.