Installing Ethers.js


npm install ethers


Importing Ethers.js


const ethers = require('ethers');


Provider


const provider = new ethers.providers.JsonRpcProvider('(link unavailable)');


Wallet


const wallet = new ethers.Wallet('YOUR_PRIVATE_KEY', provider);


Contract


const contractAddress = '0x...';
const abi = [...];
const contract = new ethers.Contract(contractAddress, abi, wallet);


Sending a Transaction


const tx = await contract.myFunction();
console.log(tx.hash);


Querying Data


const data = await contract.myFunction();
console.log(data);


Transfering Ether


const tx = await wallet.sendTransaction({
  to: '0x...',
  value: ethers.utils.parseEther('1.0')
});
console.log(tx.hash);


This example demonstrates how to:

1. Install and import Ethers.js
2. Set up a provider (Infura)
3. Create a wallet
4. Interact with a contract (send a transaction and query data)
5. Transfer Ether

Note: Replace YOUR_PROJECT_ID, YOUR_PRIVATE_KEY, and 0x... with your actual Infura project ID, private key, and contract addresses.