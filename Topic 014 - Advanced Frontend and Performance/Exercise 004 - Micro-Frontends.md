# Exercise 004 - Micro-Frontends (Module Federation)

### Objective
Scale your development teams. Implement the Micro-Frontend architectural pattern using Webpack 5 Module Federation to allow multiple independent teams to build, test, and deploy separate parts of a single web application simultaneously without interference.

### Core Concepts to Master
- **Micro-Frontends:** Breaking a monolith frontend into smaller, independent applications that are composed at runtime.
- **The Shell (Host):** The primary container application that "consumes" components and data from other remotes.
- **Remote Applications:** Independent applications that "expose" specific components or logic for use by other apps.
- **Shared Dependencies:** Configuring Module Federation so that only one copy of React (or other libraries) is loaded, regardless of how many micro-frontends are running.

### Research Topics
- "What is Webpack Module Federation"
- "Micro-frontends pros and cons"
- "Vite vs Webpack for Micro-frontends (Vite-plugin-federation)"
- "Orchestrating Micro-frontends in production"

---

### The Practical Challenge

**Part 1: The Remote Component**
1. Create a simple React application named `remote-app` using Vite and the `vite-plugin-federation`.
2. Build a sophisticated `DashboardCard` component. 
3. Configure the `vite.config.js` to "expose" this component:
   ```javascript
   federation({
     name: "remoteApp",
     filename: "remoteEntry.js",
     exposes: {
       "./DashboardCard": "./src/components/DashboardCard"
     }
   })
   ```
4. Build and preview the app. Verify that the `remoteEntry.js` file is accessible at the specified URL.

**Part 2: The Host Shell**
1. Create a second React application named `host-shell`.
2. Configure its `vite.config.js` to "consume" the remote:
   ```javascript
   federation({
     remotes: {
       remoteApp: "http://localhost:5001/assets/remoteEntry.js"
     }
   })
   ```
3. Use `React.lazy` to import and render the `<DashboardCard />` from the remote:
   `const DashboardCard = React.lazy(() => import("remoteApp/DashboardCard"));`
4. Observe the "Host" rendering a component that physically resides in a completely separate project.

**Part 3: Shared State & Style**
1. Attempt to pass props from the Host to the Remote component.
2. Note how styles (CSS) are handled. Does the remote's CSS automatically load in the host?
3. Configure "shared" libraries in both config files (e.g., `react` and `react-dom`).
4. Prove it works: Change the version of React in the remote but not the host. Verify the host still uses its own version for both.

**Part 4: Deployment Independence**
1. Imagine the `remote-app` belongs to the "Analytics Team" and the `host-shell` belongs to the "Platform Team."
2. The Analytics team updates their `DashboardCard` to have a new color and deploys it.
3. Refresh the `host-shell` browser tab WITHOUT rebuild/redeploying the host itself.
4. Witness the new color appearing. You have successfully decoupled deployment cycles!

---

### Common Gotchas & Troubleshooting
- **Gotcha 1:** Runtime Failures. If the remote server is down, the host app will crash when trying to load the component unless you wrap the lazy import in a React **Error Boundary**.
- **Gotcha 2:** CSS Leakage. If both the host and remote define a `.button` class, they might conflict. Use CSS Modules or CSS-in-JS (Tailwind, Styled Components) to ensure styles remain isolated.

### Reflection Question
Why is the Micro-Frontend pattern compared to back-end Microservices, and under what company size/scale does the overhead of this pattern become "worth it"?
