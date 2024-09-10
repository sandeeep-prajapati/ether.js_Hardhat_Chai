To get all past events from a smart contract and filter the data using `ethers.js` on a testnet, follow these steps:

### 1. **Set Up the Environment**

1. **Install `ethers.js`:**
   If you haven’t already, install `ethers.js`:

   ```bash
   npm install ethers
   ```

2. **Obtain Infura URL and Contract Details:**
   - **Infura URL:** Get your Infura project URL for the testnet (e.g., Ropsten, Goerli).
   - **Contract Address:** The address where your smart contract is deployed.
   - **ABI (Application Binary Interface):** The ABI defines the methods and events of your contract.

### 2. **Write a Script to Fetch and Filter Past Events**

1. **Create a Script File:**
   Create a file named `fetchEvents.js`:

   ```javascript
   const { ethers } = require("ethers");
   require("dotenv").config();

   // Infura URL (replace YOUR_INFURA_PROJECT_ID with your actual Infura Project ID)
   const infuraUrl = `https://ropsten.infura.io/v3/${process.env.INFURA_PROJECT_ID}`;
   const provider = new ethers.JsonRpcProvider(infuraUrl);

   // Replace with your smart contract address
   const contractAddress = "0xYourContractAddress";

   // Replace with your smart contract ABI
   const contractABI = [
     "event ValueChanged(uint256 oldValue, uint256 newValue)",
     // Add other events from your contract ABI here
   ];

   async function main() {
     // Create a contract instance
     const contract = new ethers.Contract(contractAddress, contractABI, provider);

     // Define the filter (example: filter for ValueChanged events)
     const filter = contract.filters.ValueChanged();

     // Fetch past events
     try {
       const events = await contract.queryFilter(filter);
       console.log("Past events:");

       // Process and filter the events
       events.forEach(event => {
         console.log(`Block Number: ${event.blockNumber}`);
         console.log(`Transaction Hash: ${event.transactionHash}`);
         console.log(`Old Value: ${event.args.oldValue.toString()}`);
         console.log(`New Value: ${event.args.newValue.toString()}`);
         console.log("--------");
       });
     } catch (error) {
       console.error("Error fetching events:", error);
     }
   }

   main().catch(console.error);
   ```

   - **Replace `YOUR_INFURA_PROJECT_ID`** with your actual Infura Project ID.
   - **Replace `0xYourContractAddress`** with your deployed smart contract address.
   - **Update the ABI** array with the ABI of your contract. The example ABI includes a `ValueChanged` event for illustration.

2. **Create a `.env` File:**
   Store sensitive information in a `.env` file:

   ```
   INFURA_PROJECT_ID=YOUR_INFURA_PROJECT_ID
   ```

   Ensure `.env` is included in your `.gitignore` file to keep it secure.

3. **Run the Script:**
   Execute the script using Node.js:

   ```bash
   node fetchEvents.js
   ```

   This will print out all past `ValueChanged` events from the smart contract, along with the block number, transaction hash, old value, and new value.

### Summary

1. **Set up Infura** and obtain contract details such as address and ABI.
2. **Install `ethers.js`** and write a script to fetch past events.
3. **Define filters** based on the events you are interested in.
4. **Run the script** to fetch and process past events from your smart contract.

This approach will allow you to retrieve and filter past events from a smart contract deployed on a testnet using `ethers.js` and Infura.