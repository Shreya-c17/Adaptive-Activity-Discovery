# Metrics and Experimentation

## What This Experiment Is Trying to Prove

The product is based on a simple hypothesis:

> If activity discovery becomes more relevant as user context becomes clearer, users should progress more meaningfully toward checking availability without harming downstream quality, trust, or commercial outcomes.

The goal is **not** to maximize clicks or availability checks in isolation.

The experiment is testing whether the adaptive discovery mechanism improves the quality of the user's path toward a decision.

---

## 1. Metric Framework

### Primary Metric

#### Qualified Availability-Check Rate

The percentage of relevant activity-detail sessions that progress to an availability check.

This is the primary metric because the product problem occurs upstream of the availability decision.

A generic discovery experience may generate activity views without helping users find options that actually fit their context. A qualified availability check is therefore a stronger signal than simply measuring:

- Homepage clicks
- Activity opens
- Time spent
- Raw engagement

The experiment should measure the lift in Qualified Availability-Check Rate against the baseline experience.

---

### Supporting Metrics

These metrics help explain **why** the primary metric changed.

| Metric | What It Helps Diagnose |
|---|---|
| **Search → Relevant Activity Open** | Whether users reach useful inventory more effectively after expressing intent |
| **Time to Availability Check** | Whether users, particularly Immediate users, reach a viable decision faster |
| **Availability Check → Booking** | Whether improved upstream relevance translates into downstream commercial value |
| **Confidence-State Progression** | Whether the confidence engine is producing meaningful state changes |
| **Correction / Contradiction Rate** | Whether the system is becoming confidently wrong or over-personalized |
| **Immediate Fallback Rate** | Whether narrow same-day or nearby ranking repeatedly fails because inventory is too limited |

---

## 2. Guardrails

An improvement in the primary metric is not enough if the treatment creates worse downstream outcomes.

| Guardrail | What It Protects Against |
|---|---|
| **Booking Conversion** | More availability checks without meaningful downstream value |
| **Cancellation Rate** | Apparent conversion gains driven by poor-fit recommendations |
| **Supplier Failure Rate** | Recommendations that rely on unreliable inventory |
| **Recommendation Diversity** | Over-concentration on a small number of activities or suppliers |
| **Supplier Reliability** | Ranking commercially attractive but operationally poor options |
| **Latency** | Better relevance achieved at an unacceptable performance cost |
| **Correction / Contradiction Signals** | False confidence and over-personalization |

The key principle is:

**The product should not improve one stage of the funnel by degrading the quality of the overall experience.**

---

## 3. Experiment Design

### Control

The existing non-adaptive Activities discovery experience.

Users receive the same general discovery and ranking logic regardless of the strength of available context.

### Treatment

The adaptive experience.

The treatment uses:

- Meaningful behavioral signals
- Available contextual information
- The rules-based confidence model
- Confidence-aware discovery and ranking

The treatment becomes more specific only when stronger evidence supports the interpretation.

---

### Primary Comparison

Compare the treatment against the control on:

**Qualified Availability-Check Rate**

The analysis should also segment results by confidence state.

This is important because the expected impact is not uniform.

The adaptive mechanism should provide the greatest value when the product has meaningful context to work with.

### Expected Pattern

| User Context | Expected Impact |
|---|---|
| **Unsure** | Limited change because the product intentionally avoids strong assumptions |
| **Leaning** | Moderate improvement as emerging signals influence discovery |
| **Committed** | Stronger improvement because context can meaningfully influence ranking |
| **Immediate** | Stronger improvement if practical constraints such as timing and availability are handled well |

A uniform improvement across every state would not automatically prove the confidence mechanism is working.

It would require further investigation into whether another factor is driving the result.

---

## 4. How to Interpret the Results

A failed experiment does not automatically mean the product idea is wrong.

The result needs diagnosis.

| Observation | Possible Interpretation |
|---|---|
| Primary metric improves, guardrails remain healthy | The mechanism is working. Continue validating and expand carefully |
| Primary metric improves, but booking does not | Discovery may be creating more evaluation without improving downstream value |
| Primary metric improves, but cancellations increase | Recommendations may be relevant superficially but poor in quality or fit |
| Strong lift only in Committed and Immediate states | Expected result. Stronger context is enabling better adaptation |
| No improvement in any state | The confidence mechanism, ranking logic, or underlying hypothesis may be wrong |
| High contradiction rate | The system is making overly confident or incorrect interpretations |
| High Immediate fallback rate | Local inventory or time-window constraints may be too restrictive |

This distinction matters.

A PM should not respond to every weak result by simply adding more features.

The first question should be:

> **What part of the mechanism failed?**

---

## 5. Success Criteria

The treatment should demonstrate:

1. A credible improvement in Qualified Availability-Check Rate.
2. No material deterioration in booking conversion.
3. No material increase in cancellations or supplier failures.
4. Healthy recommendation diversity.
5. No unacceptable increase in latency.
6. No significant increase in contradiction or correction signals.

The exact statistical thresholds would depend on available traffic, baseline conversion, and experiment duration.

For this project, the important product decision is that **success is evaluated as a combination of user progression and downstream quality, not a single metric in isolation**.

---

## 6. Ship, Iterate, or Stop

| Result | Decision |
|---|---|
| Primary metric improves and guardrails remain healthy | **Ship and expand carefully** |
| Improvement is limited to specific confidence states | **Iterate and focus on where the mechanism shows value** |
| Primary metric improves but guardrails deteriorate | **Do not ship unchanged. Diagnose the tradeoff** |
| No meaningful improvement | **Reassess the signals, confidence logic, ranking, or underlying hypothesis** |
| High contradiction or fallback rates | **Reduce confidence aggressiveness and investigate inventory or signal quality** |

---

## Closing Principle

The goal of experimentation is not to prove that the solution was correct.

It is to determine whether the product mechanism creates better outcomes than the alternative.

For Adaptive Activity Discovery, the critical question is:

> **Does becoming more specific as evidence becomes stronger help users find activities that are genuinely more relevant?**

If the answer is yes, the mechanism can be expanded.

If the answer is no, the result should guide the next iteration rather than being hidden behind additional features or more sophisticated technology.
