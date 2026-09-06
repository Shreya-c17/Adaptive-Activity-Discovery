# Product Decisions

The product decisions behind Adaptive Activity Discovery were driven by one recurring constraint: **the product often has to make useful decisions before it has complete information.**

Rather than trying to eliminate that uncertainty through more onboarding, more assumptions, or more sophisticated technology, the design focuses on managing uncertainty explicitly.

Each decision reflects a tradeoff between relevance, confidence, user friction, technical complexity, and business value.

---

## 1. Do Not Classify Users Before There Is Enough Evidence

### The Decision

Start every user with one shared discovery experience rather than immediately placing them into separate journeys for browsers, planners, or immediate travelers.

### Alternatives Considered

| Approach | Why I Did Not Choose It |
|---|---|
| Separate persona-specific experiences | Requires high-confidence classification before enough evidence exists |
| Ask users to declare their intent | Creates friction before users can begin exploring |
| Infer intent immediately from location | Location does not reliably indicate destination intent or urgency |
| One adaptive experience | Allows the product to remain useful while confidence develops |

### Why

At first load, the available context may look identical across users with completely different needs.

Someone physically located in Paris could be casually browsing, planning activities for later, or looking for something to do immediately.

Building separate experiences at that point would require the product to make a high-impact decision using weak evidence.

I chose a shared experience because **a wrong early assumption is more damaging than slightly slower personalization**.

The experience becomes more specific only when meaningful behavior supports that interpretation.

### Tradeoff

Personalization may take longer to emerge than it would in a forced onboarding flow.

I accepted that tradeoff because the product should not create certainty where the evidence does not exist.

---

## 2. Let Behavior Earn Confidence Instead of Asking Users to Explain Themselves

### The Decision

Infer context progressively from meaningful behavior rather than requiring users to declare their intent upfront.

### Alternatives Considered

| Approach | Why I Did Not Choose It |
|---|---|
| Intent-selection onboarding | Adds friction and depends on users accurately describing their needs |
| Passive behavior alone | Weak evidence can easily be misinterpreted |
| Immediate personalization from one action | Creates overconfident recommendations |
| Progressive confidence from meaningful actions | Allows specificity to increase with evidence |

### Why

Not all interactions mean the same thing.

Passive scrolling may indicate curiosity.

A destination search is stronger evidence.

Selecting dates strengthens the interpretation further.

Repeated exploration around the same destination or theme strengthens it again.

The important product decision was to treat **behavior as evidence rather than a binary answer**.

A single signal should not automatically determine the experience.

Confidence should accumulate.

This allows the product to adapt gradually instead of jumping from generic discovery to highly personalized recommendations after one interaction.

### Tradeoff

Some users will remain in a lower-confidence state longer.

I accepted this because broad but useful discovery is preferable to confident personalization based on weak evidence.

---

## 3. Use Rules Before Machine Learning

### The Decision

Use a rules-based confidence and ranking system for V1 rather than introducing a trained model immediately.

### Alternatives Considered

| Approach | Why I Did Not Choose It for V1 |
|---|---|
| Trained ranking model | Requires sufficient reliable outcome data |
| Complex predictive system | Adds complexity before validating the core product hypothesis |
| Rules-based confidence model | Explainable, testable, and easier to iterate on |

### Why

The first product question is not:

> How do we build the most sophisticated personalization system?

It is:

> **Does progressively adapting discovery based on stronger evidence actually improve relevance?**

A rules-based system allows every state transition and ranking decision to be traced back to identifiable evidence.

That matters during experimentation.

If the experience underperforms, the team should be able to understand whether the problem comes from:

- Weak signals
- Incorrect confidence transitions
- Ineffective ranking logic
- An incorrect underlying product hypothesis

A more sophisticated model would not automatically solve those problems.

### Tradeoff

Rules cannot capture the same complexity or nuance as a mature learned system.

I accepted that limitation because **explainability and learning velocity are more valuable than sophistication when validating a new mechanism**.

---

## 4. Put Commercial Optimization Inside a Relevance Constraint

### The Decision

Activities must first qualify as relevant to the user's current context before commercial factors influence their ranking.

### Alternatives Considered

| Approach | Risk |
|---|---|
| Commercial-first ranking | Can surface a worse option because it generates more revenue |
| Optimize for raw clicks | Encourages attention rather than useful outcomes |
| Supplier-first ranking | Can distort recommendations toward business incentives |
| Relevance first, commercial tie-breaking | Protects user value while still allowing business optimization |

### Why

Business value matters.

But commercial value should not compensate for poor user fit.

The ranking system therefore works in two stages.

**First:** determine whether an option is genuinely relevant.

**Then:** differentiate between relevant options using factors such as supplier reliability, content quality, value, and commercial terms.

This is not a decision to ignore revenue.

It is a decision about **where revenue optimization belongs in the decision process**.

Commercial factors can help choose between two good options.

They should not allow a materially worse option to outrank a better one.

### Tradeoff

This can limit short-term commercial optimization.

I accepted that tradeoff because repeatedly showing users options that are commercially attractive but poorly matched to their needs is likely to damage trust and reduce long-term product value.

---

## 5. Treat Contradictory Behavior as New Evidence, Not System Failure

### The Decision

When new behavior contradicts the current interpretation, reweight confidence instead of either ignoring the new signal or completely resetting the user's context.

### Alternatives Considered

| Approach | Problem |
|---|---|
| Ignore contradictory behavior | Keeps the experience anchored to outdated assumptions |
| Hard reset everything | Discards potentially useful context |
| Reweight toward newer evidence | Allows the interpretation to change without losing all context |

### Why

User intent is not static.

Someone may begin exploring Paris and later shift attention to Mumbai.

The system should not continue centering Paris simply because that was the first destination observed.

But a complete reset is also unnecessarily destructive.

Earlier context may still be useful.

The better approach is to treat newer meaningful behavior as stronger evidence and shift confidence accordingly.

This reflects an important principle in the design:

**The system should be able to change its mind.**

### Tradeoff

Reweighting is more complex than a simple reset.

I accepted that complexity because a personalization system that cannot adapt to changing context will eventually become confidently wrong.

---

## 6. Validate the Mechanism Before Expanding the Product

### The Decision

Prioritize the adaptive discovery mechanism and confidence engine before investing in improvements across every product surface.

### Alternatives Considered

| Approach | Why I Did Not Choose It |
|---|---|
| Improve every surface simultaneously | Makes it difficult to identify what actually caused improvement |
| Build advanced personalization first | Increases complexity before validating the core hypothesis |
| Optimize downstream conversion surfaces first | Risks optimizing later stages before improving upstream relevance |
| Validate the adaptive mechanism first | Creates a clearer learning loop and reduces unnecessary investment |

### Why

The highest-value question is whether the product can meaningfully improve discovery by adapting to stronger evidence.

If that mechanism does not work, improving every downstream surface will not solve the underlying problem.

The V1 should therefore focus on:

- Capturing meaningful signals
- Building confidence progressively
- Adapting discovery
- Measuring whether relevance improves downstream behavior

Only after validating that mechanism should the product expand into more sophisticated ranking, deeper personalization, or additional surfaces.

### Tradeoff

Some potentially valuable improvements are delayed.

I accepted that because **sequencing product investment around the biggest uncertainty produces faster learning than building the complete solution upfront**.

---

## The Decision Framework Behind the Product

These decisions follow the same underlying logic.

| Product Question | Decision Principle |
|---|---|
| Do we know enough to personalize? | Specificity should follow evidence |
| Should we ask the user for more information? | Avoid friction when behavior can provide useful evidence |
| Should we use more sophisticated technology? | Validate the mechanism before increasing complexity |
| How should ranking balance users and business? | Optimize business value within a relevance constraint |
| What happens when the system is wrong? | Allow new evidence to change the interpretation |
| What should we build first? | Prioritize the biggest uncertainty and highest-leverage mechanism |

---

## Closing Perspective

The central product challenge was not designing a more personalized Activities homepage.

It was deciding **when the product has enough evidence to become more specific and what it should do when that evidence changes**.

That led to a design that deliberately avoids several tempting shortcuts:

- Classifying users too early
- Asking users to explain themselves before they can explore
- Treating one signal as certainty
- Introducing ML before validating the underlying mechanism
- Optimizing revenue before relevance
- Building the full solution before proving the core hypothesis

The product instead manages uncertainty progressively.

**Start useful. Gather evidence. Increase confidence. Adapt the experience. Change the interpretation when the evidence changes.**
