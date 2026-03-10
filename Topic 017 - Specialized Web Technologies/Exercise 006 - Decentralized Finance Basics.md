# Exercise 006 - Decentralized Finance (DeFi) Basics

### Objective
Disrupt the banking system. Explore the world of **DeFi** by building a "Lending" or "Swapping" simulation. Learn how automated protocols like **Uniswap** (trading) and **Aave** (lending) use Smart Contracts to replace banks, brokers, and traditional financial intermediaries.

### Core Concepts to Master
- **DEX (Decentralized Exchange):** An automated platform for swapping tokens without a middleman.
- **Liquidity Pools:** A "pot" of tokens provided by users that allows others to trade.
- **AMM (Automated Market Maker):** The mathematical formula (usually `x * y = k`) that calculates the price of a token based on supply and demand.
- **Yield Farming:** Earning rewards/interest by providing liquidity to a DeFi protocol.

### Research Topics
- "How Uniswap works (Constant Product Formula)"
- "What is a Liquidity Provider (LP)?"
- "Introduction to DeFi lending and borrowing"
- "Impermanent Loss explained"

---

### The Practical Challenge

**Part 1: The Constant Product Formula**
1. In a JavaScript script, implement the `x * y = k` formula.
2. Assume you have a pool with 100 "Token A" and 1000 "Token B."
3. Calculate `k` (100 * 1000 = 100,000).
4. Simulate a user "Swapping" 10 Token A into the pool. 
5. Calculate how many Token B they get back to keep `k` at 100,000.
6. Notice that as the pool gets smaller, the "Price" of the token increases automatically. This is an AMM.

**Part 2: The Staking Contract**
1. Create a smart contract `StakingPool.sol` in Remix.
2. Users can "Stake" an ERC-20 token (from Exercise 005) into the contract.
3. Every 10 seconds, the contract "mints" a reward token for every user based on their shares.
4. Implement a `claimRewards` function.

**Part 3: Interacting with Uniswap**
1. You don't need to build a DEX from scratch; you can "Compose" with existing ones.
2. In Remix, write a script that uses the **Uniswap Router v2** interface.
3. Call the `getAmountsOut` function to check the current real-world price of ETH/USDC.
4. This is called **DeFi Composability** (or "Money Legos")—building new apps on top of existing global financial infrastructure.

**Part 4: The Risk Audit**
1. Research the "Flash Loan Attack" or "Reentrancy Bug."
2. Analyze your `StakingPool.sol`. Is it possible for a user to "Stake," "Claim," and "Unstake" in the same transaction to trick the reward logic?
3. Discuss how "Smart Contract Risk" is the primary barrier to mass DeFi adoption.

---

### Common Gotchas & Troubleshooting
- **Gotcha 1:** Slippage. In a real DEX, if you buy 1 million dollars worth of a token, the price will increase *while* you are buying it. This difference between the expected price and the actual price is "Slippage."
- **Gotcha 2:** Reentrancy. This is the bug that stole 50 million dollars from "The DAO." Always update your internal state (balances) *before* sending money out of a contract.

### Reflection Question
Why are DeFi protocols considered "Permissionless," and how does this enable financial services for people who don't have access to traditional banks?
