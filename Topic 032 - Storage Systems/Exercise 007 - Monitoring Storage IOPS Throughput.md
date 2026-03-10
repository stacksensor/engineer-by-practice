# Exercise 007 - Monitoring Storage (IOPS & Throughput)

### Objective
Measure the pressure. Master the two metrics that define storage speed: **IOPS (Input/Output Operations Per Second)** and **Throughput (MB/s)**. Learn how to identify a "Disk Bottleneck" and understand how **Latency** (the time for one request) differs from **Throughput** (the total volume of requests).

### Core Concepts to Master
- **Throughput:** The amount of data moved per second (e.g., "I can copy a 1GB file in 1 second = 1,000 MB/s").
- **IOPS:** The number of distinct "Read/Write" actions per second (e.g., "I can read 5,000 tiny log entries per second").
- **Disk Wait (%iowait):** The % of time the CPU is sitting idle because it is waiting for the slow disk to finish a job.
- **Queue Depth:** How many requests are waiting in line for the disk. High queue depth usually means the disk is overwhelmed.

### Research Topics
- "IOPS vs Throughput: A simple analogy"
- "How to use iostat and iotop"
- "Testing disk speed with 'fio' or 'dd'"
- "Why database performance is limited by IOPS, not Throughput"

---

### The Practical Challenge

**Part 1: The Throughput Test (Direct)**
1. Use `dd` to write a dummy 1GB file: 
   - `dd if=/dev/zero of=testfile bs=1M count=1000`.
   - Observe the "MB/s" reported.
2. Discuss: Is this testing the disk, or is it testing the OS cache? (Hint: Use `conv=fdatasync` to force it to hit the physical disk).

**Part 2: The IOPS Trap**
1. Imagine two disks:
   - Disk A: 1000 MB/s Throughput, but only 100 IOPS.
   - Disk B: 100 MB/s Throughput, but 10,000 IOPS.
2. Which disk is better for:
   - Copying a 10GB 4K movie file? (Answer: A).
   - Running a high-traffic SQL database? (Answer: B).

**Part 3: The `%iowait` Investigation**
1. On Linux, run `top` or `iostat -x 1`. 
2. Identify the `%wa` or `%iowait` column. 
3. If this number is >10%, your CPU is being "stolen" by the slow storage. 
4. Discuss: How do you fix this? (Answer: Get an SSD, use RAID, or use a cache).

**Part 4: Real-world benchmark**
1. Install a tool like **AmorphousDiskMark** (Mac) or **CrystalDiskMark** (Windows).
2. Look at the results for "Sequential" vs "4K Random." 
3. Observe how the "4K Random" speed is much, much slower than the Sequential speed. Why?

---

### Common Gotchas & Troubleshooting
- **Gotcha 1:** Cloud IOPS limits. In AWS/GCP, you can actually "buy" more IOPS for your disk. If you run out of "Burst Credits," your database will suddenly drop to a crawl.
- **Gotcha 2:** The "Controller" bottleneck. Sometimes you have an ultra-fast SSD, but it's connected to an old SATA port that can only handle 300MB/s. The slowest part of the chain always wins.

### Reflection Question
Why is the "Latency" of a disk (the time for one request) the most important metric for user-facing applications? (Answer: Because it determines if the app "feels" snappy vs lagged).
