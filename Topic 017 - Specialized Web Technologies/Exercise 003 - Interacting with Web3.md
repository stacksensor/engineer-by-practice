# Exercise 003 - Interacting with Web3 (ethers.js)

### Objective
Bridge the Web2 and Web3 worlds. Build a standard web frontend (React/Vite) that interacts with the blockchain. Master the **ethers.js** library to connect to user wallets (MetaMask), read contract data, and send transactions directly from a browser interface.

### Core Concepts to Master
- **Provider:** The connection to the blockchain network (e.g., MetaMask's `window.ethereum`).
- **Signer:** The user's account that can sign and send transactions.
- **Contract Instance:** A JavaScript object that represents a smart contract on the blockchain, created using the contract's **Address** and **ABI** (Application Binary Interface).
- **ABI (Application Binary Interface):** A JSON file that acts as a "Manual" for your contract, telling the frontend which functions exist and what arguments they take.

### Research Topics
- "Connecting MetaMask to a React app tutorial"
- "ethers.js v6 documentation basics"
- "What is an ABI and where do I get it?"
- "Handling Web3 provider errors"

---

### The Practical Challenge

**Part 1: The Wallet Connection**
1. Bootstrap a new React/Vite project. Install `ethers`.
2. Create a "Connect Wallet" button.
3. Use the following logic to request the user's account:
   ```javascript
   const provider = new ethers.BrowserProvider(window.ethereum);
   const accounts = await provider.send("eth_requestAccounts", []);
   console.log("Connected to:", accounts[0]);
   ```
4. Display the connected wallet address on the screen.

**Part 2: Reading Blockchain Data**
1. You don't need a wallet to "Read" data.
2. Use ethers to connect to the Ethereum Mainnet (via a public provider like Infura or Alchemy).
3. Fetch the current block number: `await provider.getBlockNumber()`.
4. Fetch the balance of a famous address (e.g., Vitalik Buterin's address).
5. Format the result from BigInt/Wei to ETH using `ethers.formatEther(balance)`.

**Part 3: Interacting with your Contract**
1. Copy the **Address** and **ABI** of the `SimpleStorage` contract you deployed in Exercise 002.
2. Initialize a contract instance in your frontend:
   `const contract = new ethers.Contract(address, abi, provider);`
3. Call the `favoriteNumber()` function and display the result in your UI.
4. Observe how reading data is free and fast.

**Part 4: Sending a Transaction**
1. Now, get the **Signer**: `const signer = await provider.getSigner();`.
2. Re-initialize the contract with the signer: `const contractWithSigner = contract.connect(signer);`.
3. Link an HTML form to call `contractWithSigner.set(newValue)`.
4. Observe MetaMask popping up to ask for "Permission" and "Gas Payment."
5. Wait for the transaction to be "Mined" (using `await tx.wait()`) and then update your UI automatically.

---

### Common Gotchas & Troubleshooting
- **Gotcha 1:** BigInt. Blockchain numbers are huge. `ethers` returns them as `BigInt`. You cannot use `Math.floor()` on them directly. Always use `ethers.formatUnits()` or convert them carefully.
- **Gotcha 2:** Network Mismatch. If your contract is on the "Sepolia Testnet" but your MetaMask is set to "Mainnet," your API calls will fail with a "Contract Not Found" error. Always check `provider.getNetwork()` in your code.

### Reflection Question
Why must the "Signer" (the user) approve every transaction in MetaMask rather than the application simply taking the money automatically?
