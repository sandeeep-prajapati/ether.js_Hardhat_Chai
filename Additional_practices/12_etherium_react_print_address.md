To print an Ethereum address in a React app, you need to integrate with `ethers.js` (or another library) to interact with the Ethereum blockchain. Here’s a step-by-step guide to accomplish this:

### 1. **Set Up Your React Project**

If you don’t have a React project set up yet, you can create one using Create React App:

```bash
npx create-react-app my-app
cd my-app
```

### 2. **Install `ethers.js`**

Install `ethers.js` in your React project:

```bash
npm install ethers
```

### 3. **Set Up the React Component**

Create a React component that connects to the Ethereum network and prints an address. Here’s an example:

1. **Create a New Component:**
   - Create a file named `EthereumAddress.js` in the `src` directory.

   ```javascript
   // src/EthereumAddress.js
   import React, { useEffect, useState } from 'react';
   import { ethers } from 'ethers';

   function EthereumAddress() {
     const [address, setAddress] = useState(null);

     useEffect(() => {
       async function fetchAddress() {
         try {
           // Connect to the Ethereum network (use a provider like Infura)
           const provider = new ethers.JsonRpcProvider("https://ropsten.infura.io/v3/YOUR_INFURA_PROJECT_ID");

           // Example: Fetch the address of the first account (for demonstration purposes)
           const accounts = await provider.listAccounts();
           if (accounts.length > 0) {
             setAddress(accounts[0]);
           } else {
             console.error("No accounts found.");
           }
         } catch (error) {
           console.error("Error fetching address:", error);
         }
       }

       fetchAddress();
     }, []);

     return (
       <div>
         <h1>Ethereum Address</h1>
         {address ? (
           <p>Address: {address}</p>
         ) : (
           <p>Loading address...</p>
         )}
       </div>
     );
   }

   export default EthereumAddress;
   ```

   - **Replace `YOUR_INFURA_PROJECT_ID`** with your actual Infura Project ID.

2. **Use the Component in Your App:**
   - Open `src/App.js` and import the `EthereumAddress` component.

   ```javascript
   // src/App.js
   import React from 'react';
   import './App.css';
   import EthereumAddress from './EthereumAddress';

   function App() {
     return (
       <div className="App">
         <header className="App-header">
           <EthereumAddress />
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

Your React app should now display the Ethereum address fetched from the provider. If everything is set up correctly, you should see the address printed on the screen.

### Summary

1. **Set up your React project** and install `ethers.js`.
2. **Create a React component** that fetches an Ethereum address using `ethers.js`.
3. **Render the component** in your app to display the Ethereum address.

This approach shows how to fetch and display an Ethereum address in a React app using `ethers.js` and Infura. If you want to connect to a specific Ethereum wallet or account, you would need to implement wallet integration (e.g., MetaMask) for users to connect their wallets.