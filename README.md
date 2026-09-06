# Adaptive Activity Discovery

A product case study on designing a travel Activities experience that becomes more relevant as user context becomes clearer.

**Interactive Prototype:** [https://onarrival-activities.vercel.app/](https://onarrival-activities.vercel.app/)

## Overview

Activity discovery presents a difficult product problem: the same user behavior can represent very different underlying needs.

Someone opening an activity might be casually browsing for ideas, actively planning a future trip, or looking for something practical to do immediately. At first, these users can look similar. The product may have limited context, and a single signal such as location does not reliably explain what the user actually needs.

This case study explores how an Activities experience can adapt to those differences without forcing users to declare their intent upfront or making strong assumptions too early.

The core principle behind the design is simple:

**Start with one useful experience. Observe the evidence. Become more specific only when the evidence earns it.**

---

## The Problem

Consider three users who all open an activity but do not immediately check availability.

**The Browser** is exploring out of curiosity and may have no immediate intention to book.

**The Planner** has meaningful intent but has not yet found activities that fit their destination, dates, or plans closely enough.

**The Immediate Traveler** is looking for something practical to do soon and may find the activity too far away, unavailable, or unsuitable for their remaining time window.

The visible behavior is similar. The underlying reason is not.

Treating all of these users as one funnel problem and applying the same intervention risks solving the wrong problem.

The product question is therefore not simply:

> How do we increase availability checks?

It is:

> How do we make activity discovery more relevant to what the user is actually trying to do?

---

## The Approach

Rather than assigning users to fixed personas or building separate experiences for assumed user types, I designed one adaptive experience that starts broadly and becomes more specific as meaningful evidence emerges.

The experience is built around three ideas:

### Start useful with limited context

The product should still provide useful discovery when it knows very little about the user. It should not require an onboarding flow or intent questionnaire before someone can start exploring.

### Let behavior earn confidence

Meaningful actions provide stronger evidence than passive browsing.

A destination search, selected dates, saved activity, or repeated pattern of interaction can gradually increase confidence in what the user is trying to do.

One weak signal should not trigger a highly personalized experience.

### Allow the interpretation to change

User context is not permanent.

New behavior can strengthen the current interpretation, weaken it, or contradict it entirely. The experience should adapt accordingly rather than remaining anchored to an outdated assumption.

---

## The Confidence Model

The proposed system moves through five states:

**Unsure → Leaning → Committed → Immediate → Contradiction**

These are not fixed user personas. They represent the system's confidence in its current interpretation of the user's context.

### Unsure

There is limited evidence about what the user needs.

The experience remains broad and useful without making strong assumptions.

### Leaning

A meaningful signal suggests a possible direction.

For example, a destination search can increase the prominence of relevant activities while preserving broader discovery.

### Committed

Stronger or corroborating evidence supports a clearer interpretation.

At this stage, discovery can become more specific around factors such as destination, dates, themes, and activity suitability.

### Immediate

The user appears to have a short decision window.

The experience prioritizes practical options based on availability, timing, distance, travel time, and relevance.

### Contradiction

New behavior conflicts with the current interpretation.

Rather than permanently following the earlier assumption or completely resetting everything, the system reweights confidence toward newer evidence.

This state was particularly important to me because adaptive systems should be able to admit when their previous interpretation is no longer the best one.

---

## How the Experience Adapts

The product starts with one shared discovery experience.

As confidence increases, the experience becomes more specific.

With limited context, users can explore broadly.

As meaningful signals emerge, relevant destinations or themes receive greater prominence.

With stronger evidence, ranking can account more heavily for destination fit, dates, preferences, and practical constraints.

When the decision window is immediate, the experience prioritizes activities that can realistically be acted on soon.

The key design principle is that **specificity follows evidence**.

The system should not act highly confident simply because it has one piece of contextual information.

---

## Ranking Activities

One of the most important decisions in the project was separating **user relevance** from **commercial optimization**.

The proposed ranking process works in two stages.

### First: Establish relevance

An activity should first be evaluated based on how well it fits the user's current context.

Relevant factors can include:

- Destination or theme fit
- Date fit
- Proximity
- Travel time
- Time-window fit
- Availability

The first question is:

> Is this activity genuinely appropriate for the user's current situation?

### Then: Differentiate between relevant options

Once multiple activities are already good fits, additional factors can help determine their order.

These can include:

- Availability reliability
- Content quality
- Price or value
- Commercial considerations

The principle is:

**Commercial factors can break ties between relevant options. They should not override materially better user relevance.**

This protects the experience from optimizing short-term economics at the expense of user trust.

---

## Key Product Decisions

### One adaptive experience instead of persona-specific journeys

At first load, the product does not have enough evidence to reliably determine whether someone is browsing, planning, or looking for something immediate.

Instead of forcing an early classification, I chose to let confidence build through behavior.

The tradeoff is slower personalization in some sessions, but the benefit is avoiding high-confidence assumptions based on weak evidence.

### Rules before a learned model for V1

I chose a rules-based confidence system for the initial version.

The goal of V1 is to validate whether the adaptive mechanism itself improves the experience. A rules-based system makes the logic explainable and easier to debug.

A learned model could be explored later once there is sufficient evidence and outcome data to justify the additional complexity.

### Reweighting instead of resetting on contradiction

User behavior can change.

A hard reset may unnecessarily discard useful context, while ignoring new behavior can trap the user in an outdated experience.

The proposed approach gives newer evidence more weight while keeping earlier context available where appropriate.

### Validate the mechanism before expanding the product

I deliberately scoped V1 around the core adaptive discovery mechanism rather than trying to build a complete personalization platform immediately.

The goal is to learn whether the approach works before investing in more complex capabilities.

---

## V1 Scope

The proposed V1 focuses on the capabilities required to validate the product hypothesis:

- Event logging and meaningful behavioral signals
- Rules-based confidence transitions
- Adaptive discovery
- Context-aware activity ranking
- Destination and date relevance where supported by available context
- Same-day and nearby discovery for immediate use cases
- Basic multi-supplier tie-breaking
- Experimentation and confidence-state analysis

I deliberately deferred:

- Learned ranking
- Deep cross-session personalization
- Traffic-aware travel time
- Events and festival intelligence
- Collaborative recommendations
- Advanced price intelligence

These capabilities may be valuable, but they are not necessary to answer the first product question: **does adapting discovery based on stronger evidence improve relevance?**

---

## Measuring Success

The central hypothesis is:

> If activity discovery becomes more relevant as user context becomes clearer, users should progress more meaningfully toward checking availability without harming trust or downstream product quality.

The proposed primary metric is the **Qualified Availability-Check Rate**.

This measures meaningful progression toward checking availability rather than simply optimizing for clicks.

Supporting metrics would examine:

- Search to relevant activity open
- Time to availability check
- Availability check to booking
- Confidence-state progression

The experiment would compare the adaptive experience against a non-adaptive baseline.

The primary metric alone would not determine success.

Key guardrails would include:

- Booking conversion
- Cancellation and supplier failure rates
- Recommendation diversity
- Supplier reliability
- Latency
- Trust-related signals

A lift in availability checks would not be enough if downstream quality or user trust deteriorated.

---

## The Prototype

The interactive prototype demonstrates how the Activities experience adapts as different levels of context and confidence emerge.

**View the prototype:**

[https://onarrival-activities.vercel.app/](https://onarrival-activities.vercel.app/)

---

## Supporting Documentation

This README provides the core product narrative.

The supporting documents go deeper into specific parts of the work:

### Product Specification

Detailed requirements, signal architecture, confidence logic, ranking behavior, scope, and edge cases.

### Product Decisions

The reasoning, alternatives, and tradeoffs behind the major product decisions.

### Metrics and Experimentation

The product hypothesis, success metrics, guardrails, experiment design, and ship criteria.

---

## Closing Thought

The central idea behind this project is not that products should personalize everything immediately.

It is that they should become more specific when they have earned the right to do so.

A useful experience should work with limited context.

Meaningful behavior should strengthen confidence.

Contradictory behavior should be able to change the system's interpretation.

And user relevance should remain more important than a confident assumption or short-term commercial incentive.

That principle is the foundation of Adaptive Activity Discovery.
