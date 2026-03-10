# Exercise 001 - gRPC & Protocol Buffers

### Objective
Move beyond REST/JSON. Master **gRPC** and **Protocol Buffers (Protobuf)** to build highly efficient, type-safe, and low-latency communication between services. Learn why binary serialization is faster than text-based JSON and how to define service contracts that work across different programming languages.

### Core Concepts to Master
- **Protocol Buffers:** A language-neutral, platform-neutral, extensible mechanism for serializing structured data.
- **Service Definition:** Writing `.proto` files to define the "API Contract" (methods and message types).
- **HTTP/2 Transport:** How gRPC uses features like multiplexing and binary framing to improve performance over HTTP/1.1.
- **Code Generation:** Using the `protoc` compiler to generate client and server stubs in your language of choice.

### Research Topics
- "gRPC vs REST: When to use which?"
- "Protocol Buffers language guide (proto3)"
- "HTTP/2 vs HTTP/1.1 for API developers"

---

### The Practical Challenge

**Part 1: Defining the Contract**
1. Create a `message.proto` file.
2. Define a simple `Greeter` service with a `SayHello` method.
3. Define the Request and Response messages (using types like `string`, `int32`, etc.).

**Part 2: Generating Code**
1. Install the `protoc` compiler and the gRPC plugins for your preferred language (e.g., Python, Node.js, or Go).
2. Generate the client and server code from your `.proto` file.

**Part 3: The gRPC Server**
1. Implement the `SayHello` logic on the server side.
2. Start the server on a specific port (e.g., 50051).

**Part 4: The gRPC Client**
1. Write a client script that connects to the server and calls the `SayHello` method.
2. Compare the payload size of a gRPC message vs a JSON equivalent. (Hint: Use a network tool or just print the byte length).

---

### Common Gotchas & Troubleshooting
- **Gotcha 1:** Breaking Changes. If you change a field's "Tag Number" (e.g., changing `string name = 1;` to `string name = 2;`), you will break all existing clients. Tags are the "Identity" of the data in the binary stream.
- **Gotcha 2:** Load Balancing. Standard Load Balancers (Layer 4) struggle with gRPC because it uses long-lived HTTP/2 connections. You often need a "Linkerd" or "Envoy" proxy to do proper Layer 7 balancing.

### Reflection Question
How does gRPC's use of "Strong Types" in the contract help prevent bugs that usually occur in REST APIs (like a client sending a string where the server expects an integer)?
