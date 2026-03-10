# Exercise 001 - The Cost of Latency: $1M per 100ms

### Objective
Money is time. Master the financial impact of your code's performance. Learn about the famous **Amazon/Google Latency Study** and understand why a 100ms delay in a mobile app can result in a 1% drop in sales. Learn how to calculate the "ROI" (Return on Investment) of a performance fix and how to speak about "Speed" in terms of "Dollars."

### Core Concepts to Master
- **The Latency-to-Revenue link:** As your app gets slower, users get bored and leave before buying.
- **Conversion Rate:** The % of users who buy something. (e.g., 2% for a fast app; 1.5% for a slow app).
- **Opportunity Cost:** The money you AREN'T making because your code is inefficient.
- **The "Business Case" for Speed:** How to convince your boss to let you spend 1 week "Optimizing the DB" by showing them the potential money saved.

### Research Topics
- "Amazon: 100ms of latency cost 1% in sales (The 2006 study)"
- "Google: 0.5s of search delay dropped traffic by 20%"
- "Determining the financial value of a 'Page Load' second"
- "The performance budget in ecommerce"

---

### The Practical Challenge

**Part 1: The Amazon Math (Simulation)**
1. Company: $1,000,000,000 in annual sales.
2. Latency: Current 500ms.
3. Fix: You spend 2 weeks and get it down to 400ms (100ms improvement).
4. If the "1% more sales" rule holds, how much "New Money" did you just generate for the company? 
5. (Answer: $10,000,000).
6. Discuss: Was your 2-week salary worth it for the company? (Answer: Extremely!).

**Part 2: The Google "Bail" Point**
1. Research the "Bail" point: At what number of seconds do 50% of users "Close the tab" before the page even loads?
2. (Answer: Usually ~3 seconds).
3. If your app takes 4 seconds to load, calculate how many users you are "Losing" every day compared to a 2-second app.

**Part 3: The "Wait" Cost (Internal Productivity)**
1. A company has 1,000 developers. 
2. Every build takes 5 minutes. They build 10 times a day.
3. Total "Wait" time for the whole company: (1,000 * 50 minutes) = 50,000 minutes = ~833 hours PER DAY.
4. Calculate the monthly cost if an average developer costs $100/hour. 
5. (Answer: ~833 * 100 * 20 days = $1.6 Million per month).
6. Discuss why buying faster laptops (or speeding up the build) is the smartest business decision.

**Part 4: Identifying the "Critical" page**
1. Which page is "Worth more" to optimize?
   - **Checkout Page:** (Answer: High. Any delay here loses a sale).
   - **Terms & Conditions Page:** (Answer: Low. Almost no one reads it).
   - **Search Page:** (Answer: Medium-High. If people can't find it, they can't buy it).

---

### Common Gotchas & Troubleshooting
- **Gotcha 1:** Diminishing Returns. Moving from 10 seconds to 1 second is worth millions. Moving from 0.01ms to 0.005ms is useless for humans. Don't "Over-optimize" where it doesn't matter.
- **Gotcha 2:** The "Cheap" Trap. Buying a cheap database that crashes once a week saves $500/month but costs $50,000/hour in lost sales during an outage.

### Reflection Question
Why is the "Fastest" company in a market (like Amazon or Google) almost always the "Largest" company in that market? (Answer: Because speed is the fundamental part of the 'User Experience' that creates 'Trust' and 'Loyalty').
