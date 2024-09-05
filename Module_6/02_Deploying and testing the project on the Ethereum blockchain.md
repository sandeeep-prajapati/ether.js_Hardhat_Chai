To deploy and test the project on the Ethereum blockchain, follow these steps:

1. Compile the contract: Use Hardhat to compile the contract by running npx hardhat compile in the terminal.

2. Deploy the contract: Use Hardhat to deploy the contract to the Ethereum blockchain by running npx hardhat run scripts/deploy.js in the terminal.

3. Test the contract: Use Hardhat to test the contract by running npx hardhat test in the terminal.

4. Verify the contract: Use Etherscan to verify the contract by following these steps:
    - Go to Etherscan and search for the contract address.
    - Click on the "Verify and Publish" button.
    - Select the contract source code and compiler version.
    - Click on the "Verify and Publish" button.

5. Interact with the contract: Use Ethers.js to interact with the contract by following these steps:
    - Import the contract ABI and address.
    - Use the ethers.getContractAt method to get the contract instance.
    - Call the contract functions using the contract instance.

Example code to interact with the contract:

const { ethers } = require("ethers");

const contractAddress = "0x...";
const contractABI = [...];

const provider = new ethers.providers.JsonRpcProvider("(link unavailable)");
const contract = new ethers.Contract(contractAddress, contractABI, provider);

async function main() {
  const result = await contract.balanceOf("0x...");
  console.log(result);
}

main();

Note: Replace YOUR_PROJECT_ID with your actual Infura project ID.