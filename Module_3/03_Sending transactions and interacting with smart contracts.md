### Expanded Guide: Sending Transactions and Interacting with Smart Contracts using **Ethers.js**

In this section, you'll learn how to:
- Send Ether via transactions
- Interact with smart contracts (read data, send transactions)
- Send a transaction with additional data
- Estimate gas for a transaction
- Retrieve a transaction receipt

### 1. **Sending a Transaction (Ether Transfer)**

This basic example demonstrates how to transfer **1 Ether** to another Ethereum address.

```javascript
const tx = await wallet.sendTransaction({
  to: '0xRecipientAddress',  // Replace with the recipient's Ethereum address
  value: ethers.utils.parseEther('1.0')  // Sending 1 Ether
});

console.log(tx.hash);  // Transaction hash, which can be used to track the status
```

### 2. **Interacting with a Smart Contract**

To interact with a deployed smart contract, you'll need the contract's **ABI** (Application Binary Interface) and **address**. This example covers calling a read function and sending a transaction to change the state.

#### 2.1 **Calling a Read-Only Function**

```javascript
const contractAddress = '0xContractAddress';  // Replace with your contract address
const abi = [...];  // Replace with your contract's ABI

// Initialize the contract
const contract = new ethers.Contract(contractAddress, abi, wallet);

// Call a function that returns data
const result = await contract.myFunction();  // Replace with your function
console.log(result);  // Output the result from the smart contract
```

#### 2.2 **Sending a Transaction to a Contract Function**

If you want to change the contract state, for example, sending tokens or triggering an event, you can do this by sending a transaction.

```javascript
const tx = await contract.myFunction('arg1', 'arg2');  // Replace with your function and arguments
console.log(tx.hash);  // Log the transaction hash
```

### 3. **Sending a Transaction with Data**

You can also send a transaction with data to call a specific function from the smart contract without using the contract object directly. This example shows how to encode function data and send it.

```javascript
const tx = await wallet.sendTransaction({
  to: contractAddress,  // Contract address
  data: contract.interface.encodeFunctionData('myFunction', ['arg1', 'arg2'])  // Encode function call with arguments
});

console.log(tx.hash);  // Log the transaction hash
```

### 4. **Estimating Gas**

It's a good practice to estimate the gas needed for a transaction, especially if the function involves complex computations or interactions.

```javascript
const estimatedGas = await contract.estimateGas.myFunction('arg1', 'arg2');  // Replace with your function and args
console.log(estimatedGas.toString());  // Log the estimated gas in units
```

### 5. **Getting a Transaction Receipt**

Once a transaction is sent, you can wait for it to be mined by calling `tx.wait()` and then get the transaction receipt. The receipt contains details such as gas used, block number, etc.

```javascript
const receipt = await tx.wait();  // Wait for the transaction to be confirmed (mined)
console.log(receipt);  // Log the transaction receipt details
```

### Summary:
This guide walks you through:
1. Sending basic Ether transactions.
2. Interacting with smart contracts via function calls and state-changing transactions.
3. Sending transactions with encoded data directly.
4. Estimating gas to predict transaction costs.
5. Retrieving and inspecting transaction receipts.

**Note:** Remember to replace placeholders like `YOUR_PRIVATE_KEY`, `contractAddress`, and `abi` with actual values from your setup. This code is based on using **Ethers.js** for interacting with Ethereum, Infura, or another Ethereum provider.