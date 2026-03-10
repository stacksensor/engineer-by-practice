# Exercise 006 - Serverless Economics & The "Free Tier"

### Objective
Scale to zero. Master the economics of **Serverless** (Lambda, Cloud Functions, Fargate). Learn how to determine the "Break-even" point where Serverless becomes *more* expensive than a traditional server, and learn how to optimize your code (Memory and Execution Time) to reduce your monthly function bill.

### Core Concepts to Master
- **Execution-based Billing:** Paying for the millisecond of compute used.
- **Memory vs. Cost:** Why higher memory in Lambda sometimes makes the function *cheaper* overall because it finishes faster.
- **Cold vs. Warm starts:** The "Hidden Cost" of cold starts on user experience and compute overhead.
- **Scale to Zero:** The primary economic advantage: Paying $0 when nobody is using the site.

### Research Topics
- "AWS Lambda pricing example: Million requests"
- "Lambda power tuning: Finding the optimal memory/cost"
- "When is EC2 cheaper than Lambda?"

---

### The Practical Challenge

**Part 1: The Milli-second Math**
1. You have a Function that runs for 500ms on 128MB.
2. If you increase memory to 1024MB, the function runs for 50ms. 
3. Research the pricing formula for your provider. 
4. Calculate: Which configuration is cheaper? (Hint: Providers charge based on [GB-Seconds]).

**Part 2: The Break-even Analysis**
1. An EC2 instance costs $50 / month. 
2. 1 million Lambda requests cost roughly $2 / month (depending on duration).
3. Calculate: At how many millions of requests per month does the EC2 instance become cheaper than the Lambda?
4. Discuss: Beside price, why would you *still* choose Lambda even if it's 20% more expensive? (Maintenance/Scaling).

**Part 3: The "Always On" Serverless**
1. Research "Provisioned Concurrency." 
2. Discuss why paying to "Keep a Lambda warm" is essentially moving back toward the "Server" model and how it affects your FinOps strategy.

**Part 4: Monitoring for Cost Spikes**
1. (Conceptual): Design a CloudWatch Alarm that fires if a specific Lambda function starts using 5x its normal average execution time.
2. Discuss: Is this a "Performance" bug or a "Security" bug (e.g., Infinite loop or a DDOS attack)?

---

### Common Gotchas & Troubleshooting
- **Gotcha 1:** The "Logging" trap. Writing massive amounts of logs from a high-frequency Lambda can cost more in "CloudWatch Logs" storage than the actual compute! Log only what you need in production.
- **Gotcha 2:** External Dependencies. If your Lambda is "waiting" for an external API that is slow, you are paying for that Lambda to "Sit and do nothing" for those seconds.

### Reflection Question
Why is "Fast Code" in a serverless environment directly equivalent to "Saved Money"?
