Install Ethers.js


npm install ethers


Create a Hardhat project


npx hardhat


Create a contract


// contracts/MyContract.sol
pragma solidity ^0.8.0;

contract MyContract {
  function greet() public pure returns (string memory) {
    return "Hello, Hardhat!";
  }
}


Create a test with Ethers.js


// test/MyContract.test.js
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


Run the test


npx hardhat test


Create a script to deploy the contract with Ethers.js


// scripts/deploy.js
const { ethers } = require("hardhat");

async function main() {
  const MyContract = await ethers.getContractFactory("MyContract");
  const myContract = await MyContract.deploy();
  await myContract.deployed();
  console.log("Contract deployed to:", myContract.address);
}

main();


Run the script


npx hardhat run scripts/deploy.js


This example demonstrates how to use Ethers.js with Hardhat to write, test, and deploy a smart contract. You can use Ethers.js to interact with the contract and perform various tasks, such as sending transactions and querying data.