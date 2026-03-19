# AI vs Deterministic Decider — Support Ticket Routing
**Problem submitted:** 2026-03-19

---

## VERDICT

**HYBRID — use deterministic first, AI only where rules break down**

---

## WHY

The majority of support tickets at 500/day will use predictable language that keyword rules can handle reliably and cheaply — "invoice", "charge", "refund" almost always means Billing; "can't log in", "error", "bug" almost always means Technical. Building a full AI classifier for the entire volume is over-engineered for what a well-tuned ruleset can handle at zero inference cost. However, free-text tickets are unpredictable enough that a pure rules system will have a meaningful miss rate — ambiguous, multi-topic, or unusually worded tickets need AI as a fallback. Start deterministic, escalate to AI only when rules can't confidently assign a category.

---

## THE TEST (4 questions)

**1. Does the input vary too much for rules to handle?**
**Partially — No for the majority, Yes for the edge cases.**
Most tickets cluster around predictable vocabulary per team. "I was charged twice", "my integration is broken", "how do I add a teammate" are all rule-catchable. But free text means you'll always get ambiguous, multi-topic, or oddly phrased tickets that no keyword list will reliably classify. Rules handle ~70-80%; the remaining 20-30% is where variation genuinely exceeds what rules can manage.

**2. Is being wrong occasionally acceptable?**
**Yes — with a condition.**
Misrouting a ticket adds friction and delay but doesn't cause irreversible harm. Teams can re-route manually. However, at 500 tickets/day even a 15% error rate means 75 misrouted tickets daily — which is a real operational cost. "Occasionally wrong" is acceptable; "systematically wrong on a predictable segment" is not. The hybrid approach minimizes systematic errors by routing ambiguous tickets through AI rather than forcing a bad rule match.

**3. Is the cost of building and maintaining AI justified by the value it adds over a simpler system?**
**No for a full AI system — Yes for a targeted fallback.**
A full classification model trained on ticket data costs engineering time, needs labelled training data, requires retraining as language and team structures evolve, and adds latency and inference cost to every ticket. That's unjustified when rules handle the bulk of volume. A lightweight LLM fallback (called only when rules return low confidence) adds AI value precisely where it's needed, at a fraction of the cost.

**4. Does this problem get better with more data over time?**
**Yes — but only if you collect it.**
A classification model trained on historically routed tickets improves as volume grows. Misrouted tickets that get manually corrected become labelled training data. At 500 tickets/day you'll accumulate enough signal quickly. This argues for building the hybrid now with logging in place, so that if you ever want to move to a full classifier, the training data already exists.

---

## IF AI: WHAT KIND

**Rule + LLM fallback**

For tickets that don't match any rule with sufficient confidence, pass the ticket text to an LLM with a structured prompt:

> *"You are a support routing assistant. Classify this ticket into exactly one of: Billing, Technical, Onboarding, General. Return only the category name."*

This approach requires no training data, no model hosting, and no retraining cycle. It handles ambiguous and edge-case tickets reliably. The LLM is only invoked when the rule engine flags low confidence — keeping inference costs proportional to actual ambiguity volume, not total ticket volume.

---

## IF DETERMINISTIC: WHAT THE RULES LOOK LIKE

Rules to handle the ~70-80% of predictable tickets:

1. **Billing:** If ticket contains any of — *invoice, charge, charged, refund, payment, subscription, pricing, plan, billing, receipt, overpaid* → route to Billing
2. **Technical:** If ticket contains any of — *error, bug, broken, not working, crash, can't log in, login issue, integration, API, sync, glitch, failed* → route to Technical
3. **Onboarding:** If ticket contains any of — *how do I, getting started, setup, first time, invite, add a user, walkthrough, tutorial, onboarding* → route to Onboarding
4. **General:** If ticket matches no rule above with confidence → flag for AI fallback (do not default to General silently)
5. **Conflict rule:** If ticket matches keywords from two or more categories → flag for AI fallback rather than forcing a guess

---

## RISK OF GETTING THIS WRONG

**If we use full AI when we should not have:** We pay inference costs on 500 tickets/day for a problem that keyword rules solve 75% of the time, add engineering complexity and latency, and introduce a system that can fail silently in ways a rule system never would — all for marginal accuracy gains on an already-catchable problem.

**If we use pure deterministic when we should not have:** We silently misroute the 20-30% of ambiguous or unusually worded tickets every day, create a growing manual correction burden for support leads, and build false confidence that the system is working because it always returns an answer — even when it's the wrong one.
