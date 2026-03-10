# Exercise 003 - API Contracts: OpenAPI & Postman

### Objective
Document the promise. Master **API Contracts**—the machine-readable descriptions of your API. Learn how to use **OpenAPI (Swagger)** to define every field, every type, and every error code, and understand how this allows you to automatically generate code, documentation, and mock servers.

### Core Concepts to Master
- **OpenAPI / Swagger:** The standard YAML/JSON format for defining REST APIs.
- **The Contract-First Approach:** Writing the YAML file and getting it signed off by the team *before* anyone writes a single line of code.
- **The Code-First Approach:** Writing your code and using a tool to "Export" the YAML file.
- **Postman:** A tool for testing, documentation, and sharing "Collections" of APIs.
- **Mock Servers:** Automatically creating fake URLs that act like your API so the frontend team can build their app while the backend team is still working.

### Research Topics
- "OpenAPI 3.1: Features and overview"
- "Contract-First vs Code-First API design"
- "Generating client SDKs from an OpenAPI file"
- "Mocking an API with Postman or Prism"

---

### The Practical Challenge

**Part 1: The Contract-First Brainstorm**
1. You are building a `GetWeather` API.
2. Before you code, write a human-readable "Contract":
   - "Input: `lat` (Decimal), `lon` (Decimal)."
   - "Output: `temp` (Number), `unit` (String: 'C' or 'F')."
3. Discuss: If you change `lat` to `latitude` tomorrow, who will be angry? (Answer: Everyone who already wrote their apps).

**Part 2: The YAML definition**
1. Research the basic structure of an **OpenAPI YAML**: `paths`, `parameters`, `responses`.
2. Draw a snippet for a `GET /hello` endpoint that returns a `200` with `{"message": "hi"}`.

**Part 3: Generating Code**
1. Research **openapi-generator**. 
2. Discuss why being able to generate 10,000 lines of Python or TypeScript code from one 100-line YAML file is the "Superpower" of API documentation.

**Part 4: The Postman Collection**
1. Create a Postman account (or use the desktop app). 
2. Discuss: Why is a "Postman Collection" better than a "Word Document" for showing a colleague how to use your API? 
3. (Answer: They can click "Import" and run it instantly).

---

### Common Gotchas & Troubleshooting
- **Gotcha 1:** Out-of-Sync docs. If you change your code but forget to update the YAML, your documentation is a lie! This happens 99% of the time in "Manual" environments.
- **Gotcha 2:** Bad type definitions. If you say a field is a `string` but you sometimes send a `null`, you will crash every "Type-safe" app (like Swift or Java) that consumes your API.

### Reflection Question
Why is the "API Contract" considered the "Boring but essential" part of building a successful software company? (Answer: Because without it, teams spend 50% of their time in meetings asking "What does this field do?").
