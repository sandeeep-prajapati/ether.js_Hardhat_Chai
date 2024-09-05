
Project: A simple ERC-20 token contract

Tools:

- Chai for testing
- Ethers.js for interacting with the Ethereum blockchain
- Hardhat for building, testing, and deploying the contract

Contract Code:

// contracts/MyToken.sol
pragma solidity ^0.8.0;

contract MyToken {
  mapping(address => uint256) public balances;
  uint256 public totalSupply;

  constructor() {
    totalSupply = 1000000;
    balances[msg.sender] = totalSupply;
  }

  function transfer(address recipient, uint256 amount) public {
    require(balances[msg.sender] >= amount, "Insufficient balance");
    balances[msg.sender] -= amount;
    balances[recipient] += amount;
  }

  function balanceOf(address account) public view returns (uint256) {
    return balances[account];
  }
}


Test Code:

// test/MyToken.test.js
const { expect } = require("chai");
const { ethers } = require("hardhat");

describe("MyToken", function () {
  it("Should have the correct total supply", async function () {
    const MyToken = await ethers.getContractFactory("MyToken");
    const myToken = await MyToken.deploy();
    await myToken.deployed();
    expect(await myToken.totalSupply()).to.equal(1000000);
  });

  it("Should transfer tokens correctly", async function () {
    const MyToken = await ethers.getContractFactory("MyToken");
    const myToken = await MyToken.deploy();
    await myToken.deployed();
    const recipient = "0x1234567890123456789012345678901234567890";
    await myToken.transfer(recipient, 100);
    expect(await myToken.balanceOf(recipient)).to.equal(100);
  });
});


Deployment Script:

// scripts/deploy.js
const { ethers } = require("hardhat");

async function main() {
  const MyToken = await ethers.getContractFactory("MyToken");
  const myToken = await MyToken.deploy();
  await myToken.deployed();
  console.log("MyToken deployed to:", myToken.address);
}

main();


This example demonstrates how to build, test, and deploy a simple ERC-20 token contract using Chai, Ethers.js, and Hardhat. The contract has two functions: transfer and balanceOf. The test code uses Chai to write tests for these functions, and the deployment script uses Hardhat to deploy the contract to the Ethereum blockchain.