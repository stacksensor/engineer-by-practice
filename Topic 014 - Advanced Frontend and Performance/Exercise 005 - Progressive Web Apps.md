# Exercise 005 - Progressive Web Apps (PWA)

### Objective
Build "Offline-First" experiences. Implement Service Workers and Manifest files to transform your standard web application into a Progressive Web App that users can "Install" on their mobile devices and use even when the internet is disconnected.

### Core Concepts to Master
- **Service Workers:** A client-side proxy that sits between your app and the network, capable of intercepting requests and serving cached data.
- **The Web App Manifest:** A JSON file that defines how the app appears when "Installed" (Icons, theme colors, display mode).
- **Caching Strategies:** Understanding when to use "Cache-First" (for images/static assets) vs "Network-First" (for dynamic API data).
- **Background Sync:** Allowing the browser to defer actions (like sending an email or submitting a form) until the user's connection is restored.

### Research Topics
- "What is a Service Worker lifecycle (Install, Activate, Fetch)"
- "PWA requirements for the 'Install' prompt to appear"
- "Using Workbox for Service Worker management"
- "Testing PWAs with Chrome Lighthouse"

---

### The Practical Challenge

**Part 1: The Manifest**
1. Create a `manifest.json` file in your project's public directory.
2. Define the `name`, `short_name`, and `start_url`.
3. Provide an array of icons in various sizes (e.g., 192x192, 512x512).
4. Link the manifest in your HTML `<head>`. 
5. Open Chrome DevTools > Application > Manifest. Verify that the browser correctly identifies your app as "Installable."

**Part 2: Registering the Service Worker**
1. Create a `sw.js` file in your public root.
2. Add the registration script to your main `index.js`:
   ```javascript
   if ('serviceWorker' in navigator) {
     navigator.serviceWorker.register('/sw.js');
   }
   ```
3. Inside `sw.js`, listen for the `install` event and cache your core assets (CSS, JS, index.html) using the `caches.open()` API.

**Part 3: The Interceptor**
1. In `sw.js`, add a listener for the `fetch` event.
2. Implement a "Stale-While-Revalidate" strategy: 
   - Check if the requested file is in the cache. 
   - If yes, return it immediately to the user.
   - Simultaneously, fetch the latest version from the network and update the cache for next time.
3. Test by turning on "Offline" mode in the Network tab. Refresh the page. Your app should still load!

**Part 4: Custom Offline Pages**
1. Create a simple `offline.html` page.
2. Update your Service Worker logic: If a network request fails and the resource is NOT in the cache, serve the `offline.html` page instead of the generic browser "No Internet" screen.
3. Run a **Lighthouse** audit in Chrome. Observe your "PWA" score. Fix any remaining issues (e.g., missing theme colors or HTTPS requirements).

---

### Common Gotchas & Troubleshooting
- **Gotcha 1:** Service Worker Scope. By default, a Service Worker located at `/js/sw.js` can only intercept requests starting with `/js/`. Always place your `sw.js` in the absolute root directory of your project.
- **Gotcha 2:** Caching old files. If you don't implement a cache-versioning strategy (e.g., naming your cache `static-v2`), users might get stuck with an old version of your CSS even after you've updated the server.

### Reflection Question
How does a PWA bridge the gap between "Web Applications" and "Native Apps" on mobile platforms like iOS and Android?
