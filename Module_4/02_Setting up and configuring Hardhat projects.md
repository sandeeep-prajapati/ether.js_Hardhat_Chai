Step 1: Install Hardhat


npm install --save-dev hardhat


Step 2: Create a New Hardhat Project


npx hardhat


Step 3: Configure Hardhat

Create a hardhat.config.js file with the following configuration:


module.exports = {
  solidity: "0.8.0",
  networks: {
    hardhat: {
      chainId: 1337
    }
  }
};


Step 4: Create a Smart Contract

Create a new file contracts/MyContract.sol with the following Solidity code:


pragma solidity ^0.8.0;

contract MyContract {
  function greet() public pure returns (string memory) {
    return "Hello, Hardhat!";
  }
}


Step 5: Compile the Smart Contract

Run the following command to compile the smart contract:


npx hardhat compile


Step 6: Write a Test

Create a new file test/MyContract.test.js with the following JavaScript code:


const { expect } = require("chai");
const { ethers } = require("hardhat");

describe("MyContract", function () {
  it("Should return 'Hello, Hardhat!'", async function () {
    const MyContract = await ethers.getContractFactory("MyContract");
    const myContract = await MyContract.deploy();
    await myContract.deployed();
    expect(await myContract.greet()).to.equal("Hello, Hardhat!");
  });
});


Step 7: Run the Test

Run the following command to run the test:


npx hardhat test


This is a basic example of setting up and configuring a Hardhat project. You can customize the configuration and add more features as needed.