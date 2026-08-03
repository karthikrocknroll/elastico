# Escalation Rules

Scoped to the Match Making + Approve/Reject loop only. Timer-based escalations — the 8-hour Super Admin handoff and the At-Risk notify-once rule — belong to the Pulse Check trigger, which is outside this prototype's live loop, and are not evaluated here.

## 1. Low Confidence

If the agent is unsure a candidate genuinely clears every eligibility rule, it stops rather than guessing and surfaces the ambiguity instead of recommending.

## 2. Missing Data

If a candidate record is missing a field required to evaluate an eligibility rule (for example, a blank Gender for a Girls-only request, or a blank Age or AgeGroup), the agent does not evaluate eligibility on the incomplete record. It flags the record for correction and excludes that candidate from this run. It never assumes a value.

## 3. Gap In Business Logic

If a case turns on a rule or parameter the source documents don't fully specify, the agent flags it rather than silently deciding on incomplete rules.

## 4. Out-Of-Policy Candidate

If every available candidate fails at least one hard eligibility rule (age/play-up cap, division, team category, availability, same-team exclusion, concurrent-borrow cap), the agent rejects. It never recommends a candidate that fails a rule, and it never proceeds silently. If no valid candidate exists, the Borrow request stays Open and the agent escalates to the Age Coordinator feed instead of forcing a match.

## Not Applicable To This Loop

- Anger or legal language — no free-text, user-facing channel exists in this workflow.
- High-stakes timers (8-hour stall, At-Risk unresolved) — handled by the Pulse Check trigger, not built in this prototype.
