# Exercise 007 - Write-Ahead Logging (WAL) & Recovery Flow

### Objective
The source of truth. Master the **Write-Ahead Log (WAL)**—the actual "Record" of every change made to the database. Learn how the WAL enables **Durability** (surviving crashes), **Replication** (sending data to other servers), and **Point-in-Time Recovery** (restoring the DB to 1:04 PM last Tuesday).

### Core Concepts to Master
- **The WAL:** An append-only file on disk that records every change *before* it is applied to the main tables.
- **LSN (Log Sequence Number):** The unique ID for every entry in the WAL.
- **Checkpointing:** The process of flushing the data from memory into the main table files so the WAL can be safely deleted or archived.
- **Streaming Replication:** Sending the WAL entries over the network to a "Follower" server in real-time.
- **PITR (Point-in-Time Recovery):** Replaying the WAL on top of a base backup to reach a specific microsecond in the past.

### Research Topics
- "What is a Write-Ahead Log (WAL)?"
- "Postgres WAL and Checkpoints"
- "Synchronous vs Asynchronous Replication"
- "Physical vs Logical Replication"

---

### The Practical Challenge

**Part 1: The Crash Test (Conceptual)**
1. Transaction: "Subtract $10 from Alice, Add $10 to Bob."
2. The DB writes this to the **WAL** and says "Success!"
3. The power dies before the DB updates the main `accounts` table.
4. Explain the recovery: On reboot, the DB reads the WAL, sees the entry, and applies it to the table. 
5. Why is this safer than just updating the table directly? (Answer: Because appending to a log is atomic and fast).

**Part 2: Inspecting the Log**
1. On a local Postgres, look in the `pg_wal` directory. 
2. Observe the files (usually 16MB each). 
3. Discuss: What happens if this directory fills up your disk? (Answer: The DB will crash and stay down!).

**Part 3: Replication Sync**
1. Research **Synchronous Replication**. 
2. Discuss: If you set it to "Synchronous," the Primary server waits for the Follower to acknowledge the WAL before telling the user "Success."
3. How does this affect your **Write Latency**?

**Part 4: The Recovery Speed**
1. Discuss the "Checkpoint" frequency. 
2. If you only checkpoint once every 24 hours, and you crash at hour 23, how long will it take to reboot? (Answer: A long time! You have to replay 23 hours of log).

---

### Common Gotchas & Troubleshooting
- **Gotcha 1:** WAL Bloat. A single long-running transaction or a broken replica can cause the WAL to grow indefinitely. Always monitor your WAL size.
- **Gotcha 2:** The "Fsync" bottleneck. Every commit requires an `fsync` of the WAL to the disk. This is the ultimate physical limit on how many transactions per second a single-server database can handle.

### Reflection Question
Why is the WAL often considered "The Real Database" while the actual tables are just a convenient "Cache" or projection of that log?
