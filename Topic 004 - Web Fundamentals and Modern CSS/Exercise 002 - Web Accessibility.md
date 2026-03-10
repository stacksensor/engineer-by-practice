# Exercise 002 - Web Accessibility (a11y)

### Objective
Ensure your web content is legally compliant and functionally accessible to all users, specifically targeting those using assistive technologies like screen readers or keyboard-only navigation.

### Core Concepts to Master
- **WCAG (Web Content Accessibility Guidelines):** The international standard outlining exactly how to make web content accessible.
- **ARIA (Accessible Rich Internet Applications):** A set of specific HTML attributes (`role`, `aria-label`, `aria-hidden`) added to elements to declare extra semantic information to screen readers parsing complex JavaScript interfaces.
- **Focus States and Keyboard Navigation:** Ensuring users without a mouse can navigate your application purely using `Tab`, `Shift+Tab`, `Enter`, and `Space`.

### Research Topics
- "Web Accessibility (a11y) checklist"
- "When to use ARIA attributes vs Semantic HTML"
- "HTML tabindex attribute explained"
- "Image alt text best practices"

---

### The Practical Challenge

**Part 1: Keyboard Exclusivity**
1. Open the `index.html` blog file you built yesterday.
2. Unplug your mouse entirely, or promise not to touch your trackpad.
3. Open the file in your browser. Hit the `Tab` key. Notice how a visible focus ring (usually a blue outline) jumps between your three navigation links.
4. Add a standard `<button>Submit</button>` to the bottom of the page. Tab to it and press `Enter`. Native interactive elements are focusable by default.
5. Add a fake button using a div: `<div class="fake-btn">Click Me</div>`. Tab through your page. Assume you don't have a mouse. **Notice how the fake button is totally invisible to keyboard navigation!**

**Part 2: Fixing the Focus**
1. To make the div focusable, add a tabindex: `<div class="fake-btn" tabindex="0">Click Me</div>`. Try jumping to it with `Tab` now.
2. Understand that even though it is focusable, pressing `Enter` on it will do nothing (unlike a real `<button>`), because divs do not inherently bind keyboard events. You would need to write complex JavaScript to handle `keydown(enter)` to simulate a button.
3. *Lesson:* Always use native Semantic tags (`<button>`, `<a>`, `<input>`) before injecting `tabindex` hacks onto `<div>` or `<span>` elements. Remove the fake button from your code.

**Part 3: The Image Alternative**
1. Add an image to one of your articles: `<img src="https://via.placeholder.com/150" />`.
2. A screen reader hitting this tag will literally read aloud "H-T-T-P-S colon slash slash via dot placeholder..." to the blind user. This is a terrible UX experience.
3. Add the `alt` tag: `<img src="https://via.placeholder.com/150" alt="A grey placeholder square for the article" />`. Now, the screen reader will read the descriptive text aloud instead.
4. Add a purely decorative, meaningless visual flair using an image (like a tiny swirly underline icon beneath your header). Give it an empty alt tag: `alt=""`. This instructs screen readers to completely skip it.

**Part 4: ARIA Labels for Iconography**
1. Many modern websites use icon fonts (like FontAwesome text `fa-bars`) to render a "Hamburger" mobile menu button without printing the actual word "Menu".
2. Create an icon-only button: `<button>☰</button>`. Note: A screen reader will read "Button. Three mathematical horizontal lines."
3. Fix it by explicitly defining an aria-label: `<button aria-label="Open navigation menu">☰</button>`.
4. Now, sighted users see the icon, but visually impaired users hear "Open navigation menu. Button."

---

### Common Gotchas & Troubleshooting
- **Gotcha 1:** Using `tabindex="-1"` is valid and highly useful! It permanently removes an element from the keyboard Tab flow, but allows you to programmatically focus it using JavaScript `.focus()` (vital for accessible popup modals).
- **Gotcha 2:** 'No ARIA' is infinitely better than 'Bad ARIA'. The first rule of ARIA is: If you can use a native HTML5 element (like `<nav>`) instead of an ARIA role (like `<div role="navigation">`), do it natively.
- **Gotcha 3:** Stripping the default CSS focus ring (`outline: none;`) to make your site "look cleaner" will cause you to fail basic WCAG accessibility tests instantly. If you remove it, you must dynamically paint a custom replacement ring when `:focus` state triggers.

### Reflection Question
Imagine you used CSS to visually color all invalid form inputs in red, but left the valid ones white. Why does this immediately fail WCAG Level-A accessibility compliance, and how would you fix it?