# Exercise 003 - RAID Concepts & Reliability

### Objective
Unity in numbers. Master **RAID (Redundant Array of Independent Disks)**—the technique of combining multiple physical disks into a single logical unit to improve performance, reliability, or both. Understand the trade-offs between different RAID levels and why "RAID is NOT a Backup."

### Core Concepts to Master
- **Striping (RAID 0):** Splitting data across disks to double the speed. If 1 disk fails, ALL data is lost.
- **Mirroring (RAID 1):** Copying data identically to 2 disks. If 1 fails, you are 100% safe.
- **Parity (RAID 5/6):** Using math (XOR) to store "Survival data" on extra disks. Can survive 1 or 2 disk deaths without losing anything.
- **RAID 10:** The "Gold Standard" (Mirrored + Striped). High speed AND high safety.

### Research Topics
- "RAID 0 vs RAID 1 vs RAID 5: Performance visualization"
- "The XOR math behind RAID parity"
- "What is a 'Hot Spare'?"
- "The RAID 'Write Hole' problem"

---

### The Practical Challenge

**Part 1: The Capacity Math**
1. You have four 1TB disks. 
2. Calculate the total usable space for:
   - **RAID 0:** (Answer: 4TB).
   - **RAID 1:** (Answer: 1TB).
   - **RAID 5:** (Answer: 3TB).
   - **RAID 10:** (Answer: 2TB).

**Part 2: The Failure Simulation**
1. In RAID 5 with four disks, Disk A dies. 
2. Discuss: How does the computer "calculate" the missing data from Disk A using the data on B, C, and D?
3. Research: Why is a RAID 5 system extremely slow while it is "rebuilding" after you replace the dead disk?

**Part 3: Performance Check**
1. Discuss why RAID 1 is fast at "Reading" (you can read from two disks at once) but slow at "Writing" (you have to write the same thing twice).

**Part 4: Software vs Hardware RAID**
1. Research the difference between a dedicated **RAID Controller card** and a **Software RAID** (like Linux `mdadm` or Mac `Disk Utility`).
2. Why would a data center prefer a hardware controller? (Answer: Dedicated cache with battery backup).

---

### Common Gotchas & Troubleshooting
- **Gotcha 1:** Corrupted Data. RAID protects you against a *dead* disk. If a virus deletes your files, RAID will helpfully delete them from both disks simultaneously! This is why you still need a separate backup.
- **Gotcha 2:** The "Shared Batch" failure. If you buy 10 identical disks from the same factory on the same day, they likely have the same lifespan. If one dies, the others might die during the "Rebuild" process due to the heavy stress.

### Reflection Question
Why has RAID 5 become "dangerous" for massive 20TB modern drives compared to RAID 6 or RAID 10? (Hint: The time it takes to rebuild).
