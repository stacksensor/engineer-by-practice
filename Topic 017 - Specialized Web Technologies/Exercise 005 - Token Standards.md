# Exercise 005 - Token Standards (ERC-20 & ERC-721)

### Objective
Standardize digital ownership. Explore the OpenZeppelin library to implement industry-standard tokens: **ERC-20** (for fungible "Money" tokens) and **ERC-721** (for non-fungible "NFT" tokens). Understand why these standards allow different wallets and marketplaces to interact with your assets automatically.

### Core Concepts to Master
- **Fungibility:** Items that are identical and interchangable (e.g., one Dollar, one Bitcoin).
- **Non-Fungibility:** Items that are unique and distinct (e.g., a specific house, a piece of art, or a character in a game).
- **ERC-20:** The standard interface for tokens that act like currencies.
- **ERC-721:** The standard interface for tokens that act like unique collectibles (NFTs).
- **OpenZeppelin:** The industry-standard library of secure, audited smart contract templates.

### Research Topics
- "What is the difference between ERC-20 and ERC-721?"
- "Building an NFT with OpenZeppelin in 5 minutes"
- "What is a 'Mint' function in smart contracts?"
- "NFT Metadata and the tokenURI function"

---

### The Practical Challenge

**Part 1: Your First "Currency"**
1. In Remix, create `MyToken.sol`.
2. Use the OpenZeppelin ERC20 template:
   ```solidity
   pragma solidity ^0.8.0;
   import "@openzeppelin/contracts/token/ERC20/ERC20.sol";
   
   contract MyToken is ERC20 {
       constructor() ERC20("MyCoin", "MYC") {
           _mint(msg.sender, 1000 * 10**18);
       }
   }
   ```
3. Deploy the contract. Notice that you (the deployer) now have 1000 "MYC" tokens in your wallet.
4. Use the `transfer` function in Remix to send some tokens to a different address.

**Part 2: The NFT**
1. Create `MyNFT.sol`. Use the ERC721 template.
2. Implement a `mint` function that allows anyone to create a new token:
   ```javascript
   function safeMint(address to, string memory uri) public {
       uint256 tokenId = _nextTokenId++;
       _safeMint(to, tokenId);
       _setTokenURI(tokenId, uri);
   }
   ```
3. Note that the `uri` should be an IPFS link to a JSON file (Exercise 004).

**Part 3: Metadata Standards**
1. Create a JSON file on your computer following the **OpenSea Metadata Standard**:
   ```json
   {
     "name": "Cool Robot #1",
     "description": "A very cool robot.",
     "image": "ipfs://CID_OF_YOUR_IMAGE"
   }
   ```
2. Upload this JSON to IPFS and get its CID.
3. Call your `safeMint` function using the `ipfs://CID_OF_YOUR_JSON` as the URI.
4. You have now "Minted" your first NFT.

**Part 4: Marketplace Inspection**
1. Deploy your NFT contract to the **Sepolia Testnet**.
2. Visit `testnets.opensea.io`.
3. Search for your contract address.
4. If your metadata is correct, OpenSea will automatically show your robot's image and description. This proves the power of the ERC-721 "Standard"—your code works with a multi-billion dollar platform without you writing a single line of integration code.

---

### Common Gotchas & Troubleshooting
- **Gotcha 1:** Decimals. ERC-20 tokens almost always have 18 decimals. If you want to send "1 token," you must send `1000000000000000000`. This is why OpenZeppelin handles the math for you.
- **Gotcha 2:** Metadata on Centralized Servers. If your NFT metadata is on `http://my-server.com/1.json` and your server goes offline, your NFT "breaks." This is why IPFS (Exercise 004) is the mandatory standard for NFT storage.

### Reflection Question
Why are "Standards" (like ERC-20) the most important innovation in the Web3 space? (Hint: Think about what would happen if every developer wrote their own custom `sendMoney` function name).
