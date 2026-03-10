# Exercise 005 - Journaling & Data Consistency

### Objective
Survival during a power cut. Master the concept of **Journaling** in filesystems. Learn how the OS ensures that your disk doesn't become "Corrupted" if the power is pulled while a file is being saved, and understand the difference between **Data Journaling** and **Metadata Journaling**.

### Core Concepts to Master
- **The Atomic Problem:** Writing a file requires updates to 3 things (The Inode, the Data blocks, and the Bitmap of free space). If the power dies after step 1 but before step 3, the disk is "Corrupted."
- **The Journal (Log):** A special high-speed area of the disk where the OS writes "Intentions" (e.g., "I'm about to write X to Y").
- **Commit:** Once the intent is in the journal, even a power cut is safe, as the OS will finish the job on the next boot.
- **FSK (File System Check):** Why older computers took 30 minutes to boot after a crash (scanning the whole disk for errors) and why journaling makes this obsolete.

### Research Topics
- "How ext4 journaling works"
- "Metadata-only journaling vs Full journaling"
- "What is a 'Dirty' bit in filesystems?"
- "Copy-on-Write (CoW) filesystems: ZFS & Btrfs"

---

### The Practical Challenge

**Part 1: The "Write" sequence**
1. Draw a diagram of what needs to happen to add one word to a file:
   - Read block.
   - Modify block in memory.
   - Update Inode size.
   - Write block back to disk.
2. Discuss: At which step would a power failure be "The worst"?

**Part 2: Checking the Journal**
1. On Linux, use `dumpe2fs /dev/sda1 | grep features`. Look for the "has_journal" flag.
2. On Mac, use `diskutil info /`. Identify if the filesystem is "Journaled" (Note: APFS uses a different technique called CoW).

**Part 3: Copy-on-Write (CoW) vs Journaling**
1. Research **APFS** or **ZFS**. 
2. These systems never "Overwrite" an existing block. They write the new data to a *fresh* block and then "flip the switch" to point to it.
3. Discuss: Why does this eliminate the need for a journal?

**Part 4: The Mount Options**
1. Research the Linux mount options for ext4: `data=journal`, `data=ordered`, `data=writeback`.
2. Which one is "Fastest"? Which one is "Safest"? (Answer: Writeback is fastest but risky; Journal is safest but slow).

---

### Common Gotchas & Troubleshooting
- **Gotcha 1:** SSD Wear. Journaling involves writing the same info twice (once to the journal and once to the data area). This uses up SSD lifespan over time.
- **Gotcha 2:** The False Promise. Journaling protects the "Filesystem structure" (the disk won't break), but it might not protect the *contents* of your file if you were in the middle of a massive write.

### Reflection Question
Why do modern servers still have "Battery-backed Cache" on their RAID cards if the filesystem already has journaling? (Answer: Speed and an extra layer of safety for data that hasn't even hit the disk yet).
