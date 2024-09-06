This is a solid example of an ERC-20 token contract, along with testing and deployment scripts. Here are a few suggestions and improvements:

### 1. **Contract Enhancements**

To fully comply with the ERC-20 standard, consider adding the following functions and events:

- **Events**: `Transfer` and `Approval` events.
- **Allowance** and **approve** functions for handling token allowances.

Here's an updated version of the contract with these enhancements:

```solidity
// contracts/MyToken.sol
pragma solidity ^0.8.0;

contract MyToken {
    mapping(address => uint256) public balances;
    mapping(address => mapping(address => uint256)) public allowances;
    uint256 public totalSupply;

    constructor() {
        totalSupply = 1000000;
        balances[msg.sender] = totalSupply;
    }

    function transfer(address recipient, uint256 amount) public returns (bool) {
        require(balances[msg.sender] >= amount, "Insufficient balance");
        balances[msg.sender] -= amount;
        balances[recipient] += amount;
        emit Transfer(msg.sender, recipient, amount);
        return true;
    }

    function balanceOf(address account) public view returns (uint256) {
        return balances[account];
    }

    function approve(address spender, uint256 amount) public returns (bool) {
        allowances[msg.sender][spender] = amount;
        emit Approval(msg.sender, spender, amount);
        return true;
    }

    function transferFrom(address sender, address recipient, uint256 amount) public returns (bool) {
        require(balances[sender] >= amount, "Insufficient balance");
        require(allowances[sender][msg.sender] >= amount, "Allowance exceeded");
        balances[sender] -= amount;
        balances[recipient] += amount;
        allowances[sender][msg.sender] -= amount;
        emit Transfer(sender, recipient, amount);
        return true;
    }

    // Events
    event Transfer(address indexed from, address indexed to, uint256 value);
    event Approval(address indexed owner, address indexed spender, uint256 value);
}
```

### 2. **Test Code Enhancements**

To test the new functions and events, you can add more tests:

```javascript
// test/MyToken.test.js
const { expect } = require("chai");
const { ethers } = require("hardhat");

describe("MyToken", function () {
  let MyToken;
  let myToken;
  let owner;
  let addr1;
  let addr2;

  beforeEach(async function () {
    MyToken = await ethers.getContractFactory("MyToken");
    [owner, addr1, addr2] = await ethers.getSigners();
    myToken = await MyToken.deploy();
    await myToken.deployed();
  });

  it("Should have the correct total supply", async function () {
    expect(await myToken.totalSupply()).to.equal(1000000);
  });

  it("Should transfer tokens correctly", async function () {
    await myToken.transfer(addr1.address, 100);
    expect(await myToken.balanceOf(addr1.address)).to.equal(100);
  });

  it("Should emit Transfer event on transfer", async function () {
    await expect(myToken.transfer(addr1.address, 100))
      .to.emit(myToken, "Transfer")
      .withArgs(owner.address, addr1.address, 100);
  });

  it("Should approve and allow transferFrom", async function () {
    await myToken.approve(addr1.address, 50);
    expect(await myToken.allowances(owner.address, addr1.address)).to.equal(50);
    await myToken.connect(addr1).transferFrom(owner.address, addr2.address, 50);
    expect(await myToken.balanceOf(addr2.address)).to.equal(50);
    expect(await myToken.allowances(owner.address, addr1.address)).to.equal(0);
  });

  it("Should emit Approval event on approve", async function () {
    await expect(myToken.approve(addr1.address, 50))
      .to.emit(myToken, "Approval")
      .withArgs(owner.address, addr1.address, 50);
  });
});
```

### 3. **Deployment Script**

Your deployment script looks good, but you may want to add error handling to manage deployment issues gracefully:

```javascript
// scripts/deploy.js
const { ethers } = require("hardhat");

async function main() {
  try {
    const MyToken = await ethers.getContractFactory("MyToken");
    const myToken = await MyToken.deploy();
    await myToken.deployed();
    console.log("MyToken deployed to:", myToken.address);
  } catch (error) {
    console.error("Error deploying contract:", error);
  }
}

main();
```

### Summary

- **Contract**: Added ERC-20 standard functions and events.
- **Tests**: Expanded to cover new functions and event emissions.
- **Deployment**: Included basic error handling.

These additions ensure that your ERC-20 token contract is compliant with the standard and robust against various scenarios.