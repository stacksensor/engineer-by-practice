# Exercise 004 - Distributed Storage (IPFS)

### Objective
"Unstoppable" file hosting. Learn how to store images, videos, and website files in a decentralized manner using the **InterPlanetary File System (IPFS)**. Move away from centralized servers (like S3 or Google Drive) to a content-addressable network where files are identified by their "Hash" rather than their "Location."

### Core Concepts to Master
- **IPFS:** A peer-to-peer protocol for storing and sharing data in a distributed file system.
- **CID (Content Identifier):** A unique cryptographic hash (e.g., `Qm...`) that identifies a specific file. If the file changes by even one pixel, its CID changes.
- **Pinning:** Ensuring that a file remains available on the network by "Pinning" it to a specific node (using services like **Pinata** or **Infura**).
- **IPFS Gateways:** Public web addresses (e.g., `https://ipfs.io/ipfs/CID`) that allow standard browsers to view decentralized files.

### Research Topics
- "What is IPFS and how is it different from HTTP?"
- "How to upload imagery to IPFS using Pinata"
- "IPFS for NFT metadata"
- "Hosting a static website on IPFS"

---

### The Practical Challenge

**Part 1: The CID Mystery**
1. Use an online IPFS desktop app or the `ipfs` CLI.
2. Create a simple text file `hello.txt` with the content "Hello IPFS".
3. Add the file to IPFS. Note the CID returned (usually starts with `Qm` or `bafy`).
4. Access your file via a public gateway: `https://ipfs.io/ipfs/<YOUR_CID>`.
5. Edit the text file to say "Hello World" and add it again. Observe that the CID is completely different.

**Part 2: Multi-Node Resilience**
1. Close your local IPFS node. 
2. Try to visit the public gateway URL again. Most likely, it will time out or show a 404.
3. Why? Because you were the only "Peer" hosting that file.
4. Use a "Pinning Service" like **Pinata**. Upload your file there.
5. Now close your local node again. Observe that the file is still accessible because Pinata's servers are still "Pinning" the data for you globally.

**Part 3: Programmable IPFS**
1. In a Node.js script, use the `ipfs-http-client` or a Pinata SDK.
2. Write a script that takes a user's local image and uploads it to IPFS automatically.
3. Log the resulting CID.
4. This is how 99% of NFTs (Topic 17 Ex 005) work: Your blockchain contract stores the `CID`, which points to the image on IPFS.

**Part 4: The IPFS Website**
1. Build a simple static HTML site (or a built React app).
2. Upload the entire `dist` or `build` folder to IPFS.
3. Access your "Unstoppable Website" via the CID.
4. Think about the implications: This website cannot be "Taken Down" by a central hosting provider because it exists on every peer that chooses to host it.

---

### Common Gotchas & Troubleshooting
- **Gotcha 1:** Privacy. IPFS is a public network. Once you upload a file and someone else "Pins" or caches it, you can NEVER delete it. Never upload sensitive PII or private documents to IPFS.
- **Gotcha 2:** Metadata Latency. Public IPFS gateways can be slow. If your app feels "Laggy" when loading images, you may need to use a "Dedicated Gateway" or a specialized Web3 CDN.

### Reflection Question
How does "Content Addressing" (finding a file by what it IS) solve the problem of "Link Rot" (finding a file by where it LIVES) in the traditional HTTP web?
