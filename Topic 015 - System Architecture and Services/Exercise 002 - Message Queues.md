# Exercise 002 - Message Queues (RabbitMQ/Kafka)

### Objective
Implement "Asynchronous Communication." Learn how to use Message Queues (like RabbitMQ) to decouple your services, allowing them to handle heavy tasks (like sending emails or generating PDFs) in the background without making the user wait for a response.

### Core Concepts to Master
- **Message Broker:** The middleman (RabbitMQ, Redis, or Kafka) that stores and routes messages between the "Producer" and the "Consumer."
- **Produce & Consume:** The workflow where one service "Produces" a task and puts it on the queue, and another service "Consumes" and executes it.
- **Publish/Subscribe (Pub-Sub):** A pattern where one message is broadcast to multiple independent services simultaneously.
- **Durability & Acknowledgement (Ack):** Ensuring a message is not deleted from the queue until the consumer successfully performs the task.

### Research Topics
- "What is a message queue and why do we need them?"
- "RabbitMQ vs Apache Kafka differences"
- "Implementing a worker queue in Node.js with amqplib"
- "The amqp protocol basics"

---

### The Practical Challenge

**Part 1: The Producer**
1. Install RabbitMQ on your local machine using Docker: `docker run -d --name rabbit -p 5672:5672 rabbitmq`.
2. Create an Express server with a `POST /tasks` endpoint.
3. Use the `amqplib` library to connect to RabbitMQ.
4. When the endpoint is called, send a "job" message (e.g., `{"userId": 1, "type": "SEND_WELCOME_EMAIL"}`) to a queue named `task_queue`.
5. Respond to the user with "Task accepted" immediately, without sending an actual email.

**Part 2: The Consumer Worker**
1. Create a separate, plain Node.js script (not a web server) called `worker.js`.
2. Connect to the same RabbitMQ instance and listen to the `task_queue`.
3. When a message arrives, simulate a heavy task using a `setTimeout` for 3 seconds.
4. Log "Finished processing task for User 1."

**Part 3: Handling Concurrency**
1. Trigger 10 tasks in a row via your Express API.
2. Observe your `worker.js`. It will handle them one-by-one, taking 30 seconds total.
3. Open a second terminal and start a *second* instance of `worker.js`.
4. Trigger the tasks again. Note how the two workers "compete" for the queue, processing the tasks twice as fast (Round-robin distribution).

**Part 4: Failure & Persistence**
1. Intentionally stop your `worker.js` while it is in the middle of a task.
2. Observe RabbitMQ. If you didn't send an "Acknowledgement" (ack), the message will stay in the queue.
3. Restart the worker. Notice it immediately picks up the task it failed to finish. 
4. This "Durability" is why queues are a vital part of reliable high-scale systems.

---

### Common Gotchas & Troubleshooting
- **Gotcha 1:** Creating too many queues. You don't need a single queue per user. You generally need one queue per "Task Type" (e.g., `email_queue`, `image_processing_queue`).
- **Gotcha 2:** Memory Overflow. If your Producer sends 1 million messages but your Consumer is too slow, RabbitMQ will use all your RAM. Always implement "Prefetch" limits to ensure workers only take 1-2 tasks at a time.

### Reflection Question
How does using a Message Queue improve the "Availability" of your application from the perspective of the end-user?
