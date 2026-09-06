# Product Specification: Adaptive Activity Discovery

## 1. Product Summary

| Area | Specification |
|---|---|
| **Problem** | Activity discovery serves users with different underlying needs, but early behavior often provides insufficient context to reliably identify them. |
| **Objective** | Improve activity relevance as user context becomes clearer without forcing upfront intent selection. |
| **Core principle** | Start useful → observe evidence → increase specificity when confidence is earned. |
| **V1 approach** | Rules-based confidence model using available context and active behavioral signals. |

---

## 2. Goals and Non-Goals

### Goals

| Goal | What it means |
|---|---|
| Improve relevance | Surface activities that better fit the user's current context |
| Reduce unnecessary drop-off | Improve upstream relevance before the availability decision |
| Avoid forced onboarding | Let users explore without declaring intent |
| Adapt gradually | Increase specificity as evidence strengthens |
| Handle changing context | Allow new behavior to weaken or change previous assumptions |
| Keep V1 explainable | Use understandable rules before introducing ML |

### Out of Scope for V1

| Deferred capability | Why |
|---|---|
| Learned ranking | Requires sufficient outcome data |
| Deep cross-session personalization | Requires identity and consent infrastructure |
| Traffic-aware travel time | Requires reliable routing data |
| Events intelligence | Requires dependable external content |
| Collaborative recommendations | Adds significant recommendation infrastructure |
| Price intelligence | Requires historical pricing data |

---

## 3. Product Principles

| Principle | Product implication |
|---|---|
| **One experience first** | Do not classify users into separate journeys immediately |
| **Specificity follows evidence** | Stronger personalization requires stronger evidence |
| **Behavior earns confidence** | Deliberate actions matter more than passive browsing |
| **Context ≠ intent** | Location alone does not equal destination intent |
| **Interpretations can change** | New evidence can override earlier assumptions |
| **Relevance before revenue** | Commercial factors cannot override materially better user fit |

---

## 4. Signal Architecture

| Signal Type | Examples | Role |
|---|---|---|
| **Contextual** | Location, time, day | Supporting context, not intent by itself |
| **Available product context** | Known trip details, destination, dates | Strengthens interpretation when available |
| **Active behavior** | Searches, dates, saves, repeated exploration | Primary evidence source in V1 |
| **Outcome signals** | Availability checks, bookings, cancellations | Evaluate whether the experience is working |

**Important:** A signal does not automatically equal certainty. Confidence should increase through meaningful and corroborating evidence.

---

## 5. Confidence Model

| State | Evidence | Experience Behavior |
|---|---|---|
| **Unsure** | Limited meaningful evidence | Broad discovery, minimal assumptions |
| **Leaning** | One meaningful directional signal | Increase prominence of relevant options while preserving exploration |
| **Committed** | Strong or corroborating evidence | Prioritize destination, date, theme, and suitability |
| **Immediate** | Short decision window | Prioritize availability, timing, distance, and practicality |
| **Contradiction** | New behavior conflicts with current interpretation | Reweight confidence toward newer evidence |

### Transition Principle

The system should not jump from one weak signal to strong personalization.

**Weak evidence → light adaptation**

**Corroborating evidence → stronger adaptation**

**Contradictory evidence → reweight or redirect**

---

## 6. Experience Requirements

### Discovery

The entry experience should:

- Support broad exploration
- Work for cold-start users
- Keep search and discovery accessible
- Avoid forced intent selection

### Adaptive Behavior

| Confidence Level | Experience |
|---|---|
| Low | Broad discovery |
| Emerging | Relevant destinations or themes gain prominence |
| Strong | Ranking increasingly reflects destination, dates, and suitability |
| Immediate | Prioritize options that can realistically be acted on soon |
| Contradictory | Adapt toward newer meaningful behavior |

### Activity Detail

Where available, provide:

- Price
- Duration
- Rating
- Availability
- Relevant travel or timing information

**Primary action:** Check Availability

**Secondary action:** Save

---

## 7. Ranking Logic

### Stage 1: Relevance Qualification

Before commercial considerations, determine whether an activity fits the user's context.

| Relevance Factors |
|---|
| Destination or theme fit |
| Date fit |
| Proximity |
| Travel time |
| Time-window fit |
| Availability |

The first question is:

> **Is this genuinely useful for the user right now?**

### Stage 2: Differentiate Relevant Options

Only after options meet a relevance threshold can additional factors influence ordering.

| Tie-Breaking Factors |
|---|
| Availability reliability |
| Content quality |
| Price or value |
| Supplier reliability |
| Commercial terms |

**Rule:** Commercial optimization can differentiate between relevant options but should not override materially better user relevance.

---

## 8. Multi-Supplier Handling

Where the same activity has multiple supplier options:

- Keep meaningful differences visible
- Rank the default option based on relevance and quality
- Allow users to compare valid alternatives
- Do not hide genuine differences in price or availability

---

## 9. V1 Scope

| Included | Deferred |
|---|---|
| Event logging | Learned ranking |
| Rules-based confidence engine | Deep cross-session personalization |
| Adaptive discovery | Traffic-aware travel time |
| Context-aware ranking | Events intelligence |
| Immediate-use ranking | Collaborative recommendations |
| Activity evaluation improvements | Price intelligence |
| Basic multi-supplier logic | Collaborative trip planning |
| Experiment instrumentation | Advanced personalization |

---

## 10. Edge Cases

| Scenario | Expected Behavior |
|---|---|
| Location unavailable | Fall back to search-first discovery |
| Missing activity information | Use appropriate fallbacks |
| No useful same-day options | Broaden time window → expand radius → return to broader discovery |
| Contradictory behavior | Reweight toward newer evidence |
| Supplier disagreement | Present distinct valid options |
| Cold start | Use session-level context and active behavior |

---

## 11. Success Criteria

### Product Hypothesis

> If activity discovery becomes more relevant as user context becomes clearer, users should progress more meaningfully toward checking availability without harming trust or downstream product quality.

### Primary Metric

**Qualified Availability-Check Rate**

### Supporting Metrics

- Search → relevant activity open
- Time to availability check
- Availability check → booking
- Confidence-state progression

### Guardrails

| Guardrail |
|---|
| Booking conversion |
| Cancellation and supplier failure rates |
| Recommendation diversity |
| Supplier reliability |
| Latency |
| Trust-related signals |

A lift in availability checks alone is **not sufficient** to justify shipping.
