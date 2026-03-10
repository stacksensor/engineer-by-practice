# Exercise 004 - Object Storage vs. Block Storage

### Objective
Store for the masses. Master the difference between **Block Storage** (like an SSD/EBS volume) and **Object Storage** (like AWS S3). Learn when to treat storage like a "Hard Drive" and when to treat it like a "Key-Value Web Service."

### Core Concepts to Master
- **Block Storage:** Low-level, raw disk access. Data is stored in blocks without metadata. Fastest for databases.
- **Object Storage:** High-level storage where data is stored as "Objects" (Files + Metadata + Unique ID). Accessed via HTTP API (not the OS filesystem). Unlimited scale.
- **Filesystem (NAS):** A middle ground where multiple servers share a folder via the network (NFS/SMB).
- **Metadata:** Why being able to tag an object with `author: alex` is a superpower of object storage compared to just `file.txt` on a block volume.

### Research Topics
- "EBS vs S3 vs EFS: Which to use when?"
- "The concept of 'Bucket' and 'Key'"
- "Why can't you run a SQL database (like Postgres) on top of S3?"
- "Consistency models in S3 (Strong vs Eventual)"

---

### The Practical Challenge

**Part 1: The API Test**
1. Use the `aws s3` CLI or a simple script to upload a file to a bucket.
2. Add custom metadata: `--metadata project=learn-and-grow`.
3. Retrieve the object and inspect the headers. 
4. Discuss: How would you do this in a regular "Block" filesystem? (Answer: You can't, unless you use a separate database to store the metadata).

**Part 2: The Latency Test**
1. Measure how long it takes to read a 1-byte file from your local SSD. (Answer: ~0.0001ms).
2. Measure how long it takes to read a 1-byte object from S3 using `curl`. (Answer: ~50ms - 200ms).
3. Discuss: Why is Object Storage bad for "High-speed small reads" but great for "Streaming massive videos"?

**Part 3: The Scalability Battle**
1. Research the "limit" of a single Block Storage volume (usually 16TB - 64TB).
2. Research the "limit" of an S3 bucket. (Answer: Infinite).
3. Discuss how you would store 1 Petabyte of user photos. Which storage would you pick?

**Part 4: Mounting the Object (Concept)**
1. Research tools like `s3fs`. 
2. Discuss why "Mounting" S3 as if it were a local folder is usually a bad idea for performance and reliability.

---

### Common Gotchas & Troubleshooting
- **Gotcha 1:** File Overwrites. In most Object storage, you cannot "Edit" a single byte in the middle of a file. You must re-upload the ENTIRE file.
- **Gotcha 2:** The "Price" of Requests. S3 is cheap for data, but expensive for "Requests." If you have a script that checks a file 1,000,000 times a minute, you will have a massive bill.

### Reflection Question
Why is the "URL-addressable" nature of Object Storage its biggest advantage for web development? (Answer: You can give a user a direct link to a file without your server being the middleman).
