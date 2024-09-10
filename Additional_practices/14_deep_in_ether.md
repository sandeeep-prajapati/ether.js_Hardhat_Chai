To call a smart contract function using React, `ethers.js`, and `JsonRpcProvider` or `Web3Provider`, follow these steps. This example demonstrates how to interact with a smart contract using both `JsonRpcProvider` (for read-only interactions) and `Web3Provider` (for user interactions).

### 1. **Set Up Your React Project**

If you don’t have a React project set up yet, create one using Create React App:

```bash
npx create-react-app my-ethereum-app
cd my-ethereum-app
```

### 2. **Install Dependencies**

Install `ethers.js` for interacting with the Ethereum blockchain:

```bash
npm install ethers
```

### 3. **Create a Component to Call a Smart Contract Function**

Here's a React component that demonstrates how to call a smart contract function using both `JsonRpcProvider` and `Web3Provider`.

1. **Create the Component:**

   - Create a file named `CallContract.js` in the `src` directory:

   ```javascript
   // src/CallContract.js
   import React, { useEffect, useState } from 'react';
   import { ethers } from 'ethers';

   function CallContract() {
     const [provider, setProvider] = useState(null);
     const [signer, setSigner] = useState(null);
     const [contractData, setContractData] = useState(null);
     const [error, setError] = useState('');
     const [result, setResult] = useState('');

     const contractAddress = "0xYourContractAddress"; // Replace with your contract address
     const contractABI = [
       "function getValue() view returns (uint256)" // Example function
     ];

     useEffect(() => {
       // Set up the provider and signer
       const setupProvider = async () => {
         if (window.ethereum) {
           const newProvider = new ethers.Web3Provider(window.ethereum);
           const newSigner = newProvider.getSigner();

           setProvider(newProvider);
           setSigner(newSigner);
         } else {
           setError('MetaMask is not installed. Please install MetaMask.');
         }
       };

       setupProvider();
     }, []);

     const callContractFunction = async () => {
       if (!provider) {
         setError('Provider not initialized.');
         return;
       }

       try {
         const contract = new ethers.Contract(contractAddress, contractABI, provider);

         // Call the smart contract function (e.g., `getValue`)
         const value = await contract.getValue();
         setResult(value.toString());
       } catch (err) {
         console.error('Error calling contract function:', err);
         setError('Error calling contract function.');
       }
     };

     return (
       <div>
         <h1>Call Smart Contract Function</h1>
         <button onClick={callContractFunction}>Call Function</button>
         {result && <p>Result: {result}</p>}
         {error && <p>Error: {error}</p>}
       </div>
     );
   }

   export default CallContract;
   ```

   - **Replace `0xYourContractAddress`** with the address of your deployed smart contract.
   - **Update the ABI** array with the ABI of your smart contract. The example ABI provided is just for illustration; use the actual ABI of your contract.

2. **Use the Component in Your App:**

   - Open `src/App.js` and import the `CallContract` component:

   ```javascript
   // src/App.js
   import React from 'react';
   import './App.css';
   import CallContract from './CallContract';

   function App() {
     return (
       <div className="App">
         <header className="App-header">
           <CallContract />
         </header>
       </div>
     );
   }

   export default App;
   ```

### 4. **Run Your React App**

Start your React application:

```bash
npm start
```

### Summary

1. **Set up your React project** and install `ethers.js`.
2. **Create a component** to call a smart contract function using `JsonRpcProvider` or `Web3Provider`.
3. **Render the component** in your app to interact with the Ethereum network.

With this setup, users can call a smart contract function directly from your React application. Make sure to handle errors and edge cases appropriately in your production app.