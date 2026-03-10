# Exercise 001 - Filesystems Internals (Inodes & Blocks)

### Objective
How data lives on disk. Master the internal structure of a modern filesystem (like ext4, APFS, or NTFS). Learn about **Blocks** (the physical units), **Inodes** (the metadata units), and **Directories** (the mapping units). Understand why a file's "Name" is actually separate from the "Data."

### Core Concepts to Master
- **Blocks:** Fixed-size chunks of disk space (usually 4KB). A 1-byte file still consumes 1 full block.
- **Inode (Index Node):** A data structure that stores everything about a file (Size, Permissions, Timestamps, Disk locations) *except* its name.
- **Directories:** A special type of file that is essentially a table of `(Name, Inode Number)` pairs.
- **Hard Link:** A new directory entry pointing to an *existing* Inode number.
- **Symbolic Link (Soft Link):** A new file that contains the *path* to another file.

### Research Topics
- "How do Inodes work?"
- "The physical layout of an ext4 filesystem"
- "Understanding hard links vs soft links"
- "What happens when a disk runs out of Inodes (but has free space)?"

---

### The Practical Challenge

**Part 1: Inode Hunting**
1. Use `ls -i` to see the Inode number of a file.
2. Use `stat <filename>` to see all the metadata stored in the Inode. 
3. Identify the number of "Links."

**Part 2: Hard Link Experiment**
1. Create a file: `echo "hello" > a.txt`.
2. Create a hard link: `ln a.txt b.txt`.
3. Check Inodes: `ls -i a.txt b.txt`. Observe they are the SAME number.
4. Edit `a.txt`. Does `b.txt` change? (Yes).
5. Delete `a.txt`. Does `b.txt` still exist? (Yes). 
6. Discuss: When is a file actually "Deleted" from the disk? (Answer: When the link count hits zero).

**Part 3: Soft Link Experiment**
1. Create a soft link: `ln -s b.txt c.txt`.
2. Check Inodes: `ls -i b.txt c.txt`. Observe they are DIFFERENT.
3. Delete `b.txt`. Try to read `c.txt`. 
4. Observe the "Broken Link" error.

**Part 4: The Block Calculation**
1. Research your disk's block size: `stat -f %k .` (Mac) or `blockdev --getbsz /dev/sda` (Linux).
2. Create a 1-byte file. 
3. Use `du -sh <file>` and compare "Actual Size" (1 byte) vs "Size on Disk" (usually 4KB or 8KB).

---

### Common Gotchas & Troubleshooting
- **Gotcha 1:** Moving files across Disks. Moving a file on the same disk just changes a directory entry (instant). Moving to another disk requires copying every block (slow).
- **Gotcha 2:** The "Open File" mystery. If you delete a massive log file while a program is still writing to it, the disk space won't be freed until the program closes.

### Reflection Question
Why are "File Names" not stored inside the Inode itself? (Hint: Think about Hard Links).
