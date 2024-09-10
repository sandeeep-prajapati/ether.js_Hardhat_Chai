To add the localhost wallets generated by Hardhat to MetaMask, follow these steps:

### 1. **Set up Hardhat and start a local node**
   - Make sure your Hardhat project is running by starting the local node:
     ```bash
     npx hardhat node
     ```
   - This will launch a local Ethereum network at `http://127.0.0.1:8545`.

### 2. **Get the private keys from Hardhat**
   When you run the Hardhat node, it generates several accounts. You can see the private keys in the terminal output, something like this:
   ```
   Accounts:
   ========
   (0) 0xYourAccountAddress
   ...

   Private Keys:
   =============
   (0) yourPrivateKey
   ...
   ```

### 3. **Connect MetaMask to the local Hardhat network**
   1. Open MetaMask.
   2. Click on the network selector (at the top of MetaMask, usually it will say "Ethereum Mainnet").
   3. Click "Add Network" (or click "Custom RPC" if the option is available).
   4. In the network details, input the following:
      - **Network Name**: Hardhat Localhost
      - **New RPC URL**: `http://127.0.0.1:8545`
      - **Chain ID**: `31337` (Hardhat's default Chain ID)
      - **Currency Symbol**: ETH
   5. Click **Save**.

### 4. **Import Hardhat wallet accounts to MetaMask**
   To add the accounts generated by Hardhat to MetaMask:
   1. Open MetaMask.
   2. Click on your account icon (top-right corner) and select **Import Account**.
   3. Copy the private key from the Hardhat node output (the one you want to use).
   4. Paste the private key into the MetaMask dialog and click **Import**.

### 5. **Check the imported accounts**
   Once imported, you should see the Hardhat accounts in MetaMask, with ETH balance that matches what Hardhat provided in the test environment.

That's it! You can now interact with the Hardhat network via MetaMask.