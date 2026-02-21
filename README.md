# ADR_SLM-Capability-Limitation-and-Cloud-Escalation
## ADR: Edge SLM Capability Limitation and Cloud Escalation Strategy

---

## 1. Status
Proposed

---

## 2. Context

After adopting Small Language Models (SLMs) at the Edge (ADR-001), several limitations were identified:

- Limited multi-step reasoning capability
- Smaller context window
- Lower accuracy for high-complexity tasks
- Limited domain knowledge compared to Cloud LLMs

**Conclusion:**  
An Edge-only architecture is insufficient for advanced reasoning tasks. A controlled Cloud escalation mechanism is required.

---

## 3. Decision

We adopt an **Edge-First with Cloud Escalation Strategy**:

- All requests are processed by Edge SLM first.
- Requests exceeding predefined thresholds are escalated to Cloud LLM.
- Escalation triggers include:
  - Complexity score
  - Token size
  - Reasoning depth
  - Low confidence level

Cloud acts as a reasoning augmentation layer — not the default processor.

---

## 4. Architecture Overview

User → Edge SLM → Complexity Evaluator → Decision Engine  
                                     ↓  
                        (If threshold exceeded)  
                                     ↓  
                                Cloud LLM  

---

## 5. Consequences

### Pros
- Maintains low latency for most tasks
- Expands reasoning capability when needed
- Reduces cloud cost
- Improves accuracy for complex cases

### Cons
- Requires routing logic
- Increases architectural complexity
- Needs monitoring of escalation rate

---

## 6. Governance & Monitoring

- Escalation rate ≤ 30% per month
- Edge handling ≥ 70% of total requests
- Average latency ≤ 500ms
- Cloud cost reduced ≥ 40% vs pure cloud model
- Continuous monitoring of escalation rate, latency, and token usage

---

## 7. Workflow Summary

| Condition | Processing |
|------------|------------|
| Complexity < 0.5 | Edge SLM |
| ≥ 1000 tokens | Cloud LLM |
| Complexity ≥ 0.7 | Cloud LLM |
| Confidence < 80% | Cloud LLM |

---

**Relationship to ADR-001:**  
ADR-001 defines the Hybrid architecture.  
ADR-002 defines the escalation mechanism and control strategy.
