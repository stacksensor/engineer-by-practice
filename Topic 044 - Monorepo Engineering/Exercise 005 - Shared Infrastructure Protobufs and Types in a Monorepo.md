# Exercise 005 - Shared Infrastructure: Protobufs and Types in a Monorepo

### Objective
Sync the language. Use the power of a monorepo to maintain **Single Source of Truth** for API contracts (Protobuf/Thrift) and TypeScript interfaces across Frontend, Backend, and Mobile codebases.

### Core Concepts to Master
- **Protobuf (Protocol Buffers):** A neutral language format (IDL) that can be compiled into Java, Go, JS, and Rust simultaneously.
- **Shared Types (`@shared/types`):** Why "Copy-pasting" a User interface between /app and /api is the #1 cause of bugs in production.
- **Contract-Driven Development:** Proposing a change in the `/proto` folder *before* writing a single line of feature code.
- **The "Breaking Change" Guard:** If you change a field in the monorepo, its "Type error" will immediately break the CI of the Frontend and Backend together.

### Research Topics
- "gRPC and Protobuf: Designing cross-language interfaces"
- "Shared TypeScript types in a monorepo: Best practices"
- "Code Generation in Nx or Turborepo from .proto files"
- "JSON Schema vs. Protobuf for shared contracts"

---

### The Practical Challenge

**Part 1: The "Copy-Paste" Bug (Scenario)**
1. You have `App` and `API`. Both use a `User` object with `id: string`.
2. You change the API to `id: number` but forget to update the App.
3. Your app crashes because `1 !== "1"`.
4. **The Monorepo fix:** Create a `/shared/types.ts` folder.
5. Link it to both. When you change `/shared`, BOTH your App and API "Error out" together in the editor.
6. Discuss: How does this "Fearless Refactoring" improve the speed of a team of 1,000 engineers?

**Part 2: The "Neutral" IDL (Concept)**
1. Backend is in **Go**. Frontend is in **TypeScript**.
2. You create a `message.proto` file.
3. You run a `compile` command. 
4. It outputs `message.go` and `message.ts`. 
5. Discuss: Why is Protobuf better than just writing the Go code and the TS code by hand? (Answer: Because they are *guaranteed* to match).

**Part 3: The "breaking" CI**
1. You delete the `email` field from the shared proto.
2. In a monorepo, YOUR PR will fail because it breaks the App.
3. In microrepos, you would merge the API change, and the App would break *later* in production.
4. Discuss: Why does a monorepo shift "Failure" from production to the PR stage?

---

### Common Gotchas & Troubleshooting
- **Gotcha 1:** Local Generation. If Developer A runs the compiler on a Mac and Developer B runs it on Linux, the "Generated Code" might be different. (Solution: Run the generation in **Docker** or as a **CI task**).
- **Gotcha 2:** Monorepo Bloat. If 1,000 files are generated every time you save, your IDE will lag. (Solution: Commit the generated code to Git so the IDE doesn't have to re-read it).

### Reflection Question
Why is a monorepo the "Ultimate Tool" for preventing API contract mismatches? (Answer: Because the 'Consumer' and the 'Producer' are in the same repository, allowing the CI to test them together).
