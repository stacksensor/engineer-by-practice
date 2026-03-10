# Exercise 006 - Event-Driven Design & Webhooks

### Objective
Master "Passive Integration." Build systems that react to events happening in other applications via Webhooks, and implement your own Webhook provider to allow third-party developers to extend your platform's functionality automatically.

### Core Concepts to Master
- **Webhooks:** A "Reverse API" where a server sends an HTTP POST request to a client's URL when an event occurs (e.g., "Payment Successful").
- **Event-Driven Architecture (EDA):** A system design where services communicate by producing and consuming "Events" rather than direct API calls.
- **Retry Logic & Idempotency:** Handling cases where a webhook delivery fails or is sent multiple times by mistake.
- **Payload Verification:** Using HMAC signatures (e.g., `X-Hub-Signature`) to prove that a webhook actually came from a trusted source.

### Research Topics
- "What is a Webhook and how does it differ from Polling?"
- "Building a webhook receiver in Node.js"
- "Stripe Webhook integration best practices"
- "Idempotency keys in API design"

---

### The Practical Challenge

**Part 1: The Webhook Receiver**
1. Use an online tool like **Hookdeck** or **Webhook.site** to get a public URL.
2. Go to your GitHub profile and set up a Webhook for one of your repositories. 
3. Configure it to send a payload whenever someone "Stars" the repo or "Pushes" code.
4. Perform the action and inspect the incoming JSON payload. Notice the specific event type header.

**Part 2: Coding the Logic**
1. Create a local Express server. Use **ngrok** to expose it to the internet: `ngrok http 3000`.
2. Update the GitHub webhook to point to your ngrok URL (e.g., `https://xyz.ngrok-free.app/webhook`).
3. In your code, listen for specific events:
   ```javascript
   app.post('/webhook', (req, res) => {
     const eventType = req.headers['x-github-event'];
     if (eventType === 'push') {
       console.log('New code pushed! Running build...');
     }
     res.status(200).send('Event Received');
   });
   ```

**Part 3: The Security Handshake**
1. GitHub (and Stripe/Shopify) provides a "Secret" for your webhook.
2. In your code, use the `crypto` library to generate a signature of the incoming request body using your secret.
3. Compare your calculated signature with the one provided in the header. 
4. If they don't match, return a `401 Unauthorized`. This prevents hackers from triggering fake events in your system.

**Part 4: The Internal Hook Provider**
1. Imagine YOU are Stripe. Build an internal "subscription" system. 
2. Create a database table `Webhooks` where users can save their URLs.
3. When a "User Sign Up" event happens in your app, loop through all saved URLs and send a `POST` request with the user data.
4. Implement a simple "Retry" mechanism (using your knowledge from Exercise 002) if the recipient's server is down.

---

### Common Gotchas & Troubleshooting
- **Gotcha 1:** 30-Second Timeout. Webhook signals should be acknowledged with a `200 OK` immediately. If you try to run a 5-minute build process inside the webhook route, the provider will mark the delivery as "Failed" because it timed out waiting for a response. Always process heavy tasks in a background worker (Topic 15 Ex 002).
- **Gotcha 2:** Public Exposure. Your webhook receiver is publicly accessible. Without HMAC signature verification, anyone can send fake "Payment Success" packets to your server to get free products.

### Reflection Question
Why is "Polling" (repeatedly asking the server for updates) considered less efficient than "Webhooks" for real-time integrations?
