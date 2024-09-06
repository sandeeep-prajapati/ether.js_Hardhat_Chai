Here’s a comprehensive guide on how to use **Ethers.js** with **Hardhat** for writing, testing, and deploying smart contracts:

### 1. Install Ethers.js

First, you need to install **Ethers.js**. Run the following command in your project directory:

```bash
npm install ethers
```

### 2. Create a Hardhat Project

Initialize a new Hardhat project using the command:

```bash
npx hardhat
```

Follow the prompts to create a basic sample project. This will set up the necessary directory structure and configuration files.

### 3. Create a Smart Contract

Create a Solidity smart contract in the `contracts/` directory. For example, create a file named `MyContract.sol`:

```solidity
// contracts/MyContract.sol
pragma solidity ^0.8.0;

contract MyContract {
  function greet() public pure returns (string memory) {
    return "Hello, Hardhat!";
  }
}
```

### 4. Create a Test with Ethers.js

Create a test file in the `test/` directory to test the functionality of your smart contract. For example, create `MyContract.test.js`:

```javascript
// test/MyContract.test.js
const { expect } = require("chai");
const { ethers } = require("hardhat");

describe("MyContract", function () {
  it("Should return 'Hello, Hardhat!'", async function () {
    // Get the contract factory
    const MyContract = await ethers.getContractFactory("MyContract");
    
    // Deploy the contract
    const myContract = await MyContract.deploy();
    await myContract.deployed();
    
    // Test the greet function
    expect(await myContract.greet()).to.equal("Hello, Hardhat!");
  });
});
```

In this test:
- **Ethers.js** is used to interact with the Ethereum network and deploy the contract.
- The `greet()` function of the contract is tested to ensure it returns "Hello, Hardhat!".

### 5. Run the Test

Execute the following command to run your tests:

```bash
npx hardhat test
```

This command will execute all test files in the `test/` directory and display the results.

### 6. Create a Script to Deploy the Contract with Ethers.js

Create a deployment script in the `scripts/` directory. For example, create `deploy.js`:

```javascript
// scripts/deploy.js
const { ethers } = require("hardhat");

async function main() {
  // Get the contract factory
  const MyContract = await ethers.getContractFactory("MyContract");
  
  // Deploy the contract
  const myContract = await MyContract.deploy();
  await myContract.deployed();
  
  // Log the contract address
  console.log("Contract deployed to:", myContract.address);
}

// Execute the deployment script
main().catch((error) => {
  console.error(error);
  process.exitCode = 1;
});
```

### 7. Run the Deployment Script

To deploy the contract, run the following command:

```bash
npx hardhat run scripts/deploy.js
```

This script will deploy your contract to the local Hardhat network and print the deployed contract's address.

### Summary:

- **Install Ethers.js**: `npm install ethers`
- **Create a Hardhat Project**: `npx hardhat`
- **Create a Contract**: Add Solidity code to `contracts/`
- **Create a Test**: Write JavaScript tests using **Chai** and **Ethers.js** in `test/`
- **Run the Test**: `npx hardhat test`
- **Create a Deployment Script**: Use **Ethers.js** to deploy the contract in `scripts/`
- **Run the Deployment Script**: `npx hardhat run scripts/deploy.js`

You now have a complete setup for writing, testing, and deploying smart contracts using Hardhat and Ethers.js! If you have further questions or need additional features, feel free to ask.