To set up a frontend application using React, Node.js, `ethers.js`, and either Alchemy or Infura, you’ll need to integrate these technologies to interact with the Ethereum blockchain. Here’s a step-by-step guide to setting up this stack:

### 1. **Set Up the Backend with Node.js**

1. **Initialize a Node.js Project:**
   Create a new directory for your project and initialize it with `npm`:

   ```bash
   mkdir my-eth-app
   cd my-eth-app
   npm init -y
   ```

2. **Install Dependencies:**
   Install the necessary packages:

   ```bash
   npm install express ethers dotenv
   ```

   - `express`: For creating a server.
   - `ethers`: For interacting with the Ethereum blockchain.
   - `dotenv`: For managing environment variables.

3. **Create a Basic Express Server:**
   Create a file named `server.js` and set up a basic Express server:

   ```javascript
   // server.js
   const express = require("express");
   const { ethers } = require("ethers");
   require("dotenv").config();

   const app = express();
   const port = process.env.PORT || 5000;

   // Set up provider using Alchemy or Infura
   const provider = new ethers.JsonRpcProvider(process.env.ALCHEMY_URL || process.env.INFURA_URL);

   app.get("/", (req, res) => {
     res.send("Hello from the backend!");
   });

   app.listen(port, () => {
     console.log(`Server is running on port ${port}`);
   });
   ```

4. **Set Up Environment Variables:**
   Create a `.env` file to store your API keys:

   ```
   ALCHEMY_URL=https://eth-mainnet.alchemyapi.io/v2/YOUR_ALCHEMY_API_KEY
   INFURA_URL=https://mainnet.infura.io/v3/YOUR_INFURA_PROJECT_ID
   ```

   Update your `.gitignore` to exclude the `.env` file:

   ```
   .env
   ```

5. **Run the Server:**
   Start the server with:

   ```bash
   node server.js
   ```

### 2. **Set Up the Frontend with React**

1. **Create a React Application:**
   Use `create-react-app` to set up your React project:

   ```bash
   npx create-react-app my-eth-frontend
   cd my-eth-frontend
   ```

2. **Install `ethers.js`:**
   Install the `ethers` package:

   ```bash
   npm install ethers
   ```

3. **Create a Component to Interact with Ethereum:**
   Create a new component, e.g., `EthereumComponent.js`, to interact with the Ethereum blockchain:

   ```javascript
   // src/EthereumComponent.js
   import React, { useState } from "react";
   import { ethers } from "ethers";

   function EthereumComponent() {
     const [account, setAccount] = useState(null);
     const [provider, setProvider] = useState(null);

     const connectWallet = async () => {
       if (window.ethereum) {
         const provider = new ethers.BrowserProvider(window.ethereum);
         setProvider(provider);

         const accounts = await provider.send("eth_requestAccounts", []);
         setAccount(accounts[0]);
       } else {
         alert("Please install MetaMask!");
       }
     };

     return (
       <div>
         <button onClick={connectWallet}>Connect Wallet</button>
         {account && <p>Connected account: {account}</p>}
       </div>
     );
   }

   export default EthereumComponent;
   ```

4. **Integrate the Component into Your React App:**
   Replace the contents of `src/App.js` with:

   ```javascript
   // src/App.js
   import React from "react";
   import EthereumComponent from "./EthereumComponent";

   function App() {
     return (
       <div className="App">
         <h1>My Ethereum App</h1>
         <EthereumComponent />
       </div>
     );
   }

   export default App;
   ```

5. **Run the React Application:**
   Start your React application with:

   ```bash
   npm start
   ```

### 3. **Integrate Backend and Frontend**

1. **Proxy API Requests from React to Node.js:**
   In your React project, add a proxy field to `package.json` to route API requests to your Node.js server:

   ```json
   {
     "name": "my-eth-frontend",
     "version": "0.1.0",
     "private": true,
     "dependencies": {
       "ethers": "^5.0.0",
       "react": "^17.0.0",
       "react-dom": "^17.0.0",
       "react-scripts": "4.0.0"
     },
     "proxy": "http://localhost:5000"
   }
   ```

2. **Fetch Data from Node.js Backend:**
   You can now make requests to your backend server from your React components. For example, to get a response from the backend:

   ```javascript
   // src/EthereumComponent.js
   const fetchData = async () => {
     const response = await fetch("/");
     const data = await response.text();
     console.log(data);
   };

   useEffect(() => {
     fetchData();
   }, []);
   ```

### Summary

- **Backend (Node.js)**: Set up an Express server to connect to Ethereum via `ethers.js` using Alchemy or Infura.
- **Frontend (React)**: Create a React application, integrate `ethers.js` to interact with the Ethereum blockchain, and connect a wallet using MetaMask.
- **Integration**: Configure React to proxy API requests to the Node.js server for seamless interaction.

By following these steps, you’ll have a full-stack setup that enables interaction with the Ethereum blockchain through a React frontend and a Node.js backend.