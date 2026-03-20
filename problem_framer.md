# Problem Framer — AI Help Center Chatbot
**Problem submitted:** 2026-03-20

---

## WHAT YOU THINK THE PROBLEM IS

You believe the problem is **too many support tickets** — and that an AI chatbot will deflect enough of them to give your support team relief.

The buried assumption: *the tickets exist because users can't find answers on their own, and a chatbot will change that.*

---

## THREE REFRAMES

**Reframe 1: The problem is that users hit friction and have no self-serve path.**
- *Problem statement:* Users encounter blockers they can't resolve without help, and the help center doesn't give them a fast enough answer.
- *Implied solution:* Improve the help center's search, structure, and content quality before building a chatbot — most deflection gains come from findability, not AI.
- *Assumption:* The bottleneck is discovery, not delivery. Users know what they're looking for but can't find it.
- *Why this might be more true:* If users could find the answer in 30 seconds, they wouldn't open a ticket. A chatbot that wraps bad content is still a bad experience. Fix the content first — it's faster, cheaper, and a prerequisite for any chatbot to work well.

---

**Reframe 2: The problem is that your support team is doing work that should never reach them.**
- *Problem statement:* A significant portion of tickets are repetitive, low-complexity questions that the same 10 answers would resolve — but nothing intercepts them before they become tickets.
- *Implied solution:* Build a ticket deflection layer — smart FAQ matching, in-app contextual help, or a triggered tooltip at the exact moment users get stuck — before investing in a full chatbot.
- *Assumption:* The ticket volume is concentrated in a small number of repeat question types, not distributed across hundreds of unique problems.
- *Why this might be more true:* Most support teams find that 20% of question types account for 60-70% of ticket volume. If that's true here, targeted deflection of the top 10 question types is faster to build, easier to measure, and more impactful than a general-purpose chatbot.

---

**Reframe 3: The problem is that your support team is under-resourced, and AI is being proposed as a substitute for hiring.**
- *Problem statement:* The support team is overwhelmed not because ticket volume is unreasonable, but because capacity hasn't scaled with growth — and a chatbot is being evaluated as a cheaper alternative to additional headcount.
- *Implied solution:* Model the actual cost: what does it cost to build and maintain a chatbot vs. hiring one support person? What ticket volume does each solve? Which is faster to value?
- *Assumption:* A chatbot is cheaper and faster than hiring. This is often wrong when implementation, maintenance, and quality monitoring are included.
- *Why this might be more true:* AI chatbots for support have a high failure rate when deployed before the underlying content and routing logic are solid. If the team is overwhelmed today, they will also be overwhelmed managing a poorly-performing chatbot tomorrow.

---

## THE HARDEST QUESTION

**Have you pulled the ticket data and identified what percentage of your volume comes from the top 5 question types — and if so, why haven't you already written better answers for those?**

If you haven't done that analysis, you don't yet know whether this is a chatbot problem, a content problem, a product UX problem, or a staffing problem. You're about to build an expensive solution to a problem you haven't fully diagnosed.

---

## WHAT TO VALIDATE FIRST

Pull the last 30 days of support tickets, tag the top 10 question types by volume, and calculate what percentage of total tickets they represent.

If the top 10 types account for more than 50% of ticket volume — you have a deflection problem that a targeted FAQ or in-app help layer can solve faster than a chatbot.

If ticket types are widely distributed with no clear clusters — you have a complexity problem that a chatbot will struggle with too.

That single analysis tells you which solution to build before you write a single line of code.

---

## RED FLAG CHECK

**Yes — there is a clear symptom/root cause risk here.**

"Users submit too many tickets" is a symptom. The root causes could be a confusing product UI, a poorly structured help center, undertrained users, a recent feature change that broke expected behavior, or genuine product gaps — any of which would generate high ticket volume regardless of whether a chatbot exists. Building a chatbot on top of an undiagnosed root cause doesn't fix the problem; it adds a layer of complexity that makes the real cause harder to find. The overwhelmed support team is the signal that something upstream is broken — the chatbot is a pressure valve, not a fix.
