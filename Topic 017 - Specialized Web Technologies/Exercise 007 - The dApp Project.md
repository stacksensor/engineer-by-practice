# Exercise 007 - The dApp Project (Final Capstone)

### Objective
Unify the Distributed Stack. Build a complete **Decentralized Application (dApp)** that combines a Smart Contract (Solidity), a Frontend (React), Distributed Storage (IPFS), and Wallet Integration (MetaMask). This project serves as the culmination of your journey into specialized web technologies.

### Core Concepts to Master
- **Full-Stack dApp Architecture:** Understanding how the "Frontend" talks to the "Blockchain" (for logic) and "IPFS" (for data).
- **Transaction Life Cycle:** Handling the "Pending," "Success," and "Reverted" states of a live user transaction.
- **Gas Optimization:** Writing your final contract to be as cheap as possible for users to interact with.
- **Professional Deployment:** Verified contracts on Etherscan and a hosted frontend on IPFS/Vercel.

### Research Topics
- "How to verify a contract on Etherscan"
- "React best practices for Web3 apps"
- "Ensuring a mobile-friendly Web3 experience"

---

### The Practical Challenge

**Part 1: The dApp Concept**
1. Choose a "Distributed" project. Ideas:
   - **NFT Art Gallery:** Users can view and buy NFTs from your collection.
   - **On-chain Voting:** A tamper-proof voting system where 1 token = 1 vote.
   - **Shared Bank:** A vault where multiple people can deposit ETH and vote on where to spend it.
2. Draft the "Contract" logic and the "UI" wireframe.

**Part 2: The Core Smart Contract**
1. Write and test your contract in Remix.
2. Deploy it to the **Sepolia Testnet**.
3. **CRITICAL:** Use the "Verify and Publish" tool on Etherscan so that users can see your source code and interact with it directly on the block explorer.

**Part 3: The Web3 Interface**
1. In your React frontend, implement the "Wallet Connection" and "Contract Connection" from Exercise 003.
2. Build a beautiful, responsive UI that displays the "Live Data" from the blockchain (e.g., the current total votes or the current NFT price).
3. Use a library like `react-toastify` to show a "Transaction Pending..." alert while the blockchain is processing.

**Part 4: The Final Launch**
1. Upload your NFT images or app assets to IPFS (Exercise 004).
2. Deploy your React frontend to the cloud (Vercel, Netlify, or IPFS).
3. Verify the "Happy Path":
   - Connect Wallet.
   - Perform an action (Vote/Buy/Stake).
   - Sign the transaction in MetaMask.
   - Watch the UI update in real-time.
4. Congratulations. You have successfully built a decentralized system that exists outside of centralized corporate control.

---

### Common Gotchas & Troubleshooting
- **Gotcha 1:** User Friction. Web3 is hard for "Normal" people. If your app requires a user to sign three different transactions just to "Sign Up," they will leave. Combine actions into a single transaction whenever possible.
- **Gotcha 2:** Error Handling. If a transaction "Reverts," don't just log it to the console. Show a user-friendly message explaining why (e.g., "Insufficient balance" or "This vote is already closed").

### Reflection Question
How does building a dApp change your perspective on "User Data" and "Ownership" compared to building a traditional centralized application?
