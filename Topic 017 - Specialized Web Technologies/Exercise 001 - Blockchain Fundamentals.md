# Exercise 001 - Blockchain Fundamentals

### Objective
Understand the architecture of trust. Move beyond the hype to learn the foundational mechanics of a Decentralized Ledger, exploring how cryptographic hashing, blocks, and distributed consensus (Proof of Work/Stake) create a tamper-proof database without a central authority.

### Core Concepts to Master
- **The Ledger:** A distributed, append-only database where every transaction is visible to every participant.
- **Hashing (SHA-256):** The "Digital Fingerprint" that links blocks together. Changing a single character in one block invalidates every subsequent block in the chain.
- **Consensus Mechanisms:** How a network of thousands of untrusted computers agrees on the "Next Block" (Proof of Work vs. Proof of Stake).
- **Public/Private Keys:** Using asymmetric cryptography to "Sign" transactions, proving ownership without revealing a password.

### Research Topics
- "How does a blockchain work visually"
- "Bitcoin vs Ethereum: Key differences"
- "What is a Genesis Block?"
- "The Byzantine Generals Problem explained"

---

### The Practical Challenge

**Part 1: The Cryptographic Hash**
1. In Node.js, use the `crypto` library to hash a string (e.g., "Transaction 1") using SHA-256.
2. Observe the resulting 64-character string.
3. Change one letter in the input. Observe how the output changes completely (The Avalanche Effect).
4. This is the foundation of blockchain "Immutability."

**Part 2: Building a "Block"**
1. Create a `Block` class. It should contain:
   - `timestamp`
   - `data` (The transactions)
   - `previousHash` (The hash of the block before it)
   - `hash` (The hash of the current block)
2. Create a small chain of 3 blocks. 
3. Manually change the data in Block 1. Observe how the `previousHash` in Block 2 no longer matches. The chain is now "Broken."

**Part 3: Proof of Work (Mining)**
1. In a real blockchain, you cannot just add blocks for free.
2. Add a `nonce` (number used once) and a `mineBlock(difficulty)` method to your class.
3. The method must loop and change the `nonce` until the block's hash starts with a specific number of zeros (e.g., "0000...").
4. Observe how increasing the "Difficulty" makes the mining process take significantly more CPU time.

**Part 4: The Distributed Network**
1. Discuss the concept of a "Peer-to-Peer" (P2P) network.
2. What happens if 51% of the network decides to change a block? 
3. Research the "51% Attack" and why a larger network is mathematically more secure than a smaller one.
4. Finalize your `Blockchain.js` implementation by adding a `isChainValid()` method that verifies the integrity of every block and its link to the previous one.

---

### Common Gotchas & Troubleshooting
- **Gotcha 1:** Assuming "Blockchain" is just a slow database. Blockchain is only useful when you do not "Trust" the other party. If you control both the client and the server, a standard SQL database is 1,000,000x faster and cheaper.
- **Gotcha 2:** Private Key Security. On a blockchain, if you lose your private key, your "Money" or "Assets" are gone forever. There is no "Forgot Password" button.

### Reflection Question
Why is "Proof of Stake" becoming the industry standard over "Proof of Work" for modern blockchains like Ethereum 2.0 and Solana?
