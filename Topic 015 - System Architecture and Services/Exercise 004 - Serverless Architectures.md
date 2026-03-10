# Exercise 004 - Serverless Architectures (AWS Lambda)

### Objective
Embrace "Code-as-a-Service." Move away from managing servers entirely by implementing event-driven Serverless functions. Learn how to package logic into independent units that only execute when triggered, offering infinite scalability and significantly lower costs for low-traffic applications.

### Core Concepts to Master
- **FaaS (Function-as-a-Service):** The paradigm where you upload code snippets (Functions) rather than entire server applications.
- **Cold Starts:** The latency period when a serverless function is first "Warmed Up" after being idle.
- **Event Triggers:** Actions that cause a function to run (e.g., an HTTP request, a file upload to S3, or a scheduled timer).
- **Statelessness:** Serverless functions cannot store data in memory between executions. Every request must be treated as independent.

### Research Topics
- "What is Serverless and how does it work?"
- "AWS Lambda vs Google Cloud Functions"
- "Serverless Framework vs SAM"
- "Pros and cons of serverless computing"

---

### The Practical Challenge

**Part 1: The First Lambda**
1. Create a free AWS account (or use a local emulator like **LocalStack**).
2. Create your first Lambda function using the AWS Console or CLI.
3. Write a simple Node.js handler:
   ```javascript
   exports.handler = async (event) => {
     return {
       statusCode: 200,
       body: JSON.stringify("Hello from Serverless!")
     };
   };
   ```
4. Test the function and view the logs in CloudWatch.

**Part 2: The API Gateway**
1. A Lambda function has no URL by default.
2. Use **AWS API Gateway** to create a REST endpoint.
3. Link the `GET` method of your endpoint to your Lambda function.
4. Visit the public URL in your browser. You just served a web request without a running server!

**Part 3: Event-Driven File Processing**
1. Create an AWS S3 bucket.
2. Configure a "Trigger" so that every time a `.txt` file is uploaded to the bucket, your Lambda function runs.
3. Have the Lambda function read the file, count the words, and log the result.
4. Upload a few files and verify the logs. This is the "Glue" that powers modern cloud architectures.

**Part 4: Deployment Automation**
1. Manually clicking in the AWS UI is not sustainable.
2. Install the **Serverless Framework** CLI: `npm install -g serverless`.
3. Create a `serverless.yml` file to define your function and its API trigger as code.
4. Deploy the stack using `sls deploy`. This demonstrates "Infrastructure as Code" (laC).

---

### Common Gotchas & Troubleshooting
- **Gotcha 1:** Execution Limits. Serverless functions usually have a maximum runtime (e.g., 15 minutes). You cannot use them for extremely long-running tasks like big data crunching or video rendering.
- **Gotcha 2:** Database Connection Limits. If 1,000 Lambda functions spawn at once, they might attempt to open 1,000 simultaneous connections to your SQL database, causing it to crash. Use a connection pooler like **RDS Proxy** or an HTTP-based database.

### Reflection Question
Why is the "Serverless" model often significantly cheaper for small projects or infrequent tasks compared to renting a dedicated EC2 server?
