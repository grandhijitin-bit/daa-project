# Presentation Speaker Script & Execution Guide
## "Sky-High Profits: Optimizing Airline Ticket Revenue with 0/1 Knapsack DP"

---

### Slide 1: Title & Hook
* **Visual:** Dark aerospace cockpit telemetry with cyan pulsing vacant seats and revenue statistics.
* **Estimated Time:** 1:00 min
* **What to Say:**
  > "Good morning, professors and fellow engineers. In the airline industry, planes take off with razor-thin margins. A single seat flying empty on a cross-country route is revenue lost forever. 
  > When group bookings arrive minutes before gate closure, airlines face a high-stakes combinatorial puzzle. Today, we will explore why standard human intuition and greedy sorting fail, and how 0/1 Knapsack Dynamic Programming guarantees mathematically optimal revenue packing for global airlines."

---

### Slide 2: Real-World Story — The Group Booking Crisis at Gate 14
* **Visual:** 3-Column scenario layout (Bottleneck, 3 Suitors, Greedy Blunder).
* **Estimated Time:** 1:30 min
* **What to Say:**
  > "Picture this: It's 45 minutes before departure for SkyConnect Flight 819. Exactly 6 seats remain on the aircraft before the doors seal.
  > Suddenly, three independent group coordinators rush the gate desk: a youth soccer squad needing 3 seats for $400, a VIP tech executive delegation offering $600 for 4 seats, and a sightseeing duo offering $300 for 2 seats. 
  > Combined demand is 9 seats, but we only have 6. The untrained gate agent panics and makes a classic heuristic error: 'Take the biggest immediate check first!' They accept the VIP group for $600. 
  > But look at what happens: 4 seats are consumed, leaving 2 seats stranded. The soccer team can't split up, so those 2 seats fly completely empty. The airline lost hundreds of dollars on that single decision."

---

### Slide 3: Why Greedy Fails & DP Wins
* **Visual:** Split-screen head-to-head comparison with red vs. green containers.
* **Estimated Time:** 1:30 min
* **What to Say:**
  > "Why did greedy logic fail here? In computer science, Greedy heuristics work wonders for *Fractional Knapsack*—problems where items can be divided continuously, like jet fuel or grain. 
  > But human passengers are strictly indivisible. You cannot board 1.5 soccer players. This indivisibility is the fundamental hallmark of the 0/1 Knapsack problem. 
  > If you sort by total revenue, you create fragmented empty space. If you sort by unit price per seat, you might pick smaller groups that leave high-capacity blocks stranded. 
  > Dynamic Programming wins because it doesn't gamble on local choices; it systematically evaluates overlapping subproblems and guarantees the global optimum."

---

### Slide 4: The 0/1 Knapsack Formulation
* **Visual:** Bento grid showcasing State $dp[i][w]$, Base Cases, and the Bellman Recurrence Equation.
* **Estimated Time:** 2:00 min
* **What to Say:**
  > "Let’s formalize this with the Bellman Optimality Equation. 
  > We define our DP state as $dp[i][w]$, representing the maximum revenue possible considering the first $i$ booking requests under an aircraft seat capacity of $w$.
  > Our base cases are simple: 0 requests or 0 remaining seats yield $0 revenue.
  > For every incoming booking, we face an binary 0/1 choice:
  > Either we reject group $i$ and carry forward the best revenue from $dp[i-1][w]$, 
  > or, if capacity allows, we accept group $i$, collect their revenue $v_i$, and add the optimal revenue from the remaining capacity $dp[i-1][w - w_i]$.
  > Taking the maximum of these two decisions at each step guarantees optimality."

---

### Slide 5: Step-by-Step Numerical Example (Problem Setup)
* **Visual:** Boeing 737 cockpit HUD with 4 detailed Boarding Pass vouchers.
* **Estimated Time:** 1:15 min
* **What to Say:**
  > "Let’s ground this in a real calculation. Our aircraft has $W = 6$ seats available, and we have 4 competing booking requests:
  > Request 1: 2 seats for $300 ($150/seat).
  > Request 2: 3 seats for $400 ($133/seat).
  > Request 3: 4 seats for $600 ($150/seat).
  > Request 4: 1 seat for $150 ($150/seat).
  > Notice that requests 1, 3, and 4 all have identical price density ($150/seat), making greedy tie-breaking completely blind. Let's see how the DP matrix handles this."

---

### Slide 6: Numerical Walkthrough (The 5x7 DP Matrix)
* **Visual:** Full 5x7 table with interactive 'Highlight Backtrack Path' action and decision inspector.
* **Estimated Time:** 2:30 min
* **What to Say:**
  > *(Click the 'Highlight Backtrack Path' button on the slide)*
  > "Here is our 5-row by 7-column DP matrix. Notice it is 5 by 7 because of the 0-based base cases for zero bookings and zero capacity.
  > Looking at the final cell $dp[4][6]$, our maximum revenue is $900.
  > How do we know which groups to board? We backtrack:
  > At $dp[4][6]$, the value matches row 3, meaning Request 4 was rejected.
  > At $dp[3][6]$, the value came from $dp[2][2] + 600$, meaning Request 3 is accepted! We deduct 4 seats, moving to capacity 2.
  > At $dp[2][2]$, the value matches row 1, meaning Request 2 was rejected.
  > At $dp[1][2]$, the value came from $dp[0][0] + 300$, meaning Request 1 is accepted!
  > Our optimal flight manifest: Request 1 (2 seats) + Request 3 (4 seats) = Exactly 6 seats filled, generating $900 in revenue."

---

### Slide 7: Live Classroom Activity ("Beat the Knapsack")
* **Visual:** Interactive 60s countdown timer with 3 options and reveal card.
* **Estimated Time:** 2:00 min
* **What to Say:**
  > *(Click 'Start' on the timer)*
  > "Now, let’s test human intuition against the algorithm. You have 60 seconds.
  > The plane has 5 seats left. 
  > Option A offers $420 for 4 seats ($105/seat).
  > Option B offers $300 for 3 seats ($100/seat).
  > Option C offers $200 for 2 seats ($100/seat).
  > Who would accept Option A? *(Wait for hands)*
  > Option A has the highest single payout and the highest price per seat! 
  > *(Click 'Reveal DP Solution')*
  > But human greed loses! Option A leaves 1 seat empty, yielding $420.
  > Dynamic Programming selects Option B plus Option C: 3 + 2 = 5 seats packed to 100% capacity, yielding $500! 
  > DP just earned the airline an extra $80 (+19%) on a single gate interaction."

---

### Slide 8: Complexity Analysis & Space Optimization
* **Visual:** 3 Complexity metric cards + Reverse traversal 1D array diagram.
* **Estimated Time:** 1:45 min
* **What to Say:**
  > "From an engineering perspective, how scalable is this?
  > Brute force requires checking $2^N$ combinations. With 40 requests, that's over 1 trillion operations—totally infeasible for real-time check-in.
  > DP runs in $O(N \cdot W)$ time. Because $W$ is a numeric value, this is pseudo-polynomial, executing in less than a millisecond for typical flight sizes.
  > Even better, we don't need a 2D matrix in production. We can optimize space to $O(W)$ using a single 1D array.
  > Crucial engineering caveat: You must iterate the capacity loop backwards from $W$ down to $w_i$. If you loop forward, you overwrite subproblem states from the current iteration and accidentally re-use the same group, turning 0/1 knapsack into unbounded knapsack!"

---

### Slide 9: Three Real-World Applications
* **Visual:** 3 Industrial Horizon Cards (Air Cargo, Hotel Room Blocks, Cloud VM Packing).
* **Estimated Time:** 1:30 min
* **What to Say:**
  > "This formulation extends far beyond passenger cabins:
  > 1. **Air Cargo & Belly Freight:** FedEx and Lufthansa Cargo use it to balance aircraft payload weight envelopes against high-tariff freight shipments.
  > 2. **Hotel Room Block Allocation:** Chains like Marriott optimize blocks for conventions and wedding parties against remaining suite inventories.
  > 3. **Cloud VM Packing:** Hyperscalers like AWS EC2 and Azure use multidimensional knapsack algorithms to pack tenant virtual machines onto physical bare-metal hardware racks with zero wasted RAM or CPU."

---

### Slide 10: Conclusion & Q&A
* **Visual:** 3 Executive Takeaways + Q&A Telemetry Landing Hub.
* **Estimated Time:** 1:00 min
* **What to Say:**
  > "To summarize:
  > First: Greedy algorithms fail when items are indivisible.
  > Second: 0/1 Knapsack DP guarantees global maximum revenue in pseudo-polynomial time.
  > Third: Reverse-traversal 1D arrays make this algorithm microsecond-fast and production-ready for live airline reservation engines.
  > Our flight is now safely parked at the gate. Thank you, and we welcome any questions from the floor!"

---

### Anticipated Q&A Questions & Model Answers

**Q1: What if flight capacity $W$ is huge, like 500 seats? Does $O(N \cdot W)$ get slow?**
> *Answer:* Even with $N = 200$ group requests and $W = 500$ seats, $N \cdot W$ is only 100,000 basic array operations. On modern CPUs, this executes in under 0.2 milliseconds. The pseudo-polynomial nature only becomes an issue if capacities reach millions or billions.

**Q2: What if groups have time preferences or seat adjacency requirements?**
> *Answer:* That becomes a Multi-Dimensional or Constrained Knapsack problem. We add a secondary constraint dimension (e.g., aisle vs. window or seat rows), which adds an extra index to our DP state: $dp[i][w][c]$.

**Q3: Why can't we use Fractional Knapsack and round the numbers?**
> *Answer:* Rounding fractional knapsack solutions often violates the capacity bound (exceeding plane seats) or leaves massive unused gaps, leading to sub-optimal revenue and angry passengers when groups are fragmented.

