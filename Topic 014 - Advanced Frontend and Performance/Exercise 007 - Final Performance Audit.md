# Exercise 007 - Final Performance Audit

### Objective
Put it all together. Take a "Monolithic" and slow application and apply everything you've learned in Topic 014—memoization, virtualization, code-splitting, and lazy loading—to achieve a 95+ score on the Chrome Lighthouse Performance audit.

### Core Concepts to Master
- **Lighthouse Performance Score:** Understanding the metrics (FCP, LCP, CLS, TBT) that define a "Fast" website.
- **Code Splitting:** Using `React.lazy` and Dynamic Imports to ensure the user only downloads the code needed for the current page.
- **Asset Optimization:** Using modern image formats (WebP/AVIF) and minification to reduce payload sizes.
- **Critical Rendering Path:** Prioritizing the loading of CSS and JS required for the "Above-the-fold" content.

### Research Topics
- "Core Web Vitals explained (LCP, FID, CLS)"
- "How to analyze a Webpack/Vite bundle"
- "React performance optimization checklist"

---

### The Practical Challenge

**Part 1: The Baseline Audit**
1. Create (or download) a sample React application that is intentionally inefficient:
   - Includes 5 MB of unoptimized JPEG images.
   - Imports massive libraries (like `lodash` or `moment`) but only uses one function.
   - Renders a table of 2,000 items without virtualization.
2. Run a Chrome Lighthouse audit. Save the report. Your goal is to improve the "Performance" score from ~20 to ~95.

**Part 2: Payload Reduction**
1. Replace heavy libraries with native JS alternatives (e.g., use `Intl.DateTimeFormat` instead of `moment`).
2. Use a "Bundle Analyzer" tool to identify which imports are taking up the most space.
3. Optimize your images. Convert them to WebP and implement responsive `srcset` attributes so mobile users get smaller files.

**Part 3: Code Splitting**
1. Implement "Route-based Code Splitting." Ensure that the "Settings" page code is not loaded when the user is on the "Home" page.
2. Use `<Suspense>` to provide a clean loading fallback while the chunks are being fetched.
3. Notice the "Network" tab in the browser. You should see new `.js` files loading only when you click on specific navigation links.

**Part 4: The Final Verification**
1. Re-run your Lighthouse audit. 
2. Review the "Opportunity" section. If your CLS (Cumulative Layout Shift) is high, ensure your image tags have explicit `width` and `height` attributes.
3. If your TBT (Total Blocking Time) is high, verify that you aren't running heavy JS loops on the main thread during startup.
4. Achieve the "Magic Green" score. Congratulations, you are now a specialized Frontend Performance Engineer.

---

### Common Gotchas & Troubleshooting
- **Gotcha 1:** False Positives. If you run Lighthouse with browser extensions (like AdBlock) enabled, your score will be lower than reality. Always run audits in an "Incognito" window.
- **Gotcha 2:** Premature Optimization. Don't spend 5 hours optimizing a component that only renders once and takes 2ms. Use the Profiler to solve real problems, not theoretical ones.

### Reflection Question
Why are "Core Web Vitals" (like Largest Contentful Paint) prioritized by Search Engines (Google) for SEO rankings rather than just simple "Page Load Time"?
