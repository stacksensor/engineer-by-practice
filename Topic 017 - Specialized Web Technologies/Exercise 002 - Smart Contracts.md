# Exercise 002 - Smart Contracts (Solidity Basics)

### Objective
Program the "Global Computer." Learn the basics of **Solidity**, the world's most popular language for writing Smart Contracts. Transition from simple scripts to "Self-Executing Agreements" that live on the Ethereum blockchain and manage assets or voting logic automatically without human intervention.

### Core Concepts to Master
- **The EVM (Ethereum Virtual Machine):** The distributed environment where smart contracts execute.
- **Solidity Syntax:** A statically-typed language similar to JavaScript/C++ but designed specifically for public ledgers.
- **State Variables:** Data that is permanently stored on the blockchain (Saving data to a state variable costs "Gas").
- **Functions & Visibility:** Understanding `public`, `private`, `internal`, and `external` functions.
- **Gas:** The fee paid in ETH to execute code on the network. Every mathematical operation has a specific cost.

### Research Topics
- "Solidity by Example"
- "Introduction to Smart Contracts"
- "How to use the Remix IDE"
- "What is a 'Pure' vs 'View' function in Solidity?"

---

### The Practical Challenge

**Part 1: The Remix IDE**
1. Open [remix.ethereum.org](https://remix.ethereum.org) in your browser. This is the industry-standard "online IDE" for smart contracts.
2. Create a new file `SimpleStorage.sol`.
3. Write a contract that stores a single number:
   ```solidity
   pragma solidity ^0.8.0;
   
   contract SimpleStorage {
       uint256 public favoriteNumber;
       
       function set(uint256 _number) public {
           favoriteNumber = _number;
       }
   }
   ```
4. Compile and deploy it to the "Remix VM" (a local simulator). Test the `set` and `favoriteNumber` buttons.

**Part 2: The "Bank" Contract**
1. Create a second contract named `SimpleBank`.
2. Implement a mapping to track user balances: `mapping(address => uint256) public balances;`.
3. Write a `deposit` function. Use the `msg.value` global variable to capture how much ETH a user is sending to the contract.
4. Write a `getBalance` function that returns the caller's balance using `msg.sender`.

**Part 3: Conditionals and Revert**
1. Implement a `withdraw` function in your Bank contract.
2. IMPORTANT: Use a `require` statement to ensure the user has enough money before sending:
   `require(balances[msg.sender] >= _amount, "Insufficient funds");`
3. Use `payable(msg.sender).transfer(_amount);` to send the money back.
4. Test the withdrawal. Try to withdraw more money than you have. Observe the "Revert" error in the logs.

**Part 4: Deployment to a Testnet**
1. Install the **MetaMask** browser extension. Set it to a test network (like Sepolia).
2. Get some "Test ETH" from a free online faucet.
3. In Remix, change the environment to "Injected Provider (MetaMask)."
4. Deploy your `SimpleBank` to the REAL testnet. 
5. View your transaction on **Etherscan**. Congratulations! You have just deployed a permanent piece of software to a global network.

---

### Common Gotchas & Troubleshooting
- **Gotcha 1:** The "Gas Limit" error. If your function is too complex (e.g., a loop through 1,000,000 users), it will exceed the block gas limit and fail. Always design your contracts to be as efficient as possible.
- **Gotcha 2:** Integer Overflow. In older versions of Solidity, adding to a maxed-out number would cause it to "flip" to zero. Modern Solidity (0.8+) handles this automatically and reverts the transaction.

### Reflection Question
Why are Smart Contracts "Immutable" (they cannot be changed after deployment), and how does this create both security and danger for developers?
