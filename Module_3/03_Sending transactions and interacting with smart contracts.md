Sending a Transaction


const tx = await wallet.sendTransaction({
  to: '0x...',
  value: ethers.utils.parseEther('1.0')
});
console.log(tx.hash);


Interacting with a Smart Contract


const contractAddress = '0x...';
const abi = [...];
const contract = new ethers.Contract(contractAddress, abi, wallet);

// Call a function
const result = await contract.myFunction();
console.log(result);

// Send a transaction to a function
const tx = await contract.myFunction('arg1', 'arg2');
console.log(tx.hash);


Sending a Transaction with Data


const tx = await wallet.sendTransaction({
  to: contractAddress,
  data: contract.interface.encodeFunctionData('myFunction', ['arg1', 'arg2'])
});
console.log(tx.hash);


Estimating Gas


const estimatedGas = await contract.estimateGas.myFunction('arg1', 'arg2');
console.log(estimatedGas);


Getting a Transaction Receipt


const receipt = await tx.wait();
console.log(receipt);


This example demonstrates how to:

1. Send a transaction
2. Interact with a smart contract (call a function and send a transaction)
3. Send a transaction with data
4. Estimate gas
5. Get a transaction receipt

Note: Replace YOUR_PROJECT_ID, YOUR_PRIVATE_KEY, and 0x... with your actual Infura project ID, private key, and contract addresses.